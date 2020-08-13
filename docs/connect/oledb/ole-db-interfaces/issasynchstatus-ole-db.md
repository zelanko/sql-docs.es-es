---
title: ISSAsynchStatus (controlador OLE DB) | Microsoft Docs
description: ISSAsynchStatus (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- ISSAsynchStatus (OLE DB)
apitype: COM
helpviewer_keywords:
- ISSAsynchStatus interface
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 75514d969f826374a52c3d441c7d75a63b31956e
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/28/2020
ms.locfileid: "87244262"
---
# <a name="issasynchstatus-ole-db"></a>ISSAsynchStatus (OLE DB)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  La interfaz **ISSAsynchStatus** expone la compatibilidad con las operaciones asincrónicas de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se trata de una interfaz opcional que se hereda de la interfaz de OLE DB **IDBAsynchStatus** principal. Además de los métodos **Abort** y **GetStatus** heredados de **IDBAsynchStatus**, **ISSAsynchStatus** proporciona un nuevo método que se usa para esperar hasta que una operación asincrónica se ha completado o se agota el tiempo de espera.  
  
|Método|Descripción|  
|------------|-----------------|  
|[ISSAsynchStatus::Abort &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/issasynchstatus-abort-ole-db.md)|Cancela una operación que se ejecuta de forma asincrónica.|  
|[ISSAsynchStatus::GetStatus &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/issasynchstatus-getstatus-ole-db.md)|Devuelve el estado de una operación de ejecución asincrónica.|  
|[ISSAsynchStatus::WaitForAsynchCompletion &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/issasynchstatus-waitforasynchcompletion-ole-db.md)|Espera hasta que la operación que se ejecuta de forma asincrónica se haya completado o hasta que se produzca un tiempo de espera.|  
  
## <a name="remarks"></a>Observaciones  
 La implementación de **ISSAsynchStatus** del método **ISSAsynchStatus::GetStatus** es la misma que el método **IDBAsynchStatus::GetStatus** salvo si se anula la inicialización de un objeto de origen de datos, se devuelve E_UNEXPECTED en lugar de DB_E_CANCELED (aunque **ISSAsynchStatus::WaitForAsynchCompletion** devuelve DB_E_CANCELED). Esto se debe a que el objeto de origen de datos no se queda en el estado habitual que sigue a una operación de anulación, de manera que se puedan intentar otras operaciones de inicialización.  
  
 Los métodos siguientes admiten el uso de ejecución asincrónica en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:  
  
-   **ICommand::Execute**  
  
-   **IOpenRowset::OpenRowset**  
  
-   **IMultipleResults::GetResult**  
  
## <a name="see-also"></a>Consulte también  
 [Interfaces &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md)    
 [Realizar operaciones asincrónicas](../../oledb/features/performing-asynchronous-operations.md)  
  
  
