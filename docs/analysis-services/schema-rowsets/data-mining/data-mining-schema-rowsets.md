---
title: "Conjuntos de filas de esquema de minería de datos | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: schema-rowsets
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- schema rowsets [Analysis Services], data mining
- schema rowsets [Analysis Services]
- rowsets [Analysis Services], data mining
- data mining [Analysis Services], schema rowsets
ms.assetid: bd7d5df5-500b-4159-8467-880e141bc043
caps.latest.revision: "44"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 35f4df3e7e01a8f0987e955a180842efde5793e1
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="data-mining-schema-rowsets"></a>Data Mining Schema Rowsets
  Un servidor que ejecuta [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] admite los siguientes conjuntos de filas de esquema de minería de datos. Para comprobar si un proveedor XML/A determinado admite un conjunto de filas específica, use la [DISCOVER_ENUMERATORS](../../../analysis-services/schema-rowsets/xml/discover-enumerators-rowset.md) conjunto de filas con el [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) método.  
  
 En [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], los conjuntos de filas de esquema de minería de datos se exponen también como tablas en el lenguaje Transact-SQL, en el esquema $SYSTEM. Por ejemplo, la consulta siguiente en una instancia de Analysis Services devuelve una lista de los esquemas que están disponibles en la instancia actual.  
  
```  
SELECT * FROM [$system].[DBSCHEMA_TABLES]  
```  
  
## <a name="in-this-section"></a>En esta sección  
  
|Conjunto de filas de esquema|Description|  
|-------------------|-----------------|  
|[Conjunto de filas DMSCHEMA_MINING_COLUMNS](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-columns-rowset.md)|Describe las columnas individuales de todos los modelos de minería de datos definidos que se implementan en el servidor.|  
|[Conjunto de filas DMSCHEMA_MINING_FUNCTIONS](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-functions-rowset.md)|Describe las funciones de predicción y de minería de datos que se pueden utilizar con cada algoritmo de la minería de datos que se instala en el servidor.|  
|[Conjunto de filas DMSCHEMA_MINING_MODEL_CONTENT](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-model-content-rowset.md)|Permite a la aplicación cliente examinar el contenido de un modelo de minería de datos entrenado.|  
|[Conjunto de filas DMSCHEMA_MINING_MODEL_CONTENT_PMML](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-model-content-pmml-rowset.md)|Devuelve la representación XML (PMML 2.1) del contenido del modelo de minería de datos.|  
|[Conjunto de filas DMSCHEMA_MINING_MODEL_XML](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-model-xml-rowset.md)|Devuelve la estructura XML (PMML 2.1) del modelo de minería de datos. Este es el mismo esquema que DMSCHEMA_MINING_MODEL_PMML, que se conserva para mantener la compatibilidad con las versiones anteriores.|  
|[Conjunto de filas DMSCHEMA_MINING_MODELS](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-models-rowset.md)|Enumera los modelos de minería de datos implementados en el servidor.|  
|[Conjunto de filas DMSCHEMA_MINING_SERVICE_PARAMETERS](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-service-parameters-rowset.md)|Proporciona una lista de los parámetros que se pueden utilizar para configurar el comportamiento de cada algoritmo de minería de datos que está instalado en el servidor.|  
|[Conjunto de filas DMSCHEMA_MINING_SERVICES](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-services-rowset.md)|Proporciona una descripción de cada algoritmo de minería de datos que está disponible en el servidor.|  
|[Conjunto de filas DMSCHEMA_MINING_STRUCTURE_COLUMNS](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-structure-columns-rowset.md)|Describe las columnas individuales de todas las estructuras de minería de datos que se implementan en el servidor.|  
|[Conjunto de filas DMSCHEMA_MINING_STRUCTURES](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-structures-rowset.md)|Enumera información sobre las estructuras de minería de datos.|  
  
 Todos los conjuntos de filas de esquema enumerados aquí son compatibles con el servidor que ejecuta [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas de esquema de Analysis Services](../../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)   
 [Conjuntos de filas de esquema de minería de datos &#40; SSAs &#41;](../../../analysis-services/data-mining/data-mining-schema-rowsets-ssas.md)  
  
  
