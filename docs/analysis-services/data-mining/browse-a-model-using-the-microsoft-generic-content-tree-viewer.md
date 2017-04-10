---
title: "Examinar un modelo usando el Visor de &#225;rbol de contenido gen&#233;rico de Microsoft | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "contenido del modelo de minería de datos, ver"
ms.assetid: 4a5f7c51-c704-4214-b05d-21cf735e6d96
caps.latest.revision: 23
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 23
---
# Examinar un modelo usando el Visor de &#225;rbol de contenido gen&#233;rico de Microsoft
  El Visor de contenido genérico del modelo de minería de datos de [!INCLUDE[msCoName](../../includes/msconame-md.md)] proporciona información detallada sobre los patrones encontrados por el algoritmo de minería de datos, y también ofrece acceso a diversas estadísticas generadas durante el proceso de análisis. La cantidad y el tipo de información dependen del algoritmo utilizado, pero pueden incluir las categorías siguientes:  
  
-   Segmentos de datos y sus características.  
  
-   Estadísticas descriptivas sobre cada grupo o sobre el conjunto completo de datos.  
  
-   Número de bifurcaciones o nodos secundarios de un árbol.  
  
-   Diversos cálculos, como la varianza y la media, para un clúster o un conjunto completo de datos.  
  
 Ver esta información puede servir de ayuda para entender mejor los resultados del análisis. También se pueden identificar distintas maneras de ajustar y volver a entrenar el modelo. O bien, se puede decidir volver a entrenar el modelo usando un algoritmo diferente.  
  
## Ver contenido del modelo de minería de datos  
 El Visor de contenido genérico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] muestra las columnas, las reglas, las propiedades, los atributos, los nodos y otro tipo de contenido del *conjunto de filas de esquema de contenido* del modelo de minería de datos. El conjunto de filas de esquema de contenido es un marco genérico para presentar información detallada sobre el contenido de un modelo de minería de datos.  
  
 Esta información detallada está contenida en una tabla HTML que representa los patrones, los clústeres, o los árboles del modelo como nodos. Puede hacer clic en cada nodo y expandirlo para ver más información, tal como las fórmulas o el recuento de valores distintos para un atributo numérico. También puede explorar las relaciones de elementos primarios y secundarios entre los nodos.  
  
 Para obtener más información sobre el significado general de los términos que se usan en el contenido del modelo de minería de datos, vea [Contenido del modelo de minería de datos &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md). El tema también contiene vínculos a información acerca del contenido del modelo de minería de datos para tipos específicos de modelos. Cada tipo de modelo de minería de datos contiene información muy específica del algoritmo y de los patrones localizados en los datos, de modo que se recomienda consultar el tema de referencia técnica de cada tipo de modelo para comprender cada tipo de modelo.  
  
## Consultar el contenido del modelo de minería de datos  
 La información proporcionada por el Visor de árbol de contenido genérico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] también se encuentra disponible si se consulta el modelo de minería de datos. Puede crear consultas en el contenido del modelo de minería de datos usando instrucciones de Extensiones de minería de datos (DMX). Por ejemplo, en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], se puede realizar una consulta de contenido ejecutando la siguiente instrucción de DMX:  
  
```  
SELECT * FROM [<mining model name>].CONTENT  
```  
  
 Para obtener más información, vea [Consultas de minería de datos](../../analysis-services/data-mining/data-mining-queries.md).  
  
## Vea también  
 [Visor de árbol de contenido genérico de Microsoft &#40;Minería de datos&#41;](../Topic/Microsoft%20Generic%20Content%20Tree%20Viewer%20\(Data%20Mining\).md)   
 [Algoritmos de minería de datos &#40;Analysis Services: Minería de datos&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)  
  
  