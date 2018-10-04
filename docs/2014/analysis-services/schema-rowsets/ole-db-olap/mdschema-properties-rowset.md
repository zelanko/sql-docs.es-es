---
title: Conjunto de filas MDSCHEMA_PROPERTIES | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MDSCHEMA_PROPERTIES
topic_type:
- apiref
helpviewer_keywords:
- MDSCHEMA_PROPERTIES rowset
ms.assetid: 95c480f7-c525-44ba-a59b-cd36f5855a4f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 17395bb081006e46b052bdaf8da2166b0366d686
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48100135"
---
# <a name="mdschemaproperties-rowset"></a>Conjunto de filas MDSCHEMA_PROPERTIES
  Describe las propiedades de los miembros de una base de datos.  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El `MDSCHEMA_PROPERTIES` conjunto de filas contiene las siguientes columnas.  
  
|Nombre de columna|Indicador de tipo|Longitud|Descripción|  
|-----------------|--------------------|------------|-----------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`||El nombre de la base de datos.|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`||Nombre del esquema al que pertenece esta propiedad. Su valor es `NULL` si el proveedor no admite esquemas.|  
|`CUBE_NAME`|`DBTYPE_WSTR`||Nombre del cubo.|  
|`DIMENSION_UNIQUE_NAME`|`DBTYPE_WSTR`||El nombre único de la dimensión. Los proveedores que generan nombres únicos por calificación tienen delimitados todos los componentes del nombre.|  
|`HIERARCHY_UNIQUE_NAME`|`DBTYPE_WSTR`||Nombre único de la jerarquía. Los proveedores que generan nombres únicos por calificación tienen delimitados todos los componentes del nombre.|  
|`LEVEL_UNIQUE_NAME`|`DBTYPE_WSTR`||Nombre único del nivel al que pertenece esta propiedad. Si el proveedor no admite los niveles con nombre, debería devolver el valor `DIMENSION_UNIQUE_NAME` para este campo. Los proveedores que generan nombres únicos por calificación tienen delimitados todos los componentes del nombre.|  
|`MEMBER_UNIQUE_NAME`|`DBTYPE_WSTR`||Nombre único del miembro al que pertenece esta propiedad. Se utiliza para los almacenes de datos que no admiten los niveles con nombre o tienen las propiedades miembro a miembro. Si la propiedad se aplica a todos los miembros en un nivel, esta columna es `NULL`. Los proveedores que generan nombres únicos por calificación tienen delimitados todos los componentes del nombre.|  
|`PROPERTY_TYPE`|`DBTYPE_I2`||Un mapa de bits que especifica el tipo de propiedad:<br /><br /> -   `MDPROP_MEMBER` (`1`) identifica una propiedad de miembro. Esta propiedad se puede utilizar en la cláusula DIMENSION PROPERTIES de la instrucción SELECT.<br />-   `MDPROP_CELL` (`2`) identifica una propiedad de una celda. Esta propiedad se puede utilizar en la cláusula CELL PROPERTIES que se produce al final de la instrucción SELECT.<br />-   `MDPROP_SYSTEM` (`4`) identifica una propiedad interna.<br />-   `MDPROP_BLOB` (`8`) identifica una propiedad que contiene un objeto binario grande (blob).|  
|`PROPERTY_NAME`|`DBTYPE_WSTR`||El nombre de la propiedad. Si la clave para la propiedad es igual que el nombre de la propiedad, `PROPERTY_NAME` estará en blanco.|  
|`PROPERTY_CAPTION`|`DBTYPE_WSTR`||Una etiqueta o una descripción asociada a la propiedad, utilizados principalmente para fines de presentación. Si no existe ninguna descripción, devuelve `PROPERTY_NAME`.|  
|`DATA_TYPE`|`DBTYPE_UI2`||El tipo de datos de la propiedad.|  
|`CHARACTER_MAXIMUM_LENGTH`|`DBTYPE_UI4`||Máxima longitud posible de la propiedad, si es un carácter, binario o tipo de bit.<br /><br /> Cero indica que no hay ninguna longitud máxima definida.<br /><br /> Para otros tipos de datos, devuelve `NULL`.|  
|`CHARACTER_OCTET_LENGTH`|`DBTYPE_UI4`||Longitud máxima posible en bytes de la propiedad, si es de caracteres o tipo binaria.<br /><br /> Cero indica que no hay ninguna longitud máxima definida.<br /><br /> Para otros tipos de datos, devuelve `NULL`.|  
|`NUMERIC_PRECISION`|`DBTYPE_UI2`||Precisión máxima de la propiedad, si es de tipo de datos numérico.<br /><br /> Para otros tipos de datos, devuelve `NULL`.|  
|`NUMERIC_SCALE`|`DBTYPE_I2`||Número de dígitos que se encuentran a la derecha del separador decimal si es de un tipo `DBTYPE_NUMERIC` o `DBTYPE_DECIMAL`.<br /><br /> Para otros tipos de datos, devuelve `NULL`.|  
|`DESCRIPTION`|`DBTYPE_WSTR`||Una descripción legible de la propiedad. `NULL` si no existe ninguna descripción.|  
|`PROPERTY_CONTENT_TYPE`|`DBTYPE_I2`||Tipo de la propiedad. Puede ser una de las siguientes enumeraciones:<br /><br /> -   **MD_PROPTYPE_REGULAR** (`0x00`)<br />-   **MD_PROPTYPE_ID** (`0x01`)<br />-   **MD_PROPTYPE_RELATION_TO_PARENT** (`0x02`)<br />-   **MD_PROPTYPE_ROLLUP_OPERATOR** (`0x03`)<br />-   **MD_PROPTYPE_ORG_TITLE** (`0x11`)<br />-   **MD_PROPTYPE_CAPTION** (`0x21`)<br />-   **MD_PROPTYPE_CAPTION_SHORT** (`0x22`)<br />-   **MD_PROPTYPE_CAPTION_DESCRIPTION** (`0x23`)<br />-   **MD_PROPTYPE_CAPTION_ABREVIATION** (`0x24`)<br />-   **MD_PROPTYPE_WEB_URL** (`0x31`)<br />-   **MD_PROPTYPE_WEB_HTML** (`0x32`)<br />-   **MD_PROPTYPE_WEB_XML_OR_XSL** (`0x33`)<br />-   **MD_PROPTYPE_WEB_MAIL_ALIAS** (`0x34`)<br />-   **MD_PROPTYPE_ADDRESS** (`0x41`)<br />-   **MD_PROPTYPE_ADDRESS_STREET** (`0x42`)<br />-   **MD_PROPTYPE_ADDRESS_HOUSE** (`0x43`)<br />-   **MD_PROPTYPE_ADDRESS_CITY** (`0x44`)<br />-   **MD_PROPTYPE_ADDRESS_STATE_OR_PROVINCE** (`0x45`)<br />-   **MD_PROPTYPE_ADDRESS_ZIP** (`0x46`)<br />-   **MD_PROPTYPE_ADDRESS_QUARTER** (`0x47`)<br />-   **MD_PROPTYPE_ADDRESS_COUNTRY** (`0x48`)<br />-   **MD_PROPTYPE_ADDRESS_BUILDING** (`0x49`)<br />-   **MD_PROPTYPE_ADDRESS_ROOM** (`0x4A`)<br />-   **MD_PROPTYPE_ADDRESS_FLOOR** (`0x4B`)<br />-   **MD_PROPTYPE_ADDRESS_FAX** (`0x4C`)<br />-   **MD_PROPTYPE_ADDRESS_PHONE** (`0x4D`)<br />-   **MD_PROPTYPE_GEO_CENTROID_X** (`0x61`)<br />-   **MD_PROPTYPE_GEO_CENTROID_Y** (`0x62`)<br />-   **MD_PROPTYPE_GEO_CENTROID_Z** (`0x63`)<br />-   **MD_PROPTYPE_GEO_BOUNDARY_TOP** (`0x64`)<br />-   **MD_PROPTYPE_GEO_BOUNDARY_LEFT** (`0x65`)<br />-   **MD_PROPTYPE_GEO_BOUNDARY_BOTTOM** (`0x66`)<br />-   **MD_PROPTYPE_GEO_BOUNDARY_RIGHT** (`0x67`)<br />-   **MD_PROPTYPE_GEO_BOUNDARY_FRONT** (`0x68`)<br />-   **MD_PROPTYPE_GEO_BOUNDARY_REAR** (`0x69`)<br />-   **MD_PROPTYPE_GEO_BOUNDARY_POLYGON** (`0x6A`)<br />-   **MD_PROPTYPE_PHYSICAL_SIZE** (`0x71`)<br />-   **MD_PROPTYPE_PHYSICAL_COLOR** (`0x72`)<br />-   **MD_PROPTYPE_PHYSICAL_WEIGHT** (`0x73`)<br />-   **MD_PROPTYPE_PHYSICAL_HEIGHT** (`0x74`)<br />-   **MD_PROPTYPE_PHYSICAL_WIDTH** (`0x75`)<br />-   **MD_PROPTYPE_PHYSICAL_DEPTH** (`0x76`)<br />-   **MD_PROPTYPE_PHYSICAL_VOLUME** (`0x77`)<br />-   **MD_PROPTYPE_PHYSICAL_DENSITY** (`0x78`)<br />-   **MD_PROPTYPE_PERSON_FULL_NAME** (`0x82`)<br />-   **MD_PROPTYPE_PERSON_FIRST_NAME** (`0x83`)<br />-   **MD_PROPTYPE_PERSON_LAST_NAME** (`0x84`)<br />-   **MD_PROPTYPE_PERSON_MIDDLE_NAME** (`0x85`)<br />-   **MD_PROPTYPE_PERSON_DEMOGRAPHIC** (`0x86`)<br />-   **MD_PROPTYPE_PERSON_CONTACT** (`0x87`)<br />-   **MD_PROPTYPE_QTY_RANGE_LOW** (`0x91`)<br />-   **MD_PROPTYPE_QTY_RANGE_HIGH** (`0x92`)<br />-   **MD_PROPTYPE_FORMATTING_COLOR** (`0xA1`)<br />-   **MD_PROPTYPE_FORMATTING_ORDER** (`0xA2`)<br />-   **MD_PROPTYPE_FORMATTING_FONT** (`0xA3`)<br />-   **MD_PROPTYPE_FORMATTING_FONT_EFFECTS** (`0xA4`)<br />-   **MD_PROPTYPE_FORMATTING_FONT_SIZE** (`0xA5`)<br />-   **MD_PROPTYPE_FORMATTING_SUB_TOTAL** (`0xA6`)<br />-   **MD_PROPTYPE_DATE** (`0xB1`)<br />-   **MD_PROPTYPE_DATE_START** (`0xB2`)<br />-   **MD_PROPTYPE_DATE_ENDED** (`0xB3`)<br />-   **MD_PROPTYPE_DATE_CANCELED** (`0xB4`)<br />-   **MD_PROPTYPE_DATE_MODIFIED** (`0xB5`)<br />-   **MD_PROPTYPE_DATE_DURATION** (`0xB6`)<br />-   **MD_PROPTYPE_VERSION** (`0xC1`)|  
|`SQL_COLUMN_NAME`|`DBTYPE_WSTR`||El nombre de la propiedad que se utiliza en consultas SQL desde la dimensión del cubo o dDimension de la base de datos.|  
|`LANGUAGE`|`DBTYPE_UI2`||La traducción expresada como `LCID`. Solo válido para las traducciones de propiedad.|  
|`PROPERTY_ORIGIN`|`DBTYPE_UI2`||Identifica el tipo de jerarquía a la que se aplica la propiedad:<br /><br /> -   `MD_USER_DEFINED` (`1`) indica que la propiedad está en una jerarquía definida por el usuario<br />-   `MD_SYSTEM_ENABLED` (`2`) indica que la propiedad está en una jerarquía de atributo<br />-   `MD_SYSTEM_DISABLED` (`4`) indica que la propiedad está en una jerarquía de atributo que no está habilitada.|  
|`PROPERTY_ATTRIBUTE_HIERARCHY_NAME`|`DBTYPE_WSTR`||El nombre de la jerarquía de atributo que origina esta propiedad.|  
|`PROPERTY_CARDINALITY`|`DBTYPE_WSTR`||Cardinalidad de la propiedad. Entre los valores posibles figuran las siguientes cadenas:<br /><br /> -   `ONE`<br />-   `MANY`|  
|`MIME_TYPE`|`DBTYPE_WSTR`||El tipo mime para los objetos binarios grandes (BLOB).|  
|`PROPERTY_IS_VISIBLE`|`DBTYPE_BOOL`||Un valor booleano que indica si la propiedad es visible.<br /><br /> `TRUE` si la propiedad es visible; de lo contrario, `FALSE`.|  
  
 Este conjunto de filas de esquema no está ordenado.  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El `MDSCHEMA_PROPERTIES` conjunto de filas puede tener restricciones en las columnas enumeradas en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`|obligatorio|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`|Opcional|  
|`CUBE_NAME`|`DBTYPE_WSTR`|Opcional|  
|`DIMENSION_UNIQUE_NAME`|`DBTYPE_WSTR`|Opcional|  
|`HIERARCHY_UNIQUE_NAME`|`DBTYPE_WSTR`|Opcional|  
|`LEVEL_UNIQUE_NAME`|`DBTYPE_WSTR`|Opcional|  
|`MEMBER_UNIQUE_NAME`|`DBTYPE_WSTR`|Opcional|  
|`PROPERTY_TYPE`|`DBTYPE_I2`|Opcional|  
|`PROPERTY_NAME`|`DBTYPE_WSTR`|Opcional|  
|`PROPERTY_CONTENT_TYPE`|`DBTYPE_I2`|(Opcional) Una restricción predeterminada está instaurada en `MDPROP_MEMBER` O `MDPROP_CELL`.|  
|`PROPERTY_ORIGIN`|`DBTYPE_UI2`|(Opcional) Una restricción predeterminada está instaurada en `MD_USER_DEFINED` O `MD_SYSTEM_ENABLED`.|  
|`CUBE_SOURCE`|`DBTYPE_UI2`|(Opcional) Mapa de bits con uno de los siguientes valores válidos:<br /><br /> -1 CUBO<br />-DIMENSIÓN DE 2<br /><br /> La restricción predeterminada es un valor de 1.|  
|`PROPERTY_VISIBILITY`|`DBTYPE_UI2`|(Opcional) Mapa de bits con uno de los siguientes valores válidos:<br /><br /> -1 Visible<br />-2 no visible<br /><br /> La restricción predeterminada es un valor de 1.|  
  
## <a name="see-also"></a>Vea también  
 [OLE DB para los conjuntos de filas de esquema OLAP](ole-db-for-olap-schema-rowsets.md)  
  
  
