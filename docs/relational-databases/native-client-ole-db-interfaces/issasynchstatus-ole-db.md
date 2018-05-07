---
title: ISSAsynchStatus (OLE DB) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-ole-db-interfaces
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
ms.assetid: c643f09f-9ccc-4d8b-9243-3cde86c2bd46
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 8e5a756b55d3a426e18f8b224659d42669ab89ac
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="issasynchstatus-ole-db"></a>ISSAsynchStatus (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  **ISSAsynchStatus** expone la compatibilidad para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] operaciones asincrónicas. Ésta es una interfaz opcional que se hereda de la interfaz de OLE DB **IDBAsynchStatus**principal. Además de los métodos **Abort** y **GetStatus** heredados de **IDBAsynchStatus**, **ISSAsynchStatus** proporciona un nuevo método que se usa para esperar hasta que una operación asincrónica se ha completado o se agota el tiempo de espera.  
  
|Método|Description|  
|------------|-----------------|  
|[Issasynchstatus:: Abort &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-abort-ole-db.md)|Cancela una operación que se ejecuta de forma asincrónica.|  
|[Issasynchstatus:: GetStatus &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-getstatus-ole-db.md)|Devuelve el estado de una operación de ejecución asincrónica.|  
|[Issasynchstatus:: Waitforasynchcompletion &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-waitforasynchcompletion-ole-db.md)|Espera hasta que la operación que se ejecuta de forma asincrónica se haya completado o hasta que se produzca un tiempo de espera.|  
  
## <a name="remarks"></a>Comentarios  
 La implementación de **ISSAsynchStatus** del método **ISSAsynchStatus::GetStatus** es la misma que el método **IDBAsynchStatus::GetStatus** salvo si se anula la inicialización de un objeto de origen de datos, se devuelve E_UNEXPECTED en lugar de DB_E_CANCELED (aunque **ISSAsynchStatus::WaitForAsynchCompletion** devuelve DB_E_CANCELED). Esto se debe a que el objeto de origen de datos no se queda en el estado habitual que sigue a una operación de anulación, de manera que se puedan intentar otras operaciones de inicialización.  
  
 Los métodos siguientes admiten el uso de ejecución asincrónica en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   **ICommand:: Execute**  
  
-   **IOpenRowset::OpenRowset**  
  
-   **IMultipleResults:: GetResult**  
  
## <a name="see-also"></a>Vea también  
 [Interfaces & #40; OLE DB & #41;](http://msdn.microsoft.com/library/34c33364-8538-45db-ae41-5654481cda93)   
 [Realizar operaciones asincrónicas](../../relational-databases/native-client/features/performing-asynchronous-operations.md)  
  
  
