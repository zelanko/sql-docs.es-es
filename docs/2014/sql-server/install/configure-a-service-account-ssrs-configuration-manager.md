---
title: Configurar una cuenta de servicio (Administrador de configuración de SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Report Server Web service, accounts
- service accounts [Reporting Services]
- Report Server Windows service, accounts
- Web service [Reporting Services], report server
ms.assetid: 25000ad5-3f80-4210-8331-d4754dc217e0
caps.latest.revision: 7
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: a8f16a73e32557345086a3363e619e56891f1c65
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37234495"
---
# <a name="configure-a-service-account-ssrs-configuration-manager"></a>Configurar una cuenta de servicio (Administrador de configuración de SSRS)
  En una instalación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], el servicio web del servidor de informes, el Administrador de informes y la aplicación de procesamiento en segundo plano se ejecutan dentro de un único servicio. La cuenta en la que el servicio se ejecuta se define durante la instalación, al especificar la cuenta en la página Identidad de servicio, pero puede utilizar la herramienta Configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] si desea usar una cuenta diferente o actualizar la contraseña.  
  
 Si tiene un servidor de informes está configurado para usar el modo integrado de SharePoint y cambiar la cuenta de servicio mediante el [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] herramienta de configuración, también debe abrir Administración Central de SharePoint y usar el [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  **Conceder acceso a la base de datos** página para volver a aplicar la configuración de instancia y el servidor de informes. Este paso, concederá la nueva cuenta service acceso a las bases de datos de SharePoint, que es necesaria para integrar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] con [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] o [!INCLUDE[SPS2010](../../includes/sps2010-md.md)].  
  
 Use siempre la herramienta Configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para actualizar la cuenta de servicio y que se pueda actualizar simultáneamente otra configuración que dependa de la identidad del servicio.  
  
> [!NOTE]  
>  Las cuentas de servicio de Windows integradas (Servicio local o Servicio de red) no se admiten como cuentas de servicio del servidor de informes en un equipo que sea controlador de dominio.  
  
 Procedimientos  
  
### <a name="to-configure-the-report-server-service-account"></a>Configurar la cuenta del servicio Servidor de informes  
  
1.  Inicie el Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y conéctese al servidor de informes.  
  
2.  En la página Cuenta de servicio, seleccione la opción que describa el tipo de cuenta que desea utilizar. Para obtener recomendaciones sobre qué tipo de cuenta para especificar, vea [configurar la cuenta de servicio del servidor de informes &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md).  
  
3.  Si seleccionó una cuenta de usuario de Windows, especifique la nueva cuenta y la contraseña. La cuenta no puede tener más de 20 caracteres.  
  
     Si el servidor de informes se implementa en una red que admite la autenticación Kerberos, debe registrar el Nombre principal de servicio (SPN) del servidor de informes con la cuenta de usuario de dominio recién especificada. Para más información, vea [Registrar un nombre de entidad de seguridad de servicio &#40;SPN&#41; para un servidor de informes](../../reporting-services/report-server/register-a-service-principal-name-spn-for-a-report-server.md).  
  
4.  Haga clic en **Aplicar**.  
  
5.  Cuando el sistema pida que cree una copia de seguridad de la clave simétrica, escriba un nombre de archivo y una ubicación para la copia de seguridad, escriba una contraseña para bloquear y desbloquear el archivo y haga clic en **Aceptar**.  
  
6.  Si el servidor de informes utiliza la cuenta de servicio para conectarse a su base de datos, la información de la conexión se actualizará para utilizar la nueva cuenta o contraseña. Para actualizar la información de la conexión se requiere que se conecte a la base de datos. Si aparece el cuadro de diálogo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Database Connection** dialog box appears, enter credentials that have permission to connect to the database, and then click **OK**.  
  
7.  Cuando el sistema pida confirmación para restaurar la clave simétrica, escriba la contraseña que especificó en el paso 5 y haga clic en **Aceptar**.  
  
8.  Revise los mensajes de estado en el panel Resultados para comprobar que todas las tareas se completaron correctamente.  
  
## <a name="troubleshooting-service-identity-update-errors"></a>Solucionar los errores de actualización de la identidad de servicio  
 Al cambiar la identidad del servicio, si usa la cuenta de servicio para conectarse a la base de datos del servidor de informes, se inicia una serie de eventos que incluyen el reinicio del servicio, la actualización de la clave de cifrado protegida mediante contraseña, la actualización de las reservas de direcciones URL y la actualización de la información de conexión de base de datos del servidor de informes. Puede supervisar el estado de estos eventos viendo las notificaciones del panel Resultados en la parte inferior de la página. Si se producen errores durante este proceso, puede intentar resolverlos utilizando las técnicas siguientes:  
  
-   Si no se puede restaurar la clave simétrica, puede intentar restaurarla manualmente mediante la opción **Restaurar** de la página Claves de cifrado. Si eso no funciona, considere eliminar el contenido cifrado. Tendrá que volver a crear la información de la conexión a un origen de datos y las suscripciones, pero el resto del contenido seguirá estando disponible. Para obtener más información, vea [Hacer copia de seguridad y restaurar claves de cifrado de Reporting Services](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md).  
  
-   Si el servicio no se inicia, reinícielo manualmente con la aplicación de consola Servicios en Herramientas del administrador.  
  
-   Pueden producirse errores de la reserva de direcciones URL al actualizar la cuenta de servicio. Cada reserva de direcciones URL incluye un descriptor de seguridad que incluye una Lista de control de acceso discrecional (DACL) que concede permisos a la cuenta de servicio para aceptar las solicitudes en la dirección URL. Al actualizar la cuenta, la dirección URL se debe volver a crear para actualizar la DACL con la información de la nueva cuenta. Si no se puede volver a crear la reserva de direcciones URL, y sabe que la cuenta es válida, intente reiniciar el equipo. Si el error persiste, intente utilizar una cuenta diferente.  
  
## <a name="see-also"></a>Vea también  
 [Administrador de configuración de Reporting Services &#40;modo nativo&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)   
 [Configurar la cuenta de servicio del servidor de informes &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [Configurar una conexión de base de datos del servidor de informes &#40;Administrador de configuración de SSRS&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [Cuenta de servicio &#40;modo nativo de SSRS&#41;](../../../2014/sql-server/install/service-account-ssrs-native-mode.md)   
 [Configurar y administrar claves de cifrado &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)  
  
  
