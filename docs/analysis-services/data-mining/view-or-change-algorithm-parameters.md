---
title: Ver o cambiar parámetros del algoritmo | Documentos de Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 58b512d726d45a8ceabb76a4ce2b1e6c8c62815b
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="view-or-change-algorithm-parameters"></a>Ver o cambiar parámetros del algoritmo
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
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
 [Tareas y tareas de modelo de minería de datos](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
  
