---
title: Modificar los nombres de tabla predeterminados | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ddd97483-a76d-43c1-8b40-fc7cc57fb0c2
caps.latest.revision: 22
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.openlocfilehash: 87328bab0552074462ec039cbcb9c8184639f350
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36112116"
---
# <a name="modifying-default-table-names"></a>Modificar los nombres de tabla predeterminados
  Puede cambiar el valor de la propiedad **FriendlyName** para los objetos de la vista del origen de datos para que sean más fáciles de identificar y usar.  
  
 En la tarea siguiente, cambiará el nombre descriptivo de cada tabla de la vista del origen de datos quitando los prefijos "**Dim**" y "**Fact**" de dichas tablas. Esto hará que los objetos del cubo y la dimensión (que definirá en la siguiente lección) sean más fáciles de identificar y usar.  
  
> [!NOTE]  
>  También puede cambiar los nombres descriptivos de las columnas, definir columnas calculadas y combinar tablas o vistas en la vista del origen de datos para que sean más fáciles de usar.  
  
### <a name="to-modify-the-default-name-of-a-table"></a>Para modificar el nombre predeterminado de una tabla  
  
1.  En el panel **Tablas** del **Diseñador de vistas del origen de datos**, haga clic con el botón derecho en la tabla **FactInternetSales** y, después, haga clic en **Propiedades**.  
  
2.  Si la ventana Propiedades situada en la parte derecha de la ventana de Microsoft Visual Studio no se muestra, haga clic en el botón **Ocultar automáticamente** de la barra de título de la ventana Propiedades para que esta ventana permanezca visible.  
  
     Es más fácil cambiar las propiedades de cada tabla en la vista del origen de datos cuando la ventana Propiedades permanece abierta. Si no fija la ventana abierta mediante el botón **Ocultar automáticamente** , la ventana se cerrará al hacer clic en un objeto distinto del panel **Diagrama** .  
  
3.  Cambiar el **FriendlyName** propiedad para la **FactInternetSales** el objeto a *`InternetSales`*.  
  
     Al hacer clic fuera de la celda de la propiedad **FriendlyName** , se aplica el cambio. En la siguiente lección, definirá un grupo de medida que se basa en esta tabla de hechos. El nombre de la tabla de hechos será InternetSales en lugar de FactInternetSales debido al cambio realizado en esta lección.  
  
4.  Haga clic en **DimProduct** en el panel **Tablas** . En la ventana Propiedades, cambie la **FriendlyName** propiedad *`Product`*.  
  
5.  Cambie la propiedad **FriendlyName** de cada una de las tablas restantes en la vista del origen de datos del mismo modo, para eliminar el prefijo "**Dim**".  
  
6.  Cuando haya finalizado, haga clic en el botón **Ocultar automáticamente** para ocultar de nuevo la ventana Propiedades.  
  
7.  En el menú **Archivo** , o en la barra de herramientas de [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], haga clic en **Guardar todo** para guardar los cambios que ha realizado hasta este momento en el proyecto Tutorial de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Si lo desea, puede detener aquí el tutorial y reanudarlo más tarde.  
  
## <a name="next-lesson"></a>Lección siguiente  
 [Lección 2: Definir e implementar un cubo](lesson-2-defining-and-deploying-a-cube.md)  
  
## <a name="see-also"></a>Vea también  
 [Vistas del origen de datos en modelos multidimensionales](multidimensional-models/data-source-views-in-multidimensional-models.md)   
 [Cambiar las propiedades de una vista del origen de datos &#40;Analysis Services&#41;](multidimensional-models/change-properties-in-a-data-source-view-analysis-services.md)  
  
  