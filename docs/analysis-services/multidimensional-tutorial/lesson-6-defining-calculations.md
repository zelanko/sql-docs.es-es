---
title: 'Lección 6: Definir cálculos | Microsoft Docs'
ms.date: 05/06/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5e4b4dbae844177fe121fcf1b22f4f6bf68c8584
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65403887"
---
# <a name="lesson-6-defining-calculations"></a>Lección 6: Definición de cálculos
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]

En esta lección, aprenderá a definir cálculos, que son scripts o expresiones de Expresiones multidimensionales (MDX). Los cálculos le permiten definir miembros calculados, conjuntos con nombre y ejecutar otros comandos de script para ampliar las capacidades de un cubo de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Por ejemplo, puede ejecutar un comando de script para definir un subcubo y, a continuación, asignar un cálculo a las celdas del subcubo.  
  
Al definir un nuevo cálculo en el Diseñador de cubos, el cálculo se agrega al panel **Organizador de script** de la pestaña **Cálculos** del Diseñador de cubos, y los campos del tipo de cálculo en cuestión aparecen en un formulario de cálculos en el panel de las **expresiones de cálculo** . Los cálculos se ejecutan en el orden en el que aparecen en el panel **Organizador de script** . Para reorganizar los cálculos, haga clic con el botón derecho en un cálculo determinado y seleccione **Subir** o **Bajar**, o haga clic en un cálculo determinado y use los iconos **Subir** o **Bajar** en la barra de herramientas de la pestaña **Cálculos** .  
  
En la pestaña **Cálculos** , puede agregar nuevos cálculos y ver o editar cálculos existentes en las vistas siguientes del panel de las **expresiones de cálculo** :  
  
-   Vista de formulario. Esta vista muestra las expresiones y propiedades de un comando único en formato de gráfico. Al editar un script MDX, un cuadro de expresión rellena la vista de formulario.  
  
-   Vista de script. Esta vista muestra todos los scripts de cálculo en un editor de código, lo que le permite cambiar fácilmente los scripts de cálculo. Cuando el panel de las **expresiones de cálculo** está en la Vista de script, el **Organizador de script** estará oculto. La Vista de script proporciona codificación de color, coincidencia de paréntesis, autocompletar y regiones de código MDX. Puede expandir o contraer las regiones de código MDX para facilitar la edición.  
  
Para cambiar de una vista a otra en el panel de las **expresiones de cálculo** , haga clic en **Vista de formulario** o **Vista de script** en la barra de herramientas de la pestaña **Cálculos** .  
  
> [!NOTE]  
> Si [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] detecta un error de sintaxis en algún cálculo, la vista de formulario no aparecerá hasta que el error se haya corregido en la Vista de script.  
  
También puede utilizar el Asistente de Business Intelligence para agregar determinados cálculos a un cubo. Por ejemplo, puede utilizar este asistente para agregar inteligencia de tiempo a un cubo, lo que significa definir miembros calculados para cálculos relacionados con el tiempo como, por ejemplo, períodos hasta fecha, medias móviles o crecimiento entre períodos. Para obtener más información, vea [Definir cálculos de inteligencia de tiempo mediante el Asistente de Business Intelligence](../multidimensional-models/define-time-intelligence-calculations-using-the-business-intelligence-wizard.md).  
  
> [!IMPORTANT]  
> En la pestaña **Cálculos** , el script de cálculo empieza por el comando CALCULATE. El comando CALCULATE controla la agregación de las celdas en el cubo y solo debería editar este comando si intenta especificar manualmente la forma en que se deberían agregar las celdas del cubo.  
  
Para obtener más información, consulte [Cálculos](../multidimensional-models-olap-logical-cube-objects/calculations.md)y [Cálculos en modelos multidimensionales](../multidimensional-models/calculations-in-multidimensional-models.md).  
  
> [!NOTE]  
> Los proyectos completos para todas las lecciones de este tutorial están disponibles en línea. Puede saltar a continuación a cualquier lección con el proyecto completado de la lección anterior como punto de partida. [Haga clic aquí](http://go.microsoft.com/fwlink/?LinkID=221866) para descargar los proyectos de ejemplo que tienen que ver con este tutorial.  
  
Esta lección contiene las siguientes tareas:  
  
[Definir miembros calculados](lesson-6-1-defining-calculated-members.md)  
En esta tarea, aprenderá a definir miembros calculados.  
  
[Definir conjuntos con nombre](lesson-6-2-defining-named-sets.md)  
En esta tarea, aprenderá a definir conjuntos con nombre.  
  
## <a name="next-lesson"></a>Lección siguiente  
[Lección 7: Definir indicadores clave de rendimiento &#40;KPI&#41;](lesson-7-defining-key-performance-indicators-kpis.md)  
  
## <a name="see-also"></a>Vea también  
[Escenario de Tutorial de Analysis Services](analysis-services-tutorial-scenario.md)  
[Crear conjuntos con nombre](../multidimensional-models/create-named-sets.md)  
[Crear miembros calculados](../multidimensional-models/create-calculated-members.md)  
  
  
  
