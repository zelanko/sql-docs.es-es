---
title: Excluir una columna de un modelo de minería de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- excluding mining model columns
- mining models [Analysis Services], columns
- columns [data mining], excluding
ms.assetid: 404fe5fe-3ba2-4b9b-8780-0d02343d467f
caps.latest.revision: 28
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d68a1251074d3815b852b1b43f63b36df744d0dc
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37269821"
---
# <a name="exclude-a-column-from-a-mining-model"></a>Excluir una columna de un modelo de minería de datos
  Cuando cree un modelo de minería de datos, es posible que no desee utilizar todas las columnas que existen en la estructura de minería de datos en la que se basa el modelo. Por ejemplo, puede que haya añadido una columna con el nombre del cliente para la obtención de detalles, pero no quiere utilizarla para el modelado. También puede ser que decida crear múltiples copias de una columna con diversas discretizaciones y usar solamente una de las copias en cada modelo, e ignorar el resto. También podría añadir de forma selectiva columnas de entrada en varios modelos distintos para ver cómo la variable añadida afecta a la columna de salida.  
  
 No necesita crear una nueva estructura de minería de datos para cada combinación de columnas; basta con que marque una columna como no usada en un modelo determinado.  
  
### <a name="to-exclude-a-column-from-a-mining-model"></a>Para excluir una columna de un modelo de minería de datos  
  
1.  En la pestaña **Modelos de minería de datos** del Diseñador de minería de datos de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], seleccione la celda que se corresponda con la columna que desee excluir bajo el modelo de minería de datos pertinente.  
  
2.  Seleccione **Omitir** en el cuadro de lista desplegable.  
  
## <a name="see-also"></a>Vea también  
 [Tareas y procedimientos de los modelos de minería de datos](mining-model-tasks-and-how-tos.md)  
  
  
