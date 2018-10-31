---
title: Configurar un firewall para el acceso al servidor de informes | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- firewall systems [Reporting Services]
- configuring servers [Reporting Services]
ms.assetid: 04dae07a-a3a4-424c-9bcb-a8000e20dc93
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 841bdd13dfbc1fe7ca29a4eb3f3dbe757a28c36c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48224455"
---
# <a name="configure-a-firewall-for-report-server-access"></a>Configurar un firewall para el acceso al servidor de informes
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] A las aplicaciones del servidor de informes y a los informes publicados se tiene acceso a través de direcciones URL que especifican una dirección IP, un puerto y un directorio virtual. Si Firewall de Windows está activado, es probable que el puerto que el servidor de informes está configurado para usar esté cerrado. Los indicios que señalan que un puerto podría estar cerrado son la aparición de una página web en blanco después de solicitar un informe o al intentar abrir el Administrador de informes desde un equipo cliente remoto.  
  
 Para abrir un puerto, debe utilizar la utilidad Firewall de Windows en el equipo del servidor de informes. Reporting Services no abrirá los puertos en su lugar; debe realizar este paso manualmente.  
  
 De forma predeterminada, el servidor de informes escucha las solicitudes HTTP en el puerto 80. Por tanto, las instrucciones siguientes incluyen los pasos que especifican ese puerto. Si configuró las direcciones URL del servidor de informes para utilizar un puerto diferente, debe especificar ese número de puerto al seguir las instrucciones siguientes.  
  
 Si está teniendo acceso a las bases de datos relacionales de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en equipos externos, o si la base de datos del servidor de informes se encuentra en una instancia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] externa, debe abrir el puerto 1433 y 1434 del equipo externo. Para obtener más información, vea [Configurar Firewall de Windows para el acceso al motor de base de datos](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md) en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obtener más información sobre la configuración predeterminada de Firewall de Windows y una descripción de los puertos TCP que afectan al [!INCLUDE[ssDE](../../includes/ssde-md.md)], a [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], a [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]y a [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], vea [Configurar Firewall de Windows para permitir el acceso a SQL Server](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md) en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="prerequisites"></a>Requisitos previos  
 En estas instrucciones se supone que ya configuró la cuenta de servicio, creó la base de datos del servidor de informes y configuró direcciones URL para el servicio web del servidor de informes y el Administrador de informes. Para obtener más información, consulte [administrar un Reporting Services modo de servidor de informes nativo](manage-a-reporting-services-native-mode-report-server.md).  
  
 También debería haber comprobado que el servidor de informes es accesible a través de una conexión del explorador web local a la instancia del servidor de informes local. Con este paso se establece que tiene una instalación activa. Debería comprobar que la instalación está configurada correctamente antes de empezar a abrir los puertos. Para completar este paso en Windows Server 2008, debe haber agregado también el sitio del servidor de informes a Sitios de confianza. Para obtener más información, vea [Configurar un servidor de informes en modo nativo para la administración local &#40;SSRS&#41;](configure-a-native-mode-report-server-for-local-administration-ssrs.md).  
  
## <a name="opening-ports-in-windows-firewall"></a>Abrir puertos en Firewall de Windows  
 Cada versión del Firewall de Windows tiene instrucciones distintas.  
  
#### <a name="to-open-port-80-on-windows-7-windows-server-2008-r2-windows-server-2012-and-2012-r2"></a>Para abrir el puerto 80 en Windows 7, Windows Server 2008 R2, Windows Server 2012 y 2012 R2  
  
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
  
14. En la página **Nombre** , escriba un nombre de**ReportServer (TCP en el puerto 80)**.  
  
15. Haga clic en **Finalizar**.  
  
16. Reinicie el equipo.  
  
#### <a name="to-open-port-80-on-windows-vista-or-windows-server-2008"></a>Para abrir el puerto 80 en Windows Vista o Windows Server 2008  
  
1.  Desde el **iniciar** menú, haga clic en **Panel de Control**, haga clic en **seguridad**y, a continuación, haga clic en **Windows Firewall**.  
  
2.  Haga clic en **permitir un programa a través de Firewall de Windows**.  
  
3.  Haga clic en **Continuar**.  
  
4.  En la ficha excepciones, haga clic en **agregar puerto**.  
  
5.  En nombre, escriba **ReportServer (TCP en el puerto 80)**.  
  
6.  En el número de puerto, escriba **80**.  
  
7.  Compruebe que **TCP** está seleccionada.  
  
8.  Haga clic en **Cambiar ámbito**.  
  
9. Haga clic en **sólo mi red (subred)** y, a continuación, haga clic en **Aceptar**.  
  
10. Haga clic en **Aceptar** para cerrar el cuadro de diálogo.  
  
11. Reinicie el equipo.  
  
## <a name="next-steps"></a>Pasos siguientes  
 Después de abrir el puerto y antes de confirmar si los usuarios remotos pueden tener acceso al servidor de informes en el puerto que abre, debe conceder acceso de usuario al servidor de informes a través de las asignaciones de roles en Inicio y en el nivel de sitio. Puede abrir un puerto correctamente y seguir teniendo conexiones del servidor de informes erróneas si los usuarios no tienen permisos suficientes. Para más información, vea [Conceder a un usuario acceso a un servidor de informes &#40;Administrador de informes&#41;](../security/grant-user-access-to-a-report-server.md) en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 También puede comprobar que el puerto se abre correctamente iniciando el Administrador de informes en un equipo diferente. Para más información, vea [Administrador de informes &#40;Modo nativo de SSRS&#41;](../report-manager-ssrs-native-mode.md) en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [Configurar la cuenta de servicio del servidor de informes &#40;Administrador de configuración de SSRS&#41;](../install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [Configurar las direcciones URL de servidor de informes &#40;Administrador de configuración de SSRS&#41;](../install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
 [Crear una base de datos del servidor de informes &#40;Administrador de configuración de SSRS&#41;](../../sql-server/install/create-a-report-server-database-ssrs-configuration-manager.md)   
 [Configurar la cuenta de servicio del servidor de informes &#40;Administrador de configuración de SSRS&#41;](../install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [Administración de un servidor de informes en modo nativo de Reporting Services](manage-a-reporting-services-native-mode-report-server.md)  
  
  
