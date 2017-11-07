---
title: "Propiedades del modelo de minería de datos | Documentos de Microsoft"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mining models [Analysis Services], properties
- data mining [Analysis Services], properties
- columns [data mining], properties
- Data Mining Designer
- properties [data mining]
ms.assetid: c5194619-8b31-42be-a95f-585711462945
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1fa45b604df0a118936f903491e707bd09d58295
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="mining-model-properties"></a>Propiedades del modelo de minería de datos
  Los modelos de minería de datos tienen las siguientes clases de propiedades:  
  
-   Las propiedades que se heredan de la estructura de minería de datos que define el tipo de datos y el tipo de contenido de los datos que usa el modelo;  
  
-   Las propiedades relacionadas con el algoritmo que se usa para crear el modelo de minería de datos, incluidos los parámetros de cliente;  
  
-   Las propiedades que definen un filtro en el modelo utilizado para entrenar el modelo.  
  
 Las propiedades de un modelo de minería de datos se definen inicialmente al crear el modelo; sin embargo, puede modificar la mayoría de las propiedades posteriormente, incluidos los parámetros de algoritmo, los filtros y las propiedades de uso de la columna. Puede cambiar las propiedades mediante la pestaña **Modelos de minería de datos** del Diseñador de minería de datos o bien usando AMO o XMLA.  
  
 Siempre que cambia alguna propiedad de un modelo, debe volver a procesarlo para que refleje los cambios. Es necesario volver a procesar incluso si el cambio afecta solamente a los metadatos, como agregar un alias o una descripción de columna.  
  
## <a name="properties-of-models"></a>Propiedades de los modelos  
 En la tabla siguiente se describen las propiedades específicas de los modelos de minería de datos. Además, hay propiedades que puede establecer en columnas individuales de la minería de datos  
  
|Propiedad|Description|  
|--------------|-----------------|  
|**Algoritmo**|Establece el tipo de algoritmo para el modelo de minería de datos.|  
|**AlgorithmParameters**|Establece los valores de los parámetros de algoritmo disponibles para cada tipo de algoritmo.|  
|**Filtro**|Establece un filtro que se aplica a los datos que se utilizan para el aprendizaje y prueba del modelo de minería de datos. La definición del filtro está almacenada con el modelo y se utiliza opcionalmente al crear consultas de predicción o al probar la exactitud del modelo.<br /><br /> El filtro de modelos no es opcional en el aprendizaje del modelo.|  
|**Nombre**|Establece el nombre del modelo de minería de datos.|  
|**AllowDrillThrough**|Especifica si se habilita la obtención de detalles en el modelo de minería de datos.|  
  
## <a name="properties-of-model-columns"></a>Propiedades de las columnas de un modelo  
 Puede configurar las siguientes propiedades específicas de la minería de datos para cada columna de un modelo de minería de datos. Puede establecer estas propiedades con un valor diferente para cada modelo de la estructura de minería de datos.  
  
|Propiedad|Description|  
|--------------|-----------------|  
|**Description**|Describe el propósito de la columna de minería.|  
|**Nombre**|Establece el nombre de la columna del modelo de minería de datos. Puede escribir un nuevo nombre que sirva de alias para la columna del modelo de minería de datos.|  
|**ModelingFlags**|Configura las marcas específicas de algoritmo de la columna.|  
|**SourceColumnID**|Indica el nombre de la columna de estructura de minería de datos en la que se basa la columna de modelo.<br /><br /> Esta propiedad es de solo lectura.|  
|**Uso**|Establece la forma en que el modelo de minería de datos va a utilizar la columna.|  
  
## <a name="see-also"></a>Vea también  
 [Columnas del modelo de minería de datos](../../analysis-services/data-mining/mining-model-columns.md)   
 [Estructuras de minería de datos &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [Tareas y procedimientos de los modelos de minería de datos](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)   
 [Cambiar las propiedades de un modelo de minería de datos](../../analysis-services/data-mining/change-the-properties-of-a-mining-model.md)   
 [Herramientas de minería de datos](../../analysis-services/data-mining/data-mining-tools.md)   
 [Crear una estructura de minería de datos relacional](../../analysis-services/data-mining/create-a-relational-mining-structure.md)   
 [Crear un alias para una columna de modelo](../../analysis-services/data-mining/create-an-alias-for-a-model-column.md)  
  
  

