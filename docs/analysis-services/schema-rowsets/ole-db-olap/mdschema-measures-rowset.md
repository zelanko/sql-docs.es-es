---
title: Conjunto de filas MDSCHEMA_MEASURES | Documentos de Microsoft
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
apiname: MDSCHEMA_MEASURES
apitype: NA
applies_to: SQL Server 2016 Preview
helpviewer_keywords: MDSCHEMA_MEASURES rowset
ms.assetid: 6ff5bd1a-aad0-49b8-9f8d-7df2637caacf
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f25b46b4a8d5ab61a848febb9f1322759ba4cc83
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="mdschemameasures-rowset"></a>Conjunto de filas MDSCHEMA_MEASURES
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Describe cada medida dentro de un cubo.  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El **MDSCHEMA_MEASURES** filas contiene las columnas siguientes.  
  
|Nombre de columna|Indicador de tipo|Longitud|Description|  
|-----------------|--------------------|------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**||El nombre del catálogo al que pertenece esta medida. **NULL** si el proveedor no admite catálogos.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**||El nombre del esquema al que pertenece esta medida. **NULL** si el proveedor no admite esquemas.|  
|**RESTRICCIONES OBLIGATORIAS CUBE_NAME**|**DBTYPE_WSTR**||Nombre del cubo al que pertenece esta medida.|  
|**MEASURE_NAME**|**DBTYPE_WSTR**||El nombre de la medida.|  
|**MEASURE_UNIQUE_NAME**|**DBTYPE_WSTR**||Nombre único de la medida. Los proveedores que generan nombres únicos por calificación tienen delimitados todos los componentes del nombre.|  
|**MEASURE_CAPTION**|**DBTYPE_WSTR**||Etiqueta o título asociado a la medida. Se utiliza principalmente para la presentación. Si no existe ningún título, **MEASURE_NAME** se devuelve.|  
|**MEASURE_GUID**|**DBTYPE_GUID**||No compatible.|  
|**MEASURE_AGGREGATOR**|**DBTYPE_I4**||Una enumeración que identifica cómo se obtuvo una medida. Puede ser uno de los siguientes valores:<br /><br /> **MDMEASURE_AGGR_SUM** (**1**) identifica que la medida se agrega de **suma**.<br /><br /> **MDMEASURE_AGGR_COUNT** (**2**) identifica que la medida se agrega de **recuento**.<br /><br /> **MDMEASURE_AGGR_MIN** (**3**) identifica que la medida se agrega de **MIN**.<br /><br /> **MDMEASURE_AGGR_MAX** (**4**) identifica que la medida se agrega de **MAX**.<br /><br /> **MDMEASURE_AGGR_AVG** (**5**) identifica que la medida se agrega de **AVG**.<br /><br /> **MDMEASURE_AGGR_VAR** (**6**) identifica que la medida se agrega de **VAR**.<br /><br /> **MDMEASURE_AGGR_STD** (**7**) identifica que la medida se agrega de **STDEV**.<br /><br /> **MDMEASURE_AGGR_DST** (**8**) identifica que la medida se agrega de **DISTINCT COUNT**.<br /><br /> **MDMEASURE_AGGR_NONE** (**9**) identifica que la medida se agrega de **NONE**.<br /><br /> **MDMEASURE_AGGR_AVGCHILDREN** (**10**) identifica que la medida se agrega de **AVERAGEOFCHILDREN**.<br /><br /> **MDMEASURE_AGGR_FIRSTCHILD** (**11**) identifica que la medida se agrega de **FIRSTCHILD**.<br /><br /> **MDMEASURE_AGGR_LASTCHILD** (**12**) identifica que la medida se agrega de **LASTCHILD**.<br /><br /> **MDMEASURE_AGGR_FIRSTNONEMPTY** (**13**) identifica que la medida se agrega de **FIRSTNONEMPTY**,<br /><br /> **MDMEASURE_AGGR_LASTNONEMPTY** (**14**) identifica que la medida se agrega de **LASTNONEMPTY**.<br /><br /> **MDMEASURE_AGGR_BYACCOUNT** (**15**) identifica que la medida se agrega de **BYACCOUNT**.<br /><br /> **MDMEASURE_AGGR_CALCULATED** (**127**) identifica que la medida se obtuvo de una fórmula que no fue anteriormente ninguna función única.<br /><br /> **MDMEASURE_AGGR_UNKNOWN** (**0**) identifica que la medida se obtuvo de una fórmula o una función de agregación desconocido.|  
|**DATA_TYPE**|**DBTYPE_UI2**||El tipo de datos de la medida.|  
|**CAMPO NUMERIC_PRECISION**|**DBTYPE_UI2**||La precisión máxima de la propiedad si el tipo de datos del objeto de medida es un valor numérico exacto. **NULL** para todos los demás tipos de propiedad.|  
|**NUMERIC_SCALE**|**DBTYPE_I2**||El número de dígitos a la derecha del separador decimal si el indicador de tipo del objeto de medida es **DBTYPE_NUMERIC** o **DBTYPE_DECIMAL**. En caso contrario, este valor es **NULL**.|  
|**MEASURE_UNITS**|**DBTYPE_WSTR**||No compatible|  
|**DESCRIPTION**|**DBTYPE_WSTR**||Una descripción inteligible de la medida. **NULL** si no existe ninguna descripción.|  
|**EXPRESIÓN**|**DBTYPE_WSTR**||Una expresión para el miembro.|  
|**MEASURE_IS_VISIBLE**|**DBTYPE_BOOL**||Un valor booleano que siempre devuelve un valor verdadero. Si la medida no está visible, no estará incluido en el conjunto de filas de esquema.|  
|**LEVELS_LIST**|**DBTYPE_WSTR**||Una cadena que siempre devuelve **NULL**.|  
|**MEASURE_NAME_SQL_COLUMN_NAME**|**DBTYPE_WSTR**||El nombre de la columna en la consulta SQL que se corresponde con el nombre de la medida.|  
|**MEASURE_UNQUALIFIED_CAPTION**|**DBTYPE_WSTR**||Nombre de la medida, no calificada con el nombre del grupo de medidas.|  
|**MEASUREGROUP_NAME**|**DBTYPE_WSTR**||Nombre del grupo de medidas al que pertenece esta medida.|  
|**MEASURE_DISPLAY_FOLDER**|**DBTYPE_WSTR**||La ruta que se va a utilizar al mostrar la medida en la interfaz de usuario. Un punto y coma separará los nombres de carpeta. Las carpetas anidadas se indican mediante una barra diagonal inversa (\\).|  
|**DEFAULT_FORMAT_STRING**|**DBTYPE_WSTR**||Cadena de formato predeterminada para la medida.|  
  
 El conjunto de filas está ordenado en **CATALOG_NAME**, **SCHEMA_NAME**, **restricciones obligatorias CUBE_NAME**, **MEASURE_NAME**.  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El **MDSCHEMA_MEASURES** se puede restringir el conjunto de filas en las columnas enumeradas en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**RESTRICCIONES OBLIGATORIAS CUBE_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**MEASURE_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**MEASURE_UNIQUE_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**MEASUREGROUP_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**CUBE_SOURCE**|**DBTYPE_UI2**|(Opcional) La restricción predeterminada es un valor de 1. Un mapa de bits con uno de los siguientes valores válidos:<br /><br /> 1 CUBO<br /><br /> 2 DIMENSIÓN|  
|**MEASURE_VISIBILITY**|**DBTYPE_UI2**|(Opcional) La restricción predeterminada es un valor de 1. Un mapa de bits con uno de los siguientes valores válidos:<br /><br /> 1 Visible<br /><br /> 2 No visible|  
  
## <a name="see-also"></a>Vea también  
 [OLE DB para los conjuntos de filas de esquema OLAP](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
