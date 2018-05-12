---
title: Excluir una columna de un modelo de minería de datos | Documentos de Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a162adfdd2eeeb1209a68f5c05251b750bf3d590
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="exclude-a-column-from-a-mining-model"></a>Excluir una columna de un modelo de minería de datos
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Cuando cree un modelo de minería de datos, es posible que no desee utilizar todas las columnas que existen en la estructura de minería de datos en la que se basa el modelo. Por ejemplo, puede que haya añadido una columna con el nombre del cliente para la obtención de detalles, pero no quiere utilizarla para el modelado. También puede ser que decida crear múltiples copias de una columna con diversas discretizaciones y usar solamente una de las copias en cada modelo, e ignorar el resto. También podría añadir de forma selectiva columnas de entrada en varios modelos distintos para ver cómo la variable añadida afecta a la columna de salida.  
  
 No necesita crear una nueva estructura de minería de datos para cada combinación de columnas; basta con que marque una columna como no usada en un modelo determinado.  
  
### <a name="to-exclude-a-column-from-a-mining-model"></a>Para excluir una columna de un modelo de minería de datos  
  
1.  En la pestaña **Modelos de minería de datos** del Diseñador de minería de datos de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], seleccione la celda que se corresponda con la columna que desee excluir bajo el modelo de minería de datos pertinente.  
  
2.  Seleccione **Omitir** en el cuadro de lista desplegable.  
  
## <a name="see-also"></a>Vea también  
 [Tareas y tareas de modelo de minería de datos](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
  
