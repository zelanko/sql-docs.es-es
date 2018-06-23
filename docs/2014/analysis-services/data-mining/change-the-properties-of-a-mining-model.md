---
title: Cambiar las propiedades de un modelo de minería de datos | Documentos de Microsoft
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
- mining models [Analysis Services], properties
- properties [data mining]
ms.assetid: aefaeb7f-d174-48d1-a188-0987a3b1196b
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 28e417708981a7184caa62ae74fe681397411d78
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36109392"
---
# <a name="change-the-properties-of-a-mining-model"></a>Cambiar las propiedades de un modelo de minería de datos
  Algunas propiedades del modelo de minería de datos se aplican al modelo en su conjunto, mientras que otras se aplican a columnas individuales. Ejemplos de propiedades que se aplican a todo el modelo sería la `Drillthrough` propiedad, que especifica si los datos del caso deben estar disponibles para las consultas, y el `Description` propiedad. Entre las propiedades que se aplican a la columna se incluyen `Usage` y `ModelingFlags`, que controlan cómo se utilizan los datos en la columna dentro del modelo.  
  
 Las propiedades del modelo siguientes disponen de editores avanzados que se pueden utilizar para crear expresiones o configurar propiedades complejas del modelo. Las propiedades siguientes proporcionan:  
  
-   `Filter` propiedad: abre el [filtro de conjunto de datos o el cuadro de diálogo de filtro de modelo](../data-set-filter-or-model-filter-dialog-box.md).  
  
-   `AlgorithmParameters` propiedad: abre el [cuadro de diálogo de parámetros de algoritmo &#40;vista de modelos de minería de datos&#41;](../algorithm-parameters-dialog-box-mining-models-view.md).  
  
 Para obtener información sobre cómo configurar las propiedades de un modelo de minería de datos, vea [Columnas del modelo de minería de datos](mining-model-columns.md).  
  
### <a name="to-change-the-properties-of-a-mining-model"></a>Para cambiar las propiedades de un modelo de minería de datos  
  
1.  En la pestaña **Modelos de minería de datos** del Diseñador de minería de datos, haga clic con el botón derecho en el encabezado de columna que contiene el nombre del modelo de minería de datos o en la fila de la cuadrícula que contiene el nombre del algoritmo de minería de datos y, después, seleccione **Propiedades**.  
  
2.  En la ventana **Propiedades** situada en el lado derecho de la pantalla, resalte el valor correspondiente a la propiedad que desee cambiar y, a continuación, escriba el nuevo valor.  
  
     El nuevo valor tendrá efecto cuando se seleccione otro elemento diferente en el diseñador.  
  
### <a name="to-change-the-properties-of-a-mining-model-column"></a>Para cambiar las propiedades de una columna del modelo de minería de datos  
  
1.  En la pestaña **Modelos de minería de datos** del Diseñador de minería de datos, haga clic con el botón derecho en la celda de cuadrícula situada en la intersección de la columna de la estructura de minería de datos con el modelo de minería de datos y, después, seleccione **Propiedades**.  
  
2.  En la ventana **Propiedades** situada en el lado derecho de la pantalla, resalte el valor correspondiente a la propiedad que desee cambiar y, a continuación, escriba el nuevo valor.  
  
    > [!NOTE]  
    >  Si el uso de las columnas se establece en `Ignore`, **propiedades** ventana de la columna está en blanco.  
  
     El nuevo valor tendrá efecto cuando se seleccione otro elemento diferente en el diseñador.  
  
## <a name="see-also"></a>Vea también  
 [Tareas y procedimientos de los modelos de minería de datos](mining-model-tasks-and-how-tos.md)  
  
  