---
title: Conjunto de filas MDSCHEMA_MEASURES | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MDSCHEMA_MEASURES
topic_type:
- apiref
helpviewer_keywords:
- MDSCHEMA_MEASURES rowset
ms.assetid: 6ff5bd1a-aad0-49b8-9f8d-7df2637caacf
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4f421e3ebd93af0eb5fe175c0d94d28ab8509289
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48094275"
---
# <a name="mdschemameasures-rowset"></a>Conjunto de filas MDSCHEMA_MEASURES
  Describe cada medida en un cubo.  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El `MDSCHEMA_MEASURES` conjunto de filas contiene las siguientes columnas.  
  
|Nombre de columna|Indicador de tipo|Longitud|Descripción|  
|-----------------|--------------------|------------|-----------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`||El nombre del catálogo al que pertenece esta medida. `NULL` si el proveedor no admite catálogos.|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`||El nombre del esquema al que pertenece esta medida. Su valor es `NULL` si el proveedor no admite esquemas.|  
|`CUBE_NAME`|`DBTYPE_WSTR`||Nombre del cubo al que pertenece esta medida.|  
|`MEASURE_NAME`|`DBTYPE_WSTR`||El nombre de la medida.|  
|`MEASURE_UNIQUE_NAME`|`DBTYPE_WSTR`||Nombre único de la medida. Los proveedores que generan nombres únicos por calificación tienen delimitados todos los componentes del nombre.|  
|`MEASURE_CAPTION`|`DBTYPE_WSTR`||Etiqueta o título asociado a la medida. Se utiliza principalmente para la presentación. Si no existe ningún título, se devuelve `MEASURE_NAME`.|  
|`MEASURE_GUID`|`DBTYPE_GUID`||No compatible.|  
|`MEASURE_AGGREGATOR`|`DBTYPE_I4`||Una enumeración que identifica cómo se obtuvo una medida. Puede ser uno de los siguientes valores:<br /><br /> -   `MDMEASURE_AGGR_SUM` (`1`) identifica que agrega la medida de `SUM`.<br />-   `MDMEASURE_AGGR_COUNT` (`2`) identifica que agrega la medida de `COUNT`.<br />-   **MDMEASURE_AGGR_MIN** (`3`) identifica que agrega la medida de `MIN`.<br />-   **MDMEASURE_AGGR_MAX** (`4`) identifica que agrega la medida de `MAX`.<br />-   `MDMEASURE_AGGR_AVG` (`5`) identifica que agrega la medida de `AVG`.<br />-   `MDMEASURE_AGGR_VAR` (`6`) identifica que agrega la medida de `VAR`.<br />-   `MDMEASURE_AGGR_STD` (`7`) identifica que agrega la medida de `STDEV`.<br />-   `MDMEASURE_AGGR_DST` (`8`) identifica que agrega la medida de `DISTINCT COUNT`.<br />-   `MDMEASURE_AGGR_NONE` (`9`) identifica que agrega la medida de `NONE`.<br />-   `MDMEASURE_AGGR_AVGCHILDREN` (`10`) identifica que agrega la medida de `AVERAGEOFCHILDREN`.<br />-   `MDMEASURE_AGGR_FIRSTCHILD` (`11`) identifica que agrega la medida de `FIRSTCHILD`.<br />-   `MDMEASURE_AGGR_LASTCHILD` (`12`) identifica que agrega la medida de `LASTCHILD`.<br />-   `MDMEASURE_AGGR_FIRSTNONEMPTY` (`13`) identifica que agrega la medida de `FIRSTNONEMPTY`,<br />-   `MDMEASURE_AGGR_LASTNONEMPTY` (`14`) identifica que agrega la medida de `LASTNONEMPTY`.<br />-   `MDMEASURE_AGGR_BYACCOUNT` (`15`) identifica que agrega la medida de `BYACCOUNT`.<br />-   `MDMEASURE_AGGR_CALCULATED` (`127`) identifica que la medida se obtuvo de una fórmula que no fue anteriormente ninguna función única.<br />-   `MDMEASURE_AGGR_UNKNOWN` (`0`) identifica que la medida se obtuvo de una fórmula o una función de agregación desconocido.|  
|`DATA_TYPE`|`DBTYPE_UI2`||El tipo de datos de la medida.|  
|`NUMERIC_PRECISION`|`DBTYPE_UI2`||La precisión máxima de la propiedad si el tipo de datos del objeto de medida es un valor numérico exacto. `NULL` para todos los otros tipos de propiedad.|  
|`NUMERIC_SCALE`|`DBTYPE_I2`||Número de dígitos que se encuentran a la derecha del separador decimal si el indicador de tipo de objeto de medida es `DBTYPE_NUMERIC` o `DBTYPE_DECIMAL`. De lo contrario, este valor es `NULL`.|  
|`MEASURE_UNITS`|`DBTYPE_WSTR`||No compatible|  
|`DESCRIPTION`|`DBTYPE_WSTR`||Una descripción inteligible de la medida. `NULL` si no existe ninguna descripción.|  
|`EXPRESSION`|`DBTYPE_WSTR`||Una expresión para el miembro.|  
|`MEASURE_IS_VISIBLE`|`DBTYPE_BOOL`||Un valor booleano que siempre devuelve un valor verdadero. Si la medida no está visible, no estará incluido en el conjunto de filas de esquema.|  
|`LEVELS_LIST`|`DBTYPE_WSTR`||Una cadena que siempre devuelve `NULL`.|  
|`MEASURE_NAME_SQL_COLUMN_NAME`|`DBTYPE_WSTR`||El nombre de la columna en la consulta SQL que se corresponde con el nombre de la medida.|  
|`MEASURE_UNQUALIFIED_CAPTION`|`DBTYPE_WSTR`||Nombre de la medida, no calificada con el nombre del grupo de medidas.|  
|`MEASUREGROUP_NAME`|`DBTYPE_WSTR`||Nombre del grupo de medidas al que pertenece esta medida.|  
|`MEASURE_DISPLAY_FOLDER`|`DBTYPE_WSTR`||La ruta que se va a utilizar al mostrar la medida en la interfaz de usuario. Un punto y coma separará los nombres de carpeta. Las carpetas anidadas se indican mediante una barra diagonal inversa (\\).|  
|`DEFAULT_FORMAT_STRING`|`DBTYPE_WSTR`||Cadena de formato predeterminada para la medida.|  
  
 El conjunto de filas se ordena en `CATALOG_NAME`, `SCHEMA_NAME`, `CUBE_NAME`, `MEASURE_NAME`.  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El `MDSCHEMA_MEASURES` conjunto de filas puede tener restricciones en las columnas enumeradas en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`CUBE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`MEASURE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`MEASURE_UNIQUE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`MEASUREGROUP_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`CUBE_SOURCE`|`DBTYPE_UI2`|(Opcional) Mapa de bits con uno de los siguientes valores válidos:<br /><br /> -1 CUBO<br />-DIMENSIÓN DE 2<br /><br /> La restricción predeterminada es un valor de 1.|  
|`MEASURE_VISIBILITY`|`DBTYPE_UI2`|(Opcional) Mapa de bits con uno de los siguientes valores válidos:<br /><br /> -1 Visible<br />-2 no es Visible<br /><br /> La restricción predeterminada es un valor de 1.|  
  
## <a name="see-also"></a>Vea también  
 [OLE DB para los conjuntos de filas de esquema OLAP](ole-db-for-olap-schema-rowsets.md)  
  
  
