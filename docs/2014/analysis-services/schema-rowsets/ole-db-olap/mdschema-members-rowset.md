---
title: Conjunto de filas MDSCHEMA_MEMBERS | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MDSCHEMA_MEMBERS
topic_type:
- apiref
helpviewer_keywords:
- MDSCHEMA_MEMBERS rowset
ms.assetid: 0b1aada0-67f8-4ef6-81b2-0100b65e0c2f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: dbe7db640163f539ba15e8418177846564731148
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48133905"
---
# <a name="mdschemamembers-rowset"></a>Conjunto de filas MDSCHEMA_MEMBERS
  Describe los miembros incluidos en una base de datos.  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El `MDSCHEMA_MEMBERS` conjunto de filas contiene las siguientes columnas.  
  
|Nombre de columna|Indicador de tipo|Longitud|Descripción|  
|-----------------|--------------------|------------|-----------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`||Nombre de la base de datos a la que pertenece este miembro.|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`||Nombre del esquema al que pertenece este miembro.|  
|`CUBE_NAME`|`DBTYPE_WSTR`||Nombre del cubo al que pertenece este miembro.|  
|`DIMENSION_UNIQUE_NAME`|`DBTYPE_WSTR`||Nombre único de la dimensión a la que pertenece este miembro.|  
|`HIERARCHY_UNIQUE_NAME`|`DBTYPE_WSTR`||Nombre único de la jerarquía a la que pertenece este miembro.|  
|`LEVEL_UNIQUE_NAME`|`DBTYPE_WSTR`||Nombre único del nivel al que pertenece este miembro.|  
|`LEVEL_NUMBER`|`DBTYPE_UI4`||Distancia al miembro desde la raíz de la jerarquía. El nivel raíz es cero (0).|  
|`MEMBER_ORDINAL`|`DBTYPE_UI4`||(Obsoleto) Siempre devuelve `0`.|  
|`MEMBER_NAME`|`DBTYPE_WSTR`||Nombre del miembro.|  
|`MEMBER_UNIQUE_NAME`|`DBTYPE_WSTR`||Nombre único del miembro.|  
|`MEMBER_TYPE`|`DBTYPE_I4`||Tipo del miembro:<br /><br /> -   `MDMEMBER_TYPE_REGULAR` (`1`)<br />-   `MDMEMBER_TYPE_ALL` (`2`)<br />-   `MDMEMBER_TYPE_MEASURE` (`3`)<br />-   `MDMEMBER_TYPE_FORMULA` (`4`)<br />-   `MDMEMBER_TYPE_UNKNOWN` (`0`)<br />-   `MDMEMBER_TYPE_FORMULA` tiene prioridad sobre `MDMEMBER_TYPE_MEASURE`. Por ejemplo, si hay un miembro (calculado) de fórmula en la dimensión Measures, aparece como `MDMEMBER_TYPE_FORMULA`.|  
|`MEMBER_GUID`|`DBTYPE_GUID`||GUID del miembro. Su valor es `NULL` si no existe ningún GUID.|  
|`MEMBER_CAPTION`|`DBTYPE_WSTR`||Etiqueta o descripción asociada al miembro. Se utiliza principalmente para la presentación. Si no existe ningún título, se devuelve `MEMBER_NAME`.|  
|`CHILDREN_CARDINALITY`|`DBTYPE_UI4`||Número de elementos secundarios que tiene este miembro. Puede ser una estimación; por tanto, los usuarios no deben pensar que este valor es el recuento exacto. Los proveedores deben devolver la mejor estimación posible.|  
|`PARENT_LEVEL`|`DBTYPE_UI4`||Distancia al primario del miembro desde el nivel raíz de la jerarquía. El nivel raíz es cero (0).|  
|`PARENT_UNIQUE_NAME`|`DBTYPE_WSTR`||Nombre único del elemento primario del miembro. Se devuelve `NULL` para todos los miembros del nivel raíz.|  
|`PARENT_COUNT`|`DBTYPE_UI4`||Número de primarios que tiene este miembro.|  
|`DESCRIPTION`|`DBTYPE_WSTR`||Esta columna siempre devuelve un valor `NULL`.<br /><br /> La columna existe por compatibilidad con versiones anteriores.|  
|`EXPRESSION`|`DBTYPE_WSTR`||Expresión para los cálculos, si el miembro es de tipo `MDMEMBER_TYPE_FORMULA`.|  
|`MEMBER_KEY`|`DBTYPE_WSTR`||Valor de la columna de clave del miembro. Devuelve `NULL` si el miembro tiene una clave compuesta.|  
|`IS_PLACEHOLDERMEMBER`|`DBTYPE_BOOL`||Valor booleano que indica si un miembro es un miembro de marcador de posición para una posición vacía en una jerarquía de dimensión.<br /><br /> Solamente es válido si la propiedad `MDX Compatibility` se ha establecido en 2.|  
|`IS_DATAMEMBER`|`DBTYPE_BOOL`||Valor booleano que indica si el miembro es un miembro de datos.<br /><br /> Devuelve True si el miembro es un miembro de datos.|  
|`SCOPE`|`DBTYPE_I4`||Ámbito del miembro. El miembro puede ser un miembro de sesión calculado o un miembro calculado global. La columna devuelve `NULL` para los miembros no calculados.<br /><br /> Esta columna admite cualquiera de los siguientes valores:<br /><br /> -MDMEMBER_SCOPE_GLOBAL = 1<br />-MDMEMBER_SCOPE_SESSION = 2|  
|`Zero or more additional columns`|`DBTYPE_UI2`||No se devuelve ninguna propiedad si es posible que los miembros se devuelvan de varios niveles. Por ejemplo, si el operador de árbol es `PARENT` y `SELF` para una jerarquía que no sea de elementos primarios y secundarios, no se devuelve ninguna propiedad de miembro.<br /><br /> Esto se aplica a las jerarquías desiguales donde los operadores de árbol pueden devolver miembros de distintos niveles (por ejemplo, si el nivel anterior contiene agujeros y se solicitan elementos primarios de los miembros).|  
  
 El conjunto de filas se ordena en `CATALOG_NAME`, `SCHEMA_NAME`, `CUBE_NAME`, `DIMENSION_UNIQUE_NAME`, `HIERARCHY_UNIQUE_NAME`, `LEVEL_UNIQUE_NAME`, `LEVEL_NUMBER`, `MEMBER_ORDINAL`.  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El `MDSCHEMA_MEMBERS` conjunto de filas puede tener restricciones en las columnas enumeradas en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`CUBE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`DIMENSION_UNIQUE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`HIERARCHY_UNIQUE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`LEVEL_UNIQUE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`LEVEL_NUMBER`|`DBTYPE_UI4`|Opcional.|  
|`MEMBER_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`MEMBER_UNIQUE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`MEMBER_CAPTION`|`DBTYPE_WSTR`|Opcional.|  
|`MEMBER_TYPE`|`DBTYPE_I4`|Opcional.|  
|`TREE_OP`|`DBTYPE_I4`|(Opcional) Solo se aplica a un único miembro:<br /><br /> -   `MDTREEOP_ANCESTORS` (`0x20`) devuelve todos los antecesores.<br />-   `MDTREEOP_CHILDREN` (`0x01`) devuelve solo los elementos secundarios inmediatos.<br />-   `MDTREEOP_SIBLINGS` (`0x02`) devuelve los miembros del mismo nivel.<br />-   `MDTREEOP_PARENT` (`0x04`) devuelve sólo el objeto primario inmediato.<br />-   `MDTREEOP_SELF` (`0x08`) devuelve a sí mismo en la lista de filas devueltas.<br />-   `MDTREEOP_DESCENDANTS` (`0x10`) devuelve todos los descendientes.|  
|`CUBE_SOURCE`|`DBTYPE_UI2`|(Opcional) Mapa de bits con uno de los siguientes valores válidos:<br /><br /> -1 CUBO<br />-DIMENSIÓN DE 2<br /><br /> La restricción predeterminada es un valor de 1.|  
  
## <a name="see-also"></a>Vea también  
 [OLE DB para los conjuntos de filas de esquema OLAP](ole-db-for-olap-schema-rowsets.md)  
  
  
