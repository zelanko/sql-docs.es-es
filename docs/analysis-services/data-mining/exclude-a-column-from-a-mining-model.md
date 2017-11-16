---
title: "Excluir una columna de un modelo de minería de datos | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- excluding mining model columns
- mining models [Analysis Services], columns
- columns [data mining], excluding
ms.assetid: 404fe5fe-3ba2-4b9b-8780-0d02343d467f
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a12584791ec8ea21a1338c09dbc0e5f7ef8f7a62
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="exclude-a-column-from-a-mining-model"></a>Excluir una columna de un modelo de minería de datos
  Cuando cree un modelo de minería de datos, es posible que no desee utilizar todas las columnas que existen en la estructura de minería de datos en la que se basa el modelo. Por ejemplo, puede que haya añadido una columna con el nombre del cliente para la obtención de detalles, pero no quiere utilizarla para el modelado. También puede ser que decida crear múltiples copias de una columna con diversas discretizaciones y usar solamente una de las copias en cada modelo, e ignorar el resto. También podría añadir de forma selectiva columnas de entrada en varios modelos distintos para ver cómo la variable añadida afecta a la columna de salida.  
  
 No necesita crear una nueva estructura de minería de datos para cada combinación de columnas; basta con que marque una columna como no usada en un modelo determinado.  
  
### <a name="to-exclude-a-column-from-a-mining-model"></a>Para excluir una columna de un modelo de minería de datos  
  
1.  En la pestaña **Modelos de minería de datos** del Diseñador de minería de datos de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], seleccione la celda que se corresponda con la columna que desee excluir bajo el modelo de minería de datos pertinente.  
  
2.  Seleccione **Omitir** en el cuadro de lista desplegable.  
  
## <a name="see-also"></a>Vea también  
 [Tareas y procedimientos de los modelos de minería de datos](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
  

