---
title: Configurar la cuenta de servicio del servidor de informes (Administrador de configuración de SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: f880c623-67c8-4167-b98b-ace17e800faa
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 546cf8172cbfc2e13b0953207078f3b2cc9dc146
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48082526"
---
# <a name="configure-the-report-server-service-account-ssrs-configuration-manager"></a>Configurar la cuenta de servicio del servidor de informes (Administrador de configuración de SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] se implementa como un servicio único que contiene el servicio web del servidor de informes, el Administrador de informes y una aplicación de procesamiento en segundo plano que se usa para el procesamiento programado de informes y la entrega de suscripciones. En este tema se explica cómo se configura inicialmente la cuenta de servicio y cómo modificar la cuenta o la contraseña con la herramienta Configuración de Reporting Services.  
  
## <a name="initial-configuration"></a>Configuración inicial  
 La cuenta del servicio Servidor de informes se define durante la instalación. Puede ejecutar el servicio en una cuenta de usuario de dominio o un integrada, como `NetworkService` cuenta. No hay ninguna cuenta predeterminada; cualquier cuenta que especifique en el [configuración del servidor - cuentas de servicio](../../sql-server/install/server-configuration-service-accounts.md) página del Asistente para instalación se convierte en la cuenta inicial del servicio servidor de informes.  
  
> [!IMPORTANT]  
>  Aunque el servicio Web del servidor de informes y el Administrador de informes son [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] aplicaciones, no se ejecutan bajo la [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] cuenta. Una única arquitectura de servicios ejecuta ambas aplicaciones ASP.NET dentro de la misma identidad del proceso Servidor de informes. Esto supone un cambio importante con respecto a las versiones anteriores, en las que el servicio web del servidor de informes y el Administrador de informes se ejecutaban con la identidad del proceso de trabajo [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] especificada en IIS.  
  
## <a name="changing-the-service-account"></a>Cambiar la cuenta de servicio  
 Ver y reconfigurar la información de la cuenta del servicio, utilice siempre la herramienta Configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. La información de la identidad del servicio se almacena internamente en varias ubicaciones. El uso de la herramienta garantiza que todas las referencias se actualizan en consecuencia siempre que se cambia la cuenta o la contraseña. La herramienta Configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] lleva a cabo los siguientes pasos adicionales para garantizar que el servidor de informes permanece disponible:  
  
-   Agrega automáticamente la cuenta nueva al grupo de servidores de informes que se crea en el equipo local. Este grupo se especifica en las listas de control de acceso (ACL) que protegen los archivos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
-   Actualiza automáticamente los permisos de inicio de sesión en la instancia del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] que se utiliza para hospedar la base de datos del servidor de informes. La cuenta nueva se agregará a **RSExecRole**.  
  
     El inicio de sesión de la base de datos de la cuenta anterior no se quitará automáticamente. Asegúrese de quitar las cuentas que ya no se usen. Para más información, vea [Administrar una base de datos del servidor de informes &#40;modo nativo de SSRS&#41;](../report-server/report-server-database-ssrs-native-mode.md) en los Libros en pantalla de SQL Server.  
  
     Solo se conceden permisos de base de datos a la nueva cuenta de servicio si la conexión de base de datos del servidor de informes se configuró para utilizar la cuenta de servicio en primer lugar. Si la conexión de base de datos del servidor de informes se configuró para utilizar una cuenta de usuario de dominio o un inicio de sesión de base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , la actualización de la cuenta de servicio no afecta a la información de conexión.  
  
-   Actualiza automáticamente la clave de cifrado para incluir la información de perfil de la nueva cuenta.  
  
    > [!NOTE]  
    >  Si el servidor de informes forma parte de la implementación escalada, solo resultará afectado el servidor de informes que se está actualizando. El cambio de cuenta de servicio no afecta a las claves de cifrado de otros servidores de informes de la implementación.  
  
 Para obtener instrucciones sobre cómo establecer la cuenta, consulte [configurar una cuenta de servicio &#40;SSRS Configuration Manager&#41;](../../sql-server/install/configure-a-service-account-ssrs-configuration-manager.md).  
  
## <a name="choosing-an-account"></a>Elegir una cuenta  
 Puede configurar el servicio Servidor de informes para ejecutarse en cualquiera de estos tipos de cuenta:  
  
-   Cuenta de usuario de Windows con privilegios mínimos  
  
-   NetworkService (Servicio de red)  
  
-   LocalSystem (Sistema local)  
  
-   LocalService (Servicio local)  
  
 No existe una única opción que sea la más adecuada para elegir un tipo de cuenta. Cada cuenta tiene ventajas y desventajas que deben sopesarse. Si está implementando [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en un servidor de producción, los procedimientos recomendados sugieren que se configure el servicio para ejecutarse bajo una cuenta de usuario de dominio para que pueda evitar daños se extiendan si un usuario malintencionado pone en peligro una cuenta compartida. Esto también facilita auditar la actividad de inicio de sesión en esta cuenta. Una desventaja de usar una cuenta de usuario de Windows es que si está implementando [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en una red que usa la autenticación Kerberos, debe registrar el servicio con la cuenta de usuario. Para más información, vea [Registrar un nombre de entidad de seguridad de servicio &#40;SPN&#41; para un servidor de informes](../report-server/register-a-service-principal-name-spn-for-a-report-server.md).  
  
 Las siguientes directrices y los vínculos de esta sección pueden ayudarle a elegir la solución que mejor se adapte a su implementación.  
  
-   [Cuenta de servicio &#40;modo nativo de SSRS&#41;](../../sql-server/install/service-account-ssrs-native-mode.md).  
  
-   [Configurar los permisos y las cuentas de servicio de Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md) en los Libros en pantalla de SQL Server.  
  
-   [Guía de planeamiento de la seguridad de servicios y cuentas de servicio](http://go.microsoft.com/fwlink/?LinkId=69155) de MSDN  
  
## <a name="updating-an-expired-password"></a>Actualizar una contraseña que ha expirado  
 Si el servicio Servidor de informes se ejecuta en una cuenta de dominio y la contraseña expira antes de que pueda actualizarla en la herramienta Configuración de Reporting Services, el servicio no se iniciará hasta que especifique una contraseña nueva. Si el servicio no se puede iniciar, no puede utilizar la herramienta Configuración de Reporting Services para conectarse a ese servidor y actualizar la cuenta. En este caso, debe utilizar una combinación de herramientas para volver a poner en conexión el servidor.  
  
 Para restablecer la contraseña, haga lo siguiente:  
  
1.  En el **iniciar** menú, elija **Panel de Control**, apunte a **herramientas administrativas**y haga clic en **servicios**.  
  
2.  Haga clic en **SQL Server Reporting Services**, seleccione **propiedades**.  
  
3.  Haga clic en **iniciar sesión**y escriba la nueva contraseña.  
  
4.  Una vez actualizada la contraseña, inicie la herramienta Configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y actualice la contraseña en la página Cuenta de servicio. Este paso adicional es necesario para actualizar la información de cuenta almacenada internamente por el servidor de informes.  
  
 Si expira la contraseña de la cuenta de servicio de [!INCLUDE[ssDE](../../includes/ssde-md.md)], se produce el error `rsReportServerDatabaseUnavailable` al intentar conectarse al servidor de informes. Restablecer la contraseña resuelve este error.  
  
## <a name="configuring-the-report-server-service-for-a-sharepoint-integrated-report-server"></a>Configurar el servicio Servidor de informes para un servidor de informes integrado de SharePoint  
 Si ejecuta un servidor de informes en el modo integrado de SharePoint, debe actualizar la información de la cuenta de servicio que está almacenada en la base de datos de configuración de SharePoint, si se cumple alguna de las condiciones siguientes:  
  
-   Modificar el [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] cuenta (por ejemplo, cambiar de NetworkService a una cuenta de usuario de dominio) del servicio.  
  
-   Se extiende un conjunto de SharePoint para que incluya una aplicación web de SharePoint adicional. Si el conjunto de servidores está configurado para la integración del servidor de informes, y se configura una aplicación recién agregada para que se ejecute en una cuenta de usuario diferente a la de las demás aplicaciones del conjunto, debe actualizar la información del acceso a las bases de datos.  
  
 Tras restablecer la información de acceso a las bases de datos, debe reiniciar el servicio  [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] para asegurarse de que ya no se use la conexión antigua.  
  
1.  En **herramientas administrativas**, haga clic en **SharePoint 2010 Central Administration**.  
  
2.  Haga clic en **administración de aplicaciones**.  
  
3.  En la sección Reporting Services, haga clic en **conceder acceso a la base de datos**.  
  
4.  Haga clic en **Aceptar**. Aparecerá el cuadro de diálogo Especificar credenciales.  
  
5.  Escriba las credenciales de un usuario que sea miembro del grupo de administradores locales en el equipo que hospeda el servidor de informes. Las credenciales se usarán para una sola conexión al equipo del servidor de informes con el propósito de recuperar información de la cuenta de servicio. El inicio de sesión de la base de datos que se crea para cada cuenta de servicio se actualizará en las bases de datos de SharePoint.  
  
6.  Para reiniciar el servicio, haga clic en **operaciones**.  
  
7.  En la topología y servicios, haga clic en **servicios en el servidor**.  
  
8.  Para la aplicación Web de Windows SharePoint Services, haga clic en **detener**.  
  
9. Espere a que se detenga el servicio.  
  
10. Haga clic en **iniciar**.  
  
> [!NOTE]  
>  Las tecnologías y productos de SharePoint requieren cuentas de dominio para la configuración de servicios como el modo de SharePoint los servicios de informes.  
  
## <a name="see-also"></a>Vea también  
 [Configurar una cuenta de servicio &#40;Administrador de configuración de SSRS&#41;](../../sql-server/install/configure-a-service-account-ssrs-configuration-manager.md)   
 [Cuenta de servicio &#40;modo nativo de SSRS&#41;](../../sql-server/install/service-account-ssrs-native-mode.md)   
 [Configurar las direcciones URL de servidor de informes &#40;Administrador de configuración de SSRS&#41;](configure-report-server-urls-ssrs-configuration-manager.md)   
 [Administrador de configuración de Reporting Services &#40;modo nativo&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)  
  
  
