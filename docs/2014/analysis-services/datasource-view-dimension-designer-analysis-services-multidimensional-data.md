---
title: (Pestaña estructura de dimensión, Diseñador de dimensiones) de la vista del origen de datos (Analysis Services - datos multidimensionales) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql.asvs.dimensiondesigner.dbv.datasourcepane.f1
ms.assetid: c4bd3c5e-8986-448f-b9db-3551f50f0696
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 989b84d027db5dc1f5956aab6e2e4fec84ae6461
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48112225"
---
# <a name="data-source-view-dimension-structure-tab-dimension-designer-analysis-services---multidimensional-data"></a>Vista del origen de datos (pestaña Estructura de dimensión, Diseñador de dimensiones) (Analysis Services - Datos multidimensionales)
  Use el panel **Vista del origen de datos** para ver las tablas y columnas desde la vista del origen de datos asociada a la dimensión seleccionada. Este panel se utiliza para crear atributos, propiedades de miembros, jerarquías y niveles al arrastrar las columnas del panel **Vista del origen de datos** al panel **Atributos** o **Jerarquías y niveles** .  
  
## <a name="options"></a>Opciones  
 **Vista del origen de datos**  
 Muestra la vista del origen de datos asociada a la dimensión seleccionada.  
  
 **(Mover punto de vista)**  
 Haga clic en la esquina inferior derecha del panel, entre las barras de desplazamiento, para seleccionar el área del panel **Vista del origen de datos** que quiere ver.  
  
## <a name="diagram-context-menu"></a>Menú contextual del diagrama  
 Las opciones mostradas en la siguiente tabla se encuentran disponibles en el menú contextual si hace clic con el botón derecho en el fondo del diagrama en el panel **Vista del origen de datos** .  
  
 **Mostrar tablas**  
 Muestra el cuadro de diálogo **Mostrar tabla**. Para más información sobre el cuadro de diálogo **Mostrar tabla**, vea [Cuadro de diálogo Mostrar tabla &#40;Analysis Services - Datos multidimensionales&#41;](show-table-dialog-box-analysis-services-multidimensional-data.md).  
  
 **Mostrar todas las tablas**  
 Muestra en el panel todas las tablas, incluida la vista del origen de datos asociada a la dimensión.  
  
 **Mostrar solo tablas usadas**  
 Muestra en el panel solamente aquellas tablas usadas por la dimensión desde la vista del origen de datos asociada.  
  
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
 Muestra el **Diseñador de vistas del origen de datos** para la vista del origen de datos asociada a la dimensión. Para más información sobre el **Diseñador de vistas del origen de datos**, vea [Diseñador de vistas del origen de datos &#40;Analysis Services - Datos multidimensionales&#41;](data-source-view-designer-analysis-services-multidimensional-data.md).  
  
 **Mostrar vista del origen de datos en**  
 Seleccione una de las siguientes opciones para cambiar la vista del panel **Vista del origen de datos** a uno de los modos siguientes:  
  
-   Diagrama  
  
     Muestra un diagrama de las tablas y columnas asociadas a la dimensión actual.  
  
-   trEE  
  
     Muestra una vista de árbol que contiene las tablas y columnas asociadas a la dimensión actual.  
  
 **Copiar diagrama desde**  
 Seleccione uno de los diagramas incluidos en la vista del origen de datos asociada a la dimensión para mostrarlo en el panel **Vista del origen de datos** .  
  
 **Zoom**  
 Seleccione una opción de zoom disponible.  
  
 **Propiedades**  
 Muestra la ventana **Propiedades** en **Herramientas de datos de SQL Server** para la vista del origen asociada a la dimensión.  
  
## <a name="table-context-menu"></a>Menú contextual de la tabla  
 Las opciones mostradas en la siguiente tabla se encuentran disponibles en el menú contextual si hace clic con el botón derecho en el nombre de una tabla o vista en el panel **Vista del origen de datos** .  
  
 **Mostrar tablas relacionadas**  
 Muestra en el panel las tablas relacionadas con la tabla seleccionada en la vista del origen de datos.  
  
 **Ocultar tabla**  
 Quita la tabla del panel.  
  
 **Explorar datos**  
 Muestra el cuadro de diálogo **Explorar datos** para la tabla seleccionada.  
  
 **Editar vista del origen de datos**  
 Muestra el **Diseñador de vistas del origen de datos** para la vista del origen de datos que contiene la tabla seleccionada. Para más información sobre el **Diseñador de vistas del origen de datos**, vea [Diseñador de vistas del origen de datos &#40;Analysis Services - Datos multidimensionales&#41;](data-source-view-designer-analysis-services-multidimensional-data.md).  
  
 **Propiedades**  
 Muestra la ventana **Propiedades** en **Herramientas de datos de SQL Server** para la tabla seleccionada.  
  
## <a name="column-context-menu"></a>Menú contextual de columna  
 Las opciones mostradas en la siguiente tabla se encuentran disponibles en el menú contextual si hace clic con el botón derecho en el nombre de una columna de una tabla o vista en el panel **Vista del origen de datos** .  
  
 **Nuevo atributo de columna**  
 Muestra en el panel las tablas relacionadas con la tabla seleccionada en la vista del origen de datos.  
  
 **Explorar datos**  
 Muestra el cuadro de diálogo **Explorar datos** para la tabla que contiene la columna seleccionada.  
  
 **Editar vista del origen de datos**  
 Muestra el **Diseñador de vistas del origen de datos** correspondiente a la vista del origen de datos que contiene la tabla seleccionada. Para más información sobre el **Diseñador de vistas del origen de datos**, vea [Diseñador de vistas del origen de datos &#40;Analysis Services - Datos multidimensionales&#41;](data-source-view-designer-analysis-services-multidimensional-data.md).  
  
 **Propiedades**  
 Muestra la ventana **Propiedades** en **Herramientas de datos de SQL Server** para la columna seleccionada.  
  
## <a name="relationship-context-menu"></a>Menú contextual de relación  
 Las opciones mostradas en la siguiente tabla se encuentran disponibles en el menú contextual si hace clic con el botón derecho en una relación del panel **Vista del origen de datos** .  
  
 **Editar vista del origen de datos**  
 Muestra el **Diseñador de vistas del origen de datos** correspondiente a la vista del origen de datos que contiene la relación seleccionada. Para más información sobre el **Diseñador de vistas del origen de datos**, vea [Diseñador de vistas del origen de datos &#40;Analysis Services - Datos multidimensionales&#41;](data-source-view-designer-analysis-services-multidimensional-data.md).  
  
 **Propiedades**  
 Muestra la ventana **Propiedades** en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para la relación seleccionada.  
  
## <a name="see-also"></a>Vea también  
 [Estructura de dimensión &#40;Diseñador de dimensiones&#41; &#40;Analysis Services - datos multidimensionales&#41;](dimension-structure-dimension-designer-analysis-services-multidimensional-data.md)   
 [Barra de herramientas &#40;pestaña estructura de dimensión, Diseñador de dimensiones&#41; &#40;Analysis Services - datos multidimensionales&#41;](toolbar-dimension-structure-designer-analysis-services-multidimensional-data.md)   
 [Atributos &#40;pestaña estructura de dimensión, Diseñador de dimensiones&#41; &#40;Analysis Services - datos multidimensionales&#41;](attributes-dimension-designer-analysis-services-multidimensional-data.md)   
 [Jerarquías &#40;pestaña estructura de dimensión, Diseñador de dimensiones&#41; &#40;Analysis Services - datos multidimensionales&#41;](hierarchies-dimension-designer-analysis-services-multidimensional-data.md)  
  
  
