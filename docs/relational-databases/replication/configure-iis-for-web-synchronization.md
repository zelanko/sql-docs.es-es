---
title: Configuración de IIS para la sincronización web | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- IIS server configuration [SQL Server replication]
- websync.log
- Web synchronization, IIS servers
ms.assetid: d651186e-c9ca-4864-a444-2cd6943b8e35
caps.latest.revision: 88
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 58937e416603bdbaa2ee33923dd783c1e1d7c228
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="configure-iis-for-web-synchronization"></a>Configurar IIS para la sincronización web
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Los procedimientos descritos en este tema son el segundo paso para configurar la sincronización web para la replicación de mezcla. Este paso se lleva a cabo después de habilitar una publicación para la sincronización web. Para obtener información general sobre el proceso de configuración, vea [Configurar sincronización web](../../relational-databases/replication/configure-web-synchronization.md). Una vez terminados los procedimientos de este tema, siga con el tercer paso: configurar una suscripción para usar la sincronización web. El tercer paso se describe en los siguientes temas:  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]: [Cómo configurar una suscripción para usar la sincronización web \(SQL Server Management Studio\)](http://msdn.microsoft.com/library/ms345214.aspx)  
  
-   Programación de la replicación con [!INCLUDE[tsql](../../includes/tsql-md.md)] : [Cómo configurar una suscripción para usar la sincronización web (programación de la replicación con Transact-SQL)](http://msdn.microsoft.com/library/ms345206.aspx)  
  
-   RMO: [Cómo configurar una suscripción para usar la sincronización web (programación con RMO)](http://msdn.microsoft.com/library/ms345207.aspx)  
  
 La sincronización web utiliza un equipo en el que se ejecuta [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Information Services (IIS) para sincronizar las suscripciones de extracción con las publicaciones de combinación. Se admiten IIS versión 5.0, IIS versión 6.0 e [!INCLUDE[iisver](../../includes/iisver-md.md)] . El Asistente para configurar la sincronización web no se admite en [!INCLUDE[iisver](../../includes/iisver-md.md)].  
  
> [!IMPORTANT]  
>  Asegúrese de que la aplicación solo utilice [!INCLUDE[dnprdnlong](../../includes/dnprdnlong-md.md)] o versiones posteriores, y de que no haya versiones anteriores de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] instaladas en el servidor IIS. Las versiones anteriores de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] pueden producir errores. Entre estos errores se incluyen los siguientes: "El formato de un mensaje durante la sincronización web no es válido. Asegúrese de que los componentes de replicación se han configurado correctamente en el servidor web".  
  
> [!CAUTION]  
>  No use WebSync y las ubicaciones alternativas de carpeta de instantáneas a la vez.  
  
 Para utilizar la sincronización web, debe configurar IIS mediante los siguientes pasos. Cada paso se describe detalladamente en este tema.  
  
1.  Configure SSL (Capa de sockets seguros). SSL es necesario para establecer comunicaciones entre IIS y todos los suscriptores.  
  
2.  Instale los componentes de conectividad de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el equipo en el que se ejecuta IIS mediante el Asistente para la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Instale los componentes de conectividad deation Wizard. Si tiene previsto usar el Asistente para configurar la sincronización web que se menciona en el paso 3, es necesario instalar también [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] en el equipo en el que se ejecuta IIS.  
  
3.  Configure el equipo en el que se ejecuta IIS para la sincronización web. Puede configurar el equipo manualmente o usar el Asistente para configurar la sincronización web. Se recomienda utilizar el asistente.  
  
    > [!NOTE]  
    >  Si el equipo en el que se está ejecutando IIS usa una versión de 64 bits de Windows, debe ejecutar el siguiente comando para asegurarse de que el servidor esté configurado correctamente para ejecutar aplicaciones de la Interfaz de programación de aplicaciones para servidores de Internet (ISAPI). Para obtener más información, vea la documentación de IIS.  
  
    ```  
    cscript %SystemDrive%\inetpub\AdminScripts\adsutil.vbs set w3svc/AppPools/Enable32bitAppOnWin64 1  
    ```  
  
4.  Seleccione los permisos adecuados para la Escucha de replicación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
5.  Ejecute la sincronización web en modo de diagnóstico para probar la conexión con el equipo en el que se ejecuta IIS y para asegurarse de que el certificado SSL está instalado correctamente.  
  
## <a name="configuring-secure-sockets-layer"></a>Configurar la Capa de sockets seguros (SSL)  
 Para configurar SSL, especifique un certificado para que lo utilice el equipo en el que se ejecuta IIS. La sincronización web para la replicación de mezcla es compatible con el uso de certificados de servidor, pero no de certificados de cliente. Para configurar IIS para implementación, primero debe obtener un certificado por parte de una entidad de certificación (CA). Una entidad de certificación es una entidad responsable de establecer y dar fe de la autenticidad de las claves de cifrado públicas de usuarios, equipos y otras entidades de certificación. Para obtener más información acerca de los certificados, vea la documentación de IIS. Cuando el certificado esté instalado, debe asociarlo al sitio web que utiliza la sincronización web.  
  
#### <a name="to-specify-a-certificate-for-deployment"></a>Para especificar un certificado para su implementación  
  
1.  Inicie sesión como administrador en el equipo en el que se ejecuta IIS.  
  
2.  Inicie el **Administrador de Internet Information Services (IIS)**:  
  
    1.  Haga clic en **Inicio**y, a continuación, haga clic en **Ejecutar**.  
  
    2.  En el cuadro **Abrir** , escriba **inetmgr**y, después, haga clic en **Aceptar**.  
  
3.  Ejecute el Asistente para certificados IIS:  
  
    1.  En el **Administrador de Internet Information Services (IIS)**, expanda el nodo **equipo local** y, a continuación, la carpeta **Sitios web** .  
  
    2.  Haga clic con el botón secundario en **Sitio web predeterminado**y, después, en **Propiedades**.  
  
    3.  En el cuadro de diálogo **Propiedades de Sitio web predeterminado** , en la pestaña **Seguridad de directorios** , haga clic en **Certificado de servidor**.  
  
    4.  Complete el Asistente para certificados de servidor web.  
  
4.  Haga clic en **Aceptar**.  
  
 Si no puede obtener un certificado de servidor de una CA, puede especificar un certificado para comprobación. Para configurar IIS 6.0 para comprobación, instale un certificado mediante la utilidad SelfSSL. Esta utilidad está disponible en el kit de recursos de IIS 6.0. Puede descargar las herramientas del [Centro de descarga de Microsoft](http://go.microsoft.com/fwlink/?LinkId=30958). Para IIS 5.0, vaya a [Ayuda y soporte técnico de Microsoft](http://go.microsoft.com/fwlink/?LinkId=46229).  
  
> [!NOTE]  
>  Un sitio web debe asociarse a un certificado antes de que pueda usar SSL. SelfSSL asocia automáticamente el certificado al sitio web predeterminado. Si ya dispone de un certificado o instala uno de una CA más adelante, deberá asociar explícitamente ese certificado al sitio web que se utilice en la sincronización web. Asegúrese de que solo hay un certificado asociado al sitio web que se utiliza para sincronizar suscripciones. Si hay varios certificados, el suscriptor utilizará el primer sitio web que esté disponible.  
  
#### <a name="to-specify-a-certificate-for-testing-in-iis-60"></a>Para especificar un certificado para su comprobación en IIS 6.0  
  
1.  Inicie sesión como administrador en el equipo en el que se ejecuta IIS.  
  
2.  Descargue e instale SelfSSL. De forma predeterminada, la aplicación se instala en \<*unidad*>:\Archivos de programa\IIS Resources\SelfSSL. Los accesos directos a la aplicación y la documentación se copian en \<*unidad*>:\Documents and Settings\All Users\Start Menu\Programs\IIS Resources\SelfSSL.  
  
3.  Ejecute SelfSSL:  
  
    -   Para ejecutar SelfSSL con los valores predeterminados para todos los parámetros, localice el directorio de instalación de la aplicación y haga doble clic en SelfSSL.exe.  
  
        > [!NOTE]  
        >  De forma predeterminada, el certificado que instala SelfSSL es válido durante siete días.  
  
    -   Para especificar valores para uno o más parámetros: haga clic en **Inicio**y, a continuación, haga clic en **Ejecutar**. En el cuadro **Abrir** , escriba **cmd**y, después, haga clic en **Aceptar**. Localice el directorio de instalación de SelfSSL, escriba `SelfSSL`y después especifique los valores para uno o más parámetros. Para obtener una lista de parámetros, escriba `SelfSSL -?`.  
  
## <a name="installing-connectivity-components-and-sql-server-management-studio"></a>Instalar los componentes de conectividad y SQL Server Management Studio  
  
#### <a name="to-install-sql-server-connectivity-components-and-sql-server-management-studio"></a>Para instalar los componentes de conectividad de SQL Server y SQL Server Management Studio  
  
1.  Inicie sesión como administrador en el equipo en el que se ejecuta IIS.  
  
2.  Inicie el Asistente para la instalación de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] desde el disco de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obtener más información sobre cómo usar este asistente, vea [Instalación de SQL Server 2016 desde el Asistente para la instalación &#40;programa de instalación&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md).  
  
3.  En la página **Selección de características** , seleccione **Conectividad con las herramientas de cliente**.  
  
4.  Si piensa utilizar el Asistente para configurar la sincronización web, seleccione **Herramientas de administración - Básica**.  
  
5.  Complete el asistente y reinicie el equipo.  
  
    > [!NOTE]  
    >  Puede instalar componentes adicionales, pero para la sincronización web solo son necesarios los componentes de conectividad.  
  
## <a name="configuring-the-computer-that-is-running-iis-by-using-the-configure-web-synchronization-wizard"></a>Configurar el equipo en el que se ejecuta IIS mediante el Asistente para configurar la sincronización web  
 Configure el servidor IIS mediante el Asistente para configurar la sincronización web o manualmente. Se recomienda utilizar el asistente, pero también se proporcionan los pasos para la configuración manual en la siguiente sección. El Asistente para configurar la sincronización web que está disponible con [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] solamente se puede utilizar para publicaciones que se crearon en un publicador en el que se ejecuta [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]o en un publicador que se actualizó a [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. El asistente no se puede utilizar para publicaciones en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Se puede usar con suscripciones en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores, y en [!INCLUDE[ssEWnoversion](../../includes/ssewnoversion-md.md)] 3.0 y versiones posteriores.  
  
 La configuración presenta las características siguientes:  
  
-   Utiliza el sitio web predeterminado en IIS. Sin embargo, puede utilizar otro sitio web. Para obtener más información acerca de cómo crear sitios web, vea la documentación de IIS.  
  
    > [!NOTE]  
    >  El sitio web que especifique proporciona acceso a los componentes que se utilizan en la sincronización web. El sitio web no proporciona acceso a otros datos o páginas web, a menos que lo configure para ello.  
  
-   Crea un directorio virtual y su alias asociado. El alias se utiliza para obtener acceso a los componentes de la sincronización web. Por ejemplo, si la dirección del servidor IIS es `https://server.domain.com` y especifica el alias "websync1", la dirección para obtener acceso al componente replisapi.dll será `https://server.domain.com/websync1/replisapi.dll`.  
  
-   Utiliza la autenticación básica. Se recomienda utilizar la autenticación básica porque permite ejecutar IIS y el publicador o distribuidor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en equipos independientes (la configuración recomendada) sin requerir la delegación Kerberos. El uso de SSL con la autenticación básica garantiza que los inicios de sesión, las contraseñas y todos los datos se cifren durante el tránsito. SSL es necesario, independientemente del tipo de autenticación que se utilice. Para obtener más información sobre las prácticas recomendadas para la sincronización web, vea la sección sobre las prácticas recomendadas de seguridad para la sincronización web en [Configurar sincronización web](../../relational-databases/replication/configure-web-synchronization.md).  
  
#### <a name="to-configure-the-computer-that-is-running-iis-by-using-the-configure-web-synchronization-wizard"></a>Para configurar el equipo en el que se ejecuta IIS mediante el Asistente para configurar la sincronización web  
  
1.  En el equipo en el que se ejecuta IIS, inicie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
2.  Conéctese al publicador y expanda el nodo de servidor.  
  
3.  Expanda la carpeta **Publicaciones locales** , haga clic con el botón secundario en la publicación y, a continuación, haga clic en **Configurar sincronización web**.  
  
4.  En el Asistente para configurar la sincronización web, en la página **Tipo de suscriptor** , seleccione **SQL Server**.  
  
5.  En la página **Servidor web** :  
  
    1.  Seleccione la instancia de IIS que sincronizará las suscripciones.  
  
    2.  Seleccione **Crear un nuevo directorio virtual**.  
  
    3.  En el panel inferior de la página, expanda la instancia de IIS, expanda **Sitios web**y, a continuación, haga clic en **Sitio web predeterminado**.  
  
6.  En la página **Información de directorio virtual** :  
  
    1.  Escriba un alias para el directorio virtual en el cuadro **Alias** .  
  
    2.  Escriba una ruta de acceso al directorio virtual en el cuadro **Ruta de acceso** . Por ejemplo, si escribió **websync1** en el cuadro **Alias** , escriba **C:\Inetpub\wwwroot\websync1** en el cuadro **Ruta de acceso** . Haga clic en **Siguiente**.  
  
    3.  Haga clic en **Sí**en los dos cuadros de diálogo. Esto indica que desea crear una carpeta nueva y que desea copiar la DLL de la Interfaz de programación de aplicaciones para servidores de Internet (ISAPI) de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . .  
  
7.  En la página **Acceso autenticado** :  
  
    1.  Asegúrese de que las casillas **Autenticación de Windows integrada** y **Autenticación implícita para servidores de dominio Windows** no están activadas.  
  
    2.  Seleccione **Autenticación básica**.  
  
    3.  En los cuadros **Dominio predeterminado** y **Territorio** , escriba el dominio del equipo en el que se ejecuta IIS.  
  
8.  En la página **Acceso a directorio** :  
  
    1.  Haga clic en **Agregar**y, a continuación, en el cuadro de diálogo **Seleccionar usuarios o grupos** , agregue las cuentas con las que los suscriptores se conectarán a IIS. Estas son las cuentas que especificará en la página **Información del servidor web** del Asistente para nueva suscripción o como el valor del parámetro [sp_addmergepullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)*@internet_login* .  
  
9. En la página **Acceso a recurso compartido de instantáneas** , escriba el recurso compartido de instantáneas: en este recurso compartido se establecen los permisos adecuados para que los suscriptores puedan obtener acceso a los archivos de instantáneas. Para obtener más información sobre los permisos del recurso compartido, vea [Proteger la carpeta de instantáneas](../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
10. En la página **Finalización del asistente** , haga clic en **Finalizar**.  
  
     Si se produce un error, como un error de red al intentar configurar un equipo remoto en el que se ejecuta IIS, todas las acciones completadas se revierten y las pendientes se cancelan. Si no se puede revertir una acción completada, el estado de la página final del asistente muestra **Correcto** y las acciones completadas no se revierten.  
  
11. Si el equipo en el que se ejecuta IIS usa una versión de 64 bits de Windows, es necesario copiar replisapi.dll en el directorio adecuado:  
  
    1.  Haga clic en **Inicio**y, a continuación, haga clic en **Ejecutar**. En el cuadro **Abrir** , escriba **iisreset**y, después, haga clic en **Aceptar**.  
  
    2.  Después de que IIS se detenga y se reinicie, copie replisapi.dll de [!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]COM\replisapi al directorio que se especifica en el paso 6b.  
  
    3.  Haga clic en **Inicio**y, a continuación, haga clic en **Ejecutar**. En el cuadro **Abrir** , escriba **cmd**y, después, haga clic en **Aceptar**.  
  
    4.  En el directorio especificado en el paso 6b, ejecute el siguiente comando:  
  
         **regsvr32 replisapi.dll**  
  
## <a name="manually-configuring-the-computer-that-is-running-iis"></a>Configurar manualmente el equipo en el que se ejecuta IIS  
 Para configurar el equipo en el que se ejecuta IIS manualmente, debe instalar y configurar la Escucha de replicación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y, a continuación, configurar la autorización para los suscriptores que se conectarán a IIS.  
  
#### <a name="to-install-and-configure-the-sql-server-replication-listener"></a>Para instalar y configurar la Escucha de replicación de SQL Server  
  
1.  Cree un directorio de archivos en el equipo que ejecute IIS para que contenga replisapi.dll. Puede crear el directorio donde desee, pero recomendamos crearlo en el directorio \<*unidad*>:\Inetpub. Por ejemplo, cree el directorio \<*drive*>:\Inetpub\SQLReplication\\.  
  
    > [!IMPORTANT]  
    >  Se recomienda encarecidamente crear este directorio en una partición del sistema de archivos NTFS, en lugar del sistema de archivos FAT. Al usar el sistema de archivos NTFS, puede utilizar los permisos del sistema de archivos NTFS para controlar con precisión los usuarios que pueden obtener acceso a la replicación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
2.  Copie replisapi.dll del directorio [!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]com\ al directorio de archivos que creó en el paso 1.  
  
3.  Registre el archivo replisapi.dll:  
  
    1.  Haga clic en **Inicio**y, a continuación, haga clic en **Ejecutar**. En el cuadro **Abrir** , escriba **cmd**y, después, haga clic en **Aceptar**.  
  
    2.  En el directorio creado en el paso 1, ejecute el siguiente comando:  
  
         **regsvr32 replisapi.dll**  
  
4.  Cree un nuevo sitio web para la replicación, o bien utilice un sitio existente. Los componentes de la replicación tendrán acceso al sitio web durante la sincronización. Para obtener más información acerca de cómo crear sitios web, vea la documentación de IIS.  
  
5.  Cree un directorio virtual en IIS. El directorio virtual se debe crear en el sitio web creado en el paso 4 y debe asignarse al directorio creado en el paso 1. Para obtener más información acerca de cómo crear directorios virtuales, vea la documentación de IIS. Se recomienda ser tan restrictivo como sea posible al asignar permisos a este directorio. Debe activar los permisos **Leer** y **Ejecutar** , pero puede desactivar los permisos **Ejecutar scripts**, **Escribir**y **Examinar** .  
  
6.  Configure IIS para permitir la ejecución de replisapi.dll. Los permisos asignados en el paso 4 son suficientes para versiones anteriores de IIS; sin embargo, IIS 6.0 requiere que se habiliten las extensiones de la Interfaz de programación de aplicaciones para servidores de Internet (ISAPI). Para obtener más información, vea los temas sobre cómo configurar extensiones ISAPI y cómo habilitar y deshabilitar contenido dinámico en la documentación de IIS 6.0.  
  
#### <a name="to-configure-iis-authentication"></a>Para configurar la autenticación IIS  
  
-   Cuando los suscriptores se conectan a IIS, IIS debe autenticarlos para que puedan tener acceso a los recursos y procesos. IIS ofrece tres tipos de autenticación: anónima, básica e integrada. La autenticación se puede aplicar a todo el sitio web o al directorio virtual que ha creado.  
  
     Se recomienda usar la autenticación básica con SSL. SSL es necesario, independientemente del tipo de autenticación que se utilice. Para obtener más información acerca de cómo configurar la autenticación, vea la documentación de IIS.  
  
## <a name="setting-permissions-for-the-sql-server-replication-listener"></a>Establecer los permisos para la Escucha de replicación de SQL Server  
 Cuando un suscriptor se conecta al equipo en el que se ejecuta IIS, se autentica usando el tipo de autenticación especificado al configurar IIS. Tras autenticar al suscriptor, IIS comprueba si el suscriptor está autorizado para invocar la replicación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Debe controlar los usuarios que pueden invocar la replicación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estableciendo permisos para replisapi.dll. Es necesario configurar permisos para impedir el acceso no autorizado a la replicación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Para configurar los permisos mínimos para la cuenta con la que se ejecuta la Escucha de replicación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , lleve a cabo el siguiente procedimiento. Los pasos de este procedimiento afectan a equipos con [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] en los que se ejecute IIS 6.0.  
  
 Además de realizar los siguientes pasos, asegúrese de que los inicios de sesión necesarios se encuentran en la lista de acceso a la publicación (PAL). Para obtener más información sobre la PAL, vea [Secure the Publisher](../../relational-databases/replication/security/secure-the-publisher.md) (Proteger el publicador).  
  
#### <a name="to-configure-the-account-and-permissions"></a>Para configurar la cuenta y los permisos  
  
1.  Cree una cuenta local en el equipo en el que se ejecuta IIS:  
  
    1.  Haga clic con el botón secundario en **Mi PC**y, a continuación, haga clic en **Administrar**.  
  
    2.  En **Administración del equipo**, expanda **Usuarios y grupos locales**.  
  
    3.  Haga clic con el botón secundario en **Usuarios**y después en **Usuario nuevo**.  
  
    4.  Escriba un nombre de usuario y una contraseña segura.  
  
    5.  Haga clic en **Crear**y, a continuación, en **Cerrar**.  
  
2.  Agregue la cuenta al grupo IIS_WPG:  
  
    1.  En **Administración del equipo**, expanda **Usuarios y grupos locales**y haga clic en **Grupos**.  
  
    2.  Haga clic con el botón secundario en **IIS_WPG**y, después, en **Agregar a grupo**.  
  
    3.  En el cuadro de diálogo **Propiedades de IIS_WPG** , haga clic en **Agregar**.  
  
    4.  En el cuadro de diálogo **Seleccionar usuarios, equipos o grupos** , agregue la cuenta que creó en el paso 1.  
  
    5.  Asegúrese de que en el campo **Desde esta ubicación** aparece el nombre del equipo local, no un dominio. Si el nombre no es un equipo local, haga clic en **Ubicaciones**. En el cuadro de diálogo **Ubicaciones** , elija el equipo local y, a continuación, haga clic en **Aceptar**.  
  
    6.  Haga clic en **Aceptar** en los cuadros de diálogo **Seleccionar usuarios** y **Propiedades de IIS_WPG**.  
  
3.  Conceda a la cuenta los permisos mínimos en la carpeta que contiene el archivo replisapi.dll:  
  
    1.  Localice la carpeta que ha creado para replisapi.dll, haga clic con el botón secundario en ella y, a continuación, haga clic en **Compartir y seguridad**.  
  
    2.  En la pestaña **Seguridad** , haga clic en **Agregar**.  
  
    3.  En el cuadro de diálogo **Seleccionar usuarios, equipos o grupos** , agregue la cuenta que creó en el paso 1.  
  
    4.  Asegúrese de que en el campo **Desde esta ubicación** aparece el nombre del equipo local, no un dominio. Si el nombre no es un equipo local, haga clic en **Ubicaciones**. En el cuadro de diálogo **Ubicaciones** , seleccione el equipo local y, a continuación, haga clic en **Aceptar**.  
  
    5.  Asegúrese de que la cuenta solo tenga permisos de **Lectura**, **Lectura y ejecución** y **Mostrar el contenido de la carpeta**.  
  
    6.  Seleccione los usuarios o grupos que no requieran acceso al directorio y, a continuación, haga clic en **Quitar**.  
  
    7.  Haga clic en **Aceptar**.  
  
4.  Cree un grupo de aplicaciones en **Administrador de Internet Information Services (IIS)**:  
  
    1.  Haga clic en **Inicio**y, a continuación, haga clic en **Ejecutar**.  
  
    2.  En el cuadro **Abrir** , escriba **inetmgr**y, después, haga clic en **Aceptar**.  
  
    3.  En **Administrador de Internet Information Services (IIS)**, expanda el nodo **equipo local** .  
  
    4.  Haga clic con el botón secundario en **Grupos de aplicaciones**, seleccione **Nuevo** y, a continuación, haga clic en **Grupo de aplicaciones**.  
  
    5.  Escriba un nombre para el grupo en el campo **Id. de grupo de aplicaciones** y haga clic en **Aceptar**.  
  
5.  Asocie la cuenta al grupo de aplicaciones:  
  
    1.  En **Administrador de Internet Information Services (IIS)**, expanda el nodo **equipo local** y, a continuación, expanda **Grupos de aplicaciones**.  
  
    2.  Haga clic con el botón secundario en el grupo de aplicaciones que ha creado y, a continuación, haga clic en **Propiedades**.  
  
    3.  En el cuadro de diálogo **\<Propiedades de <nombreDeGrupoDeAplicaciones**, en la pestaña **Identidad**, haga clic en **Configurable**.  
  
    4.  En los campos **Nombre de usuario** y **Contraseña** , escriba la cuenta y la contraseña que creó en el paso 1.  
  
    5.  Haga clic en **Aceptar**.  
  
6.  Asocie el grupo de aplicaciones al directorio virtual que se utiliza para la sincronización web:  
  
    1.  En **Administrador de Internet Information Services (IIS)**, expanda el nodo **equipo local** y, a continuación, expanda **Sitios web**.  
  
    2.  Expanda el sitio web que está utilizando para la sincronización web, haga clic con el botón secundario en el directorio virtual que creó para la sincronización web y, a continuación, haga clic en **Propiedades**.  
  
    3.  En la pestaña **Directorio virtual** del cuadro de diálogo **\<Propiedades de <nombreDeDirectorioVirtual>**, en la lista desplegable **Grupo de aplicaciones**, seleccione el grupo de aplicaciones creado en el paso 5.  
  
    4.  Haga clic en **Aceptar**.  
  
## <a name="testing-the-connection-to-replisapidll"></a>Probar la conexión con replisapi.dll  
 Ejecute la sincronización web en modo de diagnóstico para probar la conexión al equipo en el que se ejecuta IIS y para asegurarse de que el certificado SSL (Capa de sockets seguros) está instalado correctamente. Para ejecutar la sincronización web en modo de diagnóstico, debe ser administrador en el equipo donde se ejecuta IIS.  
  
#### <a name="to-test-the-connection-to-replisapidll"></a>Para probar la conexión con replisapi.dll  
  
1.  Asegúrese de que la configuración de red de área local (LAN) del suscriptor es correcta:  
  
    1.  En [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Explorer, en el menú **Herramientas** , haga clic en **Opciones de Internet**.  
  
    2.  En la pestaña **Conexiones** , haga clic en **Configuración de LAN**.  
  
    3.  Si no se utiliza ningún servidor proxy en la configuración de red de área local (LAN), desactive las casillas **Detectar la configuración automáticamente** y **Utilizar un servidor proxy para su LAN**.  
  
    4.  Si se utiliza un servidor proxy, active las casillas **Utilizar un servidor proxy para su LAN** y **No usar servidor proxy para direcciones locales**.  
  
    5.  Haga clic en **Aceptar**.  
  
2.  En el suscriptor, en Internet Explorer, conéctese al servidor en modo de diagnóstico agregando `?diag` a la dirección de replisapi.dll. Por ejemplo: `https://server.domain.com/directory/replisapi.dll?diag`.  
  
3.  Si el sistema operativo Windows no reconoce el certificado especificado para IIS, aparece el cuadro de diálogo **Alerta de seguridad** . Esta alerta puede producirse porque el certificado es un certificado de prueba, o bien porque lo emitió una entidad de certificación (CA) que Windows no reconoce.  
  
    > [!NOTE]  
    >  Si este cuadro de diálogo no aparece, asegúrese de que el certificado del servidor al que está obteniendo acceso se ha agregado al almacén de certificados del suscriptor como certificado de confianza. Para obtener más información acerca de la exportación de certificados, vea la documentación de IIS.  
  
    1.  En el cuadro de diálogo **Alerta de seguridad** , haga clic en **Ver certificado**.  
  
    2.  En el cuadro de diálogo **Certificado** de la pestaña **General** , haga clic en **Instalar certificado**.  
  
    3.  Complete el Asistente para importación de certificados, aceptando los valores predeterminados.  
  
    4.  En el cuadro de diálogo **Advertencia de seguridad** , haga clic en **Sí**.  
  
    5.  En el cuadro de diálogo de confirmación del Asistente para importación de certificados, haga clic en **Aceptar**.  
  
    6.  Cierre el cuadro de diálogo **Certificado** .  
  
    7.  En el cuadro de diálogo **Alerta de seguridad** , haga clic en **Sí**.  
  
    > [!NOTE]  
    >  Los certificados los instalan los usuarios. Este proceso lo deben realizar todos los usuarios que vayan a realizar sincronizaciones con IIS.  
  
4.  En el cuadro de diálogo **Conectarse a \<nombreDeServidor>**, especifique el nombre de usuario y la contraseña que el Agente de mezcla usará para conectarse a IIS. Estas credenciales también se especificarán en el Asistente para nueva suscripción.  
  
5.  En la ventana de Internet Explorer con **información de diagnóstico sobre la sincronización web de SQL**, compruebe que el valor de todas las columnas de **estado** de la página sea **SUCCESS**.  
  
6.  Compruebe que el certificado se haya instalado correctamente en el suscriptor:  
  
    1.  Cierre y vuelva a abrir Internet Explorer.  
  
    2.  Conéctese al servidor en modo de diagnóstico. Si el certificado se ha instalado correctamente, no aparecerá el cuadro de diálogo **Alerta de seguridad** . Si se muestra este cuadro de diálogo, se producirá un error en el Agente de mezcla cuando intente conectarse al equipo en el que se ejecuta IIS. Debe asegurarse de que el certificado del servidor al que está obteniendo acceso se ha agregado al almacén de certificados del suscriptor como certificado de confianza. Para obtener más información acerca de la exportación de certificados, vea la documentación de IIS.  
  
## <a name="see-also"></a>Ver también  
 [Configurar sincronización web](../../relational-databases/replication/configure-web-synchronization.md)  
  
  
