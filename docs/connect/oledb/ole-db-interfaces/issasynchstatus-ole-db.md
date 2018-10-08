---
title: ISSAsynchStatus (OLE DB) | Microsoft Docs
description: ISSAsynchStatus (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: reference
apiname:
- ISSAsynchStatus (OLE DB)
apitype: COM
helpviewer_keywords:
- ISSAsynchStatus interface
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: ebb48a520bc318076d2a0808fb4663974b7941a5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47833253"
---
# <a name="issasynchstatus-ole-db"></a>ISSAsynchStatus (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  La interfaz **ISSAsynchStatus** expone la compatibilidad con las operaciones asincrónicas de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se trata de una interfaz opcional que se hereda de la interfaz de OLE DB **IDBAsynchStatus** principal. Además de los métodos **Abort** y **GetStatus** heredados de **IDBAsynchStatus**, **ISSAsynchStatus** proporciona un nuevo método que se usa para esperar hasta que una operación asincrónica se ha completado o se agota el tiempo de espera.  
  
|Método|Descripción|  
|------------|-----------------|  
|[Issasynchstatus:: Abort &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/issasynchstatus-abort-ole-db.md)|Cancela una operación que se ejecuta de forma asincrónica.|  
|[Issasynchstatus:: GetStatus &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/issasynchstatus-getstatus-ole-db.md)|Devuelve el estado de una operación de ejecución asincrónica.|  
|[Issasynchstatus:: Waitforasynchcompletion &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/issasynchstatus-waitforasynchcompletion-ole-db.md)|Espera hasta que la operación que se ejecuta de forma asincrónica se haya completado o hasta que se produzca un tiempo de espera.|  
  
## <a name="remarks"></a>Notas  
 La implementación de **ISSAsynchStatus** del método **ISSAsynchStatus::GetStatus** es la misma que el método **IDBAsynchStatus::GetStatus** salvo si se anula la inicialización de un objeto de origen de datos, se devuelve E_UNEXPECTED en lugar de DB_E_CANCELED (aunque **ISSAsynchStatus::WaitForAsynchCompletion** devuelve DB_E_CANCELED). Esto se debe a que el objeto de origen de datos no se queda en el estado habitual que sigue a una operación de anulación, de manera que se puedan intentar otras operaciones de inicialización.  
  
 Los métodos siguientes admiten el uso de ejecución asincrónica en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:  
  
-   **ICommand::Execute**  
  
-   **IOpenRowset::OpenRowset**  
  
-   **IMultipleResults::GetResult**  
  
## <a name="see-also"></a>Ver también  
 [Interfaces &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md)    
 [Realizar operaciones asincrónicas](../../oledb/features/performing-asynchronous-operations.md)  
  
  
