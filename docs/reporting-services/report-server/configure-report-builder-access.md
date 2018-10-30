---
title: Configurar el acceso al Generador de informes | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services, Report Builder
- Report Builder 1.0, configuring access
- configuring servers [Reporting Services]
ms.assetid: a79003d0-c905-4d4c-9560-93a7cc1e1dd4
author: markingmyname
ms.author: maghan
ms.openlocfilehash: f980f4bb625fb0686911c7aa1cad28ca574faaf6
ms.sourcegitcommit: 3daacc4198918d33179f595ba7cd4ccb2a13b3c0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/25/2018
ms.locfileid: "50030954"
---
# <a name="configure-report-builder-access"></a>Configurar el acceso al Generador de informes
  El Generador de informes es una herramienta de notificación ad hoc que se instala con un servidor de informes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] configurado para modo nativo o para modo de integración con SharePoint.  
  
 El acceso al Generador de informes depende de los factores siguientes:  
  
-   Propiedades de servidor que determinen si el Generador de informes está disponible en el servidor de informes.  
  
-   Asignaciones de roles o permisos que hacen que el Generador de informes esté disponible para grupos o usuarios individuales.  
  
-   Configuración de autenticación que determina si las credenciales del usuario se pueden pasar al servidor de informes o está configurado el acceso anónimo en los archivos de la aplicación.  
  
 Para utilizar el Generador de informes, debe tener un modelo de informe publicado con el que trabajar.  
  
## <a name="prerequisites"></a>Prerequisites  
 El Generador de informes no está disponible en todas las ediciones de [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Características compatibles con las ediciones de SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 El equipo cliente debe tener instalado [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 2.0. [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] proporciona la infraestructura para ejecutar aplicaciones [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] .  
  
 Debe utilizar [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Explorer 6.0 o posterior.  
  
 El Generador de informes siempre se ejecuta con confianza total; no se puede configurar para ejecutarse con confianza parcial. En las versiones anteriores, era posible que el Generador de informes se ejecutara con confianza parcial, pero esa opción no se admite en [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y en versiones posteriores.  
  
## <a name="enabling-and-disabling-report-builder"></a>Habilitar y deshabilitar el Generador de informes  
 El Generador de informes está habilitado de manera predeterminada. Los administradores del servidor de informes tienen la posibilidad de deshabilitar la característica Generador de informes; para ello, deben establecer la propiedad del sistema **EnableReportDesignClientDownload** del servidor de informes en **false**. De esta manera, se deshabilitan las descargas del Generador de informes para ese servidor de informes.  
  
 Para establecer las propiedades del sistema del servidor de informes, puede usar Management Studio o script:  
  
-   Para utilizar Management Studio, conéctese al servidor de informes y utilice la página Avanzadas de Propiedades del servidor con el fin de establecer **EnableReportDesignClientDownload** en **false**. Para más información sobre cómo abrir esta página, vea [Establecer las propiedades del servidor de informes &#40;Management Studio&#41;](../../reporting-services/tools/set-report-server-properties-management-studio.md).  
  
-   Para ver un script de ejemplo donde se configura una propiedad del servidor de informes, consulte [Script para tareas administrativas y de implementación](../../reporting-services/tools/script-deployment-and-administrative-tasks.md).  
  
## <a name="role-assignments-granting-report-builder-access-on-a-native-mode-report-server"></a>Asignaciones de roles que conceden acceso al Generador de informes en un servidor de informes en modo nativo  
 En un servidor de informes en modo nativo, cree asignaciones de roles de usuario que incluyan las tareas para utilizar el Generador de informes. Debe ser administrador de contenido y administrador del sistema para crear o modificar definiciones y asignaciones de roles en los elementos y en el nivel de sitio.  
  
 En las instrucciones siguientes se supone que se utilizan roles predefinidos. Si ha modificado las definiciones de roles o ha realizado la actualización a partir de SQL Server 2000, compruebe si los roles contienen las tareas necesarias. Para más información sobre cómo crear asignaciones de roles, vea [Conceder a un usuario acceso a un servidor de informes &#40;Administrador de informes&#41;](../../reporting-services/security/grant-user-access-to-a-report-server-report-manager.md).  
  
 Después de crear las asignaciones de roles, los usuarios tendrán permiso para hacer lo siguiente:  
  
-   Los usuarios asignados a los roles Usuario del sistema y Explorador pueden ver los informes del Generador de informes publicados en un servidor de informes, sin tener que iniciar el Generador de informes.  
  
-   Los usuarios asignados a los roles Usuario del sistema y Generador de informes pueden generar modelos, iniciar el Generador de informes y crear informes, así como guardar informes en el servidor de informes.  
  
-   Los usuarios asignados a los roles Usuario del sistema y Publicador pueden publicar modelos del Diseñador de modelos en el servidor de informes. Los modelos se utilizan como orígenes de datos en el Generador de informes.  
  
-   Los usuarios asignados a los roles Administrador del sistema y Administrador de contenido tienen todos los permisos para crear, ver y administrar informes del Generador de informes.  
  
#### <a name="to-verify-required-tasks-are-in-the-role-definitions"></a>Para comprobar que las tareas necesarias están en las definiciones de roles  
  
1.  Inicie Management Studio y conéctese al servidor de informes.  
  
2.  Abra la carpeta **Seguridad** .  
  
3.  Abra la carpeta **Roles del sistema** .  
  
4.  Haga clic con el botón derecho en **Administrador del sistema**y seleccione **Propiedades**.  
  
5.  Seleccione **Ejecutar definiciones de informe** y haga clic en **Aceptar**.  
  
6.  Haga clic con el botón derecho en **Usuario del sistema**y seleccione **Propiedades**.  
  
7.  Seleccione **Ejecutar definiciones de informe** y haga clic en **Aceptar**.  
  
8.  Abra la carpeta **Roles** .  
  
9. Haga clic con el botón derecho en **Explorador**y seleccione **Propiedades**.  
  
10. Seleccione **Ver modelos** y haga clic en **Aceptar**.  
  
11. Haga clic con el botón derecho en **Administrador de contenido**y seleccione **Propiedades**.  
  
12. Seleccione **Ver modelos**, **Administrar modelos**, **Usar informes**y haga clic en **Aceptar**.  
  
13. Haga clic con el botón derecho en **Publicador**y seleccione **Propiedades**.  
  
14. Seleccione **Administrar modelos** y haga clic en **Aceptar**.  
  
15. Cree el rol del Generador de informes, si no existe:  
  
    1.  Abra la carpeta **Seguridad** .  
  
    2.  Haga clic con el botón derecho en **Roles**y seleccione **Nuevo rol**.  
  
    3.  En Nombre, escriba **Generador de informes**.  
  
    4.  En Descripción, escriba la descripción del rol de modo que los usuarios del Administrador de informes sepan para qué sirve.  
  
    5.  Agregue las tareas siguientes: **Usar informes**, **Ver informes**, **Ver modelos**, **Ver recursos**, **Ver carpetas**y **Administrar suscripciones individuales**.  
  
    6.  Haga clic en **Aceptar** para guardar el rol.  
  
#### <a name="to-create-role-assignments-that-grant-access-to-report-builder"></a>Para crear asignaciones de roles que concedan acceso al Generador de informes  
  
1.  Inicie el Administrador de informes.  
  
2.  Haga clic en **Configuración del sitio**.  
  
3.  Haga clic en **Seguridad**.  
  
4.  Si ya existe una asignación de roles para el usuario o el grupo cuyo acceso al Generador de informes desea configurar, haga clic en **Editar**.  
  
     De lo contrario, haga clic en **Nueva asignación de roles**. En Grupo o usuario, escriba una cuenta de grupo o de usuario de dominio de Windows con este formato: \<dominio>\\<cuenta\>. Si utiliza la autenticación de formularios o la seguridad personalizada, especifique la cuenta de grupo o de usuario en el formato correcto para su implementación.  
  
5.  Seleccione **Usuario del sistema**y, a continuación, haga clic en **Aceptar**.  
  
6.  Haga clic en **Inicio**.  
  
7.  Haga clic en la pestaña **Configuración de carpeta** .  
  
8.  Haga clic en la pestaña **Seguridad** .  
  
9. Si ya existe una asignación de roles para el usuario o el grupo cuyo acceso al Generador de informes desea configurar, haga clic en **Editar**.  
  
     De lo contrario, haga clic en **Nueva asignación de roles**. En Grupo o usuario, escriba una cuenta de grupo o de usuario de dominio de Windows con este formato: \<dominio>\\<cuenta\>. Si utiliza la autenticación de formularios o la seguridad personalizada, especifique la cuenta de grupo o de usuario en el formato correcto para su implementación.  
  
10. Seleccione **Generador de informes**y haga clic en **Aplicar**.  
  
11. Repita el proceso para crear o modificar asignaciones de roles para otros usuarios o grupos.  
  
## <a name="permissions-granting-report-builder-access-on-a-sharepoint-integrated-mode-report-server"></a>Permisos que conceden acceso al Generador de informes en un servidor de informes en modo integrado de SharePoint  
 En un servidor de informes en modo integrado de SharePoint, el acceso al Generador de informes se concede a los usuarios de SharePoint que tienen los niveles de permisos Colaborar o Control total.  
  
 Si utiliza niveles de permisos personalizados, debe incluir Agregar elementos y Editar elementos en el nivel de permisos. Para más información sobre el acceso al Generador de informes con los niveles de permisos integrados, vea [Usar la seguridad integrada de Windows SharePoint Services para los elementos del servidor de informes](../../reporting-services/security/use-built-in-security-in-windows-sharepoint-services-for-report-server-items.md). Para más información sobre los requisitos de permisos para niveles de permisos personalizados, vea [Establecer permisos para las operaciones del servidor de informes en una aplicación web de SharePoint](../../reporting-services/security/set-permissions-for-report-server-operations-in-a-sharepoint-web-application.md).  
  
## <a name="authentication-considerations-and-credential-reuse"></a>Consideraciones de autenticación y reutilización de credenciales  
 El Generador de informes utiliza la tecnología ClickOnce para descargar e instalar los archivos de aplicación propios en un equipo cliente. La finalidad de la tecnología ClickOnce es la implementación de aplicaciones unidireccional que coloca archivos de programa en un equipo cliente y ejecuta la aplicación como un proceso independiente bajo la identidad del usuario predeterminado. Dado que el Generador de informes debe conectarse de nuevo al servidor de informes para obtener los archivos de aplicación y los datos del servidor de informes, es importante entender cómo establece ClickOnce el contexto de seguridad y cómo emite las solicitudes a los equipos remotos en escenarios diferentes:  
  
-   ClickOnce siempre se ejecuta como un proceso independiente en el equipo cliente. La identidad del proceso son las credenciales de usuario de Windows predeterminadas. ClickOnce no comparte los datos de la sesión con Internet Explorer ni obtiene el contexto de seguridad de usuario actual de Internet Explorer.  
  
-   ClickOnce envía las solicitudes que especifican la seguridad integrada de Windows en el encabezado de autenticación. Si un servidor se configura para un tipo de autenticación diferente, el servidor emitirá un error de autenticación con las solicitudes de ClickOnce. Para evitar este problema, debe configurar un servidor para la seguridad integrada de Windows o permitir al acceso anónimo para eliminar la comprobación de autenticación.  
  
-   El Generador de informes abre su propia conexión a un servidor de informes. Si no se usa la seguridad integrada de Windows con un único inicio de sesión, los usuarios deben volver a escribir sus credenciales para la conexión del Generador de informes con el servidor de informes.  
  
 En la tabla siguiente se describen los tipos de autenticación que admite el servidor de informes y si se necesita configuración adicional para tener acceso al Generador de informes.  
  
|Tipo de autenticación del servidor de informes|Cómo responde el iniciador de aplicaciones ClickOnce y el Generador de informes|  
|---------------------------------------|--------------------------------------------------------------------|  
|Negotiate (valor predeterminado)<br /><br /> NTLM (valor predeterminado)|Con la seguridad integrada de Windows, las solicitudes autenticadas de ClickOnce y del Generador de informes suelen tener éxito si el cliente y el servidor están implementados en el mismo dominio, el usuario inicia sesión en el equipo cliente utilizando una cuenta de dominio con permiso para tener acceso al Generador de informes y el servidor de informes se configura para la autenticación de Windows.<br /><br /> Las solicitudes tienen éxito porque ClickOnce y la conexión del explorador con el servidor de informes tienen la misma identidad de usuario.<br /><br /> Se producirá un error en las solicitudes si el usuario ha abierto Internet Explorer con Ejecutar como y ha especificado credenciales no predeterminadas. Si la sesión de usuario en el servidor de informes se establece bajo una cuenta concreta y ClickOnce se ejecuta en una cuenta diferente, el servidor de informes denegará el acceso a los archivos.|  
|Kerberos|Internet Explorer, que es necesario para utilizar el Generador de informes, no admite directamente Kerberos.|  
|Autenticación básica|ClickOnce no admite la autenticación básica. No formulará solicitudes que especifiquen la autenticación básica en el encabezado de autenticación. No pasará credenciales ni pedirá al usuario que las proporcione. Estos problemas se pueden evitar habilitando el acceso anónimo a los archivos de aplicación del Generador de informes.<br /><br /> Las solicitudes tendrán éxito si se habilita el acceso anónimo a los archivos de aplicación del Generador de informes porque el servidor de informes omite el encabezado de autenticación. Para más información sobre cómo habilitar el acceso anónimo al Generador de informes, vea [Configurar la autenticación básica en el servidor de informes](../../reporting-services/security/configure-basic-authentication-on-the-report-server.md).<br /><br /> Una vez que ClickOnce recupera los archivos de aplicación, el Generador de informes abre una conexión independiente con un servidor de informes. Los usuarios deben volver a escribir sus credenciales para conseguir que el Generador de informes se conecte al servidor de informes. El Generador de informes no recopila credenciales de Internet Explorer o de ClickOnce.<br /><br /> Se producirá un error en las solicitudes si el servidor de informes se configura para la autenticación básica y no se ha habilitado el acceso anónimo a los archivos de programa del Generador de informes. Se produce un error en la solicitud porque ClickOnce especifica la seguridad integrada de Windows en sus solicitudes. Si configura el servidor de informes para autenticación básica, el servidor rechazará la solicitud porque especifica un paquete de seguridad no válido y porque carece de las credenciales que el servidor de informes espera.<br /><br /> Además, si el servidor de informes se configura para utilizar el modo integrado de SharePoint y el sitio de SharePoint utiliza la autenticación básica, los usuarios encontrarán un error 401 cuando intenten utilizar ClickOnce para instalar el Generador de informes en sus equipos cliente. Esto ocurre porque SharePoint utiliza una cookie para conservar un usuario autenticado mientras dure la sesión, pero ClickOnce no admite la cookie. Cuando un usuario inicia una aplicación ClickOnce, como el Generador de informes, la aplicación no pasa la cookie a SharePoint y, por tanto, SharePoint deniega el acceso y devuelve un error 401.<br /><br /> Puede solucionar este problema con una de las opciones siguientes:<br /><br /> -Seleccione la opción **Recordar mi contraseña** al especificar las credenciales de usuario.<br /><br /> -Habilite el acceso anónimo a la colección de sitios de SharePoint.<br /><br /> -Configure el entorno para que el usuario no tenga que especificar credenciales. Por ejemplo, en un entorno de intranet puede configurar el servidor de SharePoint para que pertenezca a un grupo de trabajo y, a continuación, crear las cuentas de usuario en el equipo local.|  
|Personalizado|Cuando se configura un servidor de informes para utilizar la autenticación personalizada, el acceso anónimo se habilita en el servidor de informes y las solicitudes se aceptan sin comprobación de la autenticación.<br /><br /> Una vez que ClickOnce recupera los archivos de aplicación, el Generador de informes abre una conexión independiente con un servidor de informes. Los usuarios deben volver a escribir sus credenciales para conseguir que el Generador de informes se conecte al servidor de informes. El Generador de informes no recopila credenciales de Internet Explorer o de ClickOnce.|  
  
## <a name="see-also"></a>Ver también  
 [Autenticación con el servidor de informes](../../reporting-services/security/authentication-with-the-report-server.md)   
 [Compatibilidad del explorador de Reporting Services y Power View](../../reporting-services/browser-support-for-reporting-services-and-power-view.md)   
 [Iniciar el Generador de informes](../../reporting-services/report-builder/start-report-builder.md)   
 [Administrador de informes &#40;Modo nativo de SSRS&#41;](https://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)   
 [Conectar con un servidor de informes en Management Studio](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [Propiedades del sistema del servidor de informes](../../reporting-services/report-server-web-service/net-framework/reporting-services-properties-report-server-system-properties.md)  
  
  
