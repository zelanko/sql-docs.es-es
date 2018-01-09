---
title: "Examinar un modelo usando el Visor de árbol de contenido genérico de Microsoft | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: mining model content, viewing
ms.assetid: 4a5f7c51-c704-4214-b05d-21cf735e6d96
caps.latest.revision: "23"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 6489f35c5d438dd234e97eeed3d042ea41cc291c
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="browse-a-model-using-the-microsoft-generic-content-tree-viewer"></a>Examinar un modelo usando el Visor de árbol de contenido genérico de Microsoft
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]El [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visor de contenido de modelo de minería de datos genérico proporciona información detallada sobre los patrones encontrados por el algoritmo de minería de datos y también proporciona acceso a diversas estadísticas generadas durante el proceso de análisis. La cantidad y el tipo de información dependen del algoritmo utilizado, pero pueden incluir las categorías siguientes:  
  
-   Segmentos de datos y sus características.  
  
-   Estadísticas descriptivas sobre cada grupo o sobre el conjunto completo de datos.  
  
-   Número de bifurcaciones o nodos secundarios de un árbol.  
  
-   Diversos cálculos, como la varianza y la media, para un clúster o un conjunto completo de datos.  
  
 Ver esta información puede servir de ayuda para entender mejor los resultados del análisis. También se pueden identificar distintas maneras de ajustar y volver a entrenar el modelo. O bien, se puede decidir volver a entrenar el modelo usando un algoritmo diferente.  
  
## <a name="viewing-mining-model-content"></a>Ver contenido del modelo de minería de datos  
 El Visor de contenido genérico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] muestra las columnas, las reglas, las propiedades, los atributos, los nodos y otro tipo de contenido del *conjunto de filas de esquema de contenido* del modelo de minería de datos. El conjunto de filas de esquema de contenido es un marco genérico para presentar información detallada sobre el contenido de un modelo de minería de datos.  
  
 Esta información detallada está contenida en una tabla HTML que representa los patrones, los clústeres, o los árboles del modelo como nodos. Puede hacer clic en cada nodo y expandirlo para ver más información, tal como las fórmulas o el recuento de valores distintos para un atributo numérico. También puede explorar las relaciones de elementos primarios y secundarios entre los nodos.  
  
 Para obtener más información sobre el significado general de los términos que se usan en el contenido del modelo de minería de datos, vea [Contenido del modelo de minería de datos &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md). El tema también contiene vínculos a información acerca del contenido del modelo de minería de datos para tipos específicos de modelos. Cada tipo de modelo de minería de datos contiene información muy específica del algoritmo y de los patrones localizados en los datos, de modo que se recomienda consultar el tema de referencia técnica de cada tipo de modelo para comprender cada tipo de modelo.  
  
## <a name="querying-mining-model-content"></a>Consultar el contenido del modelo de minería de datos  
 La información proporcionada por el Visor de árbol de contenido genérico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] también se encuentra disponible si se consulta el modelo de minería de datos. Puede crear consultas en el contenido del modelo de minería de datos usando instrucciones de Extensiones de minería de datos (DMX). Por ejemplo, en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], se puede realizar una consulta de contenido ejecutando la siguiente instrucción de DMX:  
  
```  
SELECT * FROM [<mining model name>].CONTENT  
```  
  
 Para obtener más información, vea [Consultas de minería de datos](../../analysis-services/data-mining/data-mining-queries.md).  
  
## <a name="see-also"></a>Vea también  
 [Visor de árbol de contenido genérico de Microsoft &#40;Minería de datos&#41;](http://msdn.microsoft.com/library/751b4393-f6fd-48c1-bcef-bdca589ce34c)   
 [Algoritmos de minería de datos &#40;Analysis Services: Minería de datos&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)  
  
  
