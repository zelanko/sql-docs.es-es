---
title: "Configurar un firewall para el acceso al servidor de informes | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "09/14/2015"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "sistemas firewall [Reporting Services]"
  - "configurar servidores [Reporting Services]"
ms.assetid: 04dae07a-a3a4-424c-9bcb-a8000e20dc93
caps.latest.revision: 13
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 13
---
# Configurar un firewall para el acceso al servidor de informes
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] A las aplicaciones del servidor de informes y a los informes publicados se tiene acceso a través de direcciones URL que especifican una dirección IP, un puerto y un directorio virtual. Si Firewall de Windows está activado, es probable que el puerto que el servidor de informes está configurado para usar esté cerrado. Los indicios que señalan que un puerto podría estar cerrado son una página en blanco cuando intenta abrir el **Administrador de informes** desde un equipo cliente remoto o una página web en blanco después de solicitar un informe.  
  
 Para abrir un puerto, debe utilizar la utilidad Firewall de Windows en el equipo del servidor de informes. Reporting Services no abrirá los puertos en su lugar; debe realizar este paso manualmente.  
  
 De forma predeterminada, el servidor de informes escucha las solicitudes HTTP en el puerto 80. Por tanto, las instrucciones siguientes incluyen los pasos que especifican ese puerto. Si configuró las direcciones URL del servidor de informes para utilizar un puerto diferente, debe especificar ese número de puerto al seguir las instrucciones siguientes.  
  
 Si está teniendo acceso a las bases de datos relacionales de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en equipos externos, o si la base de datos del servidor de informes se encuentra en una instancia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] externa, debe abrir el puerto 1433 y 1434 del equipo externo. Para obtener más información, vea [Configurar Firewall de Windows para el acceso al motor de base de datos](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md) en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información sobre la configuración predeterminada de Firewall de Windows y una descripción de los puertos TCP que afectan al [!INCLUDE[ssDE](../../includes/ssde-md.md)], a [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], a [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y a [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], vea [Configurar Firewall de Windows para permitir el acceso a SQL Server](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md) en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## Requisitos previos  
 En estas instrucciones se supone que ya configuró la cuenta de servicio, creó la base de datos del servidor de informes y configuró direcciones URL para el servicio web del servidor de informes y el Administrador de informes. Para obtener más información, vea [Administrar un servidor de informes en modo nativo de Reporting Services](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md).  
  
 También debería haber comprobado que el servidor de informes es accesible a través de una conexión del explorador web local a la instancia del servidor de informes local. Con este paso se establece que tiene una instalación activa. Debería comprobar que la instalación está configurada correctamente antes de empezar a abrir los puertos. Para completar este paso en Windows Server 2008, debe haber agregado también el sitio del servidor de informes a Sitios de confianza. Para obtener más información, vea [Configurar un servidor de informes en modo nativo para la administración local &#40;SSRS&#41;](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md).  
  
## Abrir puertos en Firewall de Windows  
  
#### Para abrir el puerto 80  
  
1.  En el menú **Inicio** , haga clic en **Panel de control**, en **Sistema y seguridad**y, a continuación, en **Firewall de Windows**. El Panel de control no está configurado para la vista 'Categoría', solo necesita seleccionar **Firewall de Windows.**  
  
2.  Haga clic en **Configuración avanzada**.  
  
3.  Haga clic en **Reglas de entrada**  
  
4.  Haga clic en **Nueva regla** en la ventana **Acciones****.**  
  
5.  Haga clic en **Puerto** en la sección **Regla de entrada.**  
  
6.  Haga clic en **Siguiente**.  
  
7.  En la página **Protocolos y puertos** , haga clic en **TCP**.  
  
8.  Seleccione **Puertos locales específicos** y escriba un valor de **80**.  
  
9. Haga clic en **Siguiente**.  
  
10. En la página **Acción** , haga clic en **Permitir la conexión**.  
  
11. Haga clic en **Siguiente**.  
  
12. En la página **Perfil** , haga clic en las opciones adecuadas para su entorno.  
  
13. Haga clic en **Siguiente**.  
  
14. En la página **Nombre**, escriba un nombre de**ReportServer (TCP en el puerto 80)**.  
  
15. Haga clic en **Finalizar**.  
  
16. Reinicie el equipo.  
  
## Pasos siguientes  
 Después de abrir el puerto y antes de confirmar si los usuarios remotos pueden tener acceso al servidor de informes en el puerto que abre, debe conceder acceso de usuario al servidor de informes a través de las asignaciones de roles en Inicio y en el nivel de sitio. Puede abrir un puerto correctamente y seguir teniendo conexiones del servidor de informes erróneas si los usuarios no tienen permisos suficientes. Para obtener más información, vea [Conceder a un usuario acceso a un servidor de informes &#40;Administrador de informes&#41;](../../reporting-services/security/grant-user-access-to-a-report-server-report-manager.md) en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 También puede comprobar que el puerto se abre correctamente iniciando el Administrador de informes en un equipo diferente. Para obtener más información, vea [Administrador de informes &#40;Modo nativo de SSRS&#41;](../Topic/Report%20Manager%20%20\(SSRS%20Native%20Mode\).md) en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## Vea también  
 [Configurar la cuenta de servicio del servidor de informes &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [Configurar las direcciones URL del servidor de informes &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
 [Crear una base de datos del servidor de informes &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/create-a-report-server-database-ssrs-configuration-manager.md)   
 [Configurar la cuenta de servicio del servidor de informes &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [Administrar un servidor de informes en modo nativo de Reporting Services](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md)  
  
  