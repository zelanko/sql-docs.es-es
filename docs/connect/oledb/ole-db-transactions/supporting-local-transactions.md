---
title: Compatibilidad con transacciones locales | Microsoft Docs
description: Transacciones en el controlador OLE DB para SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- autocommit mode
- transactions [OLE DB]
- ITransactionLocal interface
- OLE DB Driver for SQL Server, transactions
- local transactions [OLE DB]
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: 9aacaf8c52ad45a3d61087d1029bdd6f7176629e
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66765979"
---
# <a name="supporting-local-transactions"></a>Compatibilidad con transacciones locales
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Una sesión delimita el ámbito de transacción para un controlador de OLE DB para la transacción local de SQL Server. Cuando, en la dirección de un consumidor, el controlador OLE DB para SQL Server envía una solicitud a una instancia conectada de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], la solicitud constituye una unidad de trabajo para el controlador OLE DB para SQL Server. Las transacciones locales siempre contienen una o varias unidades de trabajo en un único controlador de OLE DB para la sesión de SQL Server.  
  
 En el modo de confirmación automática del controlador OLE DB para SQL Server predeterminado, una unidad de trabajo única se trata como el ámbito de una transacción local. Solo una unidad participa en la transacción local. Cuando se crea una sesión, el controlador OLE DB para SQL Server inicia una transacción para la sesión. Cuando se completa correctamente una unidad de trabajo, el trabajo se confirma. En caso de error, cualquier trabajo comenzado se revierte y el error se notifica al consumidor. En ambos casos, el controlador OLE DB para SQL Server empieza una nueva transacción local para la sesión de modo que todo el trabajo se realice dentro de una transacción.  
  
 El consumidor del controlador OLE DB para SQL Server puede ejercer un control más preciso sobre el ámbito de transacciones locales con la interfaz **ITransactionLocal**. Cuando una sesión del consumidor inicia una transacción, todas las unidades de trabajo de la sesión entre el punto de inicio de la transacción y las posibles llamadas a los métodos **Commit** o **Abort** se tratan como una unidad atómica. El controlador OLE DB para SQL Server iniciará implícitamente una transacción cuando se lo indique el consumidor. Si el consumidor no solicita la retención, la sesión vuelve al comportamiento de nivel de transacción primaria, la mayoría de las veces en modo de confirmación automática.  
  
 El controlador OLE DB para SQL Server admite **ITransactionLocal:: StartTransaction** parámetros como se indica a continuación.  
  
|Parámetro|Descripción|  
|---------------|-----------------|  
|*isoLevel*[in]|Nivel de aislamiento que se va a utilizar con esta transacción. En las transacciones locales, el controlador OLE DB para SQL Server admite lo siguiente:<br /><br /> **ISOLATIONLEVEL_UNSPECIFIED**<br /><br /> **ISOLATIONLEVEL_CHAOS**<br /><br /> **ISOLATIONLEVEL_READUNCOMMITTED**<br /><br /> **ISOLATIONLEVEL_READCOMMITTED**<br /><br /> **ISOLATIONLEVEL_REPEATABLEREAD**<br /><br /> **ISOLATIONLEVEL_CURSORSTABILITY**<br /><br /> **ISOLATIONLEVEL_REPEATABLEREAD**<br /><br /> **ISOLATIONLEVEL_SERIALIZABLE**<br /><br /> **ISOLATIONLEVEL_ISOLATED**<br /><br /> **ISOLATIONLEVEL_SNAPSHOT**<br /><br /> <br /><br /> Nota: A partir de [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], ISOLATIONLEVEL_SNAPSHOT es válido para el argumento *isoLevel*, independientemente de que la base de datos tenga habilitado el control de versiones. Sin embargo, se producirá un error si el usuario intenta ejecutar una instrucción y no está habilitado el control de versiones, o si la base de datos no es de solo lectura. Además, si se especifica ISOLATIONLEVEL_SNAPSHOT como el valor de *isoLevel* al conectarse a una versión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] anterior a [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], se producirá el error XACT_E_ISOLATIONLEVEL.|  
|*isoFlags*[in]|El controlador OLE DB para SQL Server devuelve un error para cualquier valor distinto de cero.|  
|*pOtherOptions*[in]|Si no es NULL, el controlador OLE DB para SQL Server solicita el objeto de opciones de la interfaz. El controlador OLE DB para SQL Server devuelve XACT_E_NOTIMEOUT si el objeto de opciones *ulTimeout* miembro no es cero. El controlador OLE DB para SQL Server se omite el valor de la *szDescription* miembro.|  
|*pulTransactionLevel*[out]|Si no es NULL, el controlador OLE DB para SQL Server devuelve el nivel de la transacción anidado.|  
  
 Para realizar transacciones locales, implementa el controlador OLE DB para SQL Server **ITransaction:: Abort** parámetros como se indica a continuación.  
  
|Parámetro|Descripción|  
|---------------|-----------------|  
|*pboidReason*[in]|Se omite si está establecido. Puede ser sin ningún riesgo NULL.|  
|*fRetaining*[in]|Si es TRUE, se inicia una nueva transacción de forma implícita para la sesión. La transacción debe ser confirmada o finalizada por el consumidor. Cuando sea FALSE, el controlador OLE DB para SQL Server vuelve al modo de confirmación automática para la sesión.|  
|*fAsync*[in]|Anulación asincrónica no es compatible con el controlador OLE DB para SQL Server. El controlador OLE DB para SQL Server devuelve XACT_E_NOTSUPPORTED si el valor no es FALSE.|  
  
 Para realizar transacciones locales, implementa el controlador OLE DB para SQL Server **ITransaction:: Commit** parámetros como se indica a continuación.  
  
|Parámetro|Descripción|  
|---------------|-----------------|  
|*fRetaining*[in]|Si es TRUE, se inicia una nueva transacción de forma implícita para la sesión. La transacción debe ser confirmada o finalizada por el consumidor. Cuando sea FALSE, el controlador OLE DB para SQL Server vuelve al modo de confirmación automática para la sesión.|  
|*grfTC*[in]|Asincrónicos ni fase uno devuelve no se admiten por el controlador OLE DB para SQL Server. El controlador OLE DB para SQL Server devuelve XACT_E_NOTSUPPORTED para cualquier valor distinto de XACTTC_SYNC.|  
|*grfRM*[in]|Debe ser 0.|  
  
 Los conjuntos de filas del controlador OLE DB para SQL Server en la sesión se conservan en una operación local de confirmación o anulación basada en los valores de las propiedades DBPROP_ABORTPRESERVE y DBPROP_COMMITPRESERVE del conjunto de filas. De forma predeterminada, estas dos propiedades son VARIANT_FALSE y todos los conjuntos de filas del controlador OLE DB para SQL Server en la sesión se pierden después de una operación de anulación o confirmación.  
  
 El controlador OLE DB para SQL Server no implementa la **ITransactionObject** interfaz. Si el consumidor intenta recuperar una referencia en la interfaz, obtiene E_NOINTERFACE.  
  
 En este ejemplo, se usa **ITransactionLocal**.  
  
```  
// Interfaces used in the example.  
IDBCreateSession*   pIDBCreateSession   = NULL;  
ITransaction*       pITransaction       = NULL;  
IDBCreateCommand*   pIDBCreateCommand   = NULL;  
IRowset*            pIRowset            = NULL;  
  
HRESULT             hr;  
  
// Get the command creation and local transaction interfaces for the  
// session.  
if (FAILED(hr = pIDBCreateSession->CreateSession(NULL,  
     IID_IDBCreateCommand, (IUnknown**) &pIDBCreateCommand)))  
    {  
    // Process error from session creation. Release any references and  
    // return.  
    }  
  
if (FAILED(hr = pIDBCreateCommand->QueryInterface(IID_ITransactionLocal,  
    (void**) &pITransaction)))  
    {  
    // Process error. Release any references and return.  
    }  
  
// Start the local transaction.  
if (FAILED(hr = ((ITransactionLocal*) pITransaction)->StartTransaction(  
    ISOLATIONLEVEL_REPEATABLEREAD, 0, NULL, NULL)))  
    {  
    // Process error from StartTransaction. Release any references and  
    // return.  
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
    // Get error from update, then terminate.  
    pITransaction->Abort(NULL, FALSE, FALSE);  
    }  
else  
    {  
    if (FAILED(hr = pITransaction->Commit(FALSE, XACTTC_SYNC, 0)))  
        {  
        // Get error from failed commit.  
        }  
    }  
  
if (FAILED(hr))  
    {  
    // Update of data or commit failed. Release any references and  
    // return.  
    }  
  
// Release any references and continue.  
```  
  
## <a name="see-also"></a>Consulte también  
 [Transactions](../../oledb/ole-db-transactions/transactions.md)   
 [Trabajar con aislamiento de instantánea](../../oledb/features/working-with-snapshot-isolation.md)  
  
  
