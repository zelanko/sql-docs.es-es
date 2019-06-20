---
title: Resaltar excepciones (herramientas de análisis de tabla para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Table Analysis tools
- highlight exceptions
ms.assetid: d90a12f8-7bc3-4fdb-95a1-7c89058f0d9a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 18bf54b7b97598c6c61d7e282ad5791d926cc25a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66080761"
---
# <a name="highlight-exceptions-table-analysis-tools-for-excel"></a>Resaltar excepciones (Herramientas de análisis de tabla para Excel)
  ![Botón Resaltar excepciones en la cinta de opciones](media/tat-highlightex.gif "botón Resaltar excepciones en la cinta de opciones")  
  
 En ocasiones, los datos pueden contener valores peculiares. Por ejemplo, la lista de edades de propietarios de casas podría empezar en cinco años. Estos valores, a menudo denominados *valores atípicos*, podrían ser incorrectos debido a un error de entrada de datos, o que podrían indicar tendencias poco habituales. De cualquier modo, las excepciones pueden afectar a la calidad del análisis. El **Resaltar excepciones** herramienta le ayuda a encontrar estos valores y revisarlos para tomar medidas.  
  
 El **Resaltar excepciones** herramienta puede trabajar con todo el rango de datos en una tabla de datos de Excel, o puede seleccionar sólo unas pocas columnas. También es posible ajustar un umbral que controle la variabilidad de los datos para encontrar más o menos excepciones.  
  
 Al completar el análisis, la herramienta crea una hoja de cálculo nueva que contiene un informe de resumen sobre el número de valores atípicos que se encontraron en cada una de las columnas analizadas. La herramienta también resalta las excepciones en la tabla de datos original. Puesto que la herramienta analiza tendencias globales, quizás encuentre que la mayoría de los valores de una fila son normales y resalte sólo una celda de esa fila. En el ejemplo de vivienda anterior, solo el **Age** columna podría resaltarse.  
  
 También puede cambiar el **umbral de excepción** valor en el **informe resumen de**. Este valor indica la probabilidad de que una celda determinada contenga un valor atípico. Por tanto, si aumenta el valor, se resaltarán menos valores como valores atípicos. Por el contrario, cuando el valor se disminuye, se verán más celdas resaltadas.  
  
## <a name="using-the-highlight-exceptions-tool"></a>Usar la herramienta Resaltar excepciones  
  
1.  Abra una tabla de Excel y haga clic en **Resaltar excepciones**.  
  
2.  Especifique las columnas que desea analizar.  
  
3.  Haga clic en **Ejecutar**.  
  
4.  Abra la hoja de cálculo denominada \<nombre de tabla > valores atípicos para ver un resumen de los valores atípicos encontrados.  
  
5.  Para cambiar el número de aspectos destacados, haga clic en arriba y flecha abajo en la **umbral de excepción** fila de la **informe de excepciones resaltadas**.  
  
### <a name="requirements"></a>Requisitos  
 Puede incluir columnas que no contengan valores erróneos si éstos contienen información que podría ser útil en la predicción de otras filas. No obstante, debe anular la selección de las columnas que tengan muchos valores cero o valores ausentes.  
  
 Dado que todas las columnas seleccionadas se utilizan para crear un patrón general, debería evitar usar columnas de entrada que sabe que tienen información no relevante, como las siguientes:  
  
-   Columnas que contienen valores únicos como los identificadores.  
  
-   Columnas que contienen un alto porcentaje de valores erróneos.  
  
-   Columnas con muchos valores ausentes.  
  
     Tenga en cuenta que hay algunos casos en los que resulta útil incluir columnas de entrada que tienen muchos valores ausentes. Por ejemplo, si siempre falta el valor del campo de dirección cuando el cliente compra a través de un minorista, el algoritmo de minería de datos pueden utilizar esta información para identificar otros clientes similares. Debe determinar caso por caso si los datos faltan por omisión o porque el estado Ausente es significativo.  
  
-   Columnas que probablemente no serán útiles para crear un patrón. Por ejemplo, una columna que tiene el mismo valor en todas las filas no agrega ninguna información de utilidad para generar patrones.  
  
## <a name="understanding-the-highlight-exceptions-report"></a>Descripción del Informe de excepciones resaltadas  
 Al hacer clic en **ejecutar**, la herramienta hace tres cosas:  
  
-   Crea la estructura de minería de datos basándose en los datos actuales de la tabla.  
  
-   Crea un nuevo modelo de minería de datos usando el algoritmo de clústeres de [!INCLUDE[msCoName](../includes/msconame-md.md)].  
  
-   Crea una consulta de predicción basándose en los patrones para determinar si algún valor de la hoja de cálculo es improbable.  
  
 El valor inicial para el umbral de excepción siempre es 75, lo que significa que el algoritmo ha calculado que existe un 75% de posibilidad de que los datos resaltados sean erróneos. La herramienta establece automáticamente este umbral para la fase de análisis inicial, pero el valor puede cambiarse en el informe.  
  
 El **Resaltar excepciones** herramienta resalta las celdas de la tabla de datos original que son sospechosas. El resaltado oscuro quiere decir que la fila necesita atención. El resaltado claro indica que el valor de esa celda en particular se identificó como sospechoso. Si cambia el umbral para las excepciones, los valores resaltados cambiarán según corresponda.  
  
 El gráfico de resumen muestra el número de celdas de cada columna que estaban por encima del umbral de excepción.  
  
## <a name="related-tools"></a>Herramientas relacionadas  
 Cuando esté limpiando o revisando datos como preparación para la minería de datos, también debería probar las características de exploración de datos del Cliente de minería de datos para Excel. Este complemento dispone de más herramientas avanzadas que le ayudarán a encontrar valores atípicos, cambiar etiquetas de datos o ver la distribución de datos. Para obtener más información acerca de las herramientas de exploración de datos en el cliente de minería de datos para Excel, vea [exploración y limpieza de datos](exploring-and-cleaning-data.md).  
  
 El **Resaltar excepciones** herramienta usa la [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmo de clústeres. Un modelo de clústeres detecta grupos de filas que comparten características similares. El cliente de minería de datos para Excel proporciona un **examinar** ventana que usa gráficos y perfiles de características que le permiten explorar modelos de minería de datos creados mediante agrupación en clústeres. Para obtener información acerca de cómo examinar el modelo de agrupación en clústeres creado por el **Resaltar excepciones** herramienta, consulte [examinar modelos (datos de cliente de minería de datos para Excel)](highlight-exceptions-table-analysis-tools-for-excel.md).  
  
 Para obtener más información sobre el algoritmo de clústeres de [!INCLUDE[msCoName](../includes/msconame-md.md)], vea el tema "Algoritmo de clústeres de Microsoft" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [Herramientas de análisis de tablas para Excel](table-analysis-tools-for-excel.md)  
  
  
