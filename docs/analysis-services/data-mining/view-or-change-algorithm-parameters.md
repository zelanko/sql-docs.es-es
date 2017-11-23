---
title: "Ver o cambiar parámetros del algoritmo | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
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
- algorithms [data mining]
- mining models [Analysis Services], algorithms
ms.assetid: 151b899b-c27a-4a09-bcf5-5c9f0ec24168
caps.latest.revision: "15"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 5bd20ff4beddb94831f634304f1a9628f21025a3
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="view-or-change-algorithm-parameters"></a>Ver o cambiar parámetros del algoritmo
  Puede cambiar los parámetros proporcionados con los algoritmos que se utilizan para crear modelos de minería de datos para personalizar los resultados del modelo.  
  
 Los parámetros de los algoritmos que se proporcionan en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] cambian mucho más que las propiedades del modelo: se pueden utilizar para modificar de manera fundamental la manera en que los datos se procesan, se agrupan y se muestran. Por ejemplo, puede usar parámetros de algoritmo para hacer lo siguiente:  
  
-   Cambiar el método de análisis, como el método de clústeres.  
  
-   Controlar el comportamiento de la selección de características.  
  
-   Especificar el tamaño de los conjuntos de elementos o la probabilidad de las reglas.  
  
-   Controlar la bifurcación y la profundidad de los árboles de decisión.  
  
-   Especificar un valor de inicialización o el tamaño del conjunto interno de exclusión que se utiliza para la creación del modelo.  
  
 Los parámetros proporcionados para cada algoritmo varían en gran medida. Para obtener una lista de los parámetros que se pueden establecer para cada algoritmo, vea los temas de referencia técnica de esta sección: [Algoritmos de minería de datos &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md).  
  
### <a name="change-an-algorithm-parameter"></a>Cambiar un parámetro de algoritmo  
  
1.  En la pestaña **Modelos de minería de datos** del Diseñador de minería de datos en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], haga clic con el botón derecho en el tipo de algoritmo del modelo de minería de datos para el que quiera ajustar el algoritmo y, después, seleccione **Establecer parámetros de algoritmo**.  
  
     Se abrirá la ventana **Parámetros de algoritmo** .  
  
2.  En la columna **Valor** , ajuste un nuevo valor para el algoritmo que desee cambiar.  
  
     Si no especifica un valor en la columna **Valor** , [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] utiliza el valor de parámetro predeterminado. La columna **Intervalo** describe los posibles valores que se pueden especificar.  
  
3.  Haga clic en **Aceptar**.  
  
     El parámetro de algoritmo se establece con el nuevo valor. El cambio de parámetro no se reflejará en el modelo de minería de datos hasta que vuelva a procesar el modelo.  
  
### <a name="view-the-parameters-used-in-an-existing-model"></a>Vea los parámetros utilizados en un modelo existente  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], abra una ventana Consulta DMX.  
  
2.  Escriba una consulta como esta:  
  
    ```  
    select MINING_PARAMETERS   
    from $system.DMSCHEMA_MINING_MODELS  
    WHERE MODEL_NAME = '<model name>'  
  
    ```  
  
## <a name="see-also"></a>Vea también  
 [Tareas y procedimientos de los modelos de minería de datos](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
  
