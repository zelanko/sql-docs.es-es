---
title: Detección de metadatos | Microsoft Docs
description: Obtenga información sobre cómo las mejoras en la detección de metadatos permiten que las aplicaciones de OLE DB Driver for SQL Server garanticen la compatibilidad de los metadatos.
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: adccad510a1126173e44015e6ecd60a90a32550b
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/25/2020
ms.locfileid: "88861478"
---
# <a name="metadata-discovery"></a>Detección de metadatos
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  La mejora de la detección de metadatos en [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] permite que las aplicaciones del controlador OLE DB para SQL Server tengan la seguridad de que los metadatos de parámetro o columna que se devuelven de la ejecución de una consulta son idénticos o compatibles con el formato de los metadatos especificados antes de ejecutar la consulta. Se producirá un error si los metadatos devueltos tras la ejecución de la consulta no son compatibles con el formato de los metadatos especificados antes de la ejecución de la consulta.  
  
 En el caso de bcp y las interfaces IBCPSession e IBCPSession2, ahora se puede especificar una lectura diferida (detección de metadatos diferida) para evitar la detección de metadatos en operaciones de salida de consulta. De este modo, mejora el rendimiento y se eliminan los errores de detección de metadatos.  
  
 Si desarrolla una aplicación mediante el controlador OLE DB para SQL Server pero se conecta a una versión de servidor anterior a [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], la funcionalidad de detección de metadatos se corresponderá con la versión del servidor.  
  
## <a name="remarks"></a>Observaciones   
 Las funciones miembro de OLE DB siguientes se han perfeccionado en [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] para proporcionar una detección de metadatos mejorada:  
  
-   IColumnsInfo::GetColumnInfo  
  
-   IColumnsRowset::GetColumnsRowset  
  
-   ICommandWithParameters::GetParameterInfo (consulte [ICommandWithParameters](../../oledb/ole-db-interfaces/icommandwithparameters.md) para más información)  
  
 También percibirá una mejora del rendimiento si especifica el formato de metadatos mediante IBCPSession::BCPSetBulkMode.  
  
 La detección de metadatos mejorada en OLE DB Driver for SQL Server es posible debido a la adición de dos procedimientos almacenados de [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]:  
  
-   sp_describe_first_result_set  
  
-   sp_describe_undeclared_parameters  
  
## <a name="see-also"></a>Consulte también  
 [Controlador OLE DB para las características de SQL Server](../../oledb/features/oledb-driver-for-sql-server-features.md)  
  
  
