---
title: ISSAsynchStatus (OLE DB) | Microsoft Docs
description: ISSAsynchStatus (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ISSAsynchStatus (OLE DB)
apitype: COM
helpviewer_keywords:
- ISSAsynchStatus interface
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 6c94fe229ab8b00ded7e0d32f45e6e2de8cdaaf4
ms.sourcegitcommit: 50838d7e767c61dd0b5e677b6833dd5c139552f2
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2018
ms.locfileid: "39105791"
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
  
  
