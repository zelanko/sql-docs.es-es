---
title: 'Issasynchstatus:: Waitforasynchcompletion (OLE DB) | Documentos de Microsoft'
description: ISSAsynchStatus::WaitForAsynchCompletion (OLE DB)
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
- ISSAsynchStatus::WaitForAsynchCompletion (OLE DB)
apitype: COM
helpviewer_keywords:
- WaitForAsynchCompletion method
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: e8d862ab9bde6a57a7f63deb46af7688d94b2586
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35305824"
---
# <a name="issasynchstatuswaitforasynchcompletion-ole-db"></a>ISSAsynchStatus::WaitForAsynchCompletion (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  Espera hasta que la operación que se ejecuta de forma asincrónica haya finalizado o hasta que se produzca un tiempo de espera.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
HRESULT WaitForAsynchCompletion(   
        DWORD dwMillisecTimeOut);  
```  
  
## <a name="arguments"></a>Argumentos  
 *dwMillisecTimeOut*[entrada]  
 Tiempo de espera en milisegundos.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 S_OK  
 El método se ha llevado a cabo de forma correcta.  
  
 E_UNEXPECTED  
 Un conjunto de filas está en un estado no usado porque **ITransaction:: Commit** o **ITransaction:: Abort** se ha llamado o el conjunto de filas se canceló durante su fase de inicialización.  
  
 DB_E_CANCELED  
 Procesamiento asincrónico se canceló durante la inicialización de objeto de origen de datos o rellenado conjunto de filas.  
  
 DB_S_ASYNCHRONOUS  
 La operación todavía no se ha completado aunque se ha alcanzado el tiempo de espera especificado.  
  
> [!NOTE]  
>  Además de los valores de código de retorno enumerados anteriormente, el método **ISSAsynchStatus::WaitForAsynchCompletion** también admite los valores de código de retorno que devuelven los métodos **ICommand::Execute** e **IDBInitialize::Initialize** de OLEDB básicos.  
  
## <a name="remarks"></a>Notas  
 No se devolverá el método **ISSAsynchStatus::WaitForAsynchCompletion** hasta que haya transcurrido el valor de tiempo de espera (en milisegundos) o se haya completado la operación pendiente. El objeto **Command** incluye una propiedad **CommandTimeout** que controla el número de segundos durante los que se ejecutará una consulta antes de que se exceda el tiempo de espera. El **CommandTimeout** propiedad se omitirá si se usa junto con **issasynchstatus:: Waitforasynchcompletion** método.  
  
 La propiedad de tiempo de espera se omite en las operaciones asincrónicas. El parámetro de tiempo de espera de **ISSAsynchStatus::WaitForAsynchCompletion** especifica el tiempo máximo que debe transcurrir antes de que se devuelva el control al autor de la llamada. Si este tiempo de espera expira, se devolverá DB_S_ASYNCHRONOUS. Los tiempos de espera nunca cancelan las operaciones asincrónicas. Si la aplicación necesita cancelar una operación asincrónica que no se ha completado en un período de tiempo de espera, debe esperar a que finalice el tiempo de espera y, a continuación, cancelar explícitamente la operación si se devuelve DB_S_ASYNCHRONOUS.  
  
> [!NOTE]  
>  Cuando se utilizan los componentes de servicio OLE DB, se puede devolver S_OK cuando se espera DB_S_ASYNCHRONOUS, por lo que las aplicaciones deben llamar a [issasynchstatus:: GetStatus](../../oledb/ole-db-interfaces/issasynchstatus-getstatus-ole-db.md) para comprobar la finalización cuando se devuelve S_OK o DB_S_ASYNCHRONOUS.  
  
 Si el valor *dwMillisecTimeOut* se establece en INFINITE, el método **ISSAsynchStatus::WaitForAsynchCompletion** se bloquea hasta que se completa la operación. Si el valor *dwMillisecTimeOut* se establece en 0, el método se devolverá inmediatamente con el estado de la operación pendiente. Si el tiempo de espera expira antes de que la operación se completa, se devolverá DB_S_ASYNCHRONOUS.  
  
 Si la operación se completa antes de que el tiempo de espera expire, el HRESULT devuelto será el HRESULT devuelto por la operación (el HRESULT que se habría devuelto si la operación se hubiese realizado de forma sincrónica).  
  
 Además, se ha agregado la propiedad SSPROP_ISSAsynchStatus al conjunto de propiedades DBPROPSET_SQLSERVERROWSET. Los proveedores que admiten el [ISSAsynchStatus](../../oledb/ole-db-interfaces/issasynchstatus-ole-db.md) interfaz debe implementar esta propiedad con un valor de VARIANT_TRUE.  
  
## <a name="see-also"></a>Vea también  
 [Realizar las operaciones asincrónicas](../../oledb/features/performing-asynchronous-operations.md)   
 [ISSAsynchStatus &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/issasynchstatus-ole-db.md)  
  
  
