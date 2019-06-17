---
title: Definir los datos de una vista del origen | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: af00938a-5a06-4fae-b2fc-f3fb0ca3cea5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 939186d48f7dd8a0cc33b24778bf8948f9938a70
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66079280"
---
# <a name="defining-a-data-source-view"></a>Definir una vista del origen de datos
  Tras definir los orígenes de datos que utilizará en un proyecto de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], el paso siguiente generalmente consiste en definir una vista del origen de datos para el proyecto. Una vista del origen de datos es una sola vista unificada de metadatos de las tablas y vistas especificadas que el origen de datos define en el proyecto. Almacenar metadatos en la vista del origen de datos permite trabajar con los metadatos durante el proceso de desarrollo sin ninguna conexión abierta con ningún origen de datos subyacente. Para más información, vea [Vistas del origen de datos en modelos multidimensionales](multidimensional-models/data-source-views-in-multidimensional-models.md).  
  
 En la tarea siguiente, definirá una vista del origen de datos que incluye cinco tablas del origen de datos **AdventureWorksDW2012** .  
  
### <a name="to-define-a-new-data-source-view"></a>Para definir una vista del origen de datos nueva  
  
1.  En el Explorador de soluciones (a la derecha de la ventana de Microsoft Visual Studio), haga clic con el botón derecho en **Vistas del origen de datos**y, después, haga clic en **Nueva vista del origen de datos**.  
  
2.  En la página **Asistente para vistas del origen de datos** , haga clic en **Siguiente**. Aparece la página **Seleccionar un origen de datos** .  
  
3.  En **Orígenes de datos relacionales**, el origen de datos **Adventure Works DW 2012** aparece seleccionado. Haga clic en **Siguiente**.  
  
    > [!NOTE]  
    >  Para crear una vista del origen de datos que se base en varios orígenes de datos, defina primero una vista del origen de datos que se base en un único origen de datos. Este origen de datos luego se llama origen de datos principal. A continuación, puede agregar tablas y vistas a partir de un origen de datos secundario. Al diseñar dimensiones que contengan atributos basados en tablas relacionadas en varios orígenes de datos, puede que necesite definir un origen de datos de [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] como el origen de datos principal para usar sus capacidades del motor de consultas distribuidas.  
  
4.  En la página **Seleccionar tablas y vistas** , seleccione las tablas y vistas de la lista de objetos disponibles del origen de datos seleccionado. Puede filtrar esta lista para ayudarle a seleccionar las tablas y vistas.  
  
    > [!NOTE]  
    >  Haga clic en el botón Maximizar situado en la esquina superior derecha para que la ventana ocupe toda la pantalla. Así es más fácil ver la lista completa de objetos disponibles.  
  
     En la lista **Objetos disponibles** , seleccione los siguientes objetos. Para seleccionar varias tablas, haga clic en cada una de ellas mientras mantiene presionada la tecla CTRL:  
  
    -   **DimCustomer (dbo)**  
  
    -   **DimDate (dbo)**  
  
    -   **DimGeography (dbo)**  
  
    -   **DimProduct (dbo)**  
  
    -   **FactInternetSales (dbo)**  
  
5.  Haga clic en **>** para agregar las tablas seleccionadas a la lista **Objetos incluidos** .  
  
6.  Haga clic en **Siguiente.**  
  
7.  En el campo Nombre, asegúrese de que aparece **Adventure Works DW 2012** y, después, haga clic en **Finalizar**.  
  
     La vista del origen de datos **Adventure Works DW 2012** aparece en la carpeta **Vistas del origen de datos** del Explorador de soluciones. El contenido de la vista del origen de datos también se muestra en el Diseñador de vistas del origen de datos de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Este diseñador contiene los elementos siguientes:  
  
    -   El panel **Diagrama** , en el que las tablas y sus relaciones se representan gráficamente.  
  
    -   El panel **Tablas** , en el que las tablas y los elementos de esquema se muestran en una vista de árbol.  
  
    -   El panel **Organizador de diagramas** , en el que puede crear subdiagramas de modo que pueda ver los subconjuntos de la vista del origen de datos.  
  
    -   Una barra de herramientas específica del Diseñador de vistas del origen de datos.  
  
8.  Para maximizar el entorno de desarrollo de [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] , haga clic en el botón **Maximizar** .  
  
9. Para ver las tablas del panel **Diagrama** al 50 por ciento, haga clic en el icono **Zoom** de la barra de herramientas del Diseñador de vistas del origen de datos. De este modo se ocultarán los detalles de columna de cada tabla.  
  
10. Para ocultar el Explorador de soluciones, haga clic en el botón **Ocultar automáticamente** , que es el icono de marcador de la barra de título. Para ver el Explorador de soluciones de nuevo, sitúe el puntero sobre la pestaña del Explorador de soluciones situada a la derecha del entorno de desarrollo. Para mostrar el Explorador de soluciones, haga clic de nuevo en el botón **Ocultar automáticamente** .  
  
11. Si las ventanas no se ocultan de manera predeterminada, haga clic en **Ocultar automáticamente** en la barra de título de las ventanas Propiedades y Explorador de soluciones.  
  
     Ahora puede ver las tablas y sus relaciones en el panel **Diagrama** . Observe que hay tres relaciones entre la tabla FactInternetSales y la tabla DimDate. Cada venta tiene tres fechas asociadas: de pedido, de vencimiento y de envío. Para ver los detalles de cualquier relación, haga doble clic en la flecha de relación del panel **Diagrama** .  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Modificar los nombres de tabla predeterminados](lesson-1-4-modifying-default-table-names.md)  
  
## <a name="see-also"></a>Vea también  
 [Vistas del origen de datos en modelos multidimensionales](multidimensional-models/data-source-views-in-multidimensional-models.md)  
  
  
