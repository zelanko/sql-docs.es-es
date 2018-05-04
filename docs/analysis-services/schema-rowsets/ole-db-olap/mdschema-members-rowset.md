---
title: Conjunto de filas MDSCHEMA_MEMBERS | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- MDSCHEMA_MEMBERS
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- MDSCHEMA_MEMBERS rowset
ms.assetid: 0b1aada0-67f8-4ef6-81b2-0100b65e0c2f
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: a199a80277c56825dad9d5ac00909244b57844d4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="mdschemamembers-rowset"></a>Conjunto de filas MDSCHEMA_MEMBERS
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Describe los miembros incluidos en una base de datos.  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El **MDSCHEMA_MEMBERS** filas contiene las columnas siguientes.  
  
|Nombre de columna|Indicador de tipo|Longitud|Description|  
|-----------------|--------------------|------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**||Nombre de la base de datos a la que pertenece este miembro.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**||Nombre del esquema al que pertenece este miembro.|  
|**RESTRICCIONES OBLIGATORIAS CUBE_NAME**|**DBTYPE_WSTR**||Nombre del cubo al que pertenece este miembro.|  
|**DIMENSION_UNIQUE_NAME**|**DBTYPE_WSTR**||Nombre único de la dimensión a la que pertenece este miembro.|  
|**HIERARCHY_UNIQUE_NAME**|**DBTYPE_WSTR**||Nombre único de la jerarquía a la que pertenece este miembro.|  
|**LEVEL_UNIQUE_NAME**|**DBTYPE_WSTR**||Nombre único del nivel al que pertenece este miembro.|  
|**LEVEL_NUMBER**|**DBTYPE_UI4**||Distancia al miembro desde la raíz de la jerarquía. El nivel raíz es cero (0).|  
|**MEMBER_ORDINAL**|**DBTYPE_UI4**||(Desusado) Siempre devuelve **0**.|  
|**MEMBER_NAME**|**DBTYPE_WSTR**||Nombre del miembro.|  
|**MEMBER_UNIQUE_NAME**|**DBTYPE_WSTR**||Nombre único del miembro.|  
|**MEMBER_TYPE**|**DBTYPE_I4**||Tipo del miembro:<br /><br /> **MDMEMBER_TYPE_UNKNOWN** (**0**)<br /><br /> **MDMEMBER_TYPE_REGULAR** (**1**)<br /><br /> **MDMEMBER_TYPE_ALL** (**2**)<br /><br /> **MDMEMBER_TYPE_MEASURE** (**3**)<br /><br /> **MDMEMBER_TYPE_FORMULA** (**4**)<br /><br /> <br /><br /> Tenga en cuenta que <br />                    **MDMEMBER_TYPE_FORMULA**tiene prioridad sobre **MDMEMBER_TYPE_MEASURE**. Por ejemplo, si hay un miembro (calculado) de fórmula en la dimensión Measures, aparece como **MDMEMBER_TYPE_FORMULA**.|  
|**MEMBER_GUID**|**DBTYPE_GUID**||GUID del miembro. **NULL** si no existe ningún GUID.|  
|**MEMBER_CAPTION**|**DBTYPE_WSTR**||Etiqueta o descripción asociada al miembro. Se utiliza principalmente para la presentación. Si no existe ningún título, **MEMBER_NAME** se devuelve.|  
|**CHILDREN_CARDINALITY**|**DBTYPE_UI4**||Número de elementos secundarios que tiene este miembro. Puede ser una estimación; por tanto, los usuarios no deben pensar que este valor es el recuento exacto. Los proveedores deben devolver la mejor estimación posible.|  
|**PARENT_LEVEL**|**DBTYPE_UI4**||Distancia al primario del miembro desde el nivel raíz de la jerarquía. El nivel raíz es cero (0).|  
|**PARENT_UNIQUE_NAME**|**DBTYPE_WSTR**||Nombre único del elemento primario del miembro. Se devuelve**NULL** para todos los miembros del nivel raíz.|  
|**PARENT_COUNT**|**DBTYPE_UI4**||Número de primarios que tiene este miembro.|  
|**DESCRIPTION**|**DBTYPE_WSTR**||Esta columna siempre devuelve un **NULL** valor.<br /><br /> La columna existe por compatibilidad con versiones anteriores.|  
|**EXPRESIÓN**|**DBTYPE_WSTR**||La expresión para los cálculos, si el miembro es de tipo **MDMEMBER_TYPE_FORMULA**.|  
|**MEMBER_KEY**|**DBTYPE_WSTR**||Valor de la columna de clave del miembro. Devuelve **NULL** si el miembro tiene una clave compuesta.|  
|**IS_PLACEHOLDERMEMBER**|**DBTYPE_BOOL**||Valor booleano que indica si un miembro es un miembro de marcador de posición para una posición vacía en una jerarquía de dimensión.<br /><br /> Es válido únicamente si el **MDX Compatibility** propiedad se ha establecido en 2.|  
|**IS_DATAMEMBER**|**DBTYPE_BOOL**||Valor booleano que indica si el miembro es un miembro de datos.<br /><br /> Devuelve True si el miembro es un miembro de datos.|  
|**ÁMBITO**|**DBTYPE_I4**||Ámbito del miembro. El miembro puede ser un miembro de sesión calculado o un miembro calculado global. Devuelve la columna **NULL** para los miembros no calculados. Esta columna admite cualquiera de los siguientes valores:<br /><br /> MDMEMBER_SCOPE_GLOBAL=1<br /><br /> MDMEMBER_SCOPE_SESSION=2|  
|**Cero o más columnas adicionales**|**DBTYPE_UI2**||No se devuelve ninguna propiedad si es posible que los miembros se devuelvan de varios niveles. Por ejemplo, si el operador de árbol es **primario** y **SELF** para una jerarquía de elementos no primarios y secundarios, se devuelve ninguna propiedad de miembro.<br /><br /> Esto se aplica a las jerarquías desiguales donde los operadores de árbol pueden devolver miembros de distintos niveles (por ejemplo, si el nivel anterior contiene agujeros y se solicitan elementos primarios de los miembros).|  
  
 El conjunto de filas está ordenado en **CATALOG_NAME**, **SCHEMA_NAME**, **restricciones obligatorias CUBE_NAME**, **DIMENSION_UNIQUE_NAME**, **HIERARCHY_ UNIQUE_NAME**, **LEVEL_UNIQUE_NAME**, **LEVEL_NUMBER**, **MEMBER_ORDINAL**.  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El **MDSCHEMA_MEMBERS** se puede restringir el conjunto de filas en las columnas enumeradas en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**RESTRICCIONES OBLIGATORIAS CUBE_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**DIMENSION_UNIQUE_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**HIERARCHY_UNIQUE_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**LEVEL_UNIQUE_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**LEVEL_NUMBER**|**DBTYPE_UI4**|Opcional.|  
|**MEMBER_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**MEMBER_UNIQUE_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**MEMBER_CAPTION**|**DBTYPE_WSTR**|Opcional.|  
|**MEMBER_TYPE**|**DBTYPE_I4**|Opcional.|  
|**TREE_OP**|**DBTYPE_I4**|(Opcional) Solo se aplica a un único miembro:<br /><br /> **MDTREEOP_ANCESTORS** (**0 x 20**) devuelve todos los antecesores.<br /><br /> **MDTREEOP_CHILDREN** (**0 x 01**) devuelve solo los elementos secundarios inmediatos.<br /><br /> **MDTREEOP_SIBLINGS** (**0 x 02**) devuelve los miembros del mismo nivel.<br /><br /> **MDTREEOP_PARENT** (**0 x 04**) devuelve solo el elemento primario inmediato.<br /><br /> **MDTREEOP_SELF** (**0 x 08**) devuelve a sí mismo en la lista de filas devueltas.<br /><br /> **MDTREEOP_DESCENDANTS** (**0 x 10**) devuelve todos los descendientes.|  
|**CUBE_SOURCE**|**DBTYPE_UI2**|(Opcional) La restricción predeterminada es un valor de 1. Un mapa de bits con uno de los siguientes valores válidos:<br /><br /> 1 CUBO<br /><br /> 2 DIMENSIÓN|  
  
## <a name="see-also"></a>Vea también  
 [OLE DB para OLAP Schema Rowsets](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
