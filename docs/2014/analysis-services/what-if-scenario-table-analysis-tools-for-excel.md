---
title: Escenario de si (herramientas de análisis de tabla para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Table Analysis tools
- what if scenario
- scenario analysis
ms.assetid: 4df5a5c5-1983-4009-a7c5-cd340649fd2f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 49b642d60da57192bc0c6bf842a16b0d12d529d5
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/28/2020
ms.locfileid: "78175554"
---
# <a name="what-if-scenario-table-analysis-tools-for-excel"></a>Escenario Y si (Herramientas de análisis de tabla para Excel)
  ![Botón Escenario Y si de las herramientas de análisis de tabla](media/tat-whatif.gif "Botón Escenario Y si de las herramientas de análisis de tabla")

 La herramienta escenario y **si** analiza patrones en los datos existentes y, a continuación, le permite evaluar el efecto que tendrían los cambios en una columna en el valor de una columna diferente.

 Por ejemplo, se podría estudiar el efecto de una subida del precio de un artículo sobre las ventas totales.

 La herramienta es flexible en cuanto al número de predicciones que se pueden crear. Una vez finalizado el análisis inicial, puede predecir cambios para todos los datos de la tabla o especificar valores de prueba de uno en uno.

## <a name="using-the-what-if-scenario-tool"></a>Usar la herramienta de escenario Y si

1.  Abra una tabla de datos de Excel.

2.  Haga clic en **escenarios**y seleccione **Qué hacer si**.

3.  En el cuadro **escenario** , seleccione la columna que contiene el valor que va a cambiar y especifique el cambio como un valor específico o como un porcentaje de cambio (aumenta o disminuye) en los valores actuales.

4.  En el cuadro **¿Qué ocurre** ?, especifique la columna para la que desea evaluar el efecto.

5.  Opcionalmente, haga clic en **elegir las columnas que se van a usar para el análisis** para seleccionar las columnas que probablemente sean útiles para realizar la predicción. También se puede anular la selección de las columnas que pueden resultar de poca utilidad a la hora de detectar patrones, como las que contienen identificadores de fila o nombres.

6.  En el cuadro **especificar fila o tabla** , elija si desea que el impacto se evalúe solo para la fila seleccionada actualmente o para el conjunto completo de datos de la tabla.

7.  Si selecciona **en esta fila**, la herramienta muestra el resultado en el cuadro de diálogo. Mientras el cuadro de diálogo permanece abierto, puede modificar las selecciones para probar otros escenarios.

8.  Si selecciona **toda la tabla**, la herramienta muestra un mensaje de estado en el cuadro de diálogo y agrega dos nuevas columnas a la tabla de datos original. Haga clic en **cerrar** para ver los resultados completos en la hoja de cálculo.

### <a name="requirements"></a>Requisitos
 Esta herramienta utiliza el algoritmo de regresión logística de Microsoft, que admite la predicción de valores numéricos o discretos. Sin embargo, para obtener los mejores resultados, se recomienda seguir las prácticas recomendadas siguientes:

-   Seleccione columnas para el análisis que contengan información útil.

-   Si incluye muy pocas columnas, puede ser difícil obtener un resultado.

-   Si usa la opción **para valor** , debe escribir un valor en el cuadro o seleccionar un valor de la lista.

-   Si usa la opción **porcentaje** , establezca el cambio en porcentaje de aumento o disminución. El valor predeterminado es 120%, lo que supone un incremento del 20% sobre el valor actual.

> [!NOTE]
>  Si no establece un valor, se podría producir un error.

## <a name="understanding-the-results-of-what-if-analysis"></a>Descripción de los resultados de un análisis Y si
 Al crear un escenario **de tipo "si"** , la herramienta hace tres cosas:

-   Crea una estructura de minería de datos que almacena hechos clave sobre los datos de la tabla.

-   Crea un modelo de minería de datos de regresión logística basado en los datos.

-   Crea una consulta de predicción para cada uno de los valores especificados.

 Puede generar todas las predicciones al mismo tiempo si especifica toda la **tabla**. En ese caso, la herramienta crea dos nuevas columnas en la tabla de datos original.

 Las columnas que se agregan a la tabla contienen dos tipos de información: el valor de predicción dado el cambio y su confianza. La confianza significa la probabilidad de que la predicción sea correcta.

 También se pueden especificar los valores de cambio uno a uno en el cuadro de diálogo y ver las predicciones de forma interactiva. Esto es lo mismo que crear una *consulta de predicción singleton*. Los resultados de la consulta de predicción incluyen la siguiente información: el éxito o el fracaso de la predicción, el valor de predicción y el nivel de confianza. El nivel de confianza aparece como una barra que contiene una línea de puntos. Cuanto más larga sea la línea de puntos, mayor será la confianza en el resultado.

 Por ejemplo, si intenta determinar el efecto de aumentar la edad del cliente en la voluntad del cliente por comprar y aumentar la edad del cliente a 25, la herramienta **What-if** consulta el modelo de minería de datos y devuelve el siguiente resultado:

 **El análisis Y si de Purchases Bicycle encontró una solución.**

 **'Purchases Bicycle' = sí**

 **Confianza: Regular**

 Dado que este resultado se basa en una fila existente de la tabla de datos, eso significa que, para un cliente concreto, si todos los datos sobre ese cliente permanecen iguales pero la edad se aumenta a 25, probablemente compraría una bicicleta.

 El obtener las predicciones con la tabla de datos original podría facilitar la determinación de si las predicciones son útiles.

## <a name="related-tools"></a>Herramientas relacionadas
 El Cliente de minería de datos para Excel, que es un complemento independiente que ofrece funciones de minería de datos más avanzadas, incluye asistentes para crear modelos de minería de datos que predicen el comportamiento. Para obtener más información, vea [crear un modelo de minería de datos](creating-a-data-mining-model.md).

 Para obtener más información acerca del algoritmo usado por la herramienta de escenario y **si** , vea el tema "algoritmo de regresión logística de Microsoft" en libros en pantalla de SQL Server.

## <a name="see-also"></a>Consulte también
 [Herramientas de análisis de tabla para Excel](table-analysis-tools-for-excel.md)


