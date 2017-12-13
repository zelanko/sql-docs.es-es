---
title: Conjunto de filas MDSCHEMA_PROPERTIES | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
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
apiname: MDSCHEMA_PROPERTIES
apitype: NA
applies_to: SQL Server 2016 Preview
helpviewer_keywords: MDSCHEMA_PROPERTIES rowset
ms.assetid: 95c480f7-c525-44ba-a59b-cd36f5855a4f
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ea7071ca436f8314fbf598484524b0c699d35d32
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="mdschemaproperties-rowset"></a>Conjunto de filas MDSCHEMA_PROPERTIES
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Describe las propiedades de los miembros dentro de una base de datos.  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El **MDSCHEMA_PROPERTIES** filas contiene las columnas siguientes.  
  
|Nombre de columna|Indicador de tipo|Longitud|Description|  
|-----------------|--------------------|------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**||El nombre de la base de datos.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**||Nombre del esquema al que pertenece esta propiedad. **NULL** si el proveedor no admite esquemas.|  
|**RESTRICCIONES OBLIGATORIAS CUBE_NAME**|**DBTYPE_WSTR**||Nombre del cubo.|  
|**DIMENSION_UNIQUE_NAME**|**DBTYPE_WSTR**||El nombre único de la dimensión. Los proveedores que generan nombres únicos por calificación tienen delimitados todos los componentes del nombre.|  
|**HIERARCHY_UNIQUE_NAME**|**DBTYPE_WSTR**||Nombre único de la jerarquía. Los proveedores que generan nombres únicos por calificación tienen delimitados todos los componentes del nombre.|  
|**LEVEL_UNIQUE_NAME**|**DBTYPE_WSTR**||Nombre único del nivel al que pertenece esta propiedad. Si el proveedor no admite niveles con nombre, debe devolver el **DIMENSION_UNIQUE_NAME** valor para este campo. Los proveedores que generan nombres únicos por calificación tienen delimitados todos los componentes del nombre.|  
|**MEMBER_UNIQUE_NAME**|**DBTYPE_WSTR**||Nombre único del miembro al que pertenece esta propiedad. Se utiliza para los almacenes de datos que no admiten los niveles con nombre o tienen las propiedades miembro a miembro. Si la propiedad se aplica a todos los miembros de un nivel, esta columna es **NULL**. Los proveedores que generan nombres únicos por calificación tienen delimitados todos los componentes del nombre.|  
|**PROPERTY_TYPE**|**DBTYPE_I2**||Un mapa de bits que especifica el tipo de propiedad:<br /><br /> **MDPROP_MEMBER** (**1**) identifica una propiedad de un miembro. Esta propiedad se puede utilizar en la cláusula DIMENSION PROPERTIES de la instrucción SELECT.<br /><br /> **MDPROP_CELL** (**2**) identifica una propiedad de una celda. Esta propiedad se puede utilizar en la cláusula CELL PROPERTIES que se produce al final de la instrucción SELECT.<br /><br /> **MDPROP_SYSTEM** (**4**) identifica una propiedad interna.<br /><br /> **MDPROP_BLOB** (**8**) identifica una propiedad que contiene un objeto binario grande (blob).|  
|**PROPERTY_NAME**|**DBTYPE_WSTR**||El nombre de la propiedad. Si la clave para la propiedad es el mismo que el nombre de la propiedad **PROPERTY_NAME** estará en blanco.|  
|**PROPERTY_CAPTION**|**DBTYPE_WSTR**||Una etiqueta o una descripción asociada a la propiedad, utilizados principalmente para fines de presentación. Devuelve **PROPERTY_NAME** si no existe ningún título.|  
|**DATA_TYPE**|**DBTYPE_UI2**||El tipo de datos de la propiedad.|  
|**CAMPO CHARACTER_MAXIMUM_LENGTH**|**DBTYPE_UI4**||Máxima longitud posible de la propiedad, si es un carácter, binario o tipo de bit.<br /><br /> Cero indica que no hay ninguna longitud máxima definida.<br /><br /> Devuelve **NULL** para todos los demás tipos de datos.|  
|**CHARACTER_OCTET_LENGTH**|**DBTYPE_UI4**||Longitud máxima posible en bytes de la propiedad, si es de caracteres o tipo binaria.<br /><br /> Cero indica que no hay ninguna longitud máxima definida.<br /><br /> Devuelve **NULL** para todos los demás tipos de datos.|  
|**CAMPO NUMERIC_PRECISION**|**DBTYPE_UI2**||Precisión máxima de la propiedad, si es de tipo de datos numérico.<br /><br /> Devuelve **NULL** para todos los demás tipos de datos.|  
|**NUMERIC_SCALE**|**DBTYPE_I2**||El número de dígitos a la derecha del separador decimal, si es un **DBTYPE_NUMERIC** o **DBTYPE_DECIMAL** tipo.<br /><br /> Devuelve **NULL** para todos los demás tipos de datos.|  
|**DESCRIPTION**|**DBTYPE_WSTR**||Una descripción legible de la propiedad. **NULL** si no existe ninguna descripción.|  
|**PROPERTY_CONTENT_TYPE**|**DBTYPE_I2**||Tipo de la propiedad. Puede ser una de las siguientes enumeraciones:<br /><br /> **MD_PROPTYPE_REGULAR** (**0 x 00**)<br /><br /> **MD_PROPTYPE_ID** (**0 x 01**)<br /><br /> **MD_PROPTYPE_RELATION_TO_PARENT** (**0 x 02**)<br /><br /> **MD_PROPTYPE_ROLLUP_OPERATOR** (**0 x 03**)<br /><br /> **MD_PROPTYPE_ORG_TITLE** (**0 x 11**)<br /><br /> **MD_PROPTYPE_CAPTION** (**0 x 21**)<br /><br /> **MD_PROPTYPE_CAPTION_SHORT** (**0 x 22**)<br /><br /> **MD_PROPTYPE_CAPTION_DESCRIPTION** (**0 x 23**)<br /><br /> **MD_PROPTYPE_CAPTION_ABREVIATION** (**0 x 24**)<br /><br /> **MD_PROPTYPE_WEB_URL** (**0 x 31**)<br /><br /> **MD_PROPTYPE_WEB_HTML** (**0 x 32**)<br /><br /> **MD_PROPTYPE_WEB_XML_OR_XSL** (**0 x 33**)<br /><br /> **MD_PROPTYPE_WEB_MAIL_ALIAS** (**0 x 34**)<br /><br /> **MD_PROPTYPE_ADDRESS** (**0 x 41**)<br /><br /> **MD_PROPTYPE_ADDRESS_STREET** (**0 x 42**)<br /><br /> **MD_PROPTYPE_ADDRESS_HOUSE** (**0x43**)<br /><br /> **MD_PROPTYPE_ADDRESS_CITY** (**0 x 44**)<br /><br /> **MD_PROPTYPE_ADDRESS_STATE_OR_PROVINCE** (**0 x 45**)<br /><br /> **MD_PROPTYPE_ADDRESS_ZIP** (**0 x 46**)<br /><br /> **MD_PROPTYPE_ADDRESS_QUARTER** (**0 x 47**)<br /><br /> **MD_PROPTYPE_ADDRESS_COUNTRY** (**0 x 48**)<br /><br /> **MD_PROPTYPE_ADDRESS_BUILDING** (**0 x 49**)<br /><br /> **MD_PROPTYPE_ADDRESS_ROOM** (**0x4A**)<br /><br /> **MD_PROPTYPE_ADDRESS_FLOOR** (**0x4B**)<br /><br /> **MD_PROPTYPE_ADDRESS_FAX** (**0x4C**)<br /><br /> **MD_PROPTYPE_ADDRESS_PHONE** (**0x4D**)<br /><br /> **MD_PROPTYPE_GEO_CENTROID_X** (**0 x 61**)<br /><br /> **MD_PROPTYPE_GEO_CENTROID_Y** (**0x62**)<br /><br /> **MD_PROPTYPE_GEO_CENTROID_Z** (**0 x 63**)<br /><br /> **MD_PROPTYPE_GEO_BOUNDARY_TOP** (**0x64**)<br /><br /> **MD_PROPTYPE_GEO_BOUNDARY_LEFT** (**0x65**)<br /><br /> **MD_PROPTYPE_GEO_BOUNDARY_BOTTOM** (**0x66**)<br /><br /> **MD_PROPTYPE_GEO_BOUNDARY_RIGHT** (**0x67**)<br /><br /> **MD_PROPTYPE_GEO_BOUNDARY_FRONT** (**0x68**)<br /><br /> **MD_PROPTYPE_GEO_BOUNDARY_REAR** (**0x69**)<br /><br /> **MD_PROPTYPE_GEO_BOUNDARY_POLYGON** (**0x6A**)<br /><br /> **MD_PROPTYPE_PHYSICAL_SIZE** (**0 x 71**)<br /><br /> **MD_PROPTYPE_PHYSICAL_COLOR** (**0x72**)<br /><br /> **MD_PROPTYPE_PHYSICAL_WEIGHT** (**0 x 73**)<br /><br /> **MD_PROPTYPE_PHYSICAL_HEIGHT** (**0 x 74**)<br /><br /> **MD_PROPTYPE_PHYSICAL_WIDTH** (**0x75**)<br /><br /> **MD_PROPTYPE_PHYSICAL_DEPTH** (**0x76**)<br /><br /> **MD_PROPTYPE_PHYSICAL_VOLUME** (**0 x 77**)<br /><br /> **MD_PROPTYPE_PHYSICAL_DENSITY** (**0 x 78**)<br /><br /> **MD_PROPTYPE_PERSON_FULL_NAME** (**0 x 82**)<br /><br /> **MD_PROPTYPE_PERSON_FIRST_NAME** (**0 x 83**)<br /><br /> **MD_PROPTYPE_PERSON_LAST_NAME** (**0 x 84**)<br /><br /> **MD_PROPTYPE_PERSON_MIDDLE_NAME** (**0x85**)<br /><br /> **MD_PROPTYPE_PERSON_DEMOGRAPHIC** (**0x86**)<br /><br /> **MD_PROPTYPE_PERSON_CONTACT** (**0 x 87**)<br /><br /> **MD_PROPTYPE_QTY_RANGE_LOW** (**0 x 91**)<br /><br /> **MD_PROPTYPE_QTY_RANGE_HIGH** (**0 x 92**)<br /><br /> **MD_PROPTYPE_FORMATTING_COLOR** (**0xA1**)<br /><br /> **MD_PROPTYPE_FORMATTING_ORDER** (**0xA2**)<br /><br /> **MD_PROPTYPE_FORMATTING_FONT** (**0xA3**)<br /><br /> **MD_PROPTYPE_FORMATTING_FONT_EFFECTS** (**0xA4**)<br /><br /> **MD_PROPTYPE_FORMATTING_FONT_SIZE** (**0xA5**)<br /><br /> **MD_PROPTYPE_FORMATTING_SUB_TOTAL** (**0xA6**)<br /><br /> **MD_PROPTYPE_DATE** (**0xB1**)<br /><br /> **MD_PROPTYPE_DATE_START** (**0xB2**)<br /><br /> **MD_PROPTYPE_DATE_ENDED** (**0xB3**)<br /><br /> **MD_PROPTYPE_DATE_CANCELED** (**0xB4**)<br /><br /> **MD_PROPTYPE_DATE_MODIFIED** (**0xB5**)<br /><br /> **MD_PROPTYPE_DATE_DURATION** (**0xB6**)<br /><br /> **MD_PROPTYPE_VERSION** (**0xC1**)|  
|**SQL_COLUMN_NAME**|**DBTYPE_WSTR**||El nombre de la propiedad que se utiliza en consultas SQL desde la dimensión del cubo o dDimension de la base de datos.|  
|**LANGUAGE**|**DBTYPE_UI2**||La traducción expresada como un **LCID**. Solo válido para las traducciones de propiedad.|  
|**PROPERTY_ORIGIN**|**DBTYPE_UI2**||Identifica el tipo de jerarquía a la que se aplica la propiedad:<br /><br /> **MD_USER_DEFINED** (**1**) indica que la propiedad está en una jerarquía definida por el usuario<br /><br /> **MD_SYSTEM_ENABLED** (**2**) indica que la propiedad está en una jerarquía de atributo<br /><br /> **MD_SYSTEM_DISABLED** (**4**) indica que la propiedad está en una jerarquía de atributo que no está habilitada.|  
|**PROPERTY_ATTRIBUTE_HIERARCHY_NAME**|**DBTYPE_WSTR**||El nombre de la jerarquía de atributo que origina esta propiedad.|  
|**PROPERTY_CARDINALITY**|**DBTYPE_WSTR**||Cardinalidad de la propiedad. Entre los valores posibles figuran las siguientes cadenas:<br /><br /> **UNO**<br /><br /> **MUCHOS**|  
|**MIME_TYPE**|**DBTYPE_WSTR**||El tipo mime para los objetos binarios grandes (BLOB).|  
|**PROPERTY_IS_VISIBLE**|**DBTYPE_BOOL**||Un valor booleano que indica si la propiedad es visible.<br /><br /> **TRUE** si la propiedad está visible; en caso contrario, **FALSE**.|  
  
 Este conjunto de filas de esquema no está ordenado.  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El **MDSCHEMA_PROPERTIES** se puede restringir el conjunto de filas en las columnas enumeradas en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|Obligatorio|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|Opcional|  
|**RESTRICCIONES OBLIGATORIAS CUBE_NAME**|**DBTYPE_WSTR**|Opcional|  
|**DIMENSION_UNIQUE_NAME**|**DBTYPE_WSTR**|Opcional|  
|**HIERARCHY_UNIQUE_NAME**|**DBTYPE_WSTR**|Opcional|  
|**LEVEL_UNIQUE_NAME**|**DBTYPE_WSTR**|Opcional|  
|**MEMBER_UNIQUE_NAME**|**DBTYPE_WSTR**|Opcional|  
|**PROPERTY_TYPE**|**DBTYPE_I2**|Opcional|  
|**PROPERTY_NAME**|**DBTYPE_WSTR**|Opcional|  
|**PROPERTY_CONTENT_TYPE**|**DBTYPE_I2**|(Opcional) Una restricción predeterminada está en su lugar en **MDPROP_MEMBER** o **MDPROP_CELL**.|  
|**PROPERTY_ORIGIN**|**DBTYPE_UI2**|(Opcional) Una restricción predeterminada está en su lugar en **MD_USER_DEFINED** o **MD_SYSTEM_ENABLED**.|  
|**CUBE_SOURCE**|**DBTYPE_UI2**|(Opcional) La restricción predeterminada es un valor de 1.  Un mapa de bits con uno de los siguientes valores válidos:<br /><br /> 1 CUBO<br /><br /> 2 DIMENSIÓN|  
|**PROPERTY_VISIBILITY**|**DBTYPE_UI2**|(Opcional) La restricción predeterminada es un valor de 1. Un mapa de bits con uno de los siguientes valores válidos:<br /><br /> 1 Visible<br /><br /> 2 no visible|  
  
## <a name="see-also"></a>Vea también  
 [OLE DB para los conjuntos de filas de esquema OLAP](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
