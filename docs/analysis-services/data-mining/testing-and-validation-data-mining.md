---
title: Prueba y validación (minería de datos) | Documentos de Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e4ce983ed5d5a645f32466ab38d5c67ff1c68897
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="testing-and-validation-data-mining"></a>Prueba y validación (minería de datos)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  La validación es el proceso de evaluar cuál sería el rendimiento de sus modelos de minería de datos con datos reales. Es importante que valide sus modelos de minería de datos entendiendo su calidad y sus características antes de implementarlos en un entorno de producción.  
  
 En esta sección se presentan algunos conceptos básicos relacionados con la calidad de los modelos y se describen las estrategias para la validación de modelos que se proporcionan en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Para obtener información general sobre cómo la validación del modelo se adapta a procesos de minería de datos de mayor tamaño, vea [Soluciones de minería de datos](../../analysis-services/data-mining/data-mining-solutions.md).  
  
## <a name="methods-for-testing-and-validation-of-data-mining-models"></a>Métodos de prueba y validación de los modelos de minería de datos  
 Existen muchos enfoques a la hora de evaluar la calidad y las características de un modelo de minería de datos.  
  
-   Use varias medidas de validez estadística para determinar si existen problemas en los datos o en el modelo.  
  
-   Separe los datos en conjuntos de entrenamiento y de prueba con el fin de probar la precisión de predicciones.  
  
-   Solicite a los expertos comerciales que revisen los resultados del modelo de minería de datos para determinar si los patrones detectados tienen sentido en un escenario empresarial concreto.  
  
 Todos estos métodos son útiles para la metodología de minería de datos y se usan de forma iterativa a la hora de crear, probar y refinar modelos para responder a un problema concreto. No hay ninguna regla completa única que pueda indicarle si un modelo es suficientemente bueno, o si cuenta con suficientes datos.  
  
## <a name="definition-of-criteria-for-validating-data-mining-models"></a>Definición de los criterios para validar los modelos de minería de datos  
 Las medidas de minería de datos se suelen agrupar en las categorías de precisión, confiabilidad y utilidad.  
  
 La*precisión* es una medida que indica hasta qué punto el modelo pone en correlación un resultado con los atributos de los datos que se han proporcionado. Existen varias medidas de precisión, pero todas ellas dependen de los datos que se utilicen. En realidad, podrían faltar valores o éstos ser aproximados, o incluso diferentes procesos podrían cambiar los datos. En particular, en la fase de exploración y desarrollo, podría decidir aceptar una cierta cantidad de errores en los datos, sobre todo si éstos son suficientemente uniformes en sus características. Por ejemplo, un modelo que predice las ventas para un almacén determinado en base a las ventas pasadas puede estar muy correlacionado y ser muy preciso, incluso si ese almacén ha utilizado un método de contabilidad equivocado continuamente. Por tanto, es necesario equilibrar las mediciones de precisión mediante las valoraciones de confiabilidad.  
  
 La*confiabilidad* evalúa la manera en la que se comporta un modelo de minería de datos en conjuntos de datos diferentes. Un modelo de minería de datos es confiable si genera el mismo tipo de predicciones o encuentra los mismos tipos generales de patrones independientemente de los datos de prueba que se proporcionen. Por ejemplo, el modelo que ha generado para el almacén que utilizó un método de contabilidad equivocado no podría extrapolarse correctamente a otros almacenes, y por tanto, no sería confiable.  
  
 La*utilidad* incluye diferentes métricas que le indican si el modelo proporciona información útil. Por ejemplo, un modelo de minería de datos que pone en correlación la ubicación del almacén con las ventas podría ser preciso y fiable, pero podría no ser útil, ya que no se podría generalizar ese resultado si se agregaran más almacenes en la misma ubicación. Es más, no responde a la pregunta comercial fundamental de porqué ciertas ubicaciones tienen más ventas que otras. También podría descubrir que un modelo que parece correcto, en realidad no tiene sentido porque está basado en correlaciones cruzadas de los datos.  
  
## <a name="tools-for-testing-and-validation-of-mining-models"></a>Herramientas de prueba y validación de modelos de minería de datos  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] admite varios enfoques para la validación de soluciones de minería de datos, que abarcan todas las fases de la metodología de prueba de la minería de datos.  
  
-   Crear particiones de los datos de los conjuntos de prueba y entrenamiento.  
  
-   Filtrar modelos para entrenar y probar combinaciones diferentes de los mismos datos de origen.  
  
-   Medir la *mejora respecto al modelo predictivo* y la *ganancia*. Un *gráfico de mejora respecto al modelo predictivo* es un método para visualizar la mejora que obtendrá de usar un modelo de minería de datos, si lo compara con una estimación aleatoria.  
  
-   Realizar una *validación cruzada* de los conjuntos de datos  
  
-   Generar *matrices de clasificación*. Estos gráficos ordenan las estimaciones buenas y malas en una tabla, lo que permite analizar rápida y fácilmente con qué precisión predice el modelo el valor de destino.  
  
-   Crear *gráficos de dispersión* para evaluar el ajuste de una fórmula de regresión.  
  
-   Crear *gráficos de beneficios* que permiten asociar ganancias o costos financieros con el uso de cierto modelo de minería de datos, para poder evaluar el valor de las recomendaciones.  
  
 Estas métricas no pretenden responder a la pregunta de si el modelo de minería de datos resuelve sus preguntas empresariales, sino que proporcionan medidas objetivas que puede usar para evaluar la confiabilidad de los datos para los análisis predictivos, y le ofrecen ayuda a la hora de decidir si debe usar una iteración determinada en el proceso de desarrollo.  
  
 Los temas de esta sección proporcionan información general de cada método y le guían en el proceso de medir la exactitud de los modelos generados mediante la minería de datos de SQL Server.  
  
### <a name="related-topics"></a>Temas relacionados  
  
|Temas|Vínculos|  
|------------|-----------|  
|Obtenga información sobre cómo configurar un conjunto de datos de prueba mediante un asistente o mediante los comandos DMX|[Conjuntos de datos de aprendizaje y prueba](../../analysis-services/data-mining/training-and-testing-data-sets.md)|  
|Obtenga información sobre cómo probar la distribución y la representatividad de los datos de una estructura de minería de datos|[La validación cruzada & #40; Analysis Services: minería de datos & #41;](../../analysis-services/data-mining/cross-validation-analysis-services-data-mining.md)|  
|Obtenga información acerca de los tipos de gráfico de precisión proporcionados.|[Gráfico de elevación & #40; Analysis Services: minería de datos & #41;](../../analysis-services/data-mining/lift-chart-analysis-services-data-mining.md)<br /><br /> [Gráfico de beneficios & #40; Analysis Services: minería de datos & #41;](../../analysis-services/data-mining/profit-chart-analysis-services-data-mining.md)<br /><br /> [Gráfico de dispersión & #40; Analysis Services: minería de datos & #41;](../../analysis-services/data-mining/scatter-plot-analysis-services-data-mining.md)|  
|Aprenda a crear una matriz de clasificación, a veces denominada una matriz de confusión, para evaluar el número de verdaderos positivos, falsos positivos, verdaderos negativos y falsos negativos.|[Matriz de clasificación & #40; Analysis Services: minería de datos & #41;](../../analysis-services/data-mining/classification-matrix-analysis-services-data-mining.md)|  
  
## <a name="see-also"></a>Vea también  
 [Herramientas de minería de datos](../../analysis-services/data-mining/data-mining-tools.md)   
 [Soluciones de minería de datos](../../analysis-services/data-mining/data-mining-solutions.md)   
 [Pruebas y las tareas de validación y procedimientos & #40; minería de datos & #41;](../../analysis-services/data-mining/testing-and-validation-tasks-and-how-tos-data-mining.md)  
  
  
