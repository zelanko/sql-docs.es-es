---
title: Algoritmos de minería de datos (datos de SQL Server a los complementos de minería de datos) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- segmentation
- data mining algorithms
- clustering [data mining]
- linear regression
- association [data mining]
- neural networks
- logistic regression
- regression
- sequence analysis
- decision tree [data mining]
- Naive Bayes
- time series [data mining]
ms.assetid: 3a1a62e4-9fb5-4cdb-a6c6-1b8b30d417ef
caps.latest.revision: 18
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 4ea33a6ee29965202189fd4149c243df3d1d91df
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36200831"
---
# <a name="data-mining-algorithms-sql-server-data-mining-add-ins"></a>Algoritmos de minería de datos (Complementos de minería de datos de SQL Server)
  Los Complementos de minería de datos para Office admiten la creación de modelos analíticos con los siguientes algoritmos de minería de datos. Todos los algoritmos se basan en métodos conocidos de aprendizaje automático y los ha implementado Microsoft Research.  
  
## <a name="algorithms"></a>Algoritmos  
  
|Método de aprendizaje automático|Funcionamiento|  
|-----------------------------|------------------|  
|Algoritmo de reglas de asociación de Microsoft|Detectar qué productos se adquieren juntos o qué eventos se producen juntos, y usar el modelo para crear recomendaciones.<br /><br /> [http://msdn.microsoft.com/library/ms174916.aspx](http://msdn.microsoft.com/library/ms174916.aspx)|  
|Algoritmo de clústeres de Microsoft|Definir segmentos de mercado, agrupar automáticamente clientes relacionados o buscar relaciones en los datos para usarlas en operaciones de minería de datos adicionales.<br /><br /> [http://msdn.microsoft.com/library/ms174879.aspx](http://msdn.microsoft.com/library/ms174879.aspx)|  
|Algoritmo de árboles de decisión de Microsoft|Identificar relaciones desconocidas previamente entre diferentes elementos de los datos para tomar decisiones más informadas o buscar los factores que conducen a resultados específicos.<br /><br /> [http://msdn.microsoft.com/library/ms174923.aspx](http://msdn.microsoft.com/library/ms174923.aspx)|  
|Algoritmo de regresión lineal de Microsoft|Buscar una fórmula matemática que describe los factores que contribuyen a un resultado numérico.<br /><br /> [http://msdn.microsoft.com/library/ms174824.aspx](http://msdn.microsoft.com/library/ms174824.aspx)|  
|Algoritmo de regresión logística de Microsoft|Identificar los factores que contribuyen a resultados binarios y aprender a utilizarlos para modificar los resultados.<br /><br /> [http://msdn.microsoft.com/library/ms174828.aspx](http://msdn.microsoft.com/library/ms174828.aspx)|  
|Algoritmo Bayes Naïve de Microsoft|Explorar las relaciones en los datos y buscar las correlacionadas más estrechamente con un resultado.<br /><br /> [http://msdn.microsoft.com/en-us/library/ms174806.aspx](http://msdn.microsoft.com/library/ms174806.aspx)|  
|Algoritmo de redes neuronales de Microsoft|Buscar relaciones ocultas entre varias entradas e incluso varias salidas. Se usa para la exploración o la predicción.<br /><br /> [http://msdn.microsoft.com/library/ms174941.aspx](http://msdn.microsoft.com/library/ms174941.aspx)|  
|Algoritmo de serie temporal de Microsoft|Usar datos históricos para predecir valores futuros.<br /><br /> [http://msdn.microsoft.com/library/ms174923.aspx](http://msdn.microsoft.com/library/ms174923.aspx)|  
  
## <a name="advanced-options"></a>Opciones avanzadas  
 Cuando utiliza el Cliente de minería de datos para Excel, tiene la posibilidad de crear sus propias estructuras y modelos de minería de datos u optimizar los parámetros de los algoritmos.  
  
 [Parámetros de algoritmo &#40;complementos de minería de datos de SQL Server&#41;](algorithm-parameters-sql-server-data-mining-add-ins.md)  
  
 Hay dos maneras de personalizar los modelos mediante estas opciones avanzadas:  
  
-   Use la **consulta de minería de datos** Asistente para crear el modelo.  
  
-   En el **cliente de minería de datos**, después de iniciar el asistente, haga clic en **parámetros**.  
  
## <a name="see-also"></a>Vea también  
 [Consulta &#40;complementos de minería de datos de SQL Server&#41;](query-sql-server-data-mining-add-ins.md)   
 [Advanced modelado &#40;datos complementos de minería de datos para Excel&#41;](advanced-modeling-data-mining-add-ins-for-excel.md)  
  
  