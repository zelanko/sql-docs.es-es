---
title: Conjuntos de filas de esquema OLE DB | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- schema rowsets [OLE DB]
- schema rowsets [Analysis Services], OLE DB
- OLE DB schema rowsets
- rowsets [Analysis Services], OLE DB
ms.assetid: ca2ee87a-ba04-4501-9125-33934c58ab31
caps.latest.revision: "37"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 10a60e9e3696076a4e3672e7bcb5037f362f161b
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="ole-db-schema-rowsets"></a>Conjuntos de filas de esquema OLE DB
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Los siguientes conjuntos de filas de esquema de OLE DB son compatibles con el [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XML para el proveedor de Analysis (XMLA). Use la **DISCOVER_ENUMERATORS** conjunto de filas con el [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) método para comprobar si un proveedor de origen de datos determinado admite un conjunto de filas.  
  
 También puede encontrar información detallada sobre estos conjuntos de filas buscando el tema sobre los conjuntos de filas de esquemas en la parte correspondiente a la referencia del programador OLE DB de MSDN® Library en el sitio web en [!INCLUDE[msCoName](../../../includes/msconame-md.md)].  
  
 En la tabla siguiente se describe este conjunto de filas de esquemas.  
  
|Conjunto de filas|Description|  
|------------|-----------------|  
|**DBSCHEMA_ASSERTIONS**|Identifica las aserciones que se definen en el catálogo y que posee un usuario determinado.|  
|[Conjunto de filas DBSCHEMA_CATALOGS](../../../analysis-services/schema-rowsets/ole-db/dbschema-catalogs-rowset.md) <sup>1</sup>|Identifica los atributos físicos asociados con los catálogos que son accesibles desde el sistema de administración de bases de datos (DBMS). En algunos sistemas, como [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Access, puede que haya solo un catálogo. En [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], este conjunto de filas enumera todos los catálogos (bases de datos) definidos en la base de datos del sistema.|  
|**DBSCHEMA_CHARACTER_SETS**|Identifica los juegos de caracteres definidos en el catálogo al que puede tener acceso un usuario determinado.|  
|**DBSCHEMA_CHECK_CONSTRAINTS**|Identifica las restricciones CHECK que se definen en el catálogo y que posee un usuario determinado.|  
|**DBSCHEMA_CHECK_CONSTRAINTS_BY_TABLE**|Identifica las restricciones CHECK para una tabla determinada, definida en un catálogo que posee un usuario determinado.|  
|**DBSCHEMA_COLLATIONS**|Identifica las intercalaciones de caracteres definidas en el catálogo al que puede tener acceso un usuario determinado.|  
|**DBSCHEMA_COLUMN_DOMAIN_USAGE**|Identifica las columnas definidas en el catálogo que dependen de un dominio definido en el catálogo y que pertenecen a un usuario determinado.|  
|**DBSCHEMA_COLUMN_PRIVILEGES**|Identifica los privilegios para columnas de las tablas definidas en el catálogo que están disponibles para un usuario determinado o que este concede.|  
|[Conjunto de filas DBSCHEMA_COLUMNS](../../../analysis-services/schema-rowsets/ole-db/dbschema-columns-rowset.md) <sup>1</sup>|Proporciona información de columna de todas las columnas que cumplen los criterios de restricción proporcionados.|  
|**DBSCHEMA_CONSTRAINT_COLUMN_USAGE**|Identifica las columnas que se usan en las restricciones referenciales, restricciones únicas, restricciones CHECK y aserciones definidas en el catálogo y que pertenecen a un usuario determinado.|  
|**DBSCHEMA_CONSTRAINT_TABLE_USAGE**|Identifica las tablas que se usan en usan las restricciones referenciales, restricciones únicas, restricciones CHECK y aserciones definidas en el catálogo y que pertenecen a un usuario determinado.|  
|**DBSCHEMA_FOREIGN_KEYS**|Identifica las columnas de clave externa definidas en el catálogo por un usuario determinado. Este conjunto de filas de esquemas se genera a partir de varias vistas de esquemas ISO por comodidad para los programadores que no usan SQL. Si se admite, este conjunto de filas de esquema debe estar sincronizada con las vistas ISO relacionadas (**REFERENTIAL_CONSTRAINTS** y **CONSTRAINT_COLUMN_USAGE**).|  
|**DBSCHEMA_INDEXES**|Identifica los índices que se definen en el catálogo y que posee un usuario determinado.|  
|**DBSCHEMA_KEY_COLUMN_USAGE**|Identifica las columnas que se definen en el catálogo y que un usuario determinado restringe como claves.|  
|**DBSCHEMA_PRIMARY_KEYS**|Identifica las columnas de clave principal definidas en el catálogo por un usuario determinado. Este conjunto de filas de esquemas se genera a partir de una vista de esquema ISO por comodidad para los programadores que no usan SQL. Si se admite, este conjunto de filas de esquema debe estar sincronizada con la vista ISO relacionada (**CONSTRAINT_COLUMN_USAGE**).|  
|**DBSCHEMA_PROCEDURE_COLUMNS**|Devuelve información sobre las columnas de los conjuntos de filas que devuelven los procedimientos.|  
|**DBSCHEMA_PROCEDURE_PARAMETERS**|Devuelve información sobre los parámetros y los códigos devueltos de los procedimientos.|  
|**DBSCHEMA_PROCEDURES**|Identifica los procedimientos que se definen en el catálogo y que posee un usuario determinado. Ésta es una extensión OLE DB.|  
|[Conjunto de filas DBSCHEMA_PROVIDER_TYPES](../../../analysis-services/schema-rowsets/ole-db/dbschema-provider-types-rowset.md) <sup>1</sup>|Identifica los tipos de datos (básicos) admitidos por el proveedor de datos.|  
|**DBSCHEMA_REFERENTIAL_CONSTRAINTS**|Identifica las restricciones referenciales que se definen en el catálogo y que posee un usuario determinado.|  
|**DBSCHEMA_SCHEMATA**|Identifica los esquemas que posee un usuario determinado.|  
|**DBSCHEMA_SQL_LANGUAGES**|Identifica los niveles, opciones y dialectos de compatibilidad que admiten los datos de procesamiento de la implementación SQL definidos en el catálogo.|  
|**DBSCHEMA_STATISTICS**|Identifica las estadísticas se definen en el catálogo y que posee un usuario determinado.<br /><br /> Esta tabla no está relacionado con la **TABLE_STATISTICS** conjunto de filas.|  
|**DBSCHEMA_TABLE_CONSTRAINTS**|Identifica las restricciones de tabla que se definen en el catálogo y que posee un usuario determinado.|  
|**DBSCHEMA_TABLE_PRIVILEGES**|Identifica los privilegios para las tablas definidas en el catálogo que están disponibles para un usuario determinado o que este concede.|  
|**DBSCHEMA_TABLE_STATISTICS**|Describe el conjunto de estadísticas disponible en tablas en el proveedor.<br /><br /> Este conjunto de filas no está relacionado con la **estadísticas** conjunto de filas.|  
|[Conjunto de filas DBSCHEMA_TABLES](../../../analysis-services/schema-rowsets/ole-db/dbschema-tables-rowset.md) <sup>1</sup>|Identifica los grupos de medida y dimensiones expuestos como tablas dentro de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|**DBSCHEMA_TABLES_INFO** <sup>1</sup>|Identifica las tablas (incluidas las vistas) definidas en el catálogo a las que puede tener acceso un usuario determinado.|  
|**DBSCHEMA_TRANSLATIONS**|Identifica las traducciones de caracteres definidas en el catálogo al que puede tener acceso un usuario determinado.|  
|**DBSCHEMA_TRUSTEE**|Enumera los administradores de confianza de un origen de datos.|  
|**DBSCHEMA_USAGE_PRIVILEGES**|Identifica la **uso** privilegios en los objetos que se definen en el catálogo y están disponibles en o concedido a un usuario determinado.|  
|**DBSCHEMA_VIEW_COLUMN_USAGE**|Identifica las vistas definidas en el catálogo a las que puede tener acceso un usuario determinado.|  
|**DBSCHEMA_VIEW_TABLE_USAGE**|Identifica las tablas de las que dependen las tablas vistas, definidas en el catálogo y que pertenecen a un usuario determinado.|  
|**DBSCHEMA_VIEWS**|Identifica las vistas definidas en el catálogo a las que puede tener acceso un usuario determinado.|  
  
 <sup>1</sup> indica conjuntos de filas de esquema admitidos por el proveedor de origen de datos MSOLAP para el [!INCLUDE[msCoName](../../../includes/msconame-md.md)] proveedor XMLA.  
  
## <a name="see-also"></a>Vea también  
 [Conjunto de filas DISCOVER_ENUMERATORS](../../../analysis-services/schema-rowsets/xml/discover-enumerators-rowset.md)   
 [Conjuntos de filas de esquema de Analysis Services](../../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)  
  
  
