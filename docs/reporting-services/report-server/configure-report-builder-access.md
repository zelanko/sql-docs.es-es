---
title: Configurar el acceso al Generador de informes | Microsoft Docs
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.date: 06/06/2019
ms.openlocfilehash: 724fac17abf7f5da45101a6ff22d3185a7ade93b
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2019
ms.locfileid: "68255173"
---
# <a name="configure-report-builder-access"></a>Configurar el acceso al Generador de informes
El Generador de informes es una herramienta de notificación ad hoc que se instala con un servidor de informes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] configurado para modo nativo o para modo de integración con SharePoint.  

El acceso al Generador de informes depende de los factores siguientes:  

- Propiedades de servidor que determinen si el Generador de informes está disponible en el servidor de informes.  

- Asignaciones de roles o permisos que hacen que el Generador de informes esté disponible para grupos o usuarios individuales.  

- Configuración de autenticación que determina si las credenciales del usuario se pueden pasar al servidor de informes o está configurado el acceso anónimo en los archivos de la aplicación.

## <a name="prerequisites"></a>Prerequisites

El Generador de informes no está disponible en todas las ediciones de [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Características compatibles con las ediciones de SQL Server 2017](../../sql-server/editions-and-components-of-sql-server-2017.md).  

El equipo cliente debe tener [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] instalado 4,6 o 4.6.1 para SSRS 2016 y 2017, respectivamente. [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] proporciona la infraestructura para ejecutar aplicaciones [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] .  

Debe usar [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Explorer 11 o posterior, u otro explorador moderno.  

El Generador de informes siempre se ejecuta con confianza total; no se puede configurar para ejecutarse con confianza parcial. En las versiones anteriores, era posible que el Generador de informes se ejecutara con confianza parcial, pero esa opción no se admite en [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y en versiones posteriores.  

## <a name="enabling-and-disabling-report-builder"></a>Habilitar y deshabilitar el Generador de informes  

El Generador de informes está habilitado de manera predeterminada. Los administradores del servidor de informes tienen la posibilidad de deshabilitar la característica Generador de informes; para ello, deben establecer la propiedad del sistema **ShowDownloadMenu** del servidor de informes en **false**. Al establecer esta propiedad, se deshabilitan las descargas de Generador de informes, Publicador de informes móviles y Power BI Mobile para ese servidor de informes.  

 Para establecer las propiedades del sistema del servidor de informes, puede usar Management Studio o script:   

 - Para utilizar Management Studio, conéctese al servidor de informes y utilice la página Avanzadas de Propiedades del servidor con el fin de establecer **ShowDownloadMenu**en **false**. Para más información sobre cómo abrir esta página, vea [Establecer las propiedades del servidor de informes &#40;Management Studio&#41;](../../reporting-services/tools/set-report-server-properties-management-studio.md).      

 - Para ver un script de ejemplo donde se configura una propiedad del servidor de informes, consulte [Script para tareas administrativas y de implementación](../../reporting-services/tools/script-deployment-and-administrative-tasks.md).  

## <a name="role-assignments-granting-report-builder-access-on-a-native-mode-report-server"></a>Asignaciones de roles que conceden acceso al Generador de informes en un servidor de informes en modo nativo  

En un servidor de informes en modo nativo, cree asignaciones de roles de usuario que incluyan las tareas para utilizar el Generador de informes. Debe ser administrador de contenido y administrador del sistema para crear o modificar definiciones y asignaciones de roles en los elementos y en el nivel de sitio.  

En las instrucciones siguientes se supone que se utilizan roles predefinidos. Si ha modificado las definiciones de roles o ha realizado la actualización a partir de SQL Server 2000, compruebe si los roles contienen las tareas necesarias. Para más información sobre cómo crear asignaciones de roles, vea [Conceder a un usuario acceso a un servidor de informes](../../reporting-services/security/grant-user-access-to-a-report-server.md).

Después de crear las asignaciones de roles, los usuarios tendrán permiso para hacer lo siguiente:  

- Los usuarios asignados a los roles Usuario del sistema y Explorador pueden ver los informes del Generador de informes publicados en un servidor de informes, sin tener que iniciar el Generador de informes.  

- Los usuarios asignados a los roles Usuario del sistema y Generador de informes pueden generar modelos, iniciar el Generador de informes y crear informes, así como guardar informes en el servidor de informes.  

- Los usuarios asignados a los roles Usuario del sistema y Publicador pueden publicar modelos del Diseñador de modelos en el servidor de informes. Los modelos se utilizan como orígenes de datos en el Generador de informes.  

- Los usuarios asignados a los roles Administrador del sistema y Administrador de contenido tienen todos los permisos para crear, ver y administrar informes del Generador de informes.  

### <a name="to-verify-required-tasks-are-in-the-role-definitions"></a>Para comprobar que las tareas necesarias están en las definiciones de roles  

1. Inicie Management Studio y conéctese al servidor de informes.  

2. Abra la carpeta **Seguridad** .  

3. Abra la carpeta **Roles del sistema** .  

4. Haga clic con el botón derecho en **Administrador del sistema**y seleccione **Propiedades**.  

5. Seleccione **Ejecutar definiciones de informe** y haga clic en **Aceptar**.  

6. Haga clic con el botón derecho en **Usuario del sistema**y seleccione **Propiedades**.  

7. Seleccione **Ejecutar definiciones de informe** y haga clic en **Aceptar**.  

8. Abra la carpeta **Roles** .  

9. Haga clic con el botón derecho en **Explorador**y seleccione **Propiedades**.  

10. Seleccione **Ver modelos** y haga clic en **Aceptar**.  

11. Haga clic con el botón derecho en **Administrador de contenido**y seleccione **Propiedades**.  

12. Seleccione **Ver modelos**, **Administrar modelos**, **Usar informes**y haga clic en **Aceptar**.  

13. Haga clic con el botón derecho en **Publicador**y seleccione **Propiedades**.  

14. Seleccione **Administrar modelos** y haga clic en **Aceptar**.  

15. Cree el rol del Generador de informes, si no existe:  

    1. Abra la carpeta **Seguridad** .  

    2. Haga clic con el botón derecho en **Roles**y seleccione **Nuevo rol**.  

    3. En Nombre, escriba **Generador de informes**.  

    4. En Descripción, escriba la descripción del rol de modo que los usuarios del portal web sepan para qué sirve.  

    5. Agregue las tareas siguientes: **Usar informes**, **Ver informes**, **Ver modelos**, **Ver recursos**, **Ver carpetas**y **Administrar suscripciones individuales**.  

    6. Haga clic en **Aceptar** para guardar el rol.  

#### <a name="to-create-role-assignments-that-grant-access-to-report-builder"></a>Para crear asignaciones de roles que concedan acceso al Generador de informes  

1. Inicie el portal web.  

2. Haga clic en el icono de engranaje en la parte superior derecha de la Página principal del portal web y seleccione **configuración del sitio** en el menú desplegable.  
![icono y menú de engranaje del portal web](../../reporting-services/report-builder/media/configure-report-builder-access/ssrswebportal-site-settings-gear-icon-and-menu.png)

3. Haga clic en **Seguridad**.  

4. Si ya existe una asignación de roles para el usuario o el grupo cuyo acceso al Generador de informes desea configurar, haga clic en **Editar**.  
De lo contrario, haga clic en **Nueva asignación de roles**. En Grupo o usuario, escriba una cuenta de grupo o de usuario de dominio de Windows con este formato: \<dominio>\\<cuenta\>. Si utiliza la autenticación de formularios o la seguridad personalizada, especifique la cuenta de grupo o de usuario en el formato correcto para su implementación.  

5. Seleccione **Usuario del sistema**y, a continuación, haga clic en **Aceptar**.  

6. Haga clic en **Inicio**.  

7. Haga clic en la pestaña **Configuración de carpeta** .  

8. Haga clic en la pestaña **Seguridad** .  

9. Si ya existe una asignación de roles para el usuario o el grupo cuyo acceso al Generador de informes desea configurar, haga clic en **Editar**.  

    De lo contrario, haga clic en **Nueva asignación de roles**. En Grupo o usuario, escriba una cuenta de grupo o de usuario de dominio de Windows con este formato: \<dominio>\\<cuenta\>. Si utiliza la autenticación de formularios o la seguridad personalizada, especifique la cuenta de grupo o de usuario en el formato correcto para su implementación.  

10. Seleccione **Generador de informes**y haga clic en **Aplicar**.  

11. Repita el proceso para crear o modificar asignaciones de roles para otros usuarios o grupos.  

## <a name="permissions-granting-report-builder-access-on-a-sharepoint-integrated-mode-report-server"></a>Permisos que conceden acceso al Generador de informes en un servidor de informes en modo integrado de SharePoint  

En un servidor de informes en modo integrado de SharePoint, el acceso al Generador de informes se concede a los usuarios de SharePoint que tienen los niveles de permisos Colaborar o Control total.  

Si utiliza niveles de permisos personalizados, debe incluir Agregar elementos y Editar elementos en el nivel de permisos. Para más información sobre el acceso al Generador de informes con los niveles de permisos integrados, vea [Usar la seguridad integrada de Windows SharePoint Services para los elementos del servidor de informes](../../reporting-services/security/use-built-in-security-in-windows-sharepoint-services-for-report-server-items.md). Para más información sobre los requisitos de permisos para niveles de permisos personalizados, vea [Establecer permisos para las operaciones del servidor de informes en una aplicación web de SharePoint](../../reporting-services/security/set-permissions-for-report-server-operations-in-a-sharepoint-web-application.md).  

## <a name="authentication-considerations-and-credential-reuse"></a>Consideraciones de autenticación y reutilización de credenciales  

- El Generador de informes abre su propia conexión a un servidor de informes. Si no se usa la seguridad integrada de Windows con un único inicio de sesión, los usuarios deben volver a escribir sus credenciales para la conexión del Generador de informes con el servidor de informes.  

En la tabla siguiente se describen los tipos de autenticación que admite el servidor de informes y si se necesita configuración adicional para tener acceso al Generador de informes.  

## <a name="see-also"></a>Vea también  

- [Autenticación con el servidor de informes](../../reporting-services/security/authentication-with-the-report-server.md)
- [Compatibilidad del explorador de Reporting Services y Power View](../../reporting-services/browser-support-for-reporting-services-and-power-view.md)
- [Inicio del Generador de informes](../../reporting-services/report-builder/start-report-builder.md)
- [El portal web de un servidor de informes (modo nativo de SSRS)](../web-portal-ssrs-native-mode.md)
- [Conexión con un servidor de informes en Management Studio](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)
- [Propiedades del sistema del servidor de informes](../../reporting-services/report-server-web-service/net-framework/reporting-services-properties-report-server-system-properties.md)
