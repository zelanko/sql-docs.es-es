---
title: Examinar el cubo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 3819946e-d3fa-4c1d-afe3-599c938b1b2e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 910bb7a425e62221dce932392e1aedfaa401a992
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66078983"
---
# <a name="browsing-the-cube"></a>Examinar el cubo
  Una vez implementado un cubo, los datos de este pueden verse en la pestaña **Explorador** del Diseñador de cubos y los datos de dimensión pueden verse en la pestaña **Explorador** del Diseñador de dimensiones. La exploración de los datos de cubos y dimensiones es una forma de comprobar el trabajo incrementalmente. Puede comprobar que los pequeños cambios en las propiedades, las relaciones y otros objetos tienen el efecto deseado una vez que se procesa el objeto. Si bien la pestaña Explorador se usa para ver datos de cubos y dimensiones, también ofrece diversas funciones dependiendo del objeto que se está examinando.  
  
 Para las dimensiones, la pestaña Explorador proporciona una manera de ver los miembros o de navegar por una jerarquía hasta el nodo hoja. Puede examinar datos de dimensiones en distintos idiomas, suponiendo que se hayan agregado las traducciones al modelo.  
  
 Para los cubos, la pestaña Explorador proporciona dos métodos para explorar datos. Puede usar el Diseñador de consultas de MDX integrado para crear consultas que devuelven un conjunto de filas plano de una base de datos multidimensional. O bien, puede usar un método abreviado de Excel. Cuando se inicia Excel desde [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], Excel se abre con una tabla dinámica en la hoja de cálculo y una conexión predefinida a la base de datos del área de trabajo del modelo.  
  
 Excel suele ofrecer una mejor experiencia de exploración porque puede explorar datos de cubos de forma interactiva, usando los ejes horizontal y vertical para analizar las relaciones de los datos. En cambio, el Diseñador de consultas de MDX está limitado a un único eje. Además, puesto que el conjunto de filas es plano, no se obtiene la obtención de detalles que ofrece una tabla dinámica de Excel. A medida que agregue más dimensiones y jerarquías al cubo, lo que hará en lecciones posteriores, Excel será la solución preferida para explorar datos.  
  
### <a name="to-browse-the-deployed-cube"></a>Para examinar el cubo implementado  
  
1.  Cambie al **Diseñador de dimensiones** para la dimensión Product en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Para ello, haga doble clic en la dimensión **Product** del nodo **Dimensiones** del Explorador de soluciones.  
  
2.  Haga clic en el **explorador** ficha para mostrar el **todas** miembro de la `Product Key` jerarquía de atributo. En la lección tres, definirá una jerarquía de usuario para la dimensión Product que le permitirá examinar la dimensión.  
  
3.  Cambie a **Diseñador de cubos** en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Para ello, haga doble clic en el cubo **Tutorial de Analysis Services** en el nodo **Cubos** del Explorador de soluciones.  
  
4.  Seleccione la pestaña **Explorador** y haga clic en el icono **Volver a conectar** en la barra de herramientas del diseñador.  
  
     En el panel izquierdo del diseñador se muestran los objetos del cubo Tutorial de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . En el lado derecho de la pestaña **Explorador** hay dos paneles: el superior es el panel **Filtro** y el inferior es el panel **Datos** . En una próxima lección, utilizará el explorador de cubo para realizar el análisis.  
  
## <a name="next-lesson"></a>Lección siguiente  
 [Lección 3: Modificar medidas, atributos y jerarquías](lesson-3-modifying-measures-attributes-and-hierarchies.md)  
  
## <a name="see-also"></a>Vea también  
 [Editor de consultas MDX &#40;Analysis Services: datos multidimensionales&#41;](mdx-query-editor-analysis-services-multidimensional-data.md)  
  
  
