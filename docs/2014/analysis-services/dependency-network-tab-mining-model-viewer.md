---
title: Pestaña red de dependencias (Visor de modelos de minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.dependencynetwork.f1
ms.assetid: e58ce1b7-20d6-42cb-ade5-916da8471e09
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 819a69ad9c1b1415726d816e2cbc1faa92bd6cd1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66081940"
---
# <a name="dependency-network-tab-mining-model-viewer"></a>Pestaña Red de dependencias (Visor de modelos de minería de datos)
  La pestaña **Red de dependencias** proporciona una vista gráfica de todos los atributos que contiene el modelo de minería de datos, y muestra cómo se relacionan los atributos.  
  
 La pestaña **Red de dependencias**  se utiliza para varios tipos de modelos de minería de datos, incluidos los modelos Bayes Naïve, modelos de árboles de decisión y modelos de asociación. Para obtener más información sobre cómo interpretar el contenido de la pestaña **Red de dependencias**  en el contexto de estos modelos, vea los siguientes vínculos:  
  
 [Examinar un modelo usando el Visor de árboles de Microsoft](data-mining/browse-a-model-using-the-microsoft-tree-viewer.md)  
  
 [Examinar un modelo usando el visor Bayes naive de Microsoft](data-mining/browse-a-model-using-the-microsoft-naive-bayes-viewer.md)  
  
 [Examinar un modelo usando el Visor de reglas de asociación de Microsoft](data-mining/browse-a-model-using-the-microsoft-association-rules-viewer.md)  
  
## <a name="options"></a>Opciones  
 **Actualizar el contenido del Visor**  
 Vuelva a cargar el modelo de minería de datos en el visor.  
  
 **Modelo de minería de datos**  
 Elija un modelo de minería de datos que desea ver de los modelos de la estructura de minería de datos actual. El modelo de minería de datos se abrirá en un visor personalizado. El algoritmo que se usa para crear el modelo determina el tipo de visor personalizado que se utiliza para cada modelo.  
  
 **Viewer**  
 Elija un visor para explorar el modelo de minería de datos seleccionado. Para cada modelo, puede utilizar el visor personalizado que se proporciona para cada modelo de minería de datos o el Visor de contenido de minería de datos de [!INCLUDE[msCoName](../includes/msconame-md.md)] . También puede utilizar visores de complemento si están disponibles. El Visor de árbol de contenido genérico de Microsoft se puede utilizar con todos los modelos, y representa el contenido del modelo en una tabla HTML.  
  
 **Acercar**  
 Acerque el diagrama para que pueda ver los atributos con más detalle.  
  
 **Alejar**  
 Aleje el diagrama para que pueda ver más atributos y los vínculos entre ellos.  
  
 **Copiar vista del gráfico**  
 Copie la sección visible del diagrama en el portapapeles.  
  
 **Copiar todo el gráfico**  
 Copie el diagrama completo en el portapapeles.  
  
 **Links**  
 Mueva el control deslizante hacia la derecha de los atributos para ajustar el número de vínculos (bordes) que muestra el visor. Si arrastra la barra deslizante hacia abajo, aumenta el valor de umbral para que solo se muestren los vínculos más fuertes. Para cada tipo modelo, se utiliza un valor ligeramente diferente para representar los vínculos en el gráfico:  
  
-   En un modelo de **árboles de decisión** , los bordes representan la fuerza de predicción de la conexión, determinada en parte por el resultado de la división.  
  
-   En un modelo **Bayes Naïve** , los vínculos entre dos nodos pueden ir en ambas direcciones: es decir, nodo A puede predecir el nodo B y viceversa. La puntuación asociada al borde representa la fuerza de predicción de la conexión.  
  
-   En un **modelo de asociación**, los bordes entre los nodos representan la puntuación de importancia de la regla que conecta dos conjuntos de elementos.  
  
 Una regla general para todos los tipos de modelo es que cuánto más fuerte es el vínculo, más fuerte es la relación de predicción entre los dos atributos.  
  
## <a name="see-also"></a>Vea también  
 [Algoritmos de minería de datos &#40;Analysis Services: Minería de datos&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Visores de modelos de minería de datos &#40;Diseñador de modelos de minería de datos&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [Visores de modelos de minería de datos](data-mining/data-mining-model-viewers.md)  
  
  
