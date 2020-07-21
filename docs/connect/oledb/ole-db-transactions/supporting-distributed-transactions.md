---
title: Compatibilidad con transacciones distribuidas | Microsoft Docs
description: Transacciones distribuidas en el controlador OLE DB para SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- distributed transactions [OLE DB]
- MS DTC
- transactions [OLE DB]
- OLE DB Driver for SQL Server, transactions
- ITransactionJoin interface
- MS DTC, about distributed transaction support
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 22527cdfa08907dfdf120ef32c918ecb9eaf86bb
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "67993980"
---
# <a name="supporting-distributed-transactions"></a>Compatibilidad con transacciones distribuidas
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Los consumidores del controlador OLE DB para SQL Server pueden usar el método **ITransactionJoin::JoinTransaction** para participar en una transacción distribuida coordinada por MS DTC (Coordinador de transacciones distribuidas).  
  
 MS DTC expone objetos COM que permiten a los clientes iniciar y participar en transacciones coordinadas a través de varias conexiones a una variedad de almacenes de datos. Para iniciar una transacción, el consumidor de OLE DB Driver for SQL Server usa la interfaz **ITransactionDispenser** de MS DTC. El miembro **BeginTransaction** de **ITransactionDispenser** devuelve una referencia en un objeto de transacción distribuida. Esta referencia se pasa a OLE DB Driver for SQL Server con **JoinTransaction**.  
  
 MS DTC admite la anulación y confirmación asincrónica en transacciones distribuidas. Para la notificación en el estado de transacción asincrónica, el consumidor implementa la interfaz y conecta la interfaz **ITransactionOutcomeEvents** a un objeto de transacción de Microsoft DTC.  
  
 Para las transacciones distribuidas, el controlador OLE DB para SQL Server implementa los parámetros **ITransactionJoin::JoinTransaction** de la siguiente manera.  
  
|Parámetro|Descripción|  
|---------------|-----------------|  
|*punkTransactionCoord*|Un puntero a un objeto de transacción de MS DTC.|  
|*IsoLevel*|OLE DB Driver for SQL Server lo omite. El nivel de aislamiento para las transacciones coordinadas por MS DTC está determinado cuando el consumidor adquiere un objeto de transacción de MS DTC.|  
|*IsoFlags*|Debe ser 0. OLE DB Driver for SQL Server devuelve XACT_E_NOISORETAIN si el consumidor especifica cualquier otro valor.|  
|*POtherOptions*|Si no es NULL, OLE DB Driver for SQL Server solicita el objeto de opciones de la interfaz. OLE DB Driver for SQL Server devuelve XACT_E_NOTIMEOUT si el miembro *ulTimeout* del objeto de opciones no es cero. OLE DB Driver for SQL Server omite el valor del miembro *szDescription*.|  
  
 En este ejemplo se coordina la transacción mediante MS DTC.  
  
```  
// Interfaces used in the example.  
IDBCreateSession*       pIDBCreateSession   = NULL;  
ITransactionJoin*       pITransactionJoin   = NULL;  
IDBCreateCommand*       pIDBCreateCommand   = NULL;  
IRowset*                pIRowset            = NULL;  
  
// Transaction dispenser and transaction from MS DTC.  
ITransactionDispenser*  pITransactionDispenser = NULL;  
ITransaction*           pITransaction       = NULL;  
  
    HRESULT             hr;  
  
// Get the command creation interface for the session.  
if (FAILED(hr = pIDBCreateSession->CreateSession(NULL,  
     IID_IDBCreateCommand, (IUnknown**) &pIDBCreateCommand)))  
    {  
    // Process error from session creation. Release any references and  
    // return.  
    }  
  
// Get a transaction dispenser object from MS DTC and  
// start a transaction.  
if (FAILED(hr = DtcGetTransactionManager(NULL, NULL,  
    IID_ITransactionDispenser, 0, 0, NULL,  
    (void**) &pITransactionDispenser)))  
    {  
    // Process error message from MS DTC, release any references,  
    // and then return.  
    }  
if (FAILED(hr = pITransactionDispenser->BeginTransaction(  
    NULL, ISOLATIONLEVEL_READCOMMITTED, ISOFLAG_RETAIN_DONTCARE,  
    NULL, &pITransaction)))  
    {  
    // Process error message from MS DTC, release any references,  
    // and then return.  
    }  
  
// Join the transaction.  
if (FAILED(pIDBCreateCommand->QueryInterface(IID_ITransactionJoin,  
    (void**) &pITransactionJoin)))  
    {  
    // Process failure to get an interface, release any references, and  
    // then return.  
    }  
if (FAILED(pITransactionJoin->JoinTransaction(  
    (IUnknown*) pITransaction, 0, 0, NULL)))  
    {  
    // Process join failure, release any references, and then return.  
    }  
  
// Get data into a rowset, then update the data. Functions are not  
// illustrated in this example.  
if (FAILED(hr = ExecuteCommand(pIDBCreateCommand, &pIRowset)))  
    {  
    // Release any references and return.  
    }  
  
// If rowset data update fails, then terminate the transaction, else  
// commit. The example doesn't retain the rowset.  
if (FAILED(hr = UpdateDataInRowset(pIRowset, bDelayedUpdate)))  
    {  
    // Get error from update, then abort.  
    pITransaction->Abort(NULL, FALSE, FALSE);  
    }  
else  
    {  
    if (FAILED(hr = pITransaction->Commit(FALSE, 0, 0)))  
        {  
        // Get error from failed commit.  
        //  
        // If a distributed commit fails, application logic could  
        // analyze failure and retry. In this example, terminate. The   
        // consumer must resolve this somehow.  
        pITransaction->Abort(NULL, FALSE, FALSE);  
        }  
    }  
  
if (FAILED(hr))  
    {  
    // Update of data or commit failed. Release any references and  
    // return.  
    }  
  
// Un-enlist from the distributed transaction by setting   
// the transaction object pointer to NULL.  
if (FAILED(pITransactionJoin->JoinTransaction(  
    (IUnknown*) NULL, 0, 0, NULL)))  
    {  
    // Process failure, and then return.  
    }  
  
// Release any references and continue.  
```  
  
## <a name="see-also"></a>Consulte también  
 [Transactions](../../oledb/ole-db-transactions/transactions.md)  
  
  
