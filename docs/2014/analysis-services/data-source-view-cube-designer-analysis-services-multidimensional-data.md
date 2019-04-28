---
title: (Pestaña estructura de cubo, Diseñador de cubos) de la vista del origen de datos (Analysis Services - datos multidimensionales) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.cubebuilder.datasourcepane.f1
ms.assetid: 1e39c910-5c10-4624-be27-ca02a461b46b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fd3d21c2371878c44accc4d7e9f501f47ce64646
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62732676"
---
# <a name="data-source-view-cube-structure-tab-cube-designer-analysis-services---multidimensional-data"></a>Vista del origen de datos (pestaña Estructura de cubo, Diseñador de cubos) (Analysis Services - Datos multidimensionales)
  Utilice el panel **Vista del origen de datos** para ver tablas y columnas de la vista del origen de datos asociada al cubo seleccionado. Este panel se utiliza para crear grupos de medida y medidas arrastrando columnas desde el panel **Vista del origen de datos** hasta el panel **Medidas** .  
  
## <a name="options"></a>Opciones  
 **Vista del origen de datos**  
 Muestra la vista del origen de datos asociada al cubo seleccionado.  
  
 **(Mover punto de vista)**  
 Haga clic en la esquina inferior derecha del panel, entre las barras de desplazamiento, para seleccionar el área del panel **Vista del origen de datos** que quiere ver.  
  
## <a name="diagram-context-menu"></a>Menú contextual del diagrama  
 Las opciones siguientes están disponibles en el menú contextual que se muestra al hacer clic con el botón derecho en el fondo del diagrama del panel **Vista del origen de datos** :  
  
 **Mostrar tablas**  
 Muestra el cuadro de diálogo **Mostrar tabla**. Para más información sobre el cuadro de diálogo **Mostrar tabla**, vea [Cuadro de diálogo Mostrar tabla &#40;Analysis Services - Datos multidimensionales&#41;](show-table-dialog-box-analysis-services-multidimensional-data.md).  
  
 **Mostrar todas las tablas**  
 Muestra en el panel todas las tablas incluidas en la vista del origen de datos asociada al cubo.  
  
 **Mostrar solo tablas usadas**  
 Solo muestra en el panel las tablas que utiliza el cubo desde la vista del origen de datos asociada.  
  
 **Mostrar nombres descriptivos**  
 Seleccione esta opción para mostrar los nombres descriptivos de los objetos del panel.  
  
 **Seleccionar todo**  
 Selecciona todos los objetos del panel.  
  
 **Buscar tabla**  
 Muestra el cuadro de diálogo **Buscar tabla**. Para más información sobre el cuadro de diálogo **Buscar tabla**, vea [Cuadro de diálogo Buscar tabla &#40;Analysis Services - Datos multidimensionales&#41;](find-table-dialog-box-analysis-services-multidimensional-data.md).  
  
 **Organizar tablas**  
 Para organizar los objetos del panel conforme al diseño especificado, seleccione **Cambiar a diseño diagonal** o **Cambiar a diseño rectangular**.  
  
 **Cambiar a diseño Diagonal**  
 Seleccione esta opción para organizar los objetos en un patrón diagonal.  
  
> [!NOTE]  
>  Esta opción solo se muestra si selecciona **Cambiar a diseño rectangular** .  
  
 **Cambiar a diseño Rectangular**  
 Seleccione esta opción para organizar los objetos en un patrón rectangular.  
  
> [!NOTE]  
>  Esta opción solo se muestra si selecciona **Cambiar a diseño diagonal** .  
  
 **Editar vista del origen de datos**  
 Muestra el Diseñador de vistas del origen de datos correspondiente a la vista del origen de datos asociada al objeto. Para más información sobre el Diseñador de vistas del origen de datos, vea [Diseñador de vistas del origen de datos &#40;Analysis Services - Datos multidimensionales&#41;](data-source-view-designer-analysis-services-multidimensional-data.md).  
  
 **Mostrar vista del origen de datos en**  
 Seleccione una de las siguientes opciones para cambiar la vista del panel **Vista del origen de datos** a uno de los modos siguientes:  
  
-   Diagrama  
  
     Muestra un diagrama de las tablas y columnas asociadas al cubo actual.  
  
-   trEE  
  
     Muestra una vista de árbol que contiene las tablas y columnas asociadas al cubo actual.  
  
 **Copiar diagrama desde**  
 Seleccione uno de los diagramas incluidos en la vista del origen de datos asociada al cubo para mostrarlo en el panel **Vista del origen de datos** .  
  
 **Zoom**  
 Seleccione una opción de zoom disponible.  
  
 **Propiedades**  
 Muestra la ventana **Propiedades** de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] de la vista del origen de datos asociada al cubo.  
  
## <a name="table-context-menu"></a>Menú contextual de la tabla  
 Las opciones siguientes están disponibles en el menú contextual que se muestra al hacer clic con el botón derecho en el nombre de una tabla o vista del panel **Vista del origen de datos** :  
  
 **Mostrar tablas relacionadas**  
 Muestra en el panel las tablas relacionadas con la tabla seleccionada en la vista del origen de datos.  
  
 **Ocultar tabla**  
 Quita la tabla del panel.  
  
 **Explorar datos**  
 Muestra el cuadro de diálogo **Explorar datos** de la tabla seleccionada.  
  
 **Editar vista del origen de datos**  
 Muestra el Diseñador de vistas del origen de datos correspondiente a la vista del origen de datos que contiene la tabla seleccionada. Para más información sobre el Diseñador de vistas del origen de datos, vea [Diseñador de vistas del origen de datos &#40;Analysis Services - Datos multidimensionales&#41;](data-source-view-designer-analysis-services-multidimensional-data.md).  
  
 **Nuevo grupo de medida de la tabla**  
 Define un nuevo grupo de medida en el panel **Medidas** basado en la tabla seleccionada.  
  
> [!NOTE]  
>  Esta opción solo se habilita si aún no se ha hecho referencia a la tabla desde un grupo de medida en el panel **Medidas** .  
  
 **Propiedades**  
 Muestra la ventana **Propiedades** de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] de la tabla seleccionada.  
  
## <a name="column-context-menu"></a>Menú contextual de columna  
 Las opciones siguientes están disponibles en el menú contextual que se muestra al hacer clic con el botón derecho en el nombre de una columna de una tabla o vista del panel **Vista del origen de datos** :  
  
 **Nueva medida de la columna**  
 Define una nueva medida en el panel **Medidas** basado en la columna seleccionada.  
  
 **Explorar datos**  
 Muestra el cuadro de diálogo **Explorar datos** para la tabla que contiene la columna seleccionada.  
  
 **Editar vista del origen de datos**  
 Muestra el Diseñador de vistas del origen de datos correspondiente a la vista del origen de datos que contiene la columna seleccionada. Para más información sobre el Diseñador de vistas del origen de datos, vea [Diseñador de vistas del origen de datos &#40;Analysis Services - Datos multidimensionales&#41;](data-source-view-designer-analysis-services-multidimensional-data.md).  
  
 **Propiedades**  
 Muestra la ventana **Propiedades** de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] de la columna seleccionada.  
  
## <a name="relationship-context-menu"></a>Menú contextual de relación  
 Las opciones siguientes están disponibles en el menú contextual que se muestra al hacer clic con el botón derecho en una relación del panel **Vista del origen de datos** :  
  
 **Editar vista del origen de datos**  
 Muestra el Diseñador de vistas del origen de datos correspondiente a la vista del origen de datos que contiene la relación seleccionada. Para más información sobre el Diseñador de vistas del origen de datos, vea [Diseñador de vistas del origen de datos &#40;Analysis Services - Datos multidimensionales&#41;](data-source-view-designer-analysis-services-multidimensional-data.md).  
  
 **Propiedades**  
 Muestra la ventana **Propiedades** en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para la relación seleccionada.  
  
## <a name="see-also"></a>Vea también  
 [Barra de herramientas &#40;pestaña estructura de cubo, Diseñador de cubos&#41; &#40;Analysis Services - datos multidimensionales&#41;](toolbar-cube-structure-cube-designer-analysis-services-multidimensional-data.md)   
 [Las medidas &#40;pestaña estructura de cubo, Diseñador de cubos&#41; &#40;Analysis Services - datos multidimensionales&#41;](measures-cube-structure-cube-designer-analysis-services-multidimensional-data.md)   
 [Dimensiones &#40;pestaña estructura de cubo, Diseñador de cubos&#41; &#40;Analysis Services - datos multidimensionales&#41;](dimensions-cube-structure-cube-designer-analysis-services-multidimensional-data.md)   
 [Estructura de cubo &#40;Diseñador de cubos&#41; &#40;Analysis Services - datos multidimensionales&#41;](cube-structure-cube-designer-analysis-services-multidimensional-data.md)  
  
  
