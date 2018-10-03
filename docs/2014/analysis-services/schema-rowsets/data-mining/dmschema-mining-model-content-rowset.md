---
title: Conjunto de filas DMSCHEMA_MINING_MODEL_CONTENT | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DMSCHEMA_MINING_MODEL_CONTENT
topic_type:
- apiref
helpviewer_keywords:
- DMSCHEMA_MINING_MODEL_CONTENT rowset
ms.assetid: 1e85d9e7-3b74-42ac-b94e-f52f76d8a25d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e23e78bd3588dd31a11c39941572645fb11771d1
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48172285"
---
# <a name="dmschemaminingmodelcontent-rowset"></a>Conjunto de filas DMSCHEMA_MINING_MODEL_CONTENT
  Permite a la aplicación cliente examinar el contenido de un modelo de minería de datos. Las aplicaciones cliente pueden utilizar las restricciones de las operaciones de árbol especiales descritas al final de este tema para navegar por el contenido del modelo de minería de datos.  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El `DMSCHEMA_MINING_MODEL_CONTENT` conjunto de filas contiene las siguientes columnas.  
  
|Nombre de columna|Indicador de tipo|Longitud|Descripción|  
|-----------------|--------------------|------------|-----------------|  
|`MODEL_CATALOG`|`DBTYPE_WSTR`||Nombre del catálogo. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] rellena esta columna con el nombre de la base de datos de los cuales es miembro el modelo.|  
|`MODEL_SCHEMA`|`DBTYPE_WSTR`||Nombre del esquema sin certificar. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] no admite esta columna; siempre contiene `VT_NULL`.|  
|`MODEL_NAME`|`DBTYPE_WSTR`||Nombre del modelo con el que se asocia el contenido descrito por esta fila.|  
|`ATTRIBUTE_NAME`|`DBTYPE_WSTR`||Nombres de los atributos que corresponden a este nodo.|  
|`NODE_NAME`|`DBTYPE_WSTR`||Nombre del nodo. Actualmente, esta columna contiene el mismo valor que `NODE_UNIQUE_NAME`, aunque esto podría cambiar en versiones futuras.|  
|`NODE_UNIQUE_NAME`|`DBTYPE_WSTR`||Nombre único del nodo.|  
|`NODE_TYPE`|`DBTYPE_I4`||El tipo de nodo. Generará uno de los siguientes valores (los algoritmos de minería de datos desarrollados por terceros pueden ampliar esta lista):<br /><br /> -   `DM_NODE_TYPE_CLASSIFICATION_TREE_ROOT` (`2`)<br />-   `DM_NODE_TYPE_TREE_INTERIOR` (`3`)<br />-   `DM_NODE_TYPE_TREE_DISTRIBUTION` (`4`)<br />-   `DM_NODE_TYPE_CLUSTER` (`5`)<br />-   `DM_NODE_TYPE_UNKNOWN` (`6`)<br />-   `DM_NODE_TYPE_ITEMSET` (`7`)<br />-   `DM_NODE_TYPE_ASSOCIATION_RULE` (`8`)<br />-   `DM_NODE_TYPE_NB_PREDICTABLE_ATTRIBUTE` (`9`)<br />-   `DM_NODE_TYPE_NB_INPUT_ATTRIBUTE` (`10`)<br />-   `DM_NODE_TYPE_NB_INPUT_ATTRIBUTE_STATE` (`11`)<br />-   `DM_NODE_TYPE_SEQUENCE` (`13`)<br />-   `DM_NODE_TYPE_TRANSITION` (`14`)<br />-   `DM_NODE_TYPE_TIME_SERIES` (`15`)<br />-   `DM_NODE_TYPE_TS_TREE` (`16`)<br />-   `DM_NODE_TYPE_NN_SUBNETWORK` (`17`) Red neuronal, subred<br />-   `DM_NODE_TYPE_NN_INPUT_LAYER` (`18`) Red neuronal, nivel de entrada (elemento primario de los nodos de entrada)<br />-   **DM_NODE_TYPE_NN_HIDDEN_LAYER** (`19`) Red neuronal, nivel oculto (elemento primario de los nodos ocultos)<br />-   `DM_NODE_TYPE_NN_OUTPUT_LAYER` (`20`) Red neuronal, nivel de salida (elemento primario de los nodos de salida)<br />-   `DM_NODE_TYPE_NN_INPUT_NODE` (`21`) Red neuronal, nodo de entrada<br />-   `DM_NODE_TYPE_NN_HIDDEN_NODE` (`22`) Red neuronal, nodo oculto<br />-   `DM_NODE_TYPE_NN_OUTPUT_NODE` (`23`) Red neuronal, nodo de salida<br />-   `DM_NODE_TYPE_NN_MARGINAL_STAT_NODE` (`24`) Red neuronal, nodo de estadísticas marginales<br />-   **DM_NODE_TYPE_REGRESSION_TREE_ROOT** (`25`)<br />-   `DM_NODE_TYPE_NB_MARGINAL_STAT_NODE` (`26`) Red neuronal, nodo de estadísticas marginales|  
|`NODE_GUID`|`DBTYPE_GUID`||GUID del nodo. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] no admite esta columna; siempre contiene `NULL`.|  
|`NODE_CAPTION`|`DBTYPE_WSTR`||Etiqueta o título asociado al nodo. Esta propiedad se usa principalmente para la presentación.|  
|`CHILDREN_CARDINALITY`|`DBTYPE_UI4`||Cálculo del número de elementos secundarios que tiene el nodo.|  
|`PARENT_UNIQUE_NAME`|`DBTYPE_WSTR`||Nombre único del nodo primario del nodo. Se devuelve `NULL` para todos los nodos del nivel raíz.|  
|`NODE_DESCRIPTION`|`DBTYPE_WSTR`||Descripción fácil de comprender del nodo.|  
|`NODE_RULE`|`DBTYPE_WSTR`||Descripción XML de la regla que está incrustada en el nodo.|  
|`MARGINAL_RULE`|`DBTYPE_WSTR`||Descripción XML de la regla que se mueve al nodo desde el nodo primario.|  
|`NODE_PROBABILITY`|`DBTYPE_R8`||Probabilidad asociada a este nodo.|  
|`MARGINAL_PROBABILITY`|`DBTYPE_R8`||Probabilidad de alcanzar el nodo desde el nodo primario.|  
|`NODE_DISTRIBUTION`|`DBTYPE_HCHAPTER`||Tabla que contiene el histograma de probabilidad del nodo.|  
|`NODE_SUPPORT`|`DBTYPE_R8`||Número de casos que admiten este nodo.|  
|`MSOLAP_MODEL_COLUMN`|`DBTYPE_WSTR`||Nombre de la columna de la definición de modelo a la que pertenece este nodo.|  
|`MSOLAP_NODE_SCORE`|`DBTYPE_R8`||Puntuación calculada para este nodo.|  
|`MSOLAP_NODE_SHORT_CAPTION`|`DBTYPE_WSTR`||Título corto para el nodo que se puede utilizar para la visualización a fin de mejorar la legibilidad.|  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El `DMSCHEMA_MINING_MODEL_CONTENT` conjunto de filas puede tener restricciones en las columnas enumeradas en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|`MODEL_CATALOG`|`DBTYPE_WSTR`|Opcional.|  
|`MODEL_SCHEMA`|`DBTYPE_WSTR`|Opcional.|  
|`MODEL_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`ATTRIBUTE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`NODE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`NODE_UNIQUE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`NODE_TYPE`|`DBTYPE_I4`|Opcional.|  
|`NODE_GUID`|`DBTYPE_WSTR`|Opcional.|  
|`NODE_CAPTION`|`DBTYPE_WSTR`|Opcional.|  
|`TREE_OPERATION`|`DBTYPE_UI4`|Opcional. Consulte las notas adicionales más adelante.|  
  
 La restricción, `TREE_OPERATION`, no se aplica a una columna determinada del conjunto de filas `DMSCHEMA_MINING_MODEL_CONTENT`; en su lugar, especifica un operador de árbol. El usuario puede especificar una restricción `NODE_UNIQUE_NAME` y el operador de árbol (`ANCESTORS`, `CHILDREN`, `SIBLINGS`, `PARENT`, `DESCENDANTS`, `SELF`) para obtener el conjunto de miembros solicitado. El operador `SELF` incluye la fila del propio nodo en la lista de filas devueltas. En la tabla siguiente se describen las constantes que componen la definición del mapa de bits para la restricción `TREE_OPERATION`. Pueden combinarse mediante el operador lógico `OR`.  
  
|Constante|Valor|  
|--------------|-----------|  
|**DMTREEOP_ANCESTORS**|`0x00000020`|  
|**DMTREEOP_CHILDREN**|`0x00000001`|  
|**DMTREEOP_SIBLINGS**|`0x00000002`|  
|**DMTREEOP_PARENT**|`0x00000004`|  
|**DMTREEOP_SELF**|`0x00000008`|  
|**DMTREEOP_DESCENDANTS**|`0x00000010`|  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas de esquema de minería de datos](../../schema-rowsets/data-mining/data-mining-schema-rowsets.md) 
  
  
