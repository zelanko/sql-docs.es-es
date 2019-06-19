---
title: Indicadores de rendimiento (KPI) en modelos multidimensionales clave | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- viewing Key Performance Indicators
- Key Performance Indicators [Analysis Services]
- KPIs [Analysis Services]
- OLAP objects [Analysis Services], performance indicators
- weights [Analysis Services]
- displaying Key Performance Indicators
- parent KPIs [Analysis Services]
- child KPIs
ms.assetid: 73aee2da-da30-44f1-829c-0a4c078a7768
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 35482dc6206f0ad8807cb0f9a3e46902d14061ab
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66074799"
---
# <a name="key-performance-indicators-kpis-in-multidimensional-models"></a>Indicadores clave de rendimiento (KPI) en modelos multidimensionales
  En la terminología empresarial, un indicador clave de rendimiento (KPI) es una medida cuantificable para identificar los éxitos empresariales.  
  
 En [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], un KPI es un conjunto de cálculos asociados a un grupo de medida de un cubo, que se usa para evaluar el éxito empresarial. Normalmente, estos cálculos son una combinación de expresiones MDX (Expresiones multidimensionales) o miembros calculados. Los KPI también tienen metadatos adicionales que proporcionan información acerca de cómo deberían las aplicaciones cliente mostrar los resultados de los cálculos de KPI.  
  
 Un KPI administra información sobre un objetivo establecido, la fórmula real del rendimiento registrada en el cubo y medidas para mostrar la tendencia y el estado del rendimiento. Para definir las fórmulas y otras definiciones acerca de los valores se un KPI se usa AMO. La aplicación cliente usa una interfaz de consulta, como ADOMD.NET, para recuperar y exponer los valores de KPI al usuario final. Para obtener más información, vea [Desarrollar con ADOMD.NET](https://docs.microsoft.com/bi-reference/adomd/developing-with-adomd-net).  
  
 Un objeto <xref:Microsoft.AnalysisServices.Kpi> simple se compone de la información básica, el objetivo, el valor real logrado, un valor de estado, un valor de tendencia y una carpeta donde se ve el KPI. La información básica incluye el nombre y la descripción del KPI. El objetivo es una expresión MDX que se evalúa como un número. El valor real es una expresión MDX que se evalúa como un número. El estado y el valor de tendencia son expresiones MDX que se evalúan como un número. La carpeta es una ubicación sugerida para el KPI que se va a presentar al cliente.  
  
 En la terminología empresarial, un indicador clave de rendimiento (KPI) es una medida cuantificable para identificar los éxitos empresariales. Un KPI se evalúa con frecuencia a lo largo del tiempo. Por ejemplo, el departamento de ventas de una organización puede utilizar el beneficio bruto mensual como un KPI, pero el departamento de recursos humanos de la misma organización puede utilizar la rotación de personal trimestral. Cada uno de ellos es un ejemplo de KPI. Los ejecutivos de una compañía suelen utilizar KPI agrupados en una pestaña empresarial para obtener un resumen histórico rápido y preciso de los éxitos empresariales.  
  
 En [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], un KPI es un conjunto de cálculos asociados a un grupo de medida de un cubo, que se usa para evaluar el éxito empresarial. Normalmente, estos cálculos son una combinación de expresiones MDX (Expresiones multidimensionales) y miembros calculados. Los KPI también tienen metadatos adicionales que proporcionan información acerca de cómo deberían las aplicaciones cliente mostrar los resultados de un cálculo de los KPI.  
  
 Una ventaja fundamental de los KPI de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] es que son KPI basados en el servidor que pueden ser usados por diferentes aplicaciones cliente. Un KPI basado en el servidor presenta una única versión de veracidad, en comparación con versiones independientes de la veracidad de aplicaciones cliente independientes. Además, al realizar esos cálculos que en ocasiones pueden ser complejos en el servidor, en lugar de en cada equipo cliente se pueden obtener tener algunas ventajas de rendimiento.  
  
## <a name="common-kpi-terms"></a>Términos comunes utilizados en KPI  
 En la tabla siguiente se proporcionan definiciones de términos comunes utilizados en KPI en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
|Término|Definición|  
|----------|----------------|  
|Objetivo|Expresión numérica MDX o cálculo que devuelve el valor de destino del KPI.|  
|Valor|Expresión númerica MDX que devuelve el valor real del KPI.|  
|Estado|Expresión MDX que representa el estado del KPI en un punto temporal específico.<br /><br /> La expresión MDX de estado debe devolver un valor normalizado entre -1 y 1. Los valores iguales o inferiores a -1 se interpretarán como "malos" o "bajos". El valor cero (0) se interpreta como "aceptable" o "medio." Los valores iguales o superiores a 1 se interpretarán como "correctos" o "altos".<br /><br /> Opcionalmente puede devolverse un número ilimitado de valores intermedios que se pueden utilizar para mostrar gran cantidad de estados adicionales, si la aplicación cliente lo admite.|  
|Tendencia|Expresión MDX que evalúa el valor del KPI con el paso del tiempo. La tendencia puede ser cualquier criterio basado en el tiempo que sea útil en determinado contexto empresarial.<br /><br /> La expresión MDX de tendencia permite a un usuario corporativo determinar si el KPI mejora o empeora a lo largo del tiempo.|  
|Indicador de estado|Elemento visual que proporciona una indicación rápida del estado de un KPI. La visualización del elemento se determina con el valor de la expresión MDX que evalúa el estado.|  
|Indicador de tendencia|Elemento visual que proporciona una indicación rápida de la tendencia de un KPI. La visualización del elemento se determina con el valor de la expresión MDX que evalúa la tendencia.|  
|Carpeta para mostrar|Carpeta en la que aparecerá el KPI cuando el usuario examine el cubo.|  
|KPI primario|Referencia a un KPI existente que utiliza el valor del KPI secundario como parte del cálculo del KPI primario. En ocasiones, un solo KPI será un cálculo compuesto por los valores de otros KPI. Esta propiedad facilita la visualización de los KPI secundarios situados por debajo del KPI primario en las aplicaciones cliente.|  
|Miembro de hora actual|Expresión MDX que devuelve el miembro que identifica el contexto temporal del KPI.|  
|Weight|Expresión numérica MDX que asigna una importancia relativa a un KPI. Si el KPI se asigna a un KPI primario, el peso se utiliza para ajustar proporcionalmente los resultados del valor del KPI secundario al calcular el valor del KPI primario.|  
  
## <a name="parent-kpis"></a>KPI primarios  
 Una organización puede realizar el seguimiento de distintas métricas empresariales a varios niveles. Por ejemplo, solo pueden utilizarse dos o tres KPI para medir el éxito empresarial de toda una compañía, pero estos KPI de toda la compañía pueden basarse en otros tres o cuatro KPI de los que las unidades empresariales de la compañía han realizado un seguimiento. Asimismo, las unidades empresariales de una compañía pueden utilizar estadísticas diferentes para calcular el mismo KPI, cuyos resultados se acumulan en el KPI de toda la compañía.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] permite definir una relación de elementos primarios y secundarios entre los KPI. Esta relación de elementos primarios y secundarios permite utilizar los resultados del KPI secundario para calcular los resultados del KPI primario. Las aplicaciones cliente también pueden usar esta relación para mostrar correctamente los KPI primarios y secundarios.  
  
## <a name="weights"></a>Pesos  
 También se pueden asignar pesos a los KPI secundarios. Los pesos permiten a [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ajustar proporcionalmente los resultados del KPI primario cuando se calcula el valor del KPI primario.  
  
## <a name="retrieving-and-displaying-kpis"></a>Recuperar y mostrar los KPI  
 La visualización de los KPI depende de la implementación de la aplicación cliente. Por ejemplo, al seleccionar **Vista de explorador** en la barra de herramientas en la pestaña **KPIs** del Diseñador de cubos, se demuestra una posible implementación cliente, en la que los gráficos se utilizan para mostrar los indicadores de estado y tendencia, las carpetas de visualización se utilizan para agrupar los KPI y los KPI secundarios se muestran debajo de los KPI primarios.  
  
 Puede utilizar las funciones de MDX para recuperar secciones individuales del KPI, como el valor o el objetivo, para utilizar en expresiones MDX, instrucciones y scripts.  
  
  
