---
title: Examinar el cubo | Documentos de Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d54ccdeed21f475ee90f0ec257f20c53076039ea
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34017552"
---
# <a name="lesson-2-6---browsing-the-cube"></a>Lección 2-6-examinar el cubo
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

Una vez implementado un cubo, los datos de este pueden verse en la pestaña **Explorador** del Diseñador de cubos y los datos de dimensión pueden verse en la pestaña **Explorador** del Diseñador de dimensiones. La exploración de los datos de cubos y dimensiones es una forma de comprobar el trabajo incrementalmente. Puede comprobar que los pequeños cambios en las propiedades, las relaciones y otros objetos tienen el efecto deseado una vez que se procesa el objeto. Si bien la pestaña Explorador se usa para ver datos de cubos y dimensiones, también ofrece diversas funciones dependiendo del objeto que se está examinando.  
  
Para las dimensiones, la pestaña Explorador proporciona una manera de ver los miembros o de navegar por una jerarquía hasta el nodo hoja. Puede examinar datos de dimensiones en distintos idiomas, suponiendo que se hayan agregado las traducciones al modelo.  
  
Para los cubos, la pestaña Explorador proporciona dos métodos para explorar datos. Puede usar el Diseñador de consultas de MDX integrado para crear consultas que devuelven un conjunto de filas plano de una base de datos multidimensional. O bien, puede usar un método abreviado de Excel. Cuando se inicia Excel desde [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], Excel se abre con una tabla dinámica en la hoja de cálculo y una conexión predefinida a la base de datos del área de trabajo del modelo.  
  
Excel suele ofrecer una mejor experiencia de exploración porque puede explorar datos de cubos de forma interactiva, usando los ejes horizontal y vertical para analizar las relaciones de los datos. En cambio, el Diseñador de consultas de MDX está limitado a un único eje. Además, puesto que el conjunto de filas es plano, no se obtiene la obtención de detalles que ofrece una tabla dinámica de Excel. A medida que agregue más dimensiones y jerarquías al cubo, lo que hará en lecciones posteriores, Excel será la solución preferida para explorar datos.  
  
### <a name="to-browse-the-deployed-cube"></a>Para examinar el cubo implementado  
  
1.  Cambie al **Diseñador de dimensiones** para la dimensión Product en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Para ello, haga doble clic en la dimensión **Product** del nodo **Dimensiones** del Explorador de soluciones.  
  
2.  Haga clic en la pestaña **Explorador** para mostrar el miembro **All** de la jerarquía de atributo **Product Key** . En la lección tres, definirá una jerarquía de usuario para la dimensión Product que le permitirá examinar la dimensión.  
  
3.  Cambie a **Diseñador de cubos** en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Para ello, haga doble clic en el cubo **Tutorial de Analysis Services** en el nodo **Cubos** del Explorador de soluciones.  
  
4.  Seleccione la pestaña **Explorador** y haga clic en el icono **Volver a conectar** en la barra de herramientas del diseñador.  
  
    En el panel izquierdo del diseñador se muestran los objetos del cubo Tutorial de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . En el lado derecho de la pestaña **Explorador** hay dos paneles: el superior es el panel **Filtro** y el inferior es el panel **Datos** . En una próxima lección, utilizará el explorador de cubo para realizar el análisis.  
  
## <a name="next-lesson"></a>Lección siguiente  
[Lección 3: Modificar medidas, atributos y jerarquías](../analysis-services/lesson-3-modifying-measures-attributes-and-hierarchies.md)  
  
## <a name="see-also"></a>Vea también  
[Editor de consultas MDX &#40;Analysis Services: datos multidimensionales&#41;](http://msdn.microsoft.com/library/777f2c23-1c1c-4b72-9d19-48a4866551f8)  
  
  
  
