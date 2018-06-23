---
title: Pestaña validación cruzada (vista de gráfico de precisión de minería de datos) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dm.miningmodeleditor.accuracychart.crossvalidation.f1
ms.assetid: bd215a68-1ad7-4046-9c44-ec8e2be13a64
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: d5b39187ddfc3e4ce0fa8ef0fc7e0402ef54b129
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36199578"
---
# <a name="cross-validation-tab-mining-accuracy-chart-view"></a>Pestaña Validación cruzada (vista Gráfico de precisión de minería de datos)
  La validación cruzada le permite dividir una estructura de minería de datos en secciones transversales y entrenar y probar de forma iterativa los modelos con cada sección transversal. Se especifican varios subconjuntos en los que se dividirán los datos, y cada uno se usa a su vez como datos de pruebas, mientras que los datos restantes se usan para entrenar un nuevo modelo. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] a continuación, genera un conjunto de métricas de precisión estándar para cada modelo. Al comparar las medidas de los modelos generados para cada sección transversal, puede hacerse una idea del grado de confiabilidad del modelo de minería con respecto a todo el conjunto de datos.  
  
 Para más información, vea [Cross-Validation &#40;Analysis Services - Data Mining&#41;](data-mining/cross-validation-analysis-services-data-mining.md).  
  
> [!NOTE]  
>  La validación cruzada no se puede usar con modelos que se hayan generado con el algoritmo de serie temporal de [!INCLUDE[msCoName](../includes/msconame-md.md)] o con el algoritmo de clústeres de secuencia de [!INCLUDE[msCoName](../includes/msconame-md.md)] . Si ejecuta el informe en una estructura de minería de datos que contiene estos tipos de modelos, los modelos no se incluirán en el informe.  
  
## <a name="task-list"></a>Lista de tareas  
  
-   Especifique el número de subconjuntos.  
  
-   Especifique el número máximo de casos para utilizar en la validación cruzada.  
  
-   Especifique la columna de predicción.  
  
-   Si lo desea, puede especificar un estado de predicción.  
  
-   Además, puede establecer parámetros que controlen cómo se evalúa la precisión de la predicción.  
  
-   Haga clic en **Obtener resultados** para mostrar los resultados de la validación cruzada.  
  
## <a name="uielement-list"></a>Lista de UIElement  
 **Recuento de plegamientos**  
 Especifique el número de subconjuntos, o particiones, que desea crear. El valor mínimo es 2, lo que significa que se usa la mitad del conjunto de datos para las pruebas y la otra mitad para el aprendizaje.  
  
 El valor máximo es 10 para las estructuras de minería de datos de la sesión.  
  
 El valor máximo es 256, si la estructura de minería de datos está almacenada en una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
> [!NOTE]  
>  Cuando aumenta el número de subconjuntos, el tiempo que se necesita para realizar la validación cruzada aumenta de igual forma en n. Pueden producirse problemas de rendimiento si el número de casos es elevado y el valor de **Recuento de plegamientos** también es elevado.  
  
 **Máximo de casos**  
 Especifique el número máximo de casos para utilizar en la validación cruzada. El número de casos en cualquier subconjunto determinado es igual al valor **Máximo de casos** dividido por el valor de **Recuento de plegamientos** .  
  
 Si usa **0**, todos los casos de los datos de origen se usarán para la validación cruzada.  
  
 No existe ningún valor predeterminado.  
  
> [!NOTE]  
>  El tiempo de proceso también aumenta a medida que aumenta el número de casos.  
  
 **Atributo de destino**  
 Seleccione una columna de la lista de columnas de predicción que se encuentra en todos los modelos. Solo puede seleccionar una columna predecible cada vez que realice validación cruzada.  
  
 Para probar solo los modelos de agrupación en clústeres, seleccione **Clúster**.  
  
 **Estado de destino**  
 Escriba un valor o seleccione un valor de destino en una lista desplegable de valores.  
  
 El valor predeterminado es `null`, que indica que se probarán todos los estados.  
  
 Se deshabilita para modelos de agrupación en clústeres.  
  
 **Umbral**  **de destino**  
 Especifique un valor entre 0 y 1 que indique la probabilidad de la predicción anterior que se considera que un estado predicho es correcto. El valor se puede establecer en 0,1 incrementos.  
  
 El valor predeterminado es `null`, lo que indica que la predicción más probable se cuenta como correcta.  
  
> [!NOTE]  
>  Aunque puede establecer el valor en 0,0, si usa este valor aumentará el tiempo de proceso y no producirá resultados significativos.  
  
 **Obtener resultados**  
 Haga clic para comenzar la validación cruzada del modelo utilizando los parámetros especificados.  
  
 El modelo se divide en el número especificado de subconjuntos y para cada uno se prueba un modelo independiente. Por consiguiente, podría tardar algún tiempo para que la validación cruzada devuelva resultados.  
  
 Para más información sobre cómo interpretar los resultados del informe de validación cruzada, vea [Medidas en el informe de validación cruzada](data-mining/measures-in-the-cross-validation-report.md).  
  
## <a name="setting-the-accuracy-threshold"></a>Establecer el umbral de precisión  
 Puede controlar el estándar para medir la exactitud de la predicción estableciendo un valor para **Umbral de** **destino**. Un umbral representa un tipo de barra de precisión. A cada predicción se le asigna una probabilidad de que el valor predicho sea correcto. Por consiguiente, si establece en 1 el valor de **Umbral** **de destino** , está requiriendo que la probabilidad para cualquier predicción determinada sea bastante alta para contabilizarse como una predicción correcta. Y a la inversa, si establece en 0 **Umbral** **de destino** , incluso las predicciones con valores de probabilidad más bajos se cuentan como predicciones "buenas".  
  
 No hay ningún valor de umbral recomendado porque la probabilidad de cualquier predicción depende de la cantidad de datos y del tipo de predicción que se está realizando. Debería revisar algunas predicciones en niveles de probabilidad diferentes para determinar una barra de precisión adecuada para sus datos. Es importante que haga esto, porque el valor que establece para **Umbral** **de destino** afecta a la precisión medida del modelo.  
  
 Por ejemplo, suponga que se hacen tres predicciones para un estado de destino determinado, y las probabilidades de cada predicción son 0,05, 0,15 y 0,8. Si establece el umbral en 0,5, solamente se tiene en cuenta una predicción como correcta. Si establece **Umbral** **de destino** en 0,10, se tienen en cuenta dos predicciones como correctas.  
  
 Cuando **destino** **umbral** se establece en `null`, que es el valor predeterminado, la predicción más probable para cada caso se cuenta como correcta. En el ejemplo recién citado, 0,05, 0,15 y 0,8 son las probabilidades de las predicciones de tres casos diferentes. Aunque las probabilidades son muy distintas, cada una se contaría como correcta, porque cada caso genera solo una predicción y éstas son las mejores predicciones para estos casos.  
  
## <a name="see-also"></a>Vea también  
 [Prueba y validación &#40;minería de datos&#41;](data-mining/testing-and-validation-data-mining.md)   
 [La validación cruzada &#40;Analysis Services: minería de datos&#41;](data-mining/cross-validation-analysis-services-data-mining.md)   
 [Medidas en el informe de validación cruzada](data-mining/measures-in-the-cross-validation-report.md)   
 [Procedimientos almacenados de minería de datos &#40;Analysis Services: minería de datos&#41;](/sql/analysis-services/data-mining/data-mining-stored-procedures-analysis-services-data-mining)  
  
  
