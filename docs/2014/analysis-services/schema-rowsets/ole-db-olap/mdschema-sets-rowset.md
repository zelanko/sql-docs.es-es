---
title: Conjunto de filas MDSCHEMA_SETS | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- MDSCHEMA_SETS
topic_type:
- apiref
helpviewer_keywords:
- MDSCHEMA_SETS rowset
ms.assetid: abb00dc0-2b83-48d6-b2ba-6615c1488d06
caps.latest.revision: 36
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fecc8167d697be2195c9ae44e214afcbc1f3a05b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37275481"
---
# <a name="mdschemasets-rowset"></a>Conjunto de filas MDSCHEMA_SETS
  Describe los conjuntos definidos actualmente en una base de datos, incluidos los conjuntos de ámbito de sesión.  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El `MDSCHEMA_SETS` conjunto de filas contiene las siguientes columnas.  
  
|Nombre de columna|Indicador de tipo|Longitud|Descripción|  
|-----------------|--------------------|------------|-----------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`||El nombre de la base de datos.|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`||No compatible.|  
|`CUBE_NAME`|`DBTYPE_WSTR`||Nombre del cubo.|  
|`SET_NAME`|`DBTYPE_WSTR`||Nombre del conjunto, como se especifica en la instrucción `CREATE SET`.|  
|`SCOPE`|`DBTYPE_I4`||Ámbito del conjunto:<br /><br /> -   `MDSET_SCOPE_GLOBAL` (`1`)<br />-   `MDSET_SCOPE_SESSION` (`2`)|  
|`DESCRIPTION`|`DBTYPE_WSTR`||No compatible.|  
|`EXPRESSION`|`DBTYPE_WSTR`||Expresión para el conjunto.|  
|`DIMENSIONS`|`DBTYPE_WSTR`||Lista delimitada por comas de las jerarquías incluidas en el conjunto.|  
|`SET_CAPTION`|`DBTYPE_WSTR`||Etiqueta o título asociado al conjunto. La etiqueta o el título se utilizan principalmente para la presentación.|  
|`SET_DISPLAY_FOLDER`|`DBTYPE_WSTR`||Cadena que identifica la ruta de la carpeta que usa la aplicación cliente para mostrar el conjunto. La aplicación cliente define el separador de niveles de carpetas. Para las herramientas y clientes proporcionados por [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], la barra diagonal inversa (\\) es el separador de niveles. Para proporcionar varias carpetas para mostrar, use un punto y coma (;) para separar las carpetas.|  
|`SET_EVALUATION_CONTEXT`|`DBTYPE_I4`||Contexto para el conjunto. El conjunto puede ser estático o dinámico.<br /><br /> Esta columna admite cualquiera de los siguientes valores:<br /><br /> -MDSET_RESOLUTION_STATIC = 1<br />-MDSET_RESOLUTION_DYNAMIC = 2|  
  
 El conjunto de filas se ordena en `CATALOG_NAME`, `SCHEMA_NAME`, `CUBE_NAME`.  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El `MDSCHEMA_SETS` conjunto de filas puede tener restricciones en las columnas enumeradas en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`CUBE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`SET_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`SCOPE`|`DBTYPE_I4`|Opcional.|  
|`HIERARCHY_UNIQUE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`CUBE_SOURCE`|`DBTYPE_UI2`|Opcional. **Nota:** se puede incluir sólo una jerarquía, y solo los conjuntos con nombre cuyas jerarquías coinciden exactamente con la restricción se devuelven.|  
  
## <a name="see-also"></a>Vea también  
 [OLE DB para los conjuntos de filas de esquema OLAP](ole-db-for-olap-schema-rowsets.md)  
  
  
