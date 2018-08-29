---
title: Sys.internal_partitions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- Azure SQL Database
- SQL Server 2016 Preview
dev_langs:
- TSQL
ms.assetid: 0262df2b-5ba7-4715-b17b-3d9ce470a38e
caps.latest.revision: 13
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 23d59741ab513bb7fad6dee396b6e108d6a43337
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43058308"
---
# <a name="sysinternalpartitions-transact-sql"></a>Sys.internal_partitions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Devuelve una fila para cada conjunto de filas que realiza un seguimiento de los datos internos para los índices de almacén de columnas en las tablas basadas en disco. Estos conjuntos de filas son internas a los índices de almacén de columnas y pista eliminar filas, las asignaciones de grupo de filas y delta almacenan grupos de filas. Realizan el seguimiento de datos para cada uno para cada partición de tabla; cada tabla tiene al menos una partición. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vuelve a crear los conjuntos de filas cada vez que vuelve a generar el índice de almacén de columnas.   
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|partition_id|**bigint**|Id. de partición para esta partición. Es único en la base de datos.|  
|object_id|**int**|Id. de objeto para la tabla que contiene la partición.|  
|index_id|**int**|Id. de índice para el índice de almacén de columnas definido en la tabla.<br /><br /> 1 = índice agrupado<br /><br /> 2 = índice no agrupado de almacén de columnas|  
|partition_number|**int**|El número de partición.<br /><br /> 1 = la primera partición de una tabla con particiones, o la partición única de una tabla sin particiones.<br /><br /> 2 = segunda partición y así sucesivamente.|  
|internal_object_type|**tinyint**|Objetos de conjunto de filas que realizan el seguimiento de los datos internos para el índice de almacén de columnas.<br /><br /> 2 = COLUMN_STORE_DELETE_BITMAP<br /><br /> 3 = COLUMN_STORE_DELTA_STORE<br /><br /> 4 = COLUMN_STORE_DELETE_BUFFER<br /><br /> 5 = COLUMN_STORE_MAPPING_INDEX|  
|internal_object_type_desc|**nvarchar(60)**|COLUMN_STORE_DELETE_BITMAP – este índice de mapa de bits realiza un seguimiento de las filas que se marcan como eliminadas del almacén de columnas. El mapa de bits es para cada grupo de filas, ya que las particiones pueden tener filas en varios grupos de filas. Las filas son que están siendo físicamente presente y ocupando espacio en el almacén de columnas.<br /><br /> COLUMN_STORE_DELTA_STORE: grupos de almacenes de filas, llama a los grupos de filas, que no se han comprimido en almacenamiento en columnas. Cada partición de tabla puede tener cero o más grupos de filas de almacén delta.<br /><br /> COLUMN_STORE_DELETE_BUFFER: para mantener las eliminaciones para los índices de almacén de columnas no agrupado actualizable. Cuando una consulta elimina una fila de la tabla subyacente del almacén de filas, el búfer de eliminación realiza un seguimiento de la eliminación del almacén de columnas. Cuando el número de filas eliminadas supera 1048576, se combinan en el mapa de bits de eliminación por subproceso del motor de tupla en segundo plano o por un comando Reorganize explícito.  En cualquier momento determinado, la unión del mapa de bits de eliminación y el búfer de eliminación representa las filas eliminadas todas.<br /><br /> COLUMN_STORE_MAPPING_INDEX – se utiliza únicamente cuando el índice de almacén de columnas agrupado tiene un índice no clúster secundario. Esto asigna las claves de índice no agrupado para el grupo de filas correcta y el identificador de fila en el almacén de columnas. Solo almacena las claves para las filas que se mueven a un grupo de filas distinta; Esto ocurre cuando se comprime un grupo de filas delta al almacén de columnas, y cuando una operación de combinación combina las filas de dos grupos de filas diferentes.|  
|Row_group_id|**int**|Identificador para el grupo de filas de almacén delta. Cada partición de tabla puede tener cero o más grupos de filas de almacén delta.|  
|hobt_id|**bigint**|Identificador del objeto de conjunto de filas interno. Se trata de una buena clave para combinarse con otras DMV para obtener más información acerca de las características físicas del conjunto de filas interno.|  
|rows|**bigint**|Número aproximado de filas de esta partición.|  
|data_compression|**tinyint**|El estado de compresión para el conjunto de filas:<br /><br /> 0 = NONE<br /><br /> 1 = ROW<br /><br /> 2 = PAGE|  
|data_compression_desc|**nvarchar(60)**|El estado de compresión para cada partición. Los valores posibles para las tablas de almacén de filas son NONE, ROW y PAGE. Los valores posibles para tablas de almacén de columnas son COLUMNSTORE y COLUMNSTORE_ARCHIVE.|  
  
## <a name="permissions"></a>Permisos  
 Debe pertenecer al rol **public** . Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="general-remarks"></a>Notas generales  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vuelve a crear nuevos índices de almacén de columnas interno cada vez que crea o regenera un índice de almacén de columnas.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-view-all-of-the-internal-rowsets-for-a-table"></a>A. Ver todos los conjuntos de filas interno para una tabla  
 En este ejemplo devuelve todos los conjuntos de filas del almacén de columnas interno para una tabla. También puede usar el hobt_id para obtener más información sobre el conjunto de filas específica.  
  
```  
SELECT i.object_id, i.index_id, i.name, p.hobt_id, p.internal_object_type_id, p.internal_object_type_desc  
FROM sys.internal_partitions AS p  
JOIN sys.indexes AS i  
on i.object_id = p.object_id  
WHERE p.object_id = OBJECT_ID ( '<table name' ) ;  
```  
  
## <a name="see-also"></a>Vea también  
 [Object Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  (Vistas de catálogo de objetos [Transact-SQL])  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Preguntas frecuentes sobre consultas del catálogo de sistema de SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
