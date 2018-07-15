---
title: Buscar objetivo escenario (herramientas de análisis de tabla para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Table Analysis tools
- scenario analysis
- goal seek scenario
ms.assetid: efe50306-cf7c-46b3-9cc4-e7f0b6968b0c
caps.latest.revision: 22
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2f17c85c7296daaead3b24b4d4002ad9c1be7221
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37187302"
---
# <a name="goal-seek-scenario-table-analysis-tools-for-excel"></a>Buscar objetivo (escenario de Herramientas de análisis de tabla para Excel)
  ![Botón de búsqueda de objetivo en herramientas de análisis de tabla](media/tat-goalseek.gif "botón Buscar objetivo en herramientas de análisis de tabla")  
  
 El **Buscar objetivo** herramienta de escenario es complementaria a la [¿qué ocurre si](what-if-scenario-table-analysis-tools-for-excel.md) herramienta de escenario. El **hipótesis** herramienta informa del impacto de realizar un cambio, mientras que el **Buscar objetivo** informa de los factores subyacentes que se deben cambiar para lograr un resultado deseado.  
  
 Por ejemplo, suponga que su objetivo es aumentar la satisfacción de los clientes. Puede usar **Buscar objetivo** análisis para determinar qué factores sería probablemente aumente la satisfacción del cliente, y decidir si esos cambios son rentables.  
  
 Cuando la herramienta finaliza su análisis, crea dos columnas nuevas en la tabla de datos de origen. Estas columnas muestran el *probabilidad* que se puede lograr el resultado deseado y el cambio recomendado, si existe.  
  
 La herramienta puede analizar un conjunto de datos y hacer predicciones para el conjunto completo; también es posible crear el análisis y, a continuación, ir probando los escenarios de uno en uno.  
  
## <a name="using-the-goal-seek-scenario-tool"></a>Usar la herramienta de escenario Buscar objetivo  
  
1.  Abra una tabla de Excel.  
  
2.  Haga clic en **escenarios**y seleccione **Buscar objetivo**.  
  
3.  En el **análisis de escenario: Buscar objetivo** cuadro de diálogo, seleccione la columna que contiene el destino de valor de la lista.  
  
4.  Especifique el valor que desea conseguir.  
  
     Si el objetivo de la columna contiene valores numéricos continuos, también puede especificar el aumento o la disminución que desea para el valor. Por ejemplo, podría elegir **ventas** como la columna y especificar que el destino es un aumento del 120%.  
  
     También puede especificar el objetivo como un intervalo de valores, escribiendo un límite inferior y uno superior.  
  
5.  Especifique la columna que contiene los valores que cambiará. En otras palabras, escoja la columna que se manipulará para obtener el resultado deseado.  
  
6.  Si lo desea, haga clic en **elegir las columnas que se usará para el análisis**y seleccione las columnas que contienen información útil. Anule la selección de las columnas que no contribuyan al análisis.  
  
    > [!NOTE]  
    >  No anule la selección de las columnas que usará como objetivo o para los cambios. Estas columnas son necesarias.  
  
7.  Especifique si desea realizar predicciones para toda la tabla o solo para la fila seleccionada.  
  
8.  Si ha seleccionado la **toda la tabla** opción, la herramienta agrega las predicciones a la tabla de origen en dos nuevas columnas.  
  
9. Si ha seleccionado la opción **en esta fila**, los resultados del análisis aparecen en el cuadro de diálogo para su revisión. El cuadro de diálogo permanece abierto para que pueda seguir probando valores y objetivos diferentes.  
  
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
  
 Si prueba los escenarios de búsqueda de objetivo de uno en uno, puede ver los resultados interactivamente. Esto es lo mismo que crear un *consulta de predicción singleton*.  
  
 La herramienta de informes en el **resultados** panel del cuadro de diálogo cuadro si tuvo éxito y encontró un escenario que logra el objetivo deseado. Si se encontró una solución correcta, la herramienta también genera una recomendación que le indica el cambio necesario. Por ejemplo, el **Buscar objetivo** herramienta puede indicarle que la distancia de viaje al trabajo debería ser menor que 5 millas.  
  
 Resultados del ejemplo:  
  
 **Búsqueda de objetivo para Interest in Buying encontró una solución.**  
  
 **Coincidencia más cercana obtenida al cambiar 'Conmute distance' a ' 2-5 miles'.**  
  
 Dado que este resultado se basa en una fila existente de la tabla de datos, eso significa que, para un cliente concreto, si todos los demás datos sobre ese cliente permanecieran iguales, pero su distancia al trabajo se redujera hasta situarse entre 2 y 5 millas, habría más probabilidades de que comprase una bicicleta.  
  
 Si crea predicciones de búsqueda de objetivo para todas las filas en la tabla de Excel mediante la especificación de **toda la tabla**, thetool crea dos nuevas columnas en la tabla de datos original. La primera columna que se agrega a la tabla contiene una marca de verificación en un círculo verde para indicar que se puede conseguir el objetivo o una marca X en un círculo rojo para indicar que no es posible realizar ningún cambio que permita alcanzar el objetivo.  
  
 La segunda columna contiene el cambio recomendado.  
  
> [!NOTE]  
>  El nivel de confianza de la recomendación y su éxito están predeterminados por el algoritmo y no se pueden cambiar.  
  
## <a name="related-tools"></a>Herramientas relacionadas  
 El Cliente de minería de datos para Excel, que es un complemento independiente que ofrece funciones de minería de datos más avanzadas, incluye asistentes para crear modelos de minería de datos que predicen el comportamiento. Para obtener más información, consulte [crear un modelo de minería de datos](creating-a-data-mining-model.md).  
  
 Para obtener más información acerca del algoritmo usado por el **Buscar objetivo** escenario herramienta, vea el tema "Algoritmo de regresión logística de Microsoft" en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] libros en pantalla.  
  
## <a name="see-also"></a>Vea también  
 [Herramientas de análisis de tablas para Excel](table-analysis-tools-for-excel.md)  
  
  
