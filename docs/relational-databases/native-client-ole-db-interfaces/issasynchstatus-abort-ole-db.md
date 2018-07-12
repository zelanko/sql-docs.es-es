---
title: 'Issasynchstatus:: Abort (OLE DB) | Microsoft Docs'
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ISSAsynchStatus::Abort (OLE DB)
apitype: COM
helpviewer_keywords:
- Abort method
ms.assetid: 2a4bd312-839a-45a8-a299-fc8609be9a2a
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 3edaceb5802299ec8637634bf0006fb66d5d6851
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37408684"
---
# <a name="issasynchstatusabort-ole-db"></a>ISSAsynchStatus::Abort (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Cancela una operación que se ejecuta de forma asincrónica.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
HRESULT Abort(  
        HCHAPTER hChapter,  
        DBASYNCHOP eOperation);  
```  
  
## <a name="arguments"></a>Argumentos  
 *hChapter*[in]  
 El identificador del segmento para el que se anula la operación. Si el objeto al que se llama no es un objeto de conjunto de filas o la operación no se aplica a un segmento, el autor de las llamadas debe establecer *hChapter* en DB_NULL_HCHAPTER.  
  
 *eOperation*[in]  
 Operación para anular. El valor debe ser el siguiente:  
  
 DBASYNCHOP_OPEN—La solicitud para cancelar se aplica a la apertura o rellenado asincrónico de un conjunto de filas o a la inicialización asincrónica de un objeto de origen de datos.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 S_OK  
 Se procesó la solicitud para cancelar la operación asincrónica. Esto no garantiza que la operación en sí se haya cancelado. Para determinar si se canceló la operación, el consumidor debería llamar a [ISSAsynchStatus::GetStatus](../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-getstatus-ole-db.md) y realizar una comprobación para DB_E_CANCELED; sin embargo, puede que no se devuelva en la llamada siguiente.  
  
 DB_E_CANTCANCEL  
 La operación asincrónica no puede cancelarse.  
  
 DB_E_CANCELED  
 La solicitud para anular la operación asincrónica se canceló durante las notificaciones. La operación todavía se está ejecutando de forma asincrónica.  
  
 E_FAIL  
 Se produjo un error específico del proveedor.  
  
 E_INVALIDARG  
 El parámetro *hChapter* no es DB_NULL_HCHAPTER, o *eOperation* no es DBASYNCH_OPEN.  
  
 E_UNEXPECTED  
 Se llamó a**ISSAsynchStatus::Abort** en un objeto de origen de datos en el que no se llamó a **IDBInitialize::Initialize** , o no se ha completado.  
  
 Se llamó a**ISSAsynchStatus::Abort** en un objeto de origen de datos en el que se llamó a **IDBInitialize::Initialize** pero se canceló posteriormente antes de la inicialización, o se ha superado el tiempo de espera. Todavía no se ha inicializado el objeto de origen de datos.  
  
 Se llamó a**ISSAsynchStatus::Abo at** en un conjunto de filas en el que previamente se llamó a **ITransaction::Commit** o a **ITransaction::Abo at** was previously called, and the rowset did not survive the commit o a abo at and is in a zombie state.  
  
 Se llamó a**ISSAsynchStatus::Abort** en un conjunto de filas que se canceló de forma asincrónica en su fase de inicialización. El conjunto de filas se encuentra en estado inerte.  
  
## <a name="remarks"></a>Notas  
 Al anular la inicialización de un conjunto de filas u objeto de origen de datos, se podría dejar el conjunto de filas u objeto de origen de datos en un estado zombi, de forma que todos los métodos distintos de los métodos **IUnknown** devuelvan un valor E_UNEXPECTED. Si esto sucede, la única acción posible para el consumidor es liberar el conjunto de filas u objeto de origen de datos.  
  
 Llamando a **ISSAsynchStatus::Abort** y pasando un valor para *eOperation* distinto de DBASYNCHOP_OPEN, devuelve S_OK. Esto no implica que la operación se haya completado o cancelado.  
  
## <a name="see-also"></a>Vea también  
 [Realizar operaciones asincrónicas](../../relational-databases/native-client/features/performing-asynchronous-operations.md)  
  
  
