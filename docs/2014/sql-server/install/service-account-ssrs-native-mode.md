---
title: (Modo nativo de SSRS) de la cuenta de servicio | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.serviceaccount.F1
ms.assetid: face8120-4d32-4c6c-a1e8-99f27d1ff15d
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 318e567e32ca66ba2d42e2e6333c8b2e2075f06c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66092180"
---
# <a name="service-account-ssrs-native-mode"></a>Cuenta de servicio (Modo nativo de SSRS)
  Utilice la página Cuenta de servicio para especificar la cuenta con la que se ejecuta el servicio del servidor de informes. Esta cuenta se configura inicialmente durante la instalación. Puede modificarla si desea cambiar la cuenta o la contraseña. El servicio web del servidor de informes, el Administrador de informes y la aplicación de procesamiento en segundo plano se ejecutan todos con la identidad del servicio que especifique en esta página.  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 La cuenta que especifica para el servicio Servidor de informes necesita permiso de acceso al Registro, a los archivos de programa del servidor de informes y a la base de datos del servidor de informes. Todos los permisos se configuran automáticamente para la cuenta cuando se usa el Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para establecer la cuenta. Si usa la cuenta de servicio para conectarse a la base de datos del servidor de informes, el Administrador de configuración crea un inicio de sesión de base de datos para la cuenta y configura los permisos de base de datos asignando la cuenta a RSExecRole en la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia que hospeda el base de datos de servidor de informes. La base de datos del servidor de informes es el único almacén de datos en el que un servidor de informes escribe. La cuenta de servicio no requiere permisos a cualquier otro almacén de datos.  
  
 Para abrir esta página, inicie el Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y seleccione el vínculo en el panel de navegación. Para obtener más información, vea [Administrador de configuración de Reporting Services &#40;modo nativo&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
> [!IMPORTANT]  
>  Siempre que tenga que actualizar la cuenta o la contraseña, se recomienda encarecidamente que emplee el Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . El uso del Administrador de configuración para actualizar la cuenta garantiza que los demás valores internos que dependan de la identidad del servicio se actualicen automáticamente al mismo tiempo.  
  
## <a name="options"></a>Opciones  
 **Usar una cuenta integrada**  
 Seleccione **Servicio de red**, **Sistema local**o **Servicio local** en la lista. Solo se recomienda **Servicio de red** ; sin embargo, puede configurar la cuenta para utilizar cualquier cuenta que esté disponible.  
  
 **Usar otra cuenta**  
 Seleccione esta opción para especificar una cuenta de usuario de Windows. Puede escribir una cuenta de usuario de Windows local o una cuenta de usuario de dominio. Especifique una cuenta de dominio con este formato:  *\<dominio >\\< usuario\>* . Especifique una cuenta de usuario de Windows local en este formato:  *\<nombre_equipo >\\< usuario\>* . Solo puede seleccionar una cuenta existente; no puede crear cuentas nuevas en Configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 El límite máximo es 20 caracteres para la cuenta.  
  
 Si la red utiliza la autenticación Kerberos y se configura el servidor de informes para ejecutarse en una cuenta de usuario de dominio, debe registrar el servicio con la cuenta de usuario. Para más información, vea [Registrar un nombre de entidad de seguridad de servicio &#40;SPN&#41; para un servidor de informes](../../reporting-services/report-server/register-a-service-principal-name-spn-for-a-report-server.md).  
  
 Si cambia el tipo de cuenta (por ejemplo, reemplazando una cuenta de Windows por otra o una cuenta integrada por una cuenta de dominio de Windows), se le pedirá que cree una copia de seguridad de la clave de cifrado. La copia de seguridad se restaurará automáticamente cuando seleccione la cuenta nueva.  
  
> [!NOTE]  
>  El Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] pregunta si se desea realizar una copia de seguridad y restaurar la clave de cifrado cada vez que se modifica la cuenta del servicio. Estos pasos son necesarios para asegurar que los datos cifrados permanecen disponibles para el servidor de informes. Para obtener más información acerca de estas acciones, consulte [las claves de cifrado &#40;modo nativo de SSRS&#41;](../../../2014/sql-server/install/encryption-keys-ssrs-native-mode.md).  
  
 Además, si tiene un servidor de informes que está configurado para ejecutarse en modo integrado de SharePoint y cambia la cuenta de servicio mediante el Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , debe abrir también Administración central de SharePoint y usar la página [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] **de** para volver a aplicar la configuración del servidor de informes y de la instancia. Este paso permitirá el acceso de la nueva cuenta de servicio a las bases de datos de SharePoint, lo que es necesario para integrar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] con una tecnología o producto de SharePoint. Para obtener más información acerca de cómo conceder acceso a la base de datos en Administración Central de SharePoint, vea [configuración y administración de un servidor de informes &#40;Reporting Services SharePoint Mode&#41; ](../../../2014/reporting-services/configure-administer-report-server-reporting-services-sharepoint-mode.md) y [ Instalación en modo de SharePoint de Reporting Services &#40;SharePoint 2010 y SharePoint 2013&#41;](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md).  
  
## <a name="choosing-an-account"></a>Elegir una cuenta  
 Para obtener los mejores resultados, especifique una cuenta que tenga permisos de conexión de red, con acceso a los controladores de dominio de la red y a servidores SMTP corporativos o puertas de enlace. En la tabla siguiente se resumen las cuentas y se proporcionan recomendaciones para utilizarlas.  
  
|Cuenta|Explicación|  
|-------------|-----------------|  
|Cuentas de usuario de dominio|Si tiene una cuenta de usuario de dominio de Windows que tenga los permisos mínimos requeridos para las operaciones del servidor de informes, debería utilizarla.<br /><br /> Se recomienda emplear una cuenta de usuario de dominio porque aísla el servicio Servidor de informes de otras aplicaciones. Al ejecutar varias aplicaciones en una cuenta compartida, como Servicio de red, se aumenta el riesgo de que un usuario malintencionado tome el control del servidor de informes gracias a que una infracción de seguridad de una aplicación se pueda extender con facilidad a todas las aplicaciones que se ejecutan en la misma cuenta.<br /><br /> Se requiere una cuenta de usuario de dominio si va a configurar el servidor de informes para la delegación limitada, o para el modo integrado de SharePoint con productos de SharePoint 2010 que requieren cuentas de usuario de dominio en lugar de cuentas de equipo integradas.<br /><br /> Tenga en cuenta que si usa una cuenta de usuario de dominio, tendrá que cambiar la contraseña periódicamente si la organización exige una directiva de expiración de las contraseñas. También es posible que tenga que registrar el servicio con la cuenta de usuario. Para más información, vea [Registrar un nombre de entidad de seguridad de servicio &#40;SPN&#41; para un servidor de informes](../../reporting-services/report-server/register-a-service-principal-name-spn-for-a-report-server.md).<br /><br /> Evite utilizar una cuenta de usuario de Windows local. Las cuentas locales no suelen contar con los permisos suficientes para tener acceso a los recursos de otros equipos. Para obtener más información sobre el modo en que el uso de una cuenta local limita la funcionalidad del servidor de informes, vea [Consideraciones para usar cuentas locales](#localaccounts) en este tema.|  
|**Servicio de red**|**Servicio de red** es una cuenta integrada con privilegios mínimos que tiene permisos de inicio de sesión en red. Esta cuenta se recomienda si no tiene una cuenta de usuario de dominio disponible o si desea evitar cualquier interrupción del servicio que podría producirse como resultado de las directivas de expiración de las contraseñas.<br /><br /> Si selecciona **Servicio de red**, intente reducir el número de servicios adicionales que se ejecutan en la misma cuenta. Una infracción de seguridad de cualquier aplicación pondrá en peligro la seguridad de todas las demás aplicaciones que se ejecuten en la misma cuenta.|  
|**Servicio local**|**Servicio local** es una cuenta integrada similar a una cuenta de usuario de Windows local autenticada. Los servicios que se ejecutan como cuenta **Servicio local** tienen acceso a los recursos de red como una sesión nula sin credenciales. Esta cuenta no es adecuada para los escenarios de implementación con intranets en los que el servidor de informes deba conectarse a una base de datos del servidor de informes remota o a un controlador de dominio de la red para autenticar a un usuario antes de abrir un informe o procesar una suscripción.|  
|**Sistema local**|**Sistema local** es una cuenta con muchos privilegios que no es necesaria para ejecutar un servidor de informes. No utilice esta cuenta para instalaciones de servidor de informes. En su lugar, elija una cuenta de dominio o **Servicio de red** .|  
  
##  <a name="localaccounts"></a> Consideraciones para usar cuentas locales  
 La consideración principal para utilizar cuentas locales es si el servidor de informes requiere acceso a controladores de dominio, servidores de correo y servidores de bases de datos remotos. Si configura el servidor de informes para ejecutarse en una cuenta de usuario de Windows local, Servicio local o Sistema local, introduce consideraciones que deben tenerse en cuenta para establecer otra configuración, y en la creación y entrega de las suscripciones:  
  
-   Si el servicio se ejecuta con una cuenta local, se limitarán las opciones posteriormente si configura una conexión a la base de datos de un servidor de informes remoto. Concretamente, si utiliza la base de datos de un servidor de informes remoto, tendrá que configurar la conexión para utilizar una cuenta de usuario de dominio o un usuario de base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que tenga permiso para iniciar sesión en la instancia remota de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Si el servicio se ejecuta con una cuenta local, se impondrán nuevos requisitos a la creación de suscripciones. El servidor de informes almacena información acerca del usuario que crea la suscripción. Si el usuario crea la suscripción habiendo iniciado la sesión con una cuenta de dominio, el servicio Servidor de informes intentará conectarse a un controlador de dominio para autenticar al usuario cuando la suscripción se procese. Si el servicio Servidor de informes se ejecuta con una cuenta local, la solicitud de autenticación dará error cuando el servidor de informes intente enviarla a un controlador de dominio remoto. Para subsanar esta limitación se puede usar una extensión de autenticación basada en formularios personalizada, o bien hacer que todos los usuarios se conecten a un servidor de informes con una cuenta de usuario local.  
  
-   Si el servicio se ejecuta con una cuenta local, se impondrán nuevos requisitos a la entrega de suscripciones. Algunas extensiones de entrega tienen información de cuenta de usuario en la definición de la suscripción. Si se envían informes a direcciones de correo electrónico que se basen en cuentas de usuario de dominio y se ejecuta el servicio Servidor de informes con una cuenta local, este no podrá obtener acceso a un controlador de dominio remoto para resolver la cuenta de correo electrónico de destino.  
  
-   Las cuentas de servicio de Windows integradas (Servicio local o Servicio de red) no se admiten como cuentas de servicio del servidor de informes en un equipo que sea controlador de dominio.  
  
## <a name="see-also"></a>Vea también  
 [Configurar la cuenta de servicio del servidor de informes &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [Configurar una cuenta de servicio &#40;Administrador de configuración de SSRS&#41;](../../../2014/sql-server/install/configure-a-service-account-ssrs-configuration-manager.md)   
 [Temas de Ayuda de F1 de administrador de configuración de Reporting Services &#40;modo nativo de SSRS&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)  
  
  
