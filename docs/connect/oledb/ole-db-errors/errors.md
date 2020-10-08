---
title: OLE DB Errors
description: Sepa cómo se devuelven errores en OLE DB Driver for SQL Server y cómo obtener información sobre ellos.
ms.custom: ''
ms.date: 05/06/2020
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 15b2001e7e6c0a747b77cb51df0bf38c17856d99
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/05/2020
ms.locfileid: "91727206"
---
# <a name="errors"></a>Errors
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Los objetos OLE/COM notifican errores a través del código de retorno HRESULT de funciones de miembro de objeto. Una estructura OLE/COM HRESULT es una estructura empaquetada de bits. OLE proporciona macros que eliminan referencias a los miembros de la estructura.  
  
 OLE/COM especifica la interfaz **IErrorInfo**. La interfaz expone métodos como **GetDescription**. Esto permite a los clientes extraer detalles de error de servidores OLE/COM. OLE DB extiende **IErrorInfo** para admitir el retorno de varios paquetes de información de error en una ejecución de función de miembro único.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] puede devolver varios errores. Una aplicación puede recuperar los errores de servidor de uno en uno mediante una llamada a [IMultipleResults::GetResult](/previous-versions/windows/desktop/ms721289(v=vs.85)) combinada con ISQLErrorInfo e IErrorRecords.  
  
 El controlador OLE DB para SQL Server expone la interfaz **IErrorInfo** mejorada por registro de OLE DB, la interfaz **ISQLErrorInfo** personalizada y las interfaces de objeto de error [ISQLServerErrorInfo](../ole-db-interfaces/isqlservererrorinfo-geterrorinfo-ole-db.md?view=sql-server-ver15) específicas del proveedor.  
  
 Para obtener información sobre cómo realizar un seguimiento de los errores, vea [Data Access Tracing](/previous-versions/sql/sql-server-2008/cc765421(v=sql.100)) (Seguimiento de acceso a datos). Para información sobre las mejoras en el seguimiento de errores agregadas en [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], consulte [Acceso a información de diagnóstico en el registro de eventos extendidos](../../oledb/features/accessing-diagnostic-information-in-the-extended-events-log.md).  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Códigos de retorno](../../oledb/ole-db-errors/return-codes.md)  
  
-   [Información en interfaces de error](../../oledb/ole-db-errors/information-in-error-interfaces.md)  
  
-   [Detalle del error de SQL Server](../../oledb/ole-db-errors/sql-server-error-detail.md)  
  
-   [Recuperar información sobre errores](../../oledb/ole-db-errors/retrieving-error-information.md)  
  
-   [Resultados del mensaje de SQL Server](../../oledb/ole-db-errors/sql-server-message-results.md)  
  
## <a name="see-also"></a>Consulte también  
 [Programación del controlador OLE DB para SQL Server](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
