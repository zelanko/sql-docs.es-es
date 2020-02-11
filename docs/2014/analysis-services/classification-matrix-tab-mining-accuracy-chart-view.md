---
title: Pestaña matriz de clasificación (vista gráfico de precisión de minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.accuracychart.confusionmatrix.f1
ms.assetid: 85d5a047-d656-41e0-8a31-400271c2a620
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ca3471a96a2ad171255f488b255deee55f73e2e0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66087948"
---
# <a name="classification-matrix-tab-mining-accuracy-chart-view"></a>Pestaña Matriz de clasificación (vista Gráfico de precisión de minería de datos)
  La pestaña **matriz de clasificación** muestra una matriz de clasificación para cada modelo seleccionado en la cuadrícula modelos de la pestaña asignación de **columnas** . La matriz de clasificación solo está disponible si la columna de predicción que está seleccionada en la pestaña **asignación de columnas** no es continua. Para obtener una descripción más detallada de la pestaña **Matriz de clasificación** , vea [Testing and Validation &#40;Data Mining&#41;](data-mining/testing-and-validation-data-mining.md).  
  
## <a name="options"></a>Opciones  
 **Copy**  
 Copia el contenido de cada matriz de clasificación al portapapeles.  
  
 **Recuentos de \<> \< de modelo en la columna de predicción>**  
 Muestra una matriz de clasificación para cada modelo de minería de datos de la estructura de minería de datos. La matriz contiene las siguientes columnas:  
  
|Value|Descripción|  
|-----------|-----------------|  
|**Previsto**|Contiene una fila de cada estado de la columna de predicción.|  
|**\<Estados> (real)**|Una columna para cada estado de la columna de predicción. Si el estado de la fila y la columna se corresponden, la celda representa el número de veces real que el estado existe en la base de datos. Si no se corresponden, la celda representa el error de la predicción.|  
  
## <a name="see-also"></a>Consulte también  
 [Diseñador de gráficos de precisión de minería de datos &#40;&#41;de minería de datos](mining-accuracy-chart-designer-data-mining.md)   
 [Tareas y procedimientos de prueba y validación &#40;&#41;de minería de datos](data-mining/testing-and-validation-tasks-and-how-tos-data-mining.md)   
 [Pruebas y validación &#40;&#41;de minería de datos](data-mining/testing-and-validation-data-mining.md)  
  
  
