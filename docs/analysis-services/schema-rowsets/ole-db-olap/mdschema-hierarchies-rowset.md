---
title: Conjunto de filas MDSCHEMA_HIERARCHIES | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: MDSCHEMA_HIERARCHIES
apitype: NA
applies_to: SQL Server 2016 Preview
helpviewer_keywords: MDSCHEMA_HIERARCHIES rowset
ms.assetid: 2e5b2a81-366e-4d5b-af1e-1d372bf596d9
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7ecdc6817c5a2d7e1e88b909080a3156c55f40eb
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="mdschemahierarchies-rowset"></a>Conjunto de filas MDSCHEMA_HIERARCHIES
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Describe cada jerarquía dentro de una dimensión determinada.  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El **MDSCHEMA_HIERARCHIES** filas contiene las columnas siguientes.  
  
|Nombre de columna|Indicador de tipo|Description|  
|-----------------|--------------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|El nombre del catálogo al que pertenece esta jerarquía. **NULL** si el proveedor no admite catálogos.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|No compatible|  
|**RESTRICCIONES OBLIGATORIAS CUBE_NAME**|**DBTYPE_WSTR**|(Obligatorio) Nombre único del cubo al que pertenece la jerarquía.|  
|**DIMENSION_UNIQUE_NAME**|**DBTYPE_WSTR**|Nombre único de la dimensión a la que pertenece esta jerarquía. Los proveedores que generan nombres únicos por calificación tienen delimitados todos los componentes del nombre.|  
|**HIERARCHY_NAME**|**DBTYPE_WSTR**|Es el nombre de la jerarquía. En blanco si solo hay una única jerarquía en la dimensión. Esto siempre tendrá un valor en [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|**HIERARCHY_UNIQUE_NAME**|**DBTYPE_WSTR**|Nombre único de la jerarquía.|  
|**HIERARCHY_GUID**|**DBTYPE_GUID**|No compatible|  
|**HIERARCHY_CAPTION**|**DBTYPE_WSTR**|Una etiqueta o título asociado a la jerarquía. Se utiliza principalmente para la presentación. Si no existe ningún título, **HIERARCHY_NAME** se devuelve. Si la dimensión no contiene una jerarquía o tiene únicamente una jerarquía, esta columna contendrá el nombre de la dimensión.|  
|**DIMENSION_TYPE**|**DBTYPE_I2**|El tipo de la dimensión. Los valores válidos son los siguientes:<br /><br /> **MD_DIMTYPE_UNKNOWN** (**0**)<br /><br /> **MD_DIMTYPE_TIME** (**1**)<br /><br /> **MD_DIMTYPE_MEASURE** (**2**)<br /><br /> **MD_DIMTYPE_OTHER** (**3**)<br /><br /> **MD_DIMTYPE_QUANTITATIVE** (**5**)<br /><br /> **MD_DIMTYPE_ACCOUNTS** (**6**)<br /><br /> **MD_DIMTYPE_CUSTOMERS** (**7**)<br /><br /> **MD_DIMTYPE_PRODUCTS** (**8**)<br /><br /> **MD_DIMTYPE_SCENARIO** (**9**)<br /><br /> **MD_DIMTYPE_UTILIY** (**10**)<br /><br /> **MD_DIMTYPE_CURRENCY** (**11**)<br /><br /> **MD_DIMTYPE_RATES** (**12**)<br /><br /> **MD_DIMTYPE_CHANNEL** (**13**)<br /><br /> **MD_DIMTYPE_PROMOTION** (**14**)<br /><br /> **MD_DIMTYPE_ORGANIZATION** (**15**)<br /><br /> **MD_DIMTYPE_BILL_OF_MATERIALS** (**16**)<br /><br /> **MD_DIMTYPE_GEOGRAPHY** (**17**)|  
|**HIERARCHY_CARDINALITY**|**DBTYPE_UI4**|Número de miembros de la jerarquía.|  
|**DEFAULT_MEMBER**|**DBTYPE_WSTR**|El miembro predeterminado de esta jerarquía. Éste es un nombre único. Cada jerarquía debe tener un miembro predeterminado.|  
|**ALL_MEMBER**|**DBTYPE_WSTR**|El miembro en el nivel superior del resumen.|  
|**DESCRIPTION**|**DBTYPE_WSTR**|Una descripción inteligible de la jerarquía. **NULL** si no existe ninguna descripción.|  
|**ESTRUCTURA**|**DBTYPE_I2**|Estructura de la jerarquía. Los valores válidos son los siguientes:<br /><br /> **MD_STRUCTURE_FULLYBALANCED** (**0**)<br /><br /> **MD_STRUCTURE_RAGGEDBALANCED** (**1**)<br /><br /> **MD_STRUCTURE_UNBALANCED** (**2**)<br /><br /> **MD_STRUCTURE_NETWORK** (**3**)|  
|**IS_VIRTUAL**|**DBTYPE_BOOL**|Siempre devuelve **False**.|  
|**IS_READWRITE**|**DBTYPE_BOOL**|Un booleano que indica si la columna Reescritura en la dimensión está habilitada.<br /><br /> Devuelve **TRUE** si la **reescritura en la dimensión** columna que representa esta jerarquía está habilitada.|  
|**DIMENSION_UNIQUE_SETTINGS**|**DBTYPE_I4**|Siempre devuelve **MDDIMENSIONS_MEMBER_KEY_UNIQUE** (**1**).|  
|**DIMENSION_MASTER_UNIQUE_NAME**|**DBTYPE_WSTR**|Siempre devuelve **NULL**.|  
|**DIMENSION_IS_VISIBLE**|**DBTYPE_BOOL**|Siempre devuelve **true**. Si la dimensión no está visible, no aparecerá en el conjunto de filas de esquema.|  
|**HIERARCHY_ORDINAL**|**DBTYPE_UI4**|El número ordinal de la jerarquía en todas las jerarquías del cubo.|  
|**DIMENSION_IS_SHARED**|**DBTYPE_BOOL**|Siempre devuelve **TRUE**.|  
|**HIERARCHY_IS_VISIBLE**|**DBTYPE_BOOL**|Un booleano que indica si la jerarquía está visible.<br /><br /> Devuelve **TRUE** si la jerarquía está visible; en caso contrario, **FALSE**.|  
|**HIERARCHY_ORIGIN**|**DBTYPE_UI2**|Una máscara de bits que determina el origen de la jerarquía:<br /><br /> **MD_USER_DEFINED** identifica las jerarquías definidas por el usuario y tiene un valor de **0x0000001**.<br /><br /> **MD_SYSTEM_ENABLED** identifica las jerarquías de atributo y tiene un valor de **0x0000002**.<br /><br /> **MD_SYSTEM_INTERNAL** identifica los atributos con ninguna jerarquía de atributo y tiene un valor de **0x0000004**.<br /><br /> <br /><br /> Tenga en cuenta que una jerarquía de atributo de elemento primario/secundario es **MD_USER_DEFINED** y **MD_SYSTEM_ENABLED**.|  
|**HIERARCHY_DISPLAY_FOLDER**|**DBTYPE_WSTR**|La ruta que se va a utilizar al mostrar la jerarquía en la interfaz de usuario. Un punto y coma (;) separará los nombres de carpeta. Las carpetas anidadas se indican mediante una barra diagonal inversa (\\).|  
|**INSTANCE_SELECTION**|**DBTYPE_UI2**|Una sugerencia a la aplicación cliente sobre cómo mostrar la jerarquía. Los valores válidos son los siguientes:<br /><br /> **MD_INSTANCE_SELECTION_NONE**<br /><br /> **MD_INSTANCE_SELECTION_DROPDOWN**<br /><br /> **MD_INSTANCE_SELECTION_LIST**<br /><br /> **MD_INSTANCE_SELECTION_FILTEREDLIST**<br /><br /> **MD_INSTANCE_SELECTION_MANDATORYFILTER**|  
|**GROUPING_BEHAVIOR**|**DBTYPE_I2**|Una enumeración que especifica el comportamiento de agrupación esperado de los clientes de esta jerarquía. A continuación se indican los posibles valores:<br /><br /> **EncourageGrouping** (1)<br /><br /> **DiscourageGrouping** (2)|  
|**STRUCTURE_TYPE**|**DBTYPE_WSTR**|Indica el tipo de jerarquía. Los valores válidos son los siguientes:<br /><br /> **Natural**<br /><br /> **No naturales**<br /><br /> **Unknown**|  
  
 El conjunto de filas está ordenado en **CATALOG_NAME**, **SCHEMA_NAME**, **restricciones obligatorias CUBE_NAME**, **DIMENSION_UNIQUE_NAME**, **HIERARCHY_ NOMBRE**.  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El **MDSCHEMA_HIERARCHIES** se puede restringir el conjunto de filas en las columnas enumeradas en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**RESTRICCIONES OBLIGATORIAS CUBE_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**DIMENSION_UNIQUE_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**HIERARCHY_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**HIERARCHY_UNIQUE_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**HIERARCHY_ORIGIN**|**DBTYPE_UI2**|(Opcional) Una restricción predeterminada está en vigor en MD_USER_DEFINED y MD_SYSTEM_ENABLED.|  
|**CUBE_SOURCE**|**DBTYPE_UI2**|(Opcional) La restricción predeterminada es un valor de 1. Un mapa de bits con uno de los siguientes valores válidos:<br /><br /> 1 CUBO<br /><br /> 2 DIMENSIÓN|  
|**HIERARCHY_VISIBILITY**|**DBTYPE_UI2**|(Opcional) La restricción predeterminada es un valor de 1. Un mapa de bits con uno de los siguientes valores válidos:<br /><br /> 1 Visible<br /><br /> 2 no visible|  
  
## <a name="see-also"></a>Vea también  
 [OLE DB para los conjuntos de filas de esquema OLAP](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
