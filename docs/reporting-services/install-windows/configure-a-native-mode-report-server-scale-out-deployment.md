---
title: "Configurar una implementación de ampliación horizontal del servidor de informes de modo nativo | Documentos de Microsoft"
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- report servers [Reporting Services], deployments
- deploying [Reporting Services], scale-out deployment model
- scale-out deployments [Reporting Services]
ms.assetid: b30d0308-4d9b-4f85-9f83-dece4dcb2775
caps.latest.revision: 13
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 6a90a566e3e100fff3bb17e838a368a82ac3f4f5
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---

# <a name="configure-a-native-mode-report-server-scale-out-deployment"></a>Configurar una implementación escalada horizontalmente del servidor de informes en modo nativo

  Reporting Services en modo nativo admite un modelo de implementación de ampliación horizontal que permite ejecutar varias instancias del servidor de informes que comparten una única base de datos del servidor de informes. Las implementaciones escaladas se utilizan para aumentar la escalabilidad de los servidores de informes para administrar más usuarios con acceso simultáneo y mayores cargas de ejecución de informes. También se pueden utilizar para dedicar servidores concretos en el procesamiento de informes interactivos o programados.  
  
 Los servidores de informes en modo de SharePoint utilizan la infraestructura de los Productos de SharePoint para la implementación escalada. La ampliación del modo de SharePoint se logra al agregar más servidores de informes en modo de SharePoint a la granja de servidores de SharePoint. Para obtener más información sobre la implementación escalada en el modo de SharePoint, vea [Agregar un servidor de informes adicional a una granja de servidores &#40;escalado horizontal de SSRS&#41;](../../reporting-services/install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md).  
 
  Una *implementación escalada* se usa en los escenarios siguientes:  
  
-   Como requisito previo para lograr el equilibrio de carga en varios servidores de informes de un clúster de servidores. Para poder equilibrar la carga en varios servidores de informes, debe configurarlos primero de modo que compartan la misma base de datos.  
  
-   Para segmentar las aplicaciones del servidor de informes en equipos diferentes mediante el uso de un servidor para el procesamiento interactivo de los informes y de un segundo servidor para el procesamiento programado de los informes. En este escenario, cada instancia del servidor procesa tipos diferentes de solicitudes para el contenido del mismo servidor de informes que se almacena en la base de datos compartida.  
  
 **Las implementaciones escaladas constan de:**  
  
-   Dos o más instancias del servidor de informes que comparten una única base de datos del servidor de informes.  
  
-   Opcionalmente, un clúster con equilibrio de carga de red (NLB) para distribuir la carga de usuarios interactivos en las instancias del servidor de informes.  
  
 Cuando se implementa Reporting Services en un clúster NLB, es necesario asegurarse de que el nombre del servidor virtual NLB se utiliza en la configuración de direcciones URL del servidor de informes, y que los servidores se configuran para compartir el mismo estado de vista.  
  
 Reporting Services no participa en clústeres de Servicios de Cluster Server de Microsoft. Sin embargo, se puede crear la base de datos del servidor de informes en una instancia del motor de base de datos que forma parte de un clúster de conmutación por error.  
  
 **Para planear, instalar y configurar una implementación escalada, siga estos pasos:**  
  
-   Revisión [instalar SQL Server 2016 desde el Asistente para instalación &#40; El programa de instalación &#41; ](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md) en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] libros en pantalla para obtener instrucciones sobre cómo instalar instancias del servidor de informes.  
  
-   Si tiene previsto hospedar la implementación escalada en un clúster con equilibrio de carga de red (NLB), deberá configurar el clúster NLB antes de configurar la implementación escalada. Para más información, consulte [Configure a Report Server on a Network Load Balancing Cluster](../../reporting-services/report-server/configure-a-report-server-on-a-network-load-balancing-cluster.md).  
  
-   Revise los procedimientos de este tema para saber cómo se comparte una base de datos del servidor de informes y cómo se unen servidores de informes a una implementación escalada.  
  
     Los procedimientos explican cómo configurar una implementación escalada del servidor de informes de dos nodos. Repita los pasos que se describen en este tema para agregar nodos adicionales de servidor de informes a la implementación.  
  
    -   Use el programa de instalación para instalar cada instancia del servidor de informes que se vaya a unir a la implementación escalada.  
  
         Para evitar que se produzcan errores de compatibilidad de base de datos al conectar las instancias del servidor a la base de datos compartida, asegúrese de que la versión de todas las instancias sea la misma. Por ejemplo, si crea la base de datos del servidor de informes con una instancia de servidor de informes de SQL Server 2016, todas las demás instancias de la misma implementación también deben ser SQL Server 2016.  
  
    -   Use el Administrador de configuración de Reporting Services con el fin de conectarse a cada uno de los servidores de informes para la base de datos compartida. Solo puede configurar y conectarse a un servidor de informes a la vez.  
  
    -   Utilice la herramienta Configuración de Reporting Services para completar la ampliación escalada uniendo instancias nuevas del servidor de informes a la primera instancia ya conectada a la base de datos de servidor de informes.  
  
## <a name="to-install-a-sql-server-instance-to-host-the-report-server-databases"></a>Para instalar una instancia de SQL Server para hospedar las bases de datos del servidor de informes  
  
1.  Instale una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el equipo que hospedará las bases de datos del servidor de informes. Como mínimo, instale [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] y [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
2.  Si es necesario, habilite el servidor de informes para conexiones remotas. Algunas versiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no habilitan las conexiones TCP/IP remotas ni las conexiones de canalizaciones con nombre de forma predeterminada. Para confirmar si se permiten las conexiones remotas, use el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y consulte la configuración de red de la instancia de destino. Si la instancia remota es también una instancia con nombre, compruebe que el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser está habilitado y ejecutándose en el servidor de destino. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser proporciona el número de puerto que se usa para conectarse a la instancia con nombre. 

## <a name="service-accounts"></a>Cuentas de servicio

Las cuentas de servicio para la instancia de Reporting Services son importantes cuando se trabaja con una implementación escalada. Debe realizar una de las acciones siguientes al implementar las instancias de Reporting Services.

**Opción 1:** todas las instancias de Reporting Services deben configurarse con la misma cuenta de usuario de dominio para la cuenta de servicio.

**Opción 2:** cada cuenta de servicio, cuenta de dominio o no, es necesario conceder permisos dbadmin dentro de la instancia de base de datos de SQL Server que hospeda la base de datos del catálogo ReportServer.

Si ha configurado una configuración diferente de cualquiera de las opciones anteriores, se pueden producir errores intermitentes de modificar las tareas con el Agente SQL. Esto se mostrará como un error en ambos servicios de informes de registro y en el portal web al editar una suscripción de informe.

```
An error occurred within the report server database.  This may be due to a connection failure, timeout or low disk condition within the database.
``` 

El problema será intermitente es que solo el servidor que creó la tarea de agente SQL tendrá derechos para ver, eliminar o editar el elemento. Si no hace una de las opciones anteriores, las operaciones sólo surtirán efecto cuando el equilibrador de carga todas las solicitudes de dicha suscripción envía al servidor que creó la tarea de agente SQL. 
  
## <a name="to-install-the-first-report-server-instance"></a>Para instalar la primera instancia del servidor de informes  
  
1.  Instale la primera instancia del servidor de informes que forma parte de la implementación. Cuando instale [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], elija la opción **Instalar, pero no configurar el servidor de informes** en la página Opciones de instalación del servidor de informes.  
  
2.  Inicie la herramienta de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
3.  Configure la dirección URL del servicio Web del servidor de informes, la dirección URL del Portal Web y la base de datos del servidor de informes. Para obtener más información, vea [Configurar un servidor de informes &#40;modo nativo de Reporting Services&#41;](../../reporting-services/report-server/configure-a-report-server-reporting-services-native-mode.md) en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
4.  Compruebe que el servidor de informes está operativo. Para obtener más información, vea [Comprobar una instalación de Reporting Services](../../reporting-services/install-windows/verify-a-reporting-services-installation.md) en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="to-install-and-configure-the-second-report-server-instance"></a>Para instalar y configurar la segunda instancia del servidor de informes  
  
1.  Ejecute el programa de instalación para instalar una segunda instancia de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en otro equipo o como una instancia con nombre en el mismo equipo. Cuando instale Reporting Services, elija la opción **Instalar, pero no configurar el servidor de informes** en la página Opciones de instalación del servidor de informes.  
  
2.  Inicie la herramienta de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y conéctese a la nueva instancia recién instalada.  
  
3.  Conecte el servidor de informes a la misma base de datos que usó para la primera instancia del servidor de informes:  
  
    1.  Seleccione **Base de datos** para abrir la página Base de datos.  
  
    2.  Seleccione **Cambiar base de datos**.  
  
    3.  Seleccione **Elegir una base de datos del servidor de informes existente**.  
  
    4.  Escriba el nombre del servidor de la instancia del motor de base de datos de SQL Server que hospeda la base de datos del servidor de informes que desea usar. Debe ser el mismo servidor al que se conectó en el grupo anterior de instrucciones.  
  
    5.  Seleccione **Probar conexión**y, después, **Siguiente**.  
  
    6.  En **Base de datos del servidor de informes**, seleccione la base de datos que creó para el primer servidor de informes y, después, seleccione **Siguiente**. El nombre predeterminado es ReportServer. No seleccione ReportServerTempDB; solo se usa para almacenar datos temporales al procesar los informes. Si la lista de bases de datos está vacía, repita los cuatro pasos anteriores para establecer una conexión con el servidor.  
  
    7.  En la página Credenciales, seleccione el tipo de cuenta y las credenciales que el servidor de informes utilizará para conectarse a la base de datos del servidor de informes. Puede utilizar las mismas credenciales que para la primera instancia del servidor de informes u otras. Seleccione **Siguiente**.  
  
    8.  Seleccione **Resumen** y, después, **Finalizar**.  
  
4.  Configure la **dirección URL del servicio web**del servidor de informes. No pruebe todavía la dirección URL. No se resolverá hasta que el servidor de informes se una a la implementación escalada.  
  
5.  Configure la **dirección URL del Portal web**. No pruebe todavía la dirección URL ni intente comprobar la implementación. El servidor de informes no estará disponible hasta que el servidor de informes se una a la implementación escalada.  
  
## <a name="to-join-the-second-report-server-instance-to-the-scale-out-deployment"></a>Para unir la segunda instancia del servidor de informes a la implementación escalada  
  
1.  Abra la herramienta de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y vuelva a conectarse a la primera instancia del servidor de informes. El primer servidor de informes ya se ha inicializado para operaciones de cifrado reversibles, de modo que se puede usar para unir más instancias a la implementación escalada.  
  
2.  Haga clic en **Implementación escalada** para abrir la página implementación escalada. Debería ver dos entradas, una para cada instancia del servidor de informes que esté conectada a la base de datos del servidor de informes. La primera instancia del servidor de informes debería estar unida. El segundo servidor de informes debería estar "Esperando para unirse". Si no ve entradas similares en su implementación, compruebe que está conectado al primer servidor de informes que ya está configurado e inicializado para utilizar la base de datos del servidor de informes.  
  
     ![Captura de pantalla parcial de página implementación escalada](../../reporting-services/install-windows/media/scaloutscreen.gif "captura de pantalla parcial de página de la implementación de ampliación horizontal")  
  
3.  En la página implementación escalada, seleccione la instancia de servidor de informes que está esperando para unirse a la implementación y seleccione **Agregar servidor**.  
  
    > [!NOTE]  
    >  **Issue:** al intentar combinar una instancia del servidor de informes de Reporting Services con la implementación escalada, es posible que aparezcan mensajes de error similares a “Acceso denegado”.  
    >   
    >  **Solución alternativa:** haga una copia de seguridad de la clave de cifrado de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] desde la primera instancia de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y restáurela en el segundo servidor de informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . A continuación, intente unir el segundo servidor a la implementación escalada de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
4.  Ahora debería poder para comprobar que ambas instancias del servidor de informes están operativas. Para comprobar la segunda instancia, puede usar la herramienta Configuración de Reporting Services con el fin de conectarse al servidor de informes y hacer clic en **Dirección URL del servicio web** o en **Dirección URL del Portal web**.  
  
 Si tiene previsto ejecutar los servidores de informes en un clúster de servidores con equilibrio de carga, son necesarios algunos pasos de configuración adicionales. Para más información, consulte [Configure a Report Server on a Network Load Balancing Cluster](../../reporting-services/report-server/configure-a-report-server-on-a-network-load-balancing-cluster.md).  

## <a name="next-steps"></a>Pasos siguientes

[Configurar una cuenta de servicio](http://msdn.microsoft.com/library/25000ad5-3f80-4210-8331-d4754dc217e0)   
[Configurar una dirección URL](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)   
[Crear una base de datos del servidor de informes de modo nativo](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)   
[Configurar direcciones URL del servidor de informes](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
[Configurar una conexión de base de datos del servidor de informes](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
[Agregar y quitar claves de cifrado para la implementación de ampliación horizontal](../../reporting-services/install-windows/add-and-remove-encryption-keys-for-scale-out-deployment.md)   
[Administrar un servidor de informes de modo nativo de Reporting Services](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md)  

¿Más preguntas? [Pruebe a formular el foro de Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
