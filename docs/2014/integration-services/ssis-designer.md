---
title: Diseñador SSIS | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Integration Services, SSIS Designer
- Business Intelligence Development Studio, Integration Services in
- tools [Integration Services], SSIS Designer
- SSIS, SSIS Designer
- SSIS Designer, about SSIS Designer
- Integration Services, SSIS Designer
ms.assetid: 006d68ea-1b5c-4c1e-8079-3910288e012c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ea0776247555b9a5b63e2bbaa9ae9243abf6863c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62766438"
---
# <a name="ssis-designer"></a>Diseñador SSIS
  
  [!INCLUDE[ssIS](../includes/ssis-md.md)] es una herramienta gráfica que se puede usar para crear y mantener paquetes [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . 
  [!INCLUDE[ssIS](../includes/ssis-md.md)] está disponible en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] como parte de un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
 Puede usar el Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] para realizar las tareas siguientes:  
  
-   Generar el flujo de control en un paquete.  
  
-   Generar los flujos de datos en un paquete.  
  
-   Agregar controladores de eventos al paquete y objetos de paquete.  
  
-   Ver el contenido del paquete.  
  
-   En el tiempo de ejecución, ver el progreso de ejecución del paquete.  
  
 El siguiente diagrama muestra el Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] y la ventana del **cuadro de herramientas** .  
  
 ![Captura del Diseñador y el cuadro de herramientas de SSIS](media/denali-designerandtoolbox.gif "Captura del Diseñador y el cuadro de herramientas de SSIS")  
  
 
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] incluye cuadros de diálogo y ventanas adicionales para agregar funcionalidad a los paquetes, y [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] proporciona ventanas y cuadros de diálogo para configurar el entorno de desarrollo y trabajar con paquetes. Para obtener más información, vea [Interfaz de usuario de Integration Services](integration-services-user-interface.md).  
  
 
  [!INCLUDE[ssIS](../includes/ssis-md.md)] no depende del servicio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , el servicio que administra y supervisa paquetes, y no se requiere que el servicio se esté ejecutando para crear o modificar paquetes en el Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] . Sin embargo, si detiene el servicio mientras se encuentra abierto el Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] , ya no puede abrir los cuadros de diálogo que proporciona el Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] y es posible que aparezca el mensaje de error "El servidor RPC no está disponible". Para restablecer el Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] y seguir trabajando con el paquete, debe cerrar el diseñador, salir de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]y, a continuación, volver a abrir [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] y el paquete.  
  
## <a name="undo-and-redo"></a>Deshacer y rehacer  
 Puede deshacer y rehacer hasta 20 acciones en el Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] . Para un paquete, la acción de deshacer o rehacer está disponible en las pestañas **Flujo de control**, **Flujo de datos**, **Controladores de eventos** y **Parámetros**, y en la ventana **Variables**. Para un proyecto, la acción de deshacer o rehacer está disponible en la ventana **Parámetros del proyecto** .  
  
 No se pueden deshacer ni rehacer los cambios en el nuevo **Cuadro de herramientas de SSIS**.  
  
 Cuando se realizan cambios en un componente mediante el editor de componentes, los cambios se deshacen y rehacen en conjunto, en lugar de deshacer y rehacer cambios individuales. El conjunto de cambios aparece como una sola acción en la lista desplegable de deshacer y rehacer.  
  
 Para deshacer una acción, haga clic en el botón Deshacer de la barra de herramientas, en el elemento de menú **Editar/Deshacer** o pulse CTRL+Z. Para rehacer una acción, haga clic en el botón Rehacer de la barra de herramientas, en el elemento de menú **Editar/Rehacer** o pulse CTRL+Y. Para deshacer o rehacer varias acciones, haga clic en la flecha situada junto al botón de la barra de herramientas, resalte varias acciones en la lista desplegable y, después, haga clic en la lista.  
  
## <a name="parts-of-the-ssis-designer"></a>Partes del Diseñador SSIS  
 
  [!INCLUDE[ssIS](../includes/ssis-md.md)] tiene cinco pestañas permanentes: una pestaña para cada una de las funciones de generación de flujo de control, flujos de datos, parámetros y controladores de eventos de un paquete, y una pestaña para ver el contenido de un paquete. En el tiempo de ejecución aparece una sexta pestaña que muestra el progreso de la ejecución de un paquete mientras se ejecuta y los resultados de la ejecución una vez finalizada.  
  
 Además, el Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] incluye un área de Administradores de conexión para agregar y configurar los administradores de conexión que usa un paquete para conectarse a los datos.  
  
### <a name="control-flow-tab"></a>Pestaña Flujo de control  
 Construya el flujo de control en un paquete en la superficie de diseño de la pestaña **flujo de control** . arrastre elementos desde el **cuadro de herramientas** a la superficie de diseño y conéctelos a un flujo de control haciendo clic en el icono del elemento y arrastrando la flecha desde un elemento a otro.  
  
 Para más información, consulte [Control Flow](control-flow/control-flow.md).  
  
### <a name="data-flow-tab"></a>Pestaña Flujo de datos  
 Si un paquete contiene una tarea de flujo de datos, puede agregar flujos de datos al paquete. Los flujos de datos de un paquete se construyen en la superficie de diseño de la pestaña **flujo de datos** . arrastre elementos desde el **cuadro de herramientas** a la superficie de diseño y conéctelos a un flujo de datos haciendo clic en el icono del elemento y arrastrando la flecha desde un elemento a otro.  
  
 Para más información, consulte [Data Flow](data-flow/data-flow.md).  
  
### <a name="parameters-tab"></a>Pestaña Parámetros  
 Los parámetros de Integration Services (SSIS) permiten asignar valores a las propiedades de los paquetes en el momento de la ejecución de los mismos. Puede crear parámetros de proyecto en el nivel de proyecto y parámetros de paquete en el nivel de paquete. Los parámetros de proyecto se usan para proporcionar cualquier entrada externa que el proyecto recibe a uno o más paquetes del proyecto. Los parámetros de paquete permiten modificar la ejecución del paquete sin tener que modificarlo ni volver a implementarlo. Esta pestaña permite administrar parámetros del paquete.  
  
 Para más información sobre los parámetros, vea [Parámetros de Integration Services &#40;SSIS&#41;](integration-services-ssis-package-and-project-parameters.md).  
  
> [!IMPORTANT]  
>  Los parámetros solo están disponibles en los proyectos desarrollados para el modelo de implementación del proyecto. Por consiguiente, verá la pestaña Parámetros solo en los paquetes que formen parte de un proyecto configurado para utilizar el modelo de implementación del proyecto.  
  
### <a name="event-handlers-tab"></a>Pestaña Controladores de eventos  
 Los eventos de un paquete se construyen en la superficie de diseño de la pestaña **controladores de eventos** . En la pestaña **controladores de eventos** , seleccione el paquete o el objeto de paquete para el que desea crear un controlador de eventos y, a continuación, seleccione el evento que se va a asociar al controlador de eventos. Un controlador de eventos tiene un flujo de control y flujos de datos opcionales.  
  
 Para obtener más información, consulte [Add an Event Handler to a Package](../../2014/integration-services/add-an-event-handler-to-a-package.md).  
  
### <a name="package-explorer-tab"></a>Pestaña Explorador de paquetes  
 Los paquetes pueden ser complejos e incluir muchas tareas, administradores de conexión, variables y otros elementos. La vista de explorador del paquete le permite ver una lista completa de elementos de paquete.  
  
 Para obtener más información, consulte [Ver objetos de paquete](view-package-objects.md).  
  
#### <a name="progressexecution-result-tab"></a>Pestaña Progreso/Resultados de la ejecución  
 Mientras se ejecuta un paquete, la pestaña **Progreso** muestra el progreso de la ejecución del paquete. Una vez que el paquete ha terminado de ejecutarse, los resultados de la ejecución permanecen disponibles en la pestaña **Resultados de la ejecución** .  
  
> [!NOTE]  
>  Para habilitar o deshabilitar la presentación de mensajes en la pestaña **Progreso** , active o desactive la opción **Informe de progreso de depuración** del menú **SSIS** .  
  
##### <a name="connection-managers-area"></a>Área de administradores de conexión  
 Los administradores de conexión utilizados por un paquete se agregan y modifican en el área **Administradores de conexión** . 
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] incluye administradores de conexión para conectarse a una serie de orígenes de datos, como archivos de texto, bases de datos OLE DB y proveedores .NET.  
  
 Para más información, vea [Conexiones de Integration Services &#40;SSIS&#41;](connection-manager/integration-services-ssis-connections.md) y [Crear administradores de conexiones](../../2014/integration-services/create-connection-managers.md).  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [Crear paquetes en herramientas de datos de SQL Server](create-packages-in-sql-server-data-tools.md)  
  
## <a name="see-also"></a>Consulte también  
 [Interfaz de usuario de Integration Services](integration-services-user-interface.md)  
  
  
