---
title: Conjuntos de filas de esquema de minería de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
- apinav
helpviewer_keywords:
- schema rowsets [Analysis Services], data mining
- schema rowsets [Analysis Services]
- rowsets [Analysis Services], data mining
- data mining [Analysis Services], schema rowsets
ms.assetid: bd7d5df5-500b-4159-8467-880e141bc043
caps.latest.revision: 43
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1a3b3e54f53eb93ea58a45c92e88503a186a441f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37210055"
---
# <a name="data-mining-schema-rowsets"></a>Data Mining Schema Rowsets
  Un servidor que ejecuta [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] admite los siguientes conjuntos de filas de esquema de minería de datos. Para comprobar si un proveedor XML/A determinado admite un conjunto de filas específica, use el [DISCOVER_ENUMERATORS](../xml/discover-enumerators-rowset.md) conjunto de filas con el [Discover](../../xmla/xml-elements-methods-discover.md) método.  
  
 En [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], los conjuntos de filas de esquema de minería de datos se exponen también como tablas en el lenguaje Transact-SQL, en el esquema $SYSTEM. Por ejemplo, la consulta siguiente en una instancia de Analysis Services devuelve una lista de los esquemas que están disponibles en la instancia actual.  
  
```  
SELECT * FROM [$system].[DBSCHEMA_TABLES]  
```  
  
## <a name="in-this-section"></a>En esta sección  
  
|Conjunto de filas de esquema|Descripción|  
|-------------------|-----------------|  
|[Conjunto de filas DMSCHEMA_MINING_COLUMNS](dmschema-mining-columns-rowset.md)|Describe las columnas individuales de todos los modelos de minería de datos definidos que se implementan en el servidor.|  
|[Conjunto de filas DMSCHEMA_MINING_FUNCTIONS](dmschema-mining-functions-rowset.md)|Describe las funciones de predicción y de minería de datos que se pueden utilizar con cada algoritmo de la minería de datos que se instala en el servidor.|  
|[Conjunto de filas DMSCHEMA_MINING_MODEL_CONTENT](dmschema-mining-model-content-rowset.md)|Permite a la aplicación cliente examinar el contenido de un modelo de minería de datos entrenado.|  
|[Conjunto de filas DMSCHEMA_MINING_MODEL_CONTENT_PMML](dmschema-mining-model-content-pmml-rowset.md)|Devuelve la representación XML (PMML 2.1) del contenido del modelo de minería de datos.|  
|[Conjunto de filas DMSCHEMA_MINING_MODEL_XML](dmschema-mining-model-xml-rowset.md)|Devuelve la estructura XML (PMML 2.1) del modelo de minería de datos. Este es el mismo esquema que DMSCHEMA_MINING_MODEL_PMML, que se conserva para mantener la compatibilidad con las versiones anteriores.|  
|[Conjunto de filas DMSCHEMA_MINING_MODELS](dmschema-mining-models-rowset.md)|Enumera los modelos de minería de datos implementados en el servidor.|  
|[Conjunto de filas DMSCHEMA_MINING_SERVICE_PARAMETERS](dmschema-mining-service-parameters-rowset.md)|Proporciona una lista de los parámetros que se pueden utilizar para configurar el comportamiento de cada algoritmo de minería de datos que está instalado en el servidor.|  
|[Conjunto de filas DMSCHEMA_MINING_SERVICES](dmschema-mining-services-rowset.md)|Proporciona una descripción de cada algoritmo de minería de datos que está disponible en el servidor.|  
|[Conjunto de filas DMSCHEMA_MINING_STRUCTURE_COLUMNS](dmschema-mining-structure-columns-rowset.md)|Describe las columnas individuales de todas las estructuras de minería de datos que se implementan en el servidor.|  
|[Conjunto de filas DMSCHEMA_MINING_STRUCTURES](dmschema-mining-structures-rowset.md)|Enumera información sobre las estructuras de minería de datos.|  
  
 Todos los conjuntos de filas de esquema enumerados aquí son compatibles con el servidor que ejecuta [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas de esquema de Analysis Services](../../schema-rowsets/analysis-services-schema-rowsets.md)   
 [Consultar el catálogo del sistema SQL Server](https://technet.microsoft.com/en-us/library/ms189082\(v=sql.110\).aspx)   
 [Consultar los conjuntos de filas de esquema de minería de datos &#40;Analysis Services - minería de datos&#41;](../../data-mining/data-mining-schema-rowsets-ssas.md)  
  
  
