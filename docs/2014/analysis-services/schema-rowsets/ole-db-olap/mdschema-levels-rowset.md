---
title: Conjunto de filas MDSCHEMA_LEVELS | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MDSCHEMA_LEVELS
topic_type:
- apiref
helpviewer_keywords:
- MDSCHEMA_LEVELS rowset
ms.assetid: 4313e268-33f4-4e99-96d7-2ec26775c580
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9491143a33dbd68ab0f0ea9cb3745f1e784879b8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48191813"
---
# <a name="mdschemalevels-rowset"></a>Conjunto de filas MDSCHEMA_LEVELS
  Describe cada nivel dentro de una jerarquía determinada.  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El `MDSCHEMA_LEVELS` conjunto de filas contiene las siguientes columnas.  
  
|Nombre de columna|Indicador de tipo|Longitud|Descripción|  
|-----------------|--------------------|------------|-----------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`||Nombre del catálogo al que pertenece este nivel. `NULL` si el proveedor no admite catálogos.|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`||Nombre del esquema al que pertenece este nivel. Su valor es `NULL` si el proveedor no admite esquemas.|  
|`CUBE_NAME`|`DBTYPE_WSTR`||Nombre del cubo al que pertenece este nivel.|  
|`DIMENSION_UNIQUE_NAME`|`DBTYPE_WSTR`||Nombre único de la dimensión al que pertenece este nivel. Los proveedores que generan nombres únicos por calificación tienen delimitados todos los componentes del nombre.|  
|`HIERARCHY_UNIQUE_NAME`|`DBTYPE_WSTR`||Nombre único de la jerarquía. Si el nivel pertenece a más de una jerarquía, se incluye una fila por cada jerarquía a la que pertenece el miembro. Los proveedores que generan nombres únicos por calificación tienen delimitados todos los componentes del nombre.|  
|`LEVEL_NAME`|`DBTYPE_WSTR`||El nombre del nivel.|  
|`LEVEL_UNIQUE_NAME`|`DBTYPE_WSTR`||El nombre único con carácter de escape del nivel.|  
|`LEVEL_GUID`|`DBTYPE_GUID`||No compatible.|  
|`LEVEL_CAPTION`|`DBTYPE_WSTR`||Etiqueta o título asociado a la jerarquía. Se utiliza principalmente para la presentación. Si no existe ningún título, se devuelve `LEVEL_NAME`.|  
|`LEVEL_NUMBER`|`DBTYPE_UI4`||Distancia del nivel desde la raíz de la jerarquía. El nivel raíz es cero (`0)`.|  
|`LEVEL_CARDINALITY`|`DBTYPE_UI4`||Número de miembros del nivel.|  
|`LEVEL_TYPE`|`DBTYPE_I4`||Tipo de nivel:<br /><br /> -   `MDLEVEL_TYPE_GEO_CONTINENT` (`0x2001`)<br />-   `MDLEVEL_TYPE_GEO_REGION` (`0x2002`)<br />-   `MDLEVEL_TYPE_GEO_COUNTRY` (`0x2003`)<br />-   `MDLEVEL_TYPE_GEO_STATE_OR_PROVINCE` (`0x2004`)<br />-   `MDLEVEL_TYPE_GEO_COUNTY` (`0x2005`)<br />-   `MDLEVEL_TYPE_GEO_CITY` (`0x2006`)<br />-   `MDLEVEL_TYPE_GEO_POSTALCODE` (`0x2007`)<br />-   `MDLEVEL_TYPE_GEO_POINT` (`0x2008`)<br />-   `MDLEVEL_TYPE_ORG_UNIT` (`0x1011`)<br />-   `MDLEVEL_TYPE_BOM_RESOURCE` (`0x1012`)<br />-   **MDLEVEL_TYPE_QUANTITATIVE** (`0x1013`)<br />-   `MDLEVEL_TYPE_ACCOUNT` (`0x1014`)<br />-   `MDLEVEL_TYPE_CUSTOMER` (`0x1021`)<br />-   `MDLEVEL_TYPE_CUSTOMER_GROUP` (`0x1022`)<br />-   `MDLEVEL_TYPE_CUSTOMER_HOUSEHOLD` (`0x1023`)<br />-   `MDLEVEL_TYPE_PRODUCT` (`0x1031`)<br />-   `MDLEVEL_TYPE_PRODUCT_GROUP` (`0x1032`)<br />-   `MDLEVEL_TYPE_SCENARIO` (`0x1015`)<br />-   `MDLEVEL_TYPE_UTILITY` (`0x1016`)<br />-   `MDLEVEL_TYPE_PERSON` (`0x1041`)<br />-   `MDLEVEL_TYPE_COMPANY` (`0x1042`)<br />-   `MDLEVEL_TYPE_CURRENCY_SOURCE` (`0x1051`)<br />-   `MDLEVEL_TYPE_CURRENCY_DESTINATION` (`0x1052`)<br />-   `MDLEVEL_TYPE_CHANNEL` (`0x1061`)<br />-   `MDLEVEL_TYPE_REPRESENTATIVE` (`0x1062`)<br />-   `MDLEVEL_TYPE_PROMOTION` (`0x1071`)|  
|`DESCRIPTION`|`DBTYPE_WSTR`||Descripción legible del nivel. NULL si no existe ninguna descripción.|  
|`CUSTOM_ROLLUP_SETTINGS`|`DBTYPE_I4`||Un mapa de bits que especifica las opciones de resumen personalizado:<br /><br /> -   `MDLEVELS_CUSTOM_ROLLUP_EXPRESSION` (`0x01`) indica una expresión existe para este nivel. (Desusado)<br />-   `MDLEVELS_CUSTOM_ROLLUP_COLUMN` (`0x02`) indica que hay una columna de resumen personalizado para este nivel.<br />-   `MDLEVELS_SKIPPED_LEVELS` (`0x04`) indica que hay un nivel omitido asociado con los miembros de este nivel.<br />-   `MDLEVELS_CUSTOM_MEMBER_PROPERTIES` (`0x08`) indica que los miembros del nivel tienen propiedades de miembro personalizadas.<br />-   `MDLEVELS_UNARY_OPERATOR` (`0x10`) indica que los miembros del nivel tienen operadores unarios.|  
|`LEVEL_UNIQUE_SETTINGS`|`DBTYPE_I4`||Un mapa de bits que especifica las columnas que contienen valores únicos, si el nivel solamente tiene miembros con nombres o claves únicos. El archivo Msmd.h define las constantes de valor de bit siguientes para este mapa de bits:<br /><br /> -   `MDDIMENSIONS_MEMBER_KEY_UNIQUE` (`1`)<br />-   `MDDIMENSIONS_MEMBER_NAME_UNIQUE` (`2`)<br /><br /> La clave siempre es única en [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. El nombre será único si el valor en el atributo es `UniqueInDimension` o `UniqueInAttribute`|  
|`LEVEL_IS_VISIBLE`|`DBTYPE_BOOL`||Un valor booleano que indica si el nivel está visible.<br /><br /> Siempre devuelve Verdadero. Si el nivel no está visible, no se incluirá en el conjunto de filas de esquema.|  
|`LEVEL_ORDERING_PROPERTY`|`DBTYPE_WSTR`||El identificador del atributo en que está ordenado el nivel.|  
|`LEVEL_DBTYPE`|`DBTYPE_I4`||La enumeración `DBTYPE` de la columna de clave de miembro que se utiliza para el atributo de nivel.<br /><br /> Null si las claves concatenadas se utilizan como columna de clave de miembro.|  
|`LEVEL_MASTER_UNIQUE_NAME`|`DBTYPE_WSTR`||Siempre devuelve NULL.|  
|`LEVEL_NAME_SQL_COLUMN_NAME`|`DBTYPE_WSTR`||Representación SQL de los nombres de miembros del nivel.|  
|`LEVEL_KEY_SQL_COLUMN_NAME`|`DBTYPE_WSTR`||La representación SQL de los valores de clave de miembro del nivel.|  
|`LEVEL_UNIQUE_NAME_SQL_COLUMN_NAME`|`DBTYPE_WSTR`||La representación SQL de los nombres únicos de miembro.|  
|`LEVEL_ATTRIBUTE_HIERARCHY_NAME`|`DBTYPE_WSTR`||Nombre de la jerarquía de atributo que proporciona el origen del nivel.|  
|`LEVEL_KEY_CARDINALITY`|`DBTYPE_UI2`||Número de columnas de la clave de nivel.|  
|`LEVEL_ORIGIN`|`DBTYPE_UI2`||Mapa de bits que define cómo se originó el nivel:<br /><br /> -   `MD_ORIGIN_USER_DEFINED` identifica los niveles en una jerarquía definida por el usuario.<br />-   `MD_ORIGIN_ATTRIBUTE` identifica los niveles en una jerarquía de atributo.<br />-   `MD_ORIGIN_KEY_ATTRIBUTE` identifica los niveles de una jerarquía de atributo clave.<br />-   `MD_ORIGIN_INTERNAL` identifica los niveles en las jerarquías de atributo que no están habilitadas.|  
  
 El conjunto de filas se ordena en `CATALOG_NAME`, `SCHEMA_NAME`, `CUBE_NAME`, `DIMENSION_UNIQUE_NAME`, `HIERARCHY_UNIQUE_NAME`, `LEVEL_NUMBER`.  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El `MDSCHEMA_LEVELS` conjunto de filas puede tener restricciones en las columnas enumeradas en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`CUBE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`DIMENSION_UNIQUE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`HIERARCHY_UNIQUE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`LEVEL_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`LEVEL_UNIQUE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`LEVEL_ORIGIN`|`DBTYPE_UI2`|(Opcional) Una restricción predeterminada está en vigor `MD_USER_DEFINED` y `MD_SYSTEM_ENABLED`|  
|`CUBE_SOURCE`|`DBTYPE_UI2`|(Opcional) Mapa de bits con uno de los siguientes valores válidos:<br /><br /> -1 CUBO<br />-DIMENSIÓN DE 2<br /><br /> La restricción predeterminada es un valor de 1.|  
|`LEVEL_VISIBILITY`|`DBTYPE_UI2`|(Opcional) Mapa de bits con uno de los siguientes valores:<br /><br /> -1 Visible<br />-2 no visible<br /><br /> La restricción predeterminada es un valor de 1.|  
  
## <a name="see-also"></a>Vea también  
 [OLE DB para los conjuntos de filas de esquema OLAP](ole-db-for-olap-schema-rowsets.md)  
  
  
