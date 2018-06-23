---
title: Examinador de KPI (pestaña KPI, Diseñador de cubos) (Analysis Services - datos multidimensionales) | Documentos de Microsoft
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
- sql12.asvs.cubeeditor.kpibrowserpane.f1
ms.assetid: 2f61bde6-e6ec-4511-8645-c272374014ad
caps.latest.revision: 24
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 32373127f72dae058a80712cec564af7dffca45e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36197869"
---
# <a name="kpi-browser-kpis-tab-cube-designer-analysis-services---multidimensional-data"></a>Explorador de KPI (pestaña KPI, Diseñador de cubos) (Analysis Services - Datos multidimensionales)
  Use el panel **Explorador de KPI** de la pestaña **KPI** del Diseñador de cubos para ver y comprobar el resultado de los indicadores clave de rendimiento (KPI). Antes de examinarlos, los KPI deben implementarse en una instancia de [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
> [!NOTE]  
>  Este panel solo se muestra en vista de explorador.  
  
## <a name="options"></a>Opciones  
 **Cuadrícula de subcubo**  
 Se usa para definir un subcubo y restringir el resultado de los KPI que se van a mostrar en el panel **Resultado** . La cuadrícula contiene las columnas siguientes:  
  
 **Dimension**  
 Seleccione la dimensión a la que se aplica este filtro.  
  
 **Hierarchy**  
 Seleccione la jerarquía a la que se aplica este filtro.  
  
 **Operador**  
 Seleccione el operador que define cómo se aplica la expresión de **Expresión de filtro** en la jerarquía seleccionada. En la tabla siguiente se describen los operadores disponibles.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**Igual a**|Los resultados están restringidos al conjunto definido en **Expresión de filtro**.|  
|**No igual**|Los resultados están restringidos a los miembros excluidos por el conjunto definido en **Expresión de filtro**.|  
|**Entrada**|Los resultados están restringidos al conjunto con nombre seleccionado en **Expresión de filtro**.|  
|**No en**|Los resultados están restringidos a los miembros excluidos por el conjunto con nombre seleccionado en **Expresión de filtro**.|  
|**Contiene**|El resultado se restringe a los miembros cuyos nombres contienen la cadena de **Expresión de filtro**.|  
|**Comienza con**|El resultado se restringe a los miembros cuyos nombres comienzan con la cadena de **Expresión de filtro**.|  
|**Intervalo (inclusivo)**|El resultado se restringe al intervalo elegido en **Expresión de filtro**.|  
|**Intervalo (exclusivo)**|El resultado se restringe a los miembros excluidos por el intervalo elegido en **Expresión de filtro**.|  
|**MDX**|El resultado se restringe a la expresión MDX (Expresiones multidimensionales) establecida en **Expresión de filtro**.|  
  
 **Expresión de filtro**  
 Escriba la expresión que evaluará el **Operador**, lo que restringe el resultado de KPI que se examinará.  
  
> [!NOTE]  
>  Este campo es un elemento de entrada de datos dinámico que cambia el aspecto para reflejar los tipos de datos necesarios para el operador seleccionado.  
  
 **Cuadrícula de resultados**  
 Muestra el valor evaluado, el objetivo, el estado y la tendencia de los KPI, basándose en el filtro definido en **Cuadrícula de filtro**. La cuadrícula contiene las columnas siguientes:  
  
 **Estructura de presentación**  
 Muestra los KPI que contiene el cubo, organizado jerárquicamente según los valores de **Carpeta para mostrar** o **KPI primario** de cada KPI.  
  
 **Value**  
 Muestra el valor del KPI.  
  
 **Objetivo**  
 Muestra el valor objetivo del KPI.  
  
 **Estado**  
 Muestra el gráfico de estado del KPI.  
  
 **Tendencia**  
 Muestra el gráfico de tendencia del KPI.  
  
 **Weight**  
 Muestra el factor de peso del KPI.  
  
 **(Descripción)**  
 Muestra un icono de información si se proporciona una descripción para un KPI.  
  
 Mantenga el mouse sobre el icono de información para mostrar la Información sobre herramientas que contiene la descripción del KPI.  
  
> [!NOTE]  
>  Si se produce un error al calcular un KPI en la instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , esta opción muestra información asociada con el error.  
  
## <a name="see-also"></a>Vea también  
 [KPI &#40;Diseñador de cubos&#41; &#40;Analysis Services - datos multidimensionales&#41;](kpis-cube-designer-analysis-services-multidimensional-data.md)  
  
  