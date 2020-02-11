---
title: Usar el Explorador de Utilidad para administrar la utilidad de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 74012c90-b42e-4171-b27a-9c30cf69ff98
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 232beed45a62ad9cef9f43b122d23cb4d0728a78
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63191693"
---
# <a name="use-utility-explorer-to-manage-the-sql-server-utility"></a>Utilizar el explorador de Utilidad para administrar la utilidad de SQL Server
  El explorador de Utilidad, un componente de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], se conecta a instancias de [!INCLUDE[ssDE](../../includes/ssde-md.md)] para proporcionar una vista de árbol de todos los objetos de la utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . El panel de contenido del explorador de la utilidad proporciona varias maneras para ver datos de resumen y detallados sobre el estado de las instancias administradas de SQL Server. El explorador de la utilidad también proporciona una interfaz de usuario para ver y administrar las definiciones de directiva. Las capacidades del explorador de la utilidad varían ligeramente dependiendo de los objetos de la Utilidad [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pero, generalmente, incluyen objetos, datos y directivas administrados por la Utilidad [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obtener más información, vea [Características y tareas de la utilidad de SQL Server](sql-server-utility-features-and-tasks.md).  
  
## <a name="create-utility-control-point"></a>Crear un punto de control de la utilidad  
 Antes de poder usar la Utilidad [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , debe crear un punto de control de la utilidad. Para obtener más información, vea [Características y tareas de la utilidad de SQL Server](sql-server-utility-features-and-tasks.md) o [Crear un punto de control de la utilidad de SQL Server &#40;Utilidad de SQL Server&#41;](create-a-sql-server-utility-control-point-sql-server-utility.md).  
  
## <a name="enroll-an-instance-of-sql-server-or-a-data-tier-application-from-utility-explorer"></a>Inscribir una instancia de SQL Server o un aplicación de capa de datos desde el explorador de la utilidad  
 Puede inscribir con facilidad una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la Utilidad [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . En el Explorador de Utilidad, haga clic con el botón derecho en el nodo **Instancias administradas** y, después, haga clic en **Agregar instancia administrada**. Siga los pasos del asistente para completar la operación. Para obtener más información, vea [Inscribir una instancia de SQL Server &#40;Utilidad de SQL Server&#41;](enroll-an-instance-of-sql-server-sql-server-utility.md).  
  
 Para implementar una aplicación de capa de datos en una instancia administrada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la Utilidad [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], haga clic en la pestaña **Explorador de objetos**, expanda el nodo **Administración** y, después, haga clic con el botón derecho en **Aplicaciones de capa de datos**. En el menú contextual, seleccione **Implementar aplicación de capa de datos**. Para obtener más información, vea [Implementar una aplicación de capa de datos](../data-tier-applications/deploy-a-data-tier-application.md).  
  
## <a name="viewing-utility-explorer"></a>Ver el explorador de la utilidad  
 El explorador de la utilidad no es visible de forma predeterminada en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] . Si no puede ver el explorador de la utilidad en la interfaz de usuario de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] , en el menú **Ver** , haga clic en **Explorador de la utilidad.** Para ver el panel de contenido del explorador de la utilidad, en el menú **Ver** , haga en **Contenido del Explorador de la utilidad.**  
  
## <a name="viewing-objects-in-utility-explorer"></a>Ver objetos en el explorador de la utilidad  
 El panel de navegación y el panel de contenido del explorador de la utilidad muestran datos, objetos y directivas administrados por la Utilidad [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Use el panel de navegación para especificar la información que mostrar en los puntos de vista y el panel y emplee el panel del contenido y pestañas de detalles para obtener acceso a los datos e información de directivas para los objetos administrados por la Utilidad [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
### <a name="sql-server-utility-navigation-pane"></a>Panel de navegación de la utilidad de SQL Server  
 El panel de navegación del explorador de la utilidad proporciona una vista de árbol de objetos de la Utilidad [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , agrupada por punto de control de la utilidad. Para expandir las carpetas, haga clic en el signo más (+) o en el nombre de UCP en el panel de navegación del explorador de la utilidad. Haga clic con el botón secundario en las carpetas o en los objetos para realizar tareas comunes. Los nodos de la vista de árbol son como sigue:  
  
-   El nodo superior de la vista de árbol es el punto de control de la utilidad (UCP). El nombre de nodo se crea como se indica a continuación: "Nombre_Utilidad (NombreEquipo\nombre_instancia_UCP)." Si no tiene un UCP, debe crear uno. Si no está conectado a una Utilidad [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , debe conectarse a una. Para obtener más información, vea [Características y tareas de la utilidad de SQL Server](sql-server-utility-features-and-tasks.md). Haga clic en el nombre de UCP en la vista de árbol para rellenar el panel de contenido del explorador de la utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con datos en la vista de panel. Para obtener más información, vea [Panel de la utilidad &#40;Utilidad de SQL Server&#41;](../../database-engine/utility-dashboard-sql-server-utility.md).  
  
     Haga clic con el botón secundario en el nodo UCP para actualizar los datos en el panel.  
  
-   Haga clic en el nodo **Aplicaciones de capa de datos implementadas** en la vista de árbol para obtener acceso a los datos de la vista de árbol del panel de contenido de la Utilidad [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Las pestañas de detalles en la parte inferior del panel del contenido proporcionan datos sobre el uso de la CPU y del almacenamiento, así como acceso a definiciones de directivas y detalles de propiedades para aplicaciones de capa de datos individuales en la Utilidad [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, vea [Detalles de la aplicación de capa de datos implementada &#40;Utilidad de SQL Server&#41;](../../database-engine/deployed-data-tier-application-details-sql-server-utility.md).  
  
     Haga clic con el botón derecho en el nodo **Aplicaciones de capa de datos implementadas** en la vista de árbol para tener acceso a la configuración de filtros o a los datos de actualización en la vista de lista.  
  
-   Haga clic en el nodo **Instancias administradas** en la vista de árbol para obtener acceso a los datos de la vista de árbol en el panel de contenido de la Utilidad [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Las pestañas de detalles de la parte inferior del panel de contenido proporcionan datos sobre el uso de la CPU y de los volúmenes de almacenamiento, así como acceso a las definiciones de directivas y detalles de propiedades para instancias administradas individuales de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obtener más información, vea [Detalles de las instancias administradas &#40;Utilidad de SQL Server&#41;](../../database-engine/managed-instance-details-sql-server-utility.md).  
  
     Haga clic con el botón derecho en el nodo **Instancias administradas** en la vista de árbol para agregar instancias administradas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a la utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para tener acceso a la configuración de filtros o para actualizar los datos en la vista de lista.  
  
-   Haga clic en el nodo **Administración de la utilidad** en la vista de árbol para tener acceso a las definiciones de directivas globales para todas las instancias administradas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y las aplicaciones de capa de datos implementadas en la utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para ver información del administrador de UCP y obtener acceso a la configuración del almacén de administración de datos de la utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, vea [Administración de la utilidad &#40;Utilidad de SQL Server&#41;](../../database-engine/utility-administration-sql-server-utility.md). También puede utilizar controles de la pestaña **Directiva** para cambiar el carácter para notificar las infracciones de la directiva. Para obtener más información, vea [Reducir el ruido en las directivas de uso de la CPU &#40;Utilidad de SQL Server&#41;](reduce-noise-in-cpu-utilization-policies-sql-server-utility.md).  
  
     Haga clic con el botón derecho en el nodo **Administración de la utilidad** en la vista de árbol para actualizar los datos del panel del contenido.  
  
### <a name="sql-server-utility-dashboard"></a>Panel de la utilidad de SQL Server  
 Al seleccionar el nodo UCP en la vista de árbol del explorador de Utilidad, se rellena el panel de la utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el panel de contenido del explorador de Utilidad. El panel proporciona un rápido resumen del estado de todas las instancias administradas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], de las aplicaciones de capa de datos de la utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y del uso de almacenamiento total para los objetos administrados por la utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, vea [Panel de la utilidad &#40;Utilidad de SQL Server&#41;](../../database-engine/utility-dashboard-sql-server-utility.md). Para inscribir o eliminar una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Inscribir una instancia de SQL Server &#40;Utilidad de SQL Server&#41;](enroll-an-instance-of-sql-server-sql-server-utility.md) o [Implementar una aplicación de capa de datos](../data-tier-applications/deploy-a-data-tier-application.md) o [Quitar una instancia de SQL Server de la utilidad de SQL Server](remove-an-instance-of-sql-server-from-the-sql-server-utility.md).  
  
### <a name="filtering-the-list-of-objects-in-utility-explorer-contents"></a>Filtrar la lista de objetos en el contenido del explorador de la utilidad  
 Cuando un nodo contiene un gran número de objetos, puede resultar difícil encontrar el que se busca. En estos casos, use la característica de filtro del explorador de la utilidad a fin de reducir la lista. Por ejemplo, puede que desee encontrar una instancia concreta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o solo los equipos con espacio de archivo infrautilizado. Haga clic con el botón derecho en la carpeta que quiere filtrar y, después, haga clic en **Configuración del filtro** para abrir el cuadro de diálogo Configuración del filtro del Explorador de Utilidad. Puede filtrar la lista por nombre, CPU del equipo, CPU de instancia, espacio de archivos, espacio de volumen, configuración de invalidación de directiva u hora de última notificación. Las columnas **Operador** y **Valor** proporcionan operadores de filtrado adicionales en una lista desplegable.  
  
### <a name="starting-powershell"></a>Iniciar PowerShell  
 Puede iniciar una sesión de PowerShell haciendo clic con el botón derecho en la mayoría de las carpetas y objetos en el árbol del Explorador de objetos y seleccionando **Iniciar PowerShell**. De este modo se inicia una sesión de PowerShell que tiene habilitada la compatibilidad con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell, y tiene establecida la ruta de acceso al objeto en el que hizo clic con el botón secundario en el Explorador de objetos. A continuación, puede escribir comandos de PowerShell en un entorno interactivo de PowerShell. Para más información, consulte el artículo sobre [SQL Server PowerShell](../../powershell/sql-server-powershell.md).  
  
 PowerShell no tiene ayuda F1, pero incluye un cmdlet **Get-Help** que proporciona información sobre el uso de PowerShell. Para obtener más información sobre el uso de Get-Help, vea [Obtener ayuda de SQL Server PowerShell](../../database-engine/get-help-sql-server-powershell.md).  
  
## <a name="see-also"></a>Consulte también  
 [Características y tareas de la utilidad de SQL Server](sql-server-utility-features-and-tasks.md)   
 [Configurar las directivas de mantenimiento &#40;Utilidad de SQL Server&#41;](configure-health-policies-sql-server-utility.md)   
 [Explorador de objetos](../../ssms/object/object-explorer.md)  
  
  
