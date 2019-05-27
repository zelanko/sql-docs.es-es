---
title: Herramientas de análisis de tabla para Excel | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Table Analysis tools
- getting started
ms.assetid: 6d9d1481-18e4-4108-9efa-68152b0940c9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: af4c8ae7c2ba827e6110602bd21432fec4f74393
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66067972"
---
# <a name="table-analysis-tools-for-excel"></a>Herramientas de análisis de tabla para Excel
  Las herramientas de minería de datos en el **analizar** barra de herramientas son la manera más fácil empezar a trabajar con minería de datos. Cada una de estas herramientas analiza automáticamente la distribución y el tipo de los datos, y establece los parámetros para asegurarse de que los resultados son válidos. No tiene que seleccionar un algoritmo ni configurar parámetros complejos.  
  
 ![DM](media/dm-tabletoolsanalyze.gif "DM")  
  
 El **analizar** cinta incluye las siguientes herramientas:  
  
 [Analizar Influenciadores clave &#40;herramientas de análisis de tabla para Excel&#41;](analyze-key-influencers-table-analysis-tools-for-excel.md)  
 Elija una columna o valor de salida de interés y el algoritmo analizará todos los datos de entrada para identificar los factores que ejercen mayor influencia en el destino. Opcionalmente, puede crear un informe que compare dos valores, de modo que pueda ver cómo cambian los influenciadores.  
  
 El **analizar Influenciadores clave** herramienta usa el algoritmo Bayes Naïve de Microsoft.  
  
 [Detectar categorías &#40;herramientas de análisis de tabla para Excel&#41;](detect-categories-table-analysis-tools-for-excel.md)  
 Esta herramienta le permite agregar cualquier conjunto de datos y aplicar la agrupación en clústeres para buscar agrupaciones de datos. Es útil para buscar similitudes y crear grupos para analizarlos en detalle.  
  
 El **detectar categorías** herramienta usa el algoritmo Microsoft Clustering.  
  
 [Rellenar desde ejemplo &#40;herramientas de análisis de tabla para Excel&#41;](fill-from-example-table-analysis-tools-for-excel.md)  
 Esta herramienta le ayuda a imputar valores ausentes. Proporcione algunos ejemplos de cómo deben ser los valores ausentes, y la herramienta creará patrones basados en todos los datos de la tabla; a continuación, recomendará nuevos valores basados en patrones de los datos.  
  
 El **rellenar desde ejemplo** herramienta usa el algoritmo de regresión logística de Microsoft.  
  
 [Previsión &#40;herramientas de análisis de tabla para Excel&#41;](forecast-table-analysis-tools-for-excel.md)  
 Esta herramienta toma los datos que cambian a lo largo del tiempo, y predice valores futuros.  
  
 El **previsión** herramienta usa el algoritmo de serie temporal de Microsoft.  
  
 [Resaltar excepciones &#40;herramientas de análisis de tabla para Excel&#41;](highlight-exceptions-table-analysis-tools-for-excel.md)  
 Esta herramienta analiza patrones en una tabla de datos y busca filas y valores que no se ajustan al patrón. Seguidamente, puede revisarlos, corregirlos y volver a ejecutar el modelo o marcar valores para acciones posteriores.  
  
 El **Resaltar excepciones** herramienta usa el algoritmo Microsoft Clustering.  
  
 [Escenario Buscar objetivo &#40;herramientas de análisis de tabla para Excel&#41;](goal-seek-scenario-table-analysis-tools-for-excel.md)  
 En el **Buscar objetivo** herramienta, especifique un valor de destino y la herramienta identifica los factores subyacentes que deben cambiar para alcanzar dicho destino. Por ejemplo, si sabe que debe aumentar la satisfacción de las llamadas en un 20 %, puede pedir al modelo que prediga los factores que deben cambiar para producir ese objetivo.  
  
 El **Buscar objetivo** herramienta usa el algoritmo de regresión logística de Microsoft.  
  
 [Escenario y si &#40;herramientas de análisis de tabla para Excel&#41;](what-if-scenario-table-analysis-tools-for-excel.md)  
 El **el análisis de hipótesis** herramienta complementa el **Buscar objetivo** herramienta. Con esta herramienta, se introduce el valor que se desea cambiar y el modelo predice si el cambio será suficiente para obtener el resultado deseado. Por ejemplo, podría solicitar al modelo que infiera si la adición de un operador de llamadas adicional incrementaría la satisfacción del cliente en un punto.  
  
 El **hipótesis** herramienta usa el algoritmo de regresión logística de Microsoft.  
  
 [Cálculo de predicción &#40;herramientas de análisis de tabla para Excel&#41;](prediction-calculator-table-analysis-tools-for-excel.md)  
 Esta herramienta crea un modelo que analiza los factores que conducen al resultado de destino y después predice un resultado para cualquier nueva entrada, según las reglas de puntuación derivadas de los datos. Esta herramienta también genera una hoja de cálculo interactiva de toma de decisiones que le permite puntuar las nuevas entradas con facilidad. También puede crear una versión impresa de la hoja de cálculo de puntuaciones para su uso sin conexión.  
  
 El **cálculo de predicción** herramienta usa el algoritmo de regresión logística de Microsoft.  
  
 [Análisis de cesta &#40;herramientas de análisis de tabla para Excel&#41;](shopping-basket-analysis-table-analysistools-for-excel.md)  
 Esta herramienta identifica los patrones que se pueden utilizar en la venta cruzada o en la venta de productos de mayor precio. Identifica los grupos de productos que suelen comprare juntos y también genera informes basados en el precio y el costo de paquetes de productos relacionados, para ayudar a la toma de decisiones.  
  
 La herramienta no está limitada al análisis de la cesta de la compra; puede aplicarse a cualquier problema que se preste al análisis asociativo. Por ejemplo, podría buscar los eventos que ocurren juntos con frecuencia, los factores que dan como resultado un diagnóstico o para cualquier otro posible conjunto de causas y resultados.  
  
 El **análisis de cesta de la compra** herramienta usa el algoritmo Microsoft Association.  
  
## <a name="requirements-for-the-table-analysis-tools-for-excel"></a>Requisitos para las Herramientas de análisis de tabla para Excel  
 Para utilizar las Herramientas de análisis de tabla para Excel, primero debe crear una conexión a una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Esta conexión proporciona acceso a los algoritmos de minería de datos de Microsoft que se usan para analizar los datos. Si no tiene acceso a una instancia, se recomienda que solicite al administrador que configure una instancia que pueda utilizar para experimentar con la minería de datos. Para obtener más información, consulte [conectarse a los datos de origen &#40;cliente de minería de datos para Excel&#41;](connect-to-source-data-data-mining-client-for-excel.md).  
  
 Para trabajar con datos utilizando las Herramientas de análisis de tabla, debe convertir el rango de datos que desea usar al formato de tabla de Excel.  
  
 Si no ve el **analizar** la cinta de opciones, intente hacer clic dentro de una tabla de datos en primer lugar. El menú no se activa hasta que se selecciona una tabla de datos.  
  
## <a name="see-also"></a>Vea también  
 [Cliente de minería de datos para Excel &#40;complementos de minería de datos de SQL Server&#41;](data-mining-client-for-excel-sql-server-data-mining-add-ins.md)   
 [Solución de problemas de diagramas de minería de datos de Visio &#40;complementos de minería de datos de SQL Server&#41;](troubleshooting-visio-data-mining-diagrams-sql-server-data-mining-add-ins.md)   
 [Qué se incluye en los Complementos de minería de datos para Office](what-s-included-in-the-data-mining-add-ins-for-office.md)  
  
  
