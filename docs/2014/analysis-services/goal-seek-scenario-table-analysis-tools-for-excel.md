---
title: Escenario de búsqueda de objetivos (herramientas de análisis de tabla para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Table Analysis tools
- scenario analysis
- goal seek scenario
ms.assetid: efe50306-cf7c-46b3-9cc4-e7f0b6968b0c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d547c52bc5d4cb02870fc647469b5f63af9ab7cb
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66080739"
---
# <a name="goal-seek-scenario-table-analysis-tools-for-excel"></a>Buscar objetivo (escenario de Herramientas de análisis de tabla para Excel)
  ![Botón Buscar objetivo, Herramientas de análisis de tabla](media/tat-goalseek.gif "Botón Buscar objetivo, Herramientas de análisis de tabla")  
  
 La herramienta de escenario **Buscar objetivo** es complementaria a la herramienta escenario de [What if](what-if-scenario-table-analysis-tools-for-excel.md) . La herramienta **qué** le indica el impacto de realizar un cambio, mientras que la herramienta **Buscar objetivo** le indica los factores subyacentes que deben cambiar para lograr el resultado deseado.  
  
 Por ejemplo, supongamos que su objetivo es aumentar la satisfacción del cliente. Puede usar el análisis de **búsqueda de objetivo** para determinar qué factores serían más probables para aumentar la satisfacción del cliente y decidir si esos cambios son rentables.  
  
 Cuando la herramienta finaliza su análisis, crea dos columnas nuevas en la tabla de datos de origen. Estas columnas muestran la *probabilidad* de que se pueda lograr el resultado de destino y el cambio recomendado, si existe.  
  
 La herramienta puede analizar un conjunto de datos y hacer predicciones para el conjunto completo; también es posible crear el análisis y, a continuación, ir probando los escenarios de uno en uno.  
  
## <a name="using-the-goal-seek-scenario-tool"></a>Usar la herramienta de escenario Buscar objetivo  
  
1.  Abra una tabla de Excel.  
  
2.  Haga clic en **escenarios**y seleccione **Buscar objetivo**.  
  
3.  En el cuadro de diálogo **análisis de escenario: Buscar objetivo** , seleccione la columna que contiene el valor de destino de la lista.  
  
4.  Especifique el valor que desea conseguir.  
  
     Si el objetivo de la columna contiene valores numéricos continuos, también puede especificar el aumento o la disminución que desea para el valor. Por ejemplo, puede elegir **ventas** como columna y especificar que el destino es un aumento del 120%.  
  
     También puede especificar el objetivo como un intervalo de valores, escribiendo un límite inferior y uno superior.  
  
5.  Especifique la columna que contiene los valores que cambiará. En otras palabras, escoja la columna que se manipulará para obtener el resultado deseado.  
  
6.  Opcionalmente, haga clic en **elegir las columnas que se van a usar para el análisis**y seleccione las columnas que contengan información útil. Anule la selección de las columnas que no contribuyan al análisis.  
  
    > [!NOTE]  
    >  No anule la selección de las columnas que usará como objetivo o para los cambios. Estas columnas son necesarias.  
  
7.  Especifique si desea realizar predicciones para toda la tabla o solo para la fila seleccionada.  
  
8.  Si ha seleccionado la opción de **tabla completa** , la herramienta agrega las predicciones a la tabla de origen en dos nuevas columnas.  
  
9. Si ha seleccionado la opción **en esta fila**, los resultados del análisis se muestran en el cuadro de diálogo para su revisión. El cuadro de diálogo permanece abierto para que pueda seguir probando valores y objetivos diferentes.  
  
### <a name="requirements"></a>Requisitos  
 Esta herramienta usa el algoritmo de regresión logística de Microsoft, que puede procesar valores numéricos o discretos.  
  
 Puede ejecutar la predicción varias veces y seleccionar otras columnas posteriormente, pero cada combinación de un objetivo y un cambio debe calcularse de forma independiente.  
  
 Puede obtener mejores resultados si selecciona columnas para el análisis que contengan información útil. No obstante, si incluye muy pocas columnas, puede resultar difícil obtener un resultado.  
  
 Cuando cree predicciones de una en una, asegúrese de que selecciona una fila que no contiene el resultado deseado o puede obtener un error. En otras palabras, si el propósito de la búsqueda de un objetivo consiste en determinar factores que animan a comprar bicicletas, solo debería incluir los clientes que no han comprado una bicicleta.  
  
## <a name="understanding-the-results-of-goal-seek-analysis"></a>Descripción de los resultados de un análisis Buscar objetivo  
 Cuando se crea un escenario de búsqueda de objetivo, la herramienta hace tres cosas:  
  
-   Crea una estructura de minería de datos que almacena hechos clave sobre los datos de la tabla.  
  
-   Crea un modelo de minería de datos de regresión logística basado en los datos.  
  
-   Crea una predicción para cada valor especificado.  
  
 Si prueba los escenarios de búsqueda de objetivo de uno en uno, puede ver los resultados interactivamente. Esto es lo mismo que crear una *consulta de predicción singleton*.  
  
 La herramienta informa en el panel de **resultados** del cuadro de diálogo si fue correcto encontrar un escenario que logre el objetivo deseado. Si se encontró una solución correcta, la herramienta también genera una recomendación que le indica el cambio necesario. Por ejemplo, la herramienta **Buscar objetivo** puede indicarle que la distancia de trabajo debe ser inferior a 5 kilómetros.  
  
 Resultados de ejemplo:  
  
 **La búsqueda de objetivo para Interest in Buying encontró una solución.**  
  
 **Coincidencia más cercana obtenida al cambiar 'Conmute distance' a '2-5 miles'.**  
  
 Dado que este resultado se basa en una fila existente de la tabla de datos, eso significa que, para un cliente concreto, si todos los demás datos sobre ese cliente permanecieran iguales, pero su distancia al trabajo se redujera hasta situarse entre 2 y 5 millas, habría más probabilidades de que comprase una bicicleta.  
  
 Si crea predicciones de búsqueda de objetivos para todas las filas de la tabla de Excel especificando **toda la tabla**, la herramienta crea dos nuevas columnas en la tabla de datos original. La primera columna que se agrega a la tabla contiene una marca de verificación en un círculo verde para indicar que se puede conseguir el objetivo o una marca X en un círculo rojo para indicar que no es posible realizar ningún cambio que permita alcanzar el objetivo.  
  
 La segunda columna contiene el cambio recomendado.  
  
> [!NOTE]  
>  El nivel de confianza de la recomendación y su éxito están predeterminados por el algoritmo y no se pueden cambiar.  
  
## <a name="related-tools"></a>Herramientas relacionadas  
 El Cliente de minería de datos para Excel, que es un complemento independiente que ofrece funciones de minería de datos más avanzadas, incluye asistentes para crear modelos de minería de datos que predicen el comportamiento. Para obtener más información, vea [crear un modelo de minería de datos](creating-a-data-mining-model.md).  
  
 Para obtener más información acerca del algoritmo usado por la herramienta de escenario **Buscar objetivo** , vea el tema "algoritmo de regresión logística [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] de Microsoft" en los libros en pantalla de.  
  
## <a name="see-also"></a>Consulte también  
 [Herramientas de análisis de tabla para Excel](table-analysis-tools-for-excel.md)  
  
  
