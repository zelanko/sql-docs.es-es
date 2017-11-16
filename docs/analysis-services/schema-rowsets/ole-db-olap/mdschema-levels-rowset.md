---
title: Conjunto de filas MDSCHEMA_LEVELS | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: schema-rowsets
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- MDSCHEMA_LEVELS
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- MDSCHEMA_LEVELS rowset
ms.assetid: 4313e268-33f4-4e99-96d7-2ec26775c580
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8d9a56387365489615b6b7665dedb3edc7f367f6
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="mdschemalevels-rowset"></a>Conjunto de filas MDSCHEMA_LEVELS
  Describe cada nivel dentro de una jerarquía determinada.  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El **MDSCHEMA_LEVELS** filas contiene las columnas siguientes.  
  
|Nombre de columna|Indicador de tipo|Description|  
|-----------------|--------------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|Nombre del catálogo al que pertenece este nivel. **NULL** si el proveedor no admite catálogos.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|Nombre del esquema al que pertenece este nivel. **NULL** si el proveedor no admite esquemas.|  
|**RESTRICCIONES OBLIGATORIAS CUBE_NAME**|**DBTYPE_WSTR**|Nombre del cubo al que pertenece este nivel.|  
|**DIMENSION_UNIQUE_NAME**|**DBTYPE_WSTR**|Nombre único de la dimensión al que pertenece este nivel. Los proveedores que generan nombres únicos por calificación tienen delimitados todos los componentes del nombre.|  
|**HIERARCHY_UNIQUE_NAME**|**DBTYPE_WSTR**|Nombre único de la jerarquía. Si el nivel pertenece a más de una jerarquía, se incluye una fila por cada jerarquía a la que pertenece el miembro. Los proveedores que generan nombres únicos por calificación tienen delimitados todos los componentes del nombre.|  
|**LEVEL_NAME**|**DBTYPE_WSTR**|El nombre del nivel.|  
|**LEVEL_UNIQUE_NAME**|**DBTYPE_WSTR**|El nombre único con carácter de escape del nivel.|  
|**LEVEL_GUID**|**DBTYPE_GUID**|No compatible.|  
|**LEVEL_CAPTION**|**DBTYPE_WSTR**|Etiqueta o título asociado a la jerarquía. Se utiliza principalmente para la presentación. Si no existe ningún título, **LEVEL_NAME** se devuelve.|  
|**LEVEL_NUMBER**|**DBTYPE_UI4**|Distancia del nivel desde la raíz de la jerarquía. Nivel raíz es cero (**0)**.|  
|**LEVEL_CARDINALITY**|**DBTYPE_UI4**|Número de miembros del nivel.|  
|**LEVEL_TYPE**|**DBTYPE_I4**|Tipo de nivel:<br /><br /> **MDLEVEL_TYPE_GEO_CONTINENT** (**0x2001**)<br /><br /> **MDLEVEL_TYPE_GEO_REGION** (**0 x 2002**)<br /><br /> **MDLEVEL_TYPE_GEO_COUNTRY** (**0x2003**)<br /><br /> **MDLEVEL_TYPE_GEO_STATE_OR_PROVINCE** (**0x2004**)<br /><br /> **MDLEVEL_TYPE_GEO_COUNTY** (**0x2005**)<br /><br /> **MDLEVEL_TYPE_GEO_CITY** (**0x2006**)<br /><br /> **MDLEVEL_TYPE_GEO_POSTALCODE** (**0x2007**)<br /><br /> **MDLEVEL_TYPE_GEO_POINT** (**0x2008**)<br /><br /> **MDLEVEL_TYPE_ORG_UNIT** (**0x1011**)<br /><br /> **MDLEVEL_TYPE_BOM_RESOURCE** (**0x1012**)<br /><br /> **MDLEVEL_TYPE_QUANTITATIVE** (**0x1013**)<br /><br /> **MDLEVEL_TYPE_ACCOUNT** (**0x1014**)<br /><br /> **MDLEVEL_TYPE_CUSTOMER** (**0x1021**)<br /><br /> **MDLEVEL_TYPE_CUSTOMER_GROUP** (**0x1022**)<br /><br /> **MDLEVEL_TYPE_CUSTOMER_HOUSEHOLD** (**0x1023**)<br /><br /> **MDLEVEL_TYPE_PRODUCT** (**0x1031**)<br /><br /> **MDLEVEL_TYPE_PRODUCT_GROUP** (**0x1032**)<br /><br /> **MDLEVEL_TYPE_SCENARIO** (**0x1015**)<br /><br /> **MDLEVEL_TYPE_UTILITY** (**0x1016**)<br /><br /> **MDLEVEL_TYPE_PERSON** (**0x1041**)<br /><br /> **MDLEVEL_TYPE_COMPANY** (**0x1042**)<br /><br /> **MDLEVEL_TYPE_CURRENCY_SOURCE** (**0x1051**)<br /><br /> **MDLEVEL_TYPE_CURRENCY_DESTINATION** (**0x1052**)<br /><br /> **MDLEVEL_TYPE_CHANNEL** (**0x1061**)<br /><br /> **MDLEVEL_TYPE_REPRESENTATIVE** (**0x1062**)<br /><br /> **MDLEVEL_TYPE_PROMOTION** (**0x1071**)|  
|**DESCRIPTION**|**DBTYPE_WSTR**|Descripción legible del nivel. NULL si no existe ninguna descripción.|  
|**CUSTOM_ROLLUP_SETTINGS**|**DBTYPE_I4**|Un mapa de bits que especifica las opciones de resumen personalizado:<br /><br /> **MDLEVELS_CUSTOM_ROLLUP_EXPRESSION** (**0 x 01**) indica una expresión existe para este nivel. (Desusado)<br /><br /> **MDLEVELS_CUSTOM_ROLLUP_COLUMN** (**0 x 02**) indica que hay una columna de resumen personalizado para este nivel.<br /><br /> **MDLEVELS_SKIPPED_LEVELS** (**0 x 04**) indica que hay un nivel omitido asociado a los miembros de este nivel.<br /><br /> **MDLEVELS_CUSTOM_MEMBER_PROPERTIES** (**0 x 08**) indica que los miembros del nivel tienen propiedades de miembro personalizadas.<br /><br /> **MDLEVELS_UNARY_OPERATOR** (**0 x 10**) indica que los miembros del nivel tienen operadores unarios.|  
|**LEVEL_UNIQUE_SETTINGS**|**DBTYPE_I4**|Un mapa de bits que especifica las columnas que contienen valores únicos, si el nivel solamente tiene miembros con nombres o claves únicos. El archivo Msmd.h define las constantes de valor de bit siguientes para este mapa de bits:<br /><br /> **MDDIMENSIONS_MEMBER_KEY_UNIQUE** (**1**)<br /><br /> **MDDIMENSIONS_MEMBER_NAME_UNIQUE** (**2**)<br /><br /> <br /><br /> Tenga en cuenta que siempre es única en la clave [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. El nombre será único si el valor del atributo es **UniqueInDimension** o **UniqueInAttribute**|  
|**LEVEL_IS_VISIBLE**|**DBTYPE_BOOL**|Un valor booleano que indica si el nivel está visible.<br /><br /> Siempre devuelve Verdadero. Si el nivel no está visible, no se incluirá en el conjunto de filas de esquema.|  
|**LEVEL_ORDERING_PROPERTY**|**DBTYPE_WSTR**|El identificador del atributo en que está ordenado el nivel.|  
|**LEVEL_DBTYPE**|**DBTYPE_I4**|El **DBTYPE** enumeración de la columna de clave de miembro que se utiliza para el atributo de nivel.<br /><br /> Null si las claves concatenadas se utilizan como columna de clave de miembro.|  
|**LEVEL_MASTER_UNIQUE_NAME**|**DBTYPE_WSTR**|Siempre devuelve NULL.|  
|**LEVEL_NAME_SQL_COLUMN_NAME**|**DBTYPE_WSTR**|Representación SQL de los nombres de miembros del nivel.|  
|**LEVEL_KEY_SQL_COLUMN_NAME**|**DBTYPE_WSTR**|La representación SQL de los valores de clave de miembro del nivel.|  
|**LEVEL_UNIQUE_NAME_SQL_COLUMN_NAME**|**DBTYPE_WSTR**|La representación SQL de los nombres únicos de miembro.|  
|**LEVEL_ATTRIBUTE_HIERARCHY_NAME**|**DBTYPE_WSTR**|Nombre de la jerarquía de atributo que proporciona el origen del nivel.|  
|**LEVEL_KEY_CARDINALITY**|**DBTYPE_UI2**|Número de columnas de la clave de nivel.|  
|**LEVEL_ORIGIN**|**DBTYPE_UI2**|Mapa de bits que define cómo se originó el nivel:<br /><br /> **MD_ORIGIN_USER_DEFINED** identifica los niveles en una jerarquía definida por el usuario.<br /><br /> **MD_ORIGIN_ATTRIBUTE** identifica los niveles en una jerarquía de atributo.<br /><br /> **MD_ORIGIN_KEY_ATTRIBUTE** identifica los niveles de una jerarquía de atributo de clave.<br /><br /> **MD_ORIGIN_INTERNAL** identifica los niveles en las jerarquías de atributo que no están habilitadas.|  
  
 El conjunto de filas está ordenado en **CATALOG_NAME**, **SCHEMA_NAME**, **restricciones obligatorias CUBE_NAME**, **DIMENSION_UNIQUE_NAME**, **HIERARCHY_ UNIQUE_NAME**, **LEVEL_NUMBER**.  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El **MDSCHEMA_LEVELS** se puede restringir el conjunto de filas en las columnas enumeradas en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**RESTRICCIONES OBLIGATORIAS CUBE_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**DIMENSION_UNIQUE_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**HIERARCHY_UNIQUE_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**LEVEL_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**LEVEL_UNIQUE_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**LEVEL_ORIGIN**|**DBTYPE_UI2**|(Opcional) Una restricción predeterminada tiene efecto en **MD_USER_DEFINED** y **MD_SYSTEM_ENABLED**|  
|**CUBE_SOURCE**|**DBTYPE_UI2**|(Opcional) La restricción predeterminada es un valor de 1. Un mapa de bits con uno de los siguientes valores válidos:<br /><br /> 1 CUBO<br /><br /> 2 DIMENSIÓN|  
|**LEVEL_VISIBILITY**|**DBTYPE_UI2**|(Opcional) La restricción predeterminada es un valor de 1. Un mapa de bits con uno de los siguientes valores:<br /><br /> 1 Visible<br /><br /> 2 no visible|  
  
## <a name="see-also"></a>Vea también  
 [OLE DB para OLAP Schema Rowsets](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  

