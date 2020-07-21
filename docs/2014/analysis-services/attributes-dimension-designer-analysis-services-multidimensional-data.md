---
title: Atributos (pestaña estructura de dimensión, diseñador de dimensiones) (Analysis Services-datos multidimensionales) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql.asvs.dimensiondesigner.dbv.attributespane.f1
ms.assetid: 627eaa08-7638-4edd-bdfa-0d8175a7cde5
author: minewiskan
ms.author: owend
ms.openlocfilehash: 6c5e1d6b92dce1a1be42ae1bc30ae3a3d5e48d59
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/08/2020
ms.locfileid: "84527861"
---
# <a name="attributes-dimension-structure-tab-dimension-designer-analysis-services---multidimensional-data"></a>Atributos (pestaña Estructura de dimensión, Diseñador de dimensiones) (Analysis Services - Datos multidimensionales)
  Use este panel para administrar los atributos asociados con la dimensión seleccionada. Los atributos se pueden arrastrar desde este panel hasta el panel **Jerarquías** para crear jerarquías y niveles. Para obtener más información, vea [Hierarchies &#40;Dimension Structure Tab, Dimension Designer&#41; &#40;Analysis Services - Multidimensional Data&#41;](hierarchies-dimension-designer-analysis-services-multidimensional-data.md).  
  
 Para crear un atributo, arrastre una columna desde el panel **Vista del origen de datos** hasta el panel **Atributos** mientras está en el modo de lista, árbol o vista. Para quitar un atributo, seleccione **Eliminar** en el menú contextual.  
  
 **Para mostrar el panel Atributos**  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] y, a continuación, abra la dimensión que desea.  
  
2.  Si no está seleccionada, haga clic en la pestaña **Estructura de dimensión** .  
  
## <a name="options"></a>Opciones  
 **Atributos**  
 Muestra los atributos disponibles para la dimensión seleccionada. Esta opción se puede ver en los siguientes modos:  
  
-   Modo de lista  
  
     Use este modo para crear y modificar jerarquías. Para ver los atributos en modo de lista, seleccione **Mostrar atributos en** en el menú contextual y, a continuación, haga clic en **Lista**.  
  
-   Modo de árbol  
  
     Use este modo para crear y modificar jerarquías. Para ver los atributos en modo de árbol, seleccione **Mostrar atributos en** en el menú contextual y, a continuación, haga clic en **Árbol**.  
  
-   Modo de cuadrícula  
  
     Use este modo para crear dimensiones manualmente o para modificar propiedades de atributo. Para ver los atributos en modo de cuadrícula, seleccione **Mostrar atributos en** en el menú contextual y, a continuación, haga clic en **Cuadrícula**.  
  
## <a name="grid-mode-options"></a>Opciones del modo de cuadrícula  
 Cuando se visualizan los atributos en modo de cuadrícula, se tiene acceso a las columnas enumeradas en la tabla siguiente.  
  
 **Nombre**  
 Muestra el nombre del atributo.  
  
 **Uso**  
 Establece el uso del atributo seleccionado. Haga clic en la flecha abajo para seleccionar entre las siguientes opciones:  
  
|Value|Descripción|  
|-----------|-----------------|  
|Normal|Identifica un atributo normal.|  
|Clave|Identifica el atributo clave de la dimensión. Esto corresponde a los miembros hoja de la dimensión. Solo puede haber un atributo clave por dimensión. Para modificarlo, haga clic en el botón de puntos suspensivos (**…**) que aparece junto a la propiedad **KeyColumns** en el panel **Propiedades** .|  
|Parent|Indica el atributo primario para una relación de elementos primarios y secundarios. El atributo secundario de esta relación siempre debe ser el atributo clave.|  
|AccountType|Indica un atributo de tipo de cuenta. Lo usa el servidor o el motor cuando la función de agregación para una medida está establecida en “por cuenta”.|  
  
 **Tipo**  
 Establece el tipo de atributo. Haga clic en la flecha abajo para seleccionar entre las opciones disponibles.  
  
 **Columna de clave**  
 Muestra el tipo de datos de las columnas subyacentes. Al crear un atributo nuevo, haga clic en la flecha abajo para seleccionar entre las opciones disponibles.  
  
 **Columna Nombre**  
 Muestra la ubicación de la columna subyacente. Al crear un atributo nuevo, haga clic en la flecha abajo para seleccionar entre **Igual que la clave** y **Columna separada**. Si selecciona **Columna separada** , la propiedad **NameColumn** del panel **Propiedades** establece la columna en la que se almacena el nombre que debe utilizarse para el atributo.  
  
## <a name="see-also"></a>Consulte también  
 [Estructura de dimensión &#40;diseñador de dimensiones&#41; &#40;Analysis Services de datos multidimensionales&#41;](dimension-structure-dimension-designer-analysis-services-multidimensional-data.md)   
 [Jerarquías &#40;pestaña estructura de dimensión, diseñador de dimensiones&#41; &#40;Analysis Services-datos multidimensionales&#41;](hierarchies-dimension-designer-analysis-services-multidimensional-data.md)   
 [Barra de herramientas &#40;pestaña estructura de dimensión, diseñador de dimensiones&#41; &#40;Analysis Services-datos multidimensionales&#41;](toolbar-dimension-structure-designer-analysis-services-multidimensional-data.md)  
  
  
