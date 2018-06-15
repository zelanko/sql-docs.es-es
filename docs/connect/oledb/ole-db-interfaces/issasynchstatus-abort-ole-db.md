---
title: 'Issasynchstatus:: Abort (OLE DB) | Documentos de Microsoft'
description: ISSAsynchStatus::Abort (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ISSAsynchStatus::Abort (OLE DB)
apitype: COM
helpviewer_keywords:
- Abort method
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: a62b87d7c2d8d19ce1c5ee3542932b13c37fd056
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35305474"
---
# <a name="issasynchstatusabort-ole-db"></a>ISSAsynchStatus::Abort (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Cancela una operación que se ejecuta de forma asincrónica.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
HRESULT Abort(  
        HCHAPTER hChapter,  
        DBASYNCHOP eOperation);  
```  
  
## <a name="arguments"></a>Argumentos  
 *hChapter*[in]  
 El identificador del segmento para el que se anula la operación. Si el objeto que se llama no es un objeto de conjunto de filas o la operación no se aplica a un capítulo, el llamador debe establecer *hChapter* en DB_NULL_HCHAPTER.  
  
 *eOperation*[in]  
 Operación para anular. Debe utilizarse el siguiente valor:  
  
 DBASYNCHOP_OPEN—La solicitud para cancelar se aplica a la apertura o rellenado asincrónico de un conjunto de filas o a la inicialización asincrónica de un objeto de origen de datos.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 S_OK  
 Se procesó la solicitud para cancelar la operación asincrónica. No garantiza que se ha cancelado la operación en Sí. Para determinar si se canceló la operación, el consumidor debería llamar a [ISSAsynchStatus::GetStatus](../../oledb/ole-db-interfaces/issasynchstatus-getstatus-ole-db.md) y realizar una comprobación para DB_E_CANCELED; sin embargo, puede que no se devuelva en la llamada siguiente.  
  
 DB_E_CANTCANCEL  
 La operación asincrónica no puede cancelarse.  
  
 DB_E_CANCELED  
 La solicitud para anular la operación asincrónica se canceló durante las notificaciones. La operación todavía se está ejecutando de forma asincrónica.  
  
 E_FAIL  
 Se produjo un error específico del proveedor.  
  
 E_INVALIDARG  
 El *hChapter* parámetro no es DB_NULL_HCHAPTER o *eOperation* no es DBASYNCH_OPEN.  
  
 E_UNEXPECTED  
 **Issasynchstatus:: Abort** en un objeto de origen de datos en el que se llamó **IDBInitialize:: Initialize** todavía no se ha llamado o no se ha completado.  
  
 Se llamó a**ISSAsynchStatus::Abort** en un objeto de origen de datos en el que se llamó a **IDBInitialize::Initialize** pero se canceló posteriormente antes de la inicialización, o se ha superado el tiempo de espera. Todavía no se ha inicializado el objeto de origen de datos.  
  
 **Issasynchstatus:: Abort** en un conjunto de filas en el que se llamó **ITransaction:: Commit** o **ITransaction:: Abort** se ha llamado anteriormente, y el conjunto de filas no conservó la confirmación o anulación y es en un estado inerte.  
  
 Se llamó a**ISSAsynchStatus::Abort** en un conjunto de filas que se canceló de forma asincrónica en su fase de inicialización. El conjunto de filas se encuentra en estado inerte.  
  
## <a name="remarks"></a>Notas  
 Al anular la inicialización de un conjunto de filas u objeto de origen de datos, se podría dejar el conjunto de filas u objeto de origen de datos en un estado zombi, de forma que todos los métodos distintos de los métodos **IUnknown** devuelvan un valor E_UNEXPECTED. Si esto sucede, la única acción posible para el consumidor es liberar el conjunto de filas u objeto de origen de datos.  
  
 Llamando a **ISSAsynchStatus::Abort** y pasando un valor para *eOperation* distinto de DBASYNCHOP_OPEN, devuelve S_OK. Esto no implica que la operación se completó o canceló.  
  
## <a name="see-also"></a>Vea también  
 [Realizar operaciones asincrónicas](../../oledb/features/performing-asynchronous-operations.md)  
  
  
