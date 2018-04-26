---
title: Configurar IIS 7 para la sincronización web | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2016
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
- IIS 7 server configuration [SQL Server replication]
- Web synchronization, IIS 7 servers
ms.assetid: c201fe2c-0a76-44e5-a233-05e14cd224a6
caps.latest.revision: 11
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9458cfe599a240719ad4f04c27c0bc13fb2a04a6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="configure-iis-7-for-web-synchronization"></a>Configurar IIS 7 para la sincronización web
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Los procedimientos descritos en este tema le guiarán a través del proceso de configurar manualmente [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Information Services (IIS) versión 7 y superior para su uso con la sincronización web en la replicación de mezcla. 
  
 La configuración de IIS 7 o superior es el primero de los tres pasos necesarios para habilitar la sincronización web.  
  
 Para obtener información general sobre todo el proceso de configuración, vea [Configurar sincronización web](../../relational-databases/replication/configure-web-synchronization.md).  
  
> [!IMPORTANT]  
>  Asegúrese de que la aplicación solo utilice [!INCLUDE[dnprdnlong](../../includes/dnprdnlong-md.md)] o versiones posteriores, y de que no haya versiones anteriores de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] instaladas en el servidor IIS. Las versiones anteriores de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] pueden producir los errores similares a "El formato de un mensaje durante la sincronización web no era válido. Asegúrese de que los componentes de replicación se han configurado correctamente en el servidor web."  
  
 Para utilizar la sincronización web, debe configurar IIS mediante los siguientes pasos. Cada paso se describe detalladamente en este tema.  
  
1.  Instale y configure la Escucha de replicación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el equipo en el que se ejecuta IIS.  
  
2.  Configure SSL (Capa de sockets seguros). SSL es necesario para establecer comunicaciones entre IIS y todos los suscriptores.  
  
3.  Configure la autenticación IIS.  
  
4.  Configure una cuenta y establezca permisos para la Escucha de replicación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="installing-the-sql-server-replication-listener"></a>Instalar la Escucha de replicación de SQL Server  

La sincronización web es compatible con IIS, a partir de la versión 5.0. El Asistente de configuración de sincronización web de IIS versión 5 y 6 no está disponible con IIS versión 7.0 o superior. **A partir de SQL Server 2012, para usar el componente de sincronización web en el servidor IIS, debe instalar SQL Server con replicación. Puede ser la edición gratuita de SQL Server Express.**
  
#### <a name="to-install-and-configure-the-sql-server-replication-listener"></a>Para instalar y configurar la Escucha de replicación de SQL Server  
  
1.  Instale la replicación de SQL Server en el equipo de IIS.

2. Cree un directorio de archivos para replisapi.dll en el equipo que ejecute IIS. Puede crear el directorio donde desee, pero recomendamos crearlo en el directorio \<*unidad*>:\Inetpub. Por ejemplo, cree el directorio \<*drive*>:\Inetpub\SQLReplication\\.  
  
3.  Copie replisapi.dll del directorio [!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]com\ al directorio de archivos que creó en el paso 1.  
  
4.  Registre el archivo replisapi.dll:  
  
    1.  Haga clic en **Inicio**y, a continuación, haga clic en **Ejecutar**. En el cuadro **Abrir** , escriba **cmd**y, después, haga clic en **Aceptar**.  
  
    2.  En el directorio creado en el paso 1, ejecute el siguiente comando:  
  
         **regsvr32 replisapi.dll**  
  
5.  Cree un nuevo sitio web para la replicación, o bien utilice un sitio existente. Los componentes de la replicación tendrán acceso al sitio web durante la sincronización. En los procedimientos de este tema se asume que se utiliza el sitio web predeterminado. Para obtener más información acerca de cómo crear sitios web, vea la documentación de IIS.  
  
6.  Cree un directorio virtual en IIS. El directorio virtual se debe crear en el sitio web creado en el paso 4 y asignarse al directorio creado en el paso 1. Asigne a este directorio el mínimo de permisos posible. Debe seleccionar los permisos **Lectura** y **Ejecutar** como mínimo.  
  
    1.  En **Administrador de Internet Information Services (IIS)**, en el panel **Conexiones** , haga clic con el botón secundario en **Sitio web predeterminado**y, a continuación, seleccione **Agregar directorio virtual**.  
  
    2.  En **Alias**, escriba **SQLReplication**.  
  
    3.  En **Ruta de acceso física**, escriba **\<<unidad>:\Inetpub\SQLReplication\\** y haga clic en **Aceptar**.  
  
7.  Configure IIS para permitir la ejecución de replisapi.dll.  
  
    1.  En **Administrador de Internet Information Services (IIS)**, haga clic en **Sitio web predeterminado**.  
  
    2.  En el panel del centro, haga clic en **Asignaciones de controlador**.  
  
    3.  En el panel **Acciones** , haga clic en **Agregar asignación de módulo**.  
  
    4.  En **Ruta de acceso de solicitudes** , escriba **replisapi.dll**.  
  
    5.  En la lista desplegable **Módulo** , seleccione **IsapiModule**.  
  
    6.  En **Ejecutable**, escriba **\<unidad>:\Inetpub\SQLReplication\replisapi.dll**.  
  
    7.  En **Nombre**especifique **Replisapi**.  
  
    8.  Haga clic en el botón **Restricciones de solicitudes** , en la pestaña **Acceso** y, a continuación, en **Ejecutar**.  
  
    9. Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Restricciones de solicitudes** y, a continuación, haga clic de nuevo en **Aceptar** para cerrar el cuadro de diálogo **Agregar asignación de módulo** . Cuando se le pida que permita la extensión ISAPI, haga clic en **Sí** para agregar la extensión.  
  
    10. Compruebe que Replisapi.dll está en la lista, en las asignaciones de controlador **Habilitadas** . Si está en la lista **Deshabilitadas** , haga clic con el botón secundario en la entrada de Replisapi y, a continuación, haga clic en **Modificar permisos de características**. Active la casilla **Ejecutar** y haga clic en **Aceptar**.  
  
## <a name="configuring-iis-authentication"></a>Configurar la autenticación IIS  
 Cuando los equipos suscriptores se conectan a IIS, IIS debe autenticarlos para que puedan tener acceso a los recursos y procesos. La autenticación se puede aplicar a todo el sitio web o al directorio virtual que ha creado.  
  
 Se recomienda usar la autenticación básica con SSL. SSL es necesario, independientemente del tipo de autenticación que se utilice.  
  
 Se recomienda usar la autenticación básica con SSL. SSL es necesario, independientemente del tipo de autenticación que se utilice.  
  
#### <a name="to-configure-iis-authentication"></a>Para configurar la autenticación IIS  
  
1.  En **Administrador de Internet Information Services (IIS)**, haga clic en **Sitio web predeterminado**.  
  
2.  En el panel central, haga doble clic en **Autenticación**.  
  
3.  Haga clic con el botón secundario en Autenticación anónima y, a continuación, elija Deshabilitar.  
  
4.  Haga clic con el botón secundario en Autenticación básica y, a continuación, elija Habilitar.  
  
## <a name="configuring-secure-sockets-layer"></a>Configurar la Capa de sockets seguros (SSL)  
 Para configurar SSL, especifique un certificado para que lo utilice el equipo en el que se ejecuta IIS. La sincronización web para la replicación de mezcla es compatible con el uso de certificados de servidor, pero no de certificados de cliente. Para configurar IIS para implementación, primero debe obtener un certificado por parte de una entidad de certificación (CA). Para obtener más información acerca de los certificados, vea la documentación de IIS.  
  
 Cuando el certificado esté instalado, debe asociarlo al sitio web que utiliza la sincronización web. En el caso las tareas de desarrollo y pruebas, puede especificar un certificado autofirmado. IIS 7 puede crear un certificado y registrarlo en el equipo.  
  
 La diferencia entre las implementaciones para producción y los procedimientos descritos aquí es que en producción y las pruebas de pre-producción se utilizaría un certificado emitido por una entidad de certificación en lugar de un certificado autofirmado.  
  
> [!IMPORTANT]  
>  No es recomendable utilizar un certificado autofirmado en una instalación de producción. Los certificados autofirmados no son seguros. Utilice certificados autofirmados solo en instalaciones de desarrollo y pruebas.  
  
 Para configurar SSL, debe realizar estos pasos:  
  
1.  Configure el sitio web para requiera SSL y pase por alto los certificados de cliente.  
  
2.  Obtenga un certificado de una entidad de certificación o cree un certificado autofirmado.  
  
3.  Enlace el certificado al sitio web de replicación.  
  
#### <a name="to-require-ssl-security-for-a-web-site"></a>Para exigir la seguridad SSL en un sitio web  
  
1.  En el **Administrador de Internet Information Services (IIS)**, expanda el nodo de servidor local y, a continuación, haga clic en **Sitio web predeterminado** (o el sitio de sincronización web si es diferente del sitio web predeterminado).  
  
2.  En el panel central, haga doble clic en **Configuración SSL**.  
  
3.  Active la opción **Requerir SSL** . En **Certificados cliente**, compruebe que el botón **Omitir** está seleccionado.  
  
#### <a name="to-create-a-self-signed-certificate-for-testing"></a>Para crear un certificado autofirmado para pruebas  
  
1.  En el **Administrador de Internet Information Services (IIS)**, haga clic en el nodo de servidor local y, a continuación, en el panel del centro, haga doble clic en **Certificados de servidor**.  
  
2.  En el panel **Acciones** , haga clic en **Crear certificado autofirmado**.  
  
3.  En el cuadro de diálogo **Crear certificado autofirmado** , escriba un nombre para el certificado y, a continuación, haga clic en **Aceptar**.  
  
###### <a name="to-bind-a-certificate-to-a-web-site"></a>Para enlazar un certificado a un sitio web  
  
1.  En el panel **Conexiones** , haga clic en **Sitio web predeterminado** (o el sitio de sincronización web, si es diferente del sitio web predeterminado).  
  
2.  En el panel **Acciones** , haga clic en **Enlaces**y, a continuación, haga clic en **Agregar**. Se abre el cuadro de diálogo **Agregar enlace de sitio** .  
  
3.  En la lista desplegable **Tipo** , seleccione **https**. Mantenga la configuración predeterminada en **Dirección IP** y **Puerto**.  
  
4.  En la lista desplegable **Certificado SSL** , seleccione el certificado creado en "Para crear un certificado autofirmado para pruebas", haga clic en **Aceptar**y, a continuación, en **Cerrar**.  
  
###### <a name="to-test-the-certificate"></a>Para probar el certificado  
  
1.  En **Enternet Enformation Services (IIS) Manager**, haga clic en **Sitio web predeterminado.**  
  
2.  En el panel **Acciones**, haga clic en **Examinar \*:443(https)**.  
  
3.  Se abre Internet Explorer, con un mensaje que indica que "Hay un problema con el certificado de seguridad de este sitio web". Esta advertencia indica que el certificado asociado no fue emitido por una entidad de certificación reconocida y podría no ser de confianza. Es una advertencia esperada, de modo que haga clic en **Pasar a este sitio web (no recomendado)**.  
  
4.  Si se pide confirmación para **Conectar a localhost**, escriba un nombre de usuario y contraseña para continuar. Debe aparecer la página predeterminada del sitio web.  
  
## <a name="setting-permissions-for-the-sql-server-replication-listener"></a>Establecer los permisos para la Escucha de replicación de SQL Server  
 Cuando un equipo suscriptor se conecta al equipo en el que se ejecuta IIS, se autentica usando el tipo de autenticación especificado al configurar IIS. Tras autenticar al suscriptor, IIS comprueba si el suscriptor está autorizado para invocar la replicación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Debe controlar los usuarios que pueden invocar la replicación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estableciendo permisos para replisapi.dll. Es necesario configurar permisos para impedir el acceso no autorizado a la replicación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Para configurar los permisos mínimos para la cuenta con la que se ejecuta la Escucha de replicación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , lleve a cabo el siguiente procedimiento. Los pasos del siguiente procedimiento son únicamente para [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows Server 2008 con IIS 7.0.  
  
 Además de realizar los siguientes pasos, asegúrese de que los inicios de sesión necesarios se encuentran en la lista de acceso a la publicación (PAL). Para obtener más información sobre la PAL, vea [Secure the Publisher](../../relational-databases/replication/security/secure-the-publisher.md) (Proteger el publicador).  
  
 **Importante** La cuenta creada en esta sección es la cuenta que se conectará al publicador y el distribuidor durante la sincronización. La cuenta se debe agregar como cuenta de inicio de sesión SQL en el servidor de distribución y publicación.  
  
 La cuenta utilizada para la Escucha de replicación de SQL Server debe tener los permisos descritos en el tema sobre seguridad del agente de mezcla, en la sección sobre conexión al publicador o distribuidor.  
  
 En resumen, la cuenta debe:  
  
-   Ser miembro de la lista de acceso a la publicación (PAL).  
  
-   Estar asignada un inicio de sesión asociado a un usuario en la base de datos de publicaciones.  
  
-   Estar asignada un inicio de sesión asociado a un usuario en la base de datos de distribución.  
  
-   Tener permisos de lectura en el recurso compartido de instantáneas.  
  
#### <a name="to-configure-the-account-and-permissions"></a>Para configurar la cuenta y los permisos  
  
1.  Cree una cuenta local en el equipo en el que se ejecuta IIS:  
  
    1.  Abra el **Administrador del servidor**. En el menú Inicio, haga clic con el botón secundario en **Equipo**y, a continuación, en **Administrar**.  
  
    2.  En el **Administrador del servidor**, expanda **Configuración**y, a continuación, expanda **Usuarios y grupos locales**.  
  
    3.  Haga clic con el botón secundario en **Usuarios**y después en **Usuario nuevo**.  
  
    4.  Escriba un nombre de usuario y una contraseña segura. Desactive **El usuario debe cambiar la contraseña en el siguiente inicio de sesión**.  
  
    5.  Haga clic en **Crear**y, a continuación, en **Cerrar**.  
  
2.  Agregue la cuenta al grupo IIS_IUSRS:  
  
    1.  En el **Administrador del servidor**, expanda **Configuración**, expanda **Usuarios y grupos locales**y después haga clic en **Grupos**.  
  
    2.  Haga clic con el botón secundario en **IIS_IUSRS**y, después, en **Agregar a grupo**.  
  
    3.  En el cuadro de diálogo **Propiedades de IIS_IUSRS** , haga clic en **Agregar**.  
  
    4.  En el cuadro de diálogo **Seleccionar usuarios, equipos o grupos** , agregue la cuenta que creó en el paso 1.  
  
    5.  Compruebe que en **Desde esta ubicación** aparece el nombre del equipo local (no un dominio). Si no aparece el nombre del equipo local, haga clic en **Ubicaciones**. En el cuadro de diálogo **Ubicaciones** , seleccione el equipo local y, a continuación, haga clic en **Aceptar**.  
  
    6.  Haga clic en **Aceptar** en los cuadros de diálogo **Seleccionar usuarios** , haga clic en**Aceptar**.  
  
3.  Conceda los permisos mínimos de cuenta en la carpeta que contiene el archivo replisapi.dll:  
  
    1.  En el Explorador de Windows, haga clic con el botón secundario en la carpeta que ha creado para replisapi.dll y, a continuación, haga clic en **Propiedades**.  
  
    2.  En la pestaña **Seguridad** , haga clic en **Editar**.  
  
    3.  En el cuadro de diálogo **Permisos de \<nombreDeCarpeta>**, haga clic en **Agregar** para agregar la cuenta que creó en el paso 1.  
  
    4.  Compruebe que en **Desde esta ubicación** aparece el nombre del equipo local (no un dominio). Si no aparece el nombre del equipo local, haga clic en **Ubicaciones**. En el cuadro de diálogo **Ubicaciones** , seleccione el equipo local y, a continuación, haga clic en **Aceptar**.  
  
    5.  Compruebe que la cuenta solo tiene permisos de **Lectura**, **Lectura y ejecución** y **Mostrar el contenido de la carpeta**.  
  
    6.  Seleccione los usuarios o grupos que no requieran acceso al directorio , haga clic en **Quitar**y, después, en **Aceptar**.  
  
4.  Cree un grupo de aplicaciones en **Administrador de Internet Information Services (IIS)**:  
  
    1.  En **Administrador de Internet Information Services (IIS)**, en el panel **Conexiones** , expanda el nodo del servidor local.  
  
    2.  Haga clic con el botón secundario en **Grupos de aplicaciones**y haga clic en **Grupo de aplicaciones**.  
  
    3.  Escriba un nombre para el grupo de aplicaciones, deje los valores predeterminado para el resto de los campos y, a continuación, haga clic en **Aceptar**.  
  
    > [!NOTE]  
    >  Si piensa que va a tener más de dos clientes de sincronización simultáneos, podría crear hospedaje multiproceso en una única máquina. Para obtener más información, consulte la sección Crear hospedaje multiproceso en una única máquina de [Configure Web Synchronization](../../relational-databases/replication/configure-web-synchronization.md).  
  
5.  Asocie la cuenta al grupo de aplicaciones:  
  
    1.  En **Administrador de Internet Information Services (IIS)**, expanda el nodo del servidor y, después, haga clic en **Grupos de aplicaciones**.  
  
    2.  Haga clic con el botón secundario en el grupo de aplicaciones que ha creado y, a continuación, haga clic en **Establecer valores predeterminados de grupos de aplicaciones**.  
  
    3.  En el cuadro de diálogo **Valores predeterminados de grupo de aplicaciones** , desplácese a la sección **Procesar modelo** y, a continuación, haga clic en el campo **Identidad** .  
  
    4.  Haga clic en el botón de puntos suspensivos que hay en el lado derecho de la fila **Identidad** .  
  
    5.  Haga clic en el botón de radio **Cuenta personalizada** y, a continuación, en **Establecer**.  
  
    6.  En los campos **Nombre de usuario** y **Contraseña** , escriba la cuenta y la contraseña que creó en el paso 1 y, después, haga clic en **Aceptar**.  
  
    7.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Identidad de grupo de aplicaciones** y, a continuación, de nuevo en **Aceptar** para cerrar el cuadro de diálogo **Valores predeterminados de grupo de aplicaciones**.  
  
6.  Asocie el grupo de aplicaciones al sitio web de replicación:  
  
    1.  En el **Administrador de Internet Information Services (IIS)**, expanda el nodo de servidor local y, a continuación, haga clic en **Sitio web predeterminado** (o el sitio de sincronización web si es diferente del sitio web predeterminado).  
  
    2.  En el panel **Acciones** , en **Administrar sitio web**, haga clic en **Configuración avanzada**.  
  
    3.  En el cuadro de diálogo **Configuración avanzada** , haga clic en el botón de puntos suspensivos que hay a la derecha de **Grupo de aplicaciones**.  
  
    4.  En la lista desplegable **Grupo de aplicaciones** , seleccione el grupo de aplicaciones que ha creado en el paso 4 y, a continuación, haga clic en **Aceptar**.  
  
    5.  Vuelva a hacer clic en **Aceptar** para cerrar Configuración avanzada.  
  
## <a name="testing-the-connection-to-replisapidll"></a>Probar la conexión con replisapi.dll  
 Ejecute la sincronización web en modo de diagnóstico para probar la conexión al equipo en el que se ejecuta IIS y para asegurarse de que el certificado SSL (Capa de sockets seguros) está instalado correctamente. Para ejecutar la sincronización web en modo de diagnóstico, debe ser administrador en el equipo donde se ejecuta IIS.  
  
#### <a name="to-test-the-connection-to-replisapidll"></a>Para probar la conexión con replisapi.dll  
  
1.  Asegúrese de que la configuración de red de área local (LAN) del suscriptor es correcta:  
  
    1.  En [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Explorer, en el menú **Herramientas** , haga clic en **Opciones de Internet**.  
  
    2.  En la pestaña **Conexiones** , haga clic en **Configuración de LAN**.  
  
    3.  Si no se utiliza ningún servidor proxy en la configuración de red de área local (LAN), desactive las casillas **Detectar la configuración automáticamente** y **Utilizar un servidor proxy para su LAN**.  
  
    4.  Si se utiliza un servidor proxy, haga clic en **Utilizar un servidor proxy para su LAN** y **No usar servidor proxy para direcciones locales**y, después, en **Aceptar**.  
  
2.  En el suscriptor, en Internet Explorer, conéctese al servidor en modo de diagnóstico agregando `?diag` a la dirección de replisapi.dll. Por ejemplo: `https://server.domain.com/directory/replisapi.dll?diag`.  
  
    > [!NOTE]  
    >  En el ejemplo anterior, **servidor.dominio.com** se debe reemplazar con el nombre de **Emitido** exacto que aparece en la sección **Certificados de servidor** en el Administrador de IIS.  
  
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
 [Sincronización web para la replicación de mezcla](../../relational-databases/replication/web-synchronization-for-merge-replication.md)   
 [Configurar la sincronización web](../../relational-databases/replication/configure-web-synchronization.md)  
  
  
