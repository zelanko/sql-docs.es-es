---
title: Recopilación de datos de uso de PowerPivot | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 9057cb89-fb17-466e-a1ce-192c8ca20692
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 46504906b13323ac4881ca2289e87e31f1cea72f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66071086"
---
# <a name="powerpivot-usage-data-collection"></a>Recopilación de datos de uso de PowerPivot
  La recopilación de datos de uso es una característica propia de SharePoint para las granjas. PowerPivot para SharePoint usa y extiende este sistema para proporcionar informes en el panel de administración de PowerPivot que muestran cómo se usan los datos y servicios PowerPivot. Según cómo haya instalado SharePoint, la recopilación de datos de uso podría estar desactivada para la granja. El administrador de una granja debe habilitar el registro de uso para crear los datos de uso que aparecen en el Panel de administración de PowerPivot. Para obtener más información sobre cómo habilitar y configurar la recopilación de datos de uso para los eventos de PowerPivot, vea [configurar la recopilación de datos de uso para &#40;PowerPivot para SharePoint](configure-usage-data-collection-for-power-pivot-for-sharepoint.md).  
  
 Para obtener información sobre los datos de uso en el Panel de administración de PowerPivot, vea [PowerPivot Management Dashboard and Usage Data](power-pivot-management-dashboard-and-usage-data.md).  
  
 **En este tema:**  
  
 [Recopilación de datos de uso y arquitectura de informes](#usagearch)  
  
 [Orígenes de datos de uso](#sources)  
  
 [Servicios y trabajos del temporizador](#servicesjobs)  
  
 [Informes sobre los datos de uso](#reporting)  
  
##  <a name="usagearch"></a>Recopilación de datos de uso y arquitectura de informes  
 Los datos de uso de PowerPivot se recopilan, almacenan y administran mediante una combinación de características de la infraestructura de SharePoint y de componentes de servidor de PowerPivot. La infraestructura de SharePoint proporciona un servicio de uso centralizado y trabajos del temporizador integrados. PowerPivot para SharePoint agrega un almacenamiento a mayor plazo para los datos de uso y los informes de PowerPivot que se ven en Administración central de SharePoint.  
  
 En el sistema de recopilación de datos de uso, la información de los eventos se introduce en el sistema de recopilación de datos de uso en el servidor de aplicaciones o front-end web. Los datos de uso se mueven a través del sistema como respuesta a los trabajos del temporizador que hacen que los datos se pasen de los archivos de datos temporales del servidor físico a un almacenamiento persistente en un servidor de bases de datos. El siguiente diagrama muestra los componentes y procesos que mueven los datos de uso a través del sistema de informes y recopilación de datos.  
  
 **Nota:** Compruebe que la recopilación de datos de uso está habilitada. Para ello, vaya a **Supervisión** en Administración central de SharePoint. Para obtener más información, consulte [configurar la recopilación de datos de uso para &#40;PowerPivot para SharePoint](configure-usage-data-collection-for-power-pivot-for-sharepoint.md).  
  
 ![Componentes y procesos de la recopilación de datos de uso.](../media/gmni-usagedata.gif "Componentes y procesos de la recopilación de datos de uso.")  
  
|Fase|Descripción|  
|-----------|-----------------|  
|1|La recopilación de datos de uso se desencadena mediante eventos generados por los componentes de PowerPivot y los proveedores de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en las implementaciones de SharePoint. Entre los eventos configurables que se pueden activar o desactivar se encuentran las solicitudes de conexión, las solicitudes de carga y descarga, y los eventos de sincronización en respuesta a las consultas que el servicio PowerPivot supervisa en el servidor de aplicaciones. Otros eventos son administrados solamente por el servidor y no se pueden desactivar. Por ejemplo, los de actualización de datos y los de estado del servidor.<br /><br /> Inicialmente, los datos de uso se recopilan y almacenan en archivos de registro locales mediante las características de recopilación de datos del sistema de SharePoint. Los archivos y su ubicación forman parte del sistema de recopilación de datos de uso estándar de SharePoint. La ubicación de los archivos es la misma en todos los servidores de la granja. Para ver o cambiar la ubicación del directorio de registro, vaya a **Supervisión** en Administración central de SharePoint y, a continuación, haga clic en **Configurar la recolección de datos de uso y estado**.|  
|2|En los intervalos programados (cada hora de forma predeterminada), el trabajo de temporizador Importación de datos de uso de Microsoft SharePoint Foundation mueve los datos de uso de los archivos locales a la base de datos de la aplicación de servicio PowerPivot. Si tiene varias aplicaciones de servicio PowerPivot en una granja, cada una tendrá su propia base de datos. Los eventos incluyen información interna que identifica qué aplicación de servicio PowerPivot generó el evento. Los identificadores de la aplicación se aseguran de que los datos de uso se enlazan a la aplicación que los creó.|  
|3|Los datos se copian en una base de datos de informes interna que está disponible para el panel de administración de PowerPivot en Administración central.|  
|4|El origen de datos es un libro PowerPivot al que puede tener acceso para crear informes personalizados en Excel. Solo hay una instancia del libro de origen. Todos los informes traducidos se basan en el mismo libro de origen.|  
|5|Los datos de uso se presentan en informes para los administradores de las aplicaciones de servicio PowerPivot que administran el rendimiento y la disponibilidad de los servidores. Se crean instancias localizadas de los libros para los idiomas admitidos de SharePoint.<br /><br /> Para obtener más información, vea [Informes sobre los datos de uso](#reporting) en este tema.|  
  
##  <a name="sources"></a>Orígenes de datos de uso  
 Cuando la recopilación de datos de uso está habilitada, se generan datos para los siguientes eventos de servidor.  
  
|Evento|Descripción|Configurable|  
|-----------|-----------------|------------------|  
|Conexiones|Conexiones de servidor realizadas en nombre de un usuario que consulta los datos PowerPivot en un libro de Excel. Los eventos de conexión identifican quién abrió una conexión a un libro PowerPivot. En los informes, esta información se utiliza para identificar a los usuarios más frecuentes, los orígenes de datos PowerPivot a los que tienen acceso los mismos usuarios y las tendencias en las conexiones a lo largo del tiempo.|Puede habilitar y deshabilitar la [configuración de la recopilación de datos de uso para &#40;PowerPivot para SharePoint](configure-usage-data-collection-for-power-pivot-for-sharepoint.md).|  
|Consulta de los tiempos de respuesta|Estadísticas de respuesta de las consultas que clasifican las consultas en función de cuánto tiempo tardan en completarse. Las estadísticas de respuestas de las consultan muestran patrones sobre cuánto tiempo tarda el servidor en responder a las solicitudes de consultas.|Puede habilitar y deshabilitar la [configuración de la recopilación de datos de uso para &#40;PowerPivot para SharePoint](configure-usage-data-collection-for-power-pivot-for-sharepoint.md).|  
|Carga de datos|Las operaciones de carga de datos del [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)]. Los eventos de carga de datos identifican qué orígenes de datos se usan con mayor frecuencia.|Puede habilitar y deshabilitar la [configuración de la recopilación de datos de uso para &#40;PowerPivot para SharePoint](configure-usage-data-collection-for-power-pivot-for-sharepoint.md).|  
|Descarga de datos|Las operaciones de descarga de datos de las aplicaciones de servicio PowerPivot. Un [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] descarga los orígenes de datos PowerPivot inactivos si no se usan o cuando el servidor está sufriendo presión de memoria o necesita memoria adicional para ejecutar los trabajos de actualización de datos.|Puede habilitar y deshabilitar la [configuración de la recopilación de datos de uso para &#40;PowerPivot para SharePoint](configure-usage-data-collection-for-power-pivot-for-sharepoint.md).|  
|Estado del servidor|Las operaciones de servidor que indican el estado del servidor, medidas en función de la utilización de la memoria y la CPU. Estos datos son históricos. No proporciona información de tiempo real acerca de la carga de procesamiento actual en el servidor.|No. Siempre se recopilan datos de uso para este evento.|  
|Actualización de datos|Las operaciones de actualización de datos iniciadas por el servicio PowerPivot para las actualizaciones de datos programadas. El historial de uso para la actualización de datos se recopila en el nivel de aplicación para los informes de operaciones y se refleja en las páginas de Administrar actualización de datos para los libros individuales.<br /><br /> **Nota:** En [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] las implementaciones de y SharePoint 2013, la actualización de datos la administra Excel Services, no el servidor de Analysis Services.|No. Los datos de uso siempre se recopilan si habilita la actualización de datos para la aplicación de servicio PowerPivot.|  
  
##  <a name="servicesjobs"></a>Servicios y trabajos del temporizador  
 La siguiente tabla describe los servicios y los almacenes de recopilación de datos en el sistema de recopilación de datos de uso. Para obtener instrucciones sobre cómo invalidar las programaciones de trabajos del temporizador para forzar una actualización de datos del estado del servidor y de los datos de uso en los informes del panel de administración de PowerPivot, vea [actualización de datos PowerPivot con SharePoint 2010](../powerpivot-data-refresh-with-sharepoint-2010.md). Puede ver los trabajos de temporizador en Administración central de SharePoint. Vaya a **Supervisión**y haga clic en **Comprobar estado de trabajo**. Haga clic en **Revisar definiciones de trabajo**.  
  
|Componente|Programación predeterminada|Descripción|  
|---------------|----------------------|-----------------|  
|Temporizador de extensiones de SharePoint (SPTimerV4)||Este servicio de Windows se ejecuta localmente en cada equipo miembro de la granja y procesa todos los trabajos del temporizador que se definen en el nivel de granja.|  
|Importación de datos de uso de Microsoft SharePoint Foundation|Cada 30 minutos en SharePoint 2010. Cada 5 minutos en SharePoint 2013.|Este trabajo de temporizador se configura globalmente en el nivel de granja. Mueve los datos de uso de los archivos de registro de uso locales a la base de datos de recopilación de datos de uso central. Puede ejecutar manualmente este trabajo de temporizador para forzar una operación de importación de datos.|  
|Trabajo de temporizador de procesamiento de datos de uso de Microsoft SharePoint Foundation|Diariamente a las 3:00 a.m.|**(\*)** A partir de SQL Server 2012 PowerPivot para SharePoint, este trabajo de tiempo se admite para escenarios de actualización o migración donde puede tener datos de uso más antiguos todavía en las bases de datos de uso de SharePoint. A partir de SQL Server 2012 PowerPivot para SharePoint, la base de datos de uso de SharePoint no se emplea para la recopilación de uso de PowerPivot y el flujo de trabajo del panel de administración. Se puede ejecutar manualmente el trabajo de temporizador para mover los datos relacionados de PowerPivot restantes de la base de datos de uso de SharePoint a las bases de datos de aplicación de servicio PowerPivot.<br /><br /> Este trabajo de temporizador se configura globalmente en el nivel de granja. Comprueba si hay datos de uso que hayan expirado en la base de datos de recopilación de datos de uso central (es decir, cualquier registro cuya fecha sea anterior a 30 días). Para los servidores de PowerPivot en la granja, este trabajo del temporizador realiza una comprobación adicional para los datos de uso de PowerPivot. Cuando se detectan los datos de uso de PowerPivot, el trabajo del temporizador mueve los datos a una base de datos de aplicación del servicio utilizando un identificador de la aplicación para encontrar la base de datos correcta.<br /><br /> Puede ejecutar manualmente este trabajo de temporizador para forzar que se compruebe si los datos han expirado o para forzar la importación de los datos de uso de PowerPivot a una base de datos de aplicación de servicio PowerPivot.|  
|Trabajo de temporizador de procesamiento del panel de administración de PowerPivot|Diariamente a las 3:00 a.m.|Este trabajo de temporizador actualiza el libro PowerPivot interno que proporciona datos administrativos al Panel de administración de PowerPivot. Consigue información actualizada que administra SharePoint, como son nombres de servidor, nombres de usuario, nombres de aplicación y nombres de archivo que aparecen en los informes del panel o en los elementos web.|  
  
##  <a name="reporting"></a>Informes sobre los datos de uso  
 Para ver los datos de uso de PowerPivot, puede ver los informes integrados en el Panel de administración de PowerPivot. Los informes integrados consolidan los datos de uso que se recuperan de las estructuras de datos de informes en la base de datos de aplicación del servicio. Dado que los datos de informes subyacentes se actualizan diariamente, los informes de uso integrados solo mostrarán la información actualizada cuando el trabajo de temporizador de procesamiento de datos de uso de Microsoft SharePoint Foundation copie los datos en una base de datos de aplicación de servicio PowerPivot. De forma predeterminada, esto se produce una vez al día.  
  
 Para obtener más información acerca de cómo ver los informes, vea [PowerPivot Management Dashboard and Usage Data](power-pivot-management-dashboard-and-usage-data.md).  
  
## <a name="see-also"></a>Consulte también  
 [Panel de administración de PowerPivot y datos de uso](power-pivot-management-dashboard-and-usage-data.md)   
 [&#40;de referencia de configuración de configuración PowerPivot para SharePoint&#41;](configuration-setting-reference-power-pivot-for-sharepoint.md)   
 [Configurar la recopilación de datos de uso para &#40;PowerPivot para SharePoint](configure-usage-data-collection-for-power-pivot-for-sharepoint.md)  
  
  
