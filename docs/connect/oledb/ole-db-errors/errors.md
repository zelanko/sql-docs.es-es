---
title: Errors | Microsoft Docs
description: Errores
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, errors
- OLE/COM errors
- errors [OLE DB]
- OLE DB error handling, about error handling
- OLE DB error handling
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: a9f937e130af664570b92b006a54d329b33b9e23
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66798138"
---
# <a name="errors"></a>Errores
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Los objetos OLE/COM notifican errores a través del código de retorno HRESULT de funciones de miembro de objeto. Una estructura OLE/COM HRESULT es una estructura empaquetada de bits. OLE proporciona macros que eliminan referencias a los miembros de la estructura.  
  
 OLE/COM especifica la interfaz **IErrorInfo**. La interfaz expone métodos como **GetDescription**. Esto permite a los clientes extraer detalles de error de servidores OLE/COM. OLE DB extiende **IErrorInfo** para admitir el retorno de varios paquetes de información de error en una ejecución de función de miembro único.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] puede devolver varios errores. Una aplicación puede recuperar los errores de servidor de uno en uno mediante una llamada a [IMultipleResults::GetResult](https://go.microsoft.com/fwlink/?LinkId=129630) combinada con ISQLErrorInfo e IErrorRecords.  
  
 El controlador OLE DB para SQL Server expone la interfaz **IErrorInfo** mejorada por registro de OLE DB, la interfaz **ISQLErrorInfo** personalizada y las interfaces de objeto de error [ISQLServerErrorInfo](https://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1) específicas del proveedor.  
  
 Para obtener información sobre cómo realizar un seguimiento de los errores, vea [Data Access Tracing](https://go.microsoft.com/fwlink/?LinkId=125805) (Seguimiento de acceso a datos). Para obtener información acerca de las mejoras de seguimiento de errores que agregó en [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], consulte [acceso a información de diagnóstico en el registro de eventos extendidos](../../oledb/features/accessing-diagnostic-information-in-the-extended-events-log.md).  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Códigos de retorno](../../oledb/ole-db-errors/return-codes.md)  
  
-   [Información en interfaces de error](../../oledb/ole-db-errors/information-in-error-interfaces.md)  
  
-   [Detalle del error de SQL Server](../../oledb/ole-db-errors/sql-server-error-detail.md)  
  
-   [Recuperar información sobre errores](../../oledb/ole-db-errors/retrieving-error-information.md)  
  
-   [Resultados del mensaje de SQL Server](../../oledb/ole-db-errors/sql-server-message-results.md)  
  
## <a name="see-also"></a>Consulte también  
 [Programación del controlador OLE DB para SQL Server](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
  
