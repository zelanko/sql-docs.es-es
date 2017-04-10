---
title: "Conectar con un servidor de informes en Management Studio | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "servidores de informes [Reporting Services], conexiones"
  - "conexiones [Reporting Services], servidor de informes"
  - "registrar servidores de informes"
  - "servidores de informes [Reporting Services], registrar"
ms.assetid: c875ff87-ee7d-443a-a702-bdb4b6c27c6e
caps.latest.revision: 53
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 53
---
# Conectar con un servidor de informes en Management Studio
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] proporciona el Explorador de objetos, que permite conectarse a cualquier servidor de la familia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y examinar su contenido de forma gráfica. Para Reporting Services, puede usar el Explorador de objetos para hacer lo siguiente:  
  
-   Habilitar las características del servidor de informes.  
  
-   Establecer los valores predeterminados de servidor y configurar las definiciones de roles.  
  
-   Administrar trabajos que se están ejecutando.  
  
-   Administrar las programaciones de los trabajos.  
  
 Puede conectarse a un servidor de informes en modo nativo o a un servidor de informes que se ejecuta en el modo integrado con SharePoint. La sintaxis de conexión y los tipos de operaciones que puede realizar variarán dependiendo del modo de servidor del servidor de informes y de sus permisos. Si tiene dificultades al conectarse a un servidor de informes o al realizar tareas concretas, podría deberse a que dispone de permisos insuficientes o que ha especificado el nombre del servidor de informes incorrectamente. Para obtener más información sobre permisos y la sintaxis de conexión, vea la tabla que se encuentra al final de este tema.  
  
 Tenga en cuenta que no puede usar el Explorador de objetos para ver o administrar el contenido del servidor de informes. La administración de contenido se lleva a cabo a través del Administrador de informes si el servidor de informes se ejecuta en modo nativo o a través de un sitio de SharePoint si el servidor de informes se ejecuta en el modo integrado con SharePoint.  
  
 El Explorador de objetos le permite abrir conexiones en varias instancias del servidor en la misma área de trabajo siempre y cuando los servidores se registren en el mismo grupo de servidores. Para poderse conectar a una instancia del servidor de informes en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], se debe registrar el servidor. Si el servidor de informes ya está registrado, puede omitir este paso. Al final de este tema encontrará instrucciones para registrar servidores de informes.  
  
### Para conectarse a un servidor de informes en modo nativo  
  
1.  Si el Explorador de objetos no está abierto todavía, selecciónelo en el menú Ver.  
  
2.  Haga clic en **Conectar** para ver la lista de tipos de servidor y, a continuación, seleccione **Reporting Services**.  
  
3.  En el cuadro de diálogo **Conectar al servidor** , escriba el nombre de la instancia del servidor de informes. Los nombres de instancia del servidor de informes se basan en nombres de instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . De manera predeterminada, el nombre de una instancia del servidor de informes local es únicamente el nombre del equipo. Si ha instalado el servidor de informes como una instancia con nombre, use esta sintaxis para especificar el servidor: *\<nombreDeServidor>[\\<nombreDeInstancia\>]*.  
  
4.  Seleccione el tipo de autenticación. Si está usando la autenticación de Windows, debe conectarse usando sus credenciales. Si selecciona la autenticación básica o la autenticación de formularios, escriba la cuenta y la contraseña.  
  
5.  Haga clic en **Conectar**. El servidor de informes se muestra en el Explorador de objetos.  
  
6.  Haga clic con el botón secundario en el nodo del servidor para establecer propiedades del sistema y valores predeterminados del servidor. Para obtener más información, vea [Establecer las propiedades del servidor de informes &#40;Management Studio&#41;](../../reporting-services/tools/set-report-server-properties-management-studio.md).  
  
### Para conectarse a un servidor de informes en el modo integrado con SharePoint  
  
1.  Si el Explorador de objetos no está abierto todavía, selecciónelo en el menú Ver.  
  
2.  Haga clic en Conectar para ver la lista de tipos de servidor y, a continuación, seleccione **Reporting Services**.  
  
3.  En el cuadro de diálogo **Conectar al servidor** , escriba una dirección URL para un sitio de SharePoint. En el ejemplo siguiente se muestra la sintaxis http://\<servidor web>/sitios/\<sitio>.  
  
4.  Seleccione el tipo de autenticación. Si está usando la autenticación de Windows, debe conectarse usando sus credenciales. Si selecciona la autenticación básica o la autenticación de formularios, escriba la cuenta y la contraseña.  
  
5.  Haga clic en **Conectar**. El servidor de informes se muestra en el Explorador de objetos.  
  
6.  Haga clic con el botón secundario en el nodo del servidor para establecer propiedades del sistema y valores predeterminados del servidor. Para obtener más información, vea [Establecer las propiedades del servidor de informes &#40;Management Studio&#41;](../../reporting-services/tools/set-report-server-properties-management-studio.md).  
  
### Para registrar un servidor de informes  
  
1.  Si no puede conectarse a un servidor de informes, no tiene el permiso para tener acceso al mismo o se debe registrar. Para registrar el servidor, haga clic en **Servidores registrados** en el menú Ver.  
  
2.  Haga clic en el icono Reporting Services.  
  
3.  Haga clic con el botón derecho en **Reporting Services**, seleccione **Nuevo **y, después, haga clic en **Registro de servidor**. Se muestra el cuadro de diálogo **Nuevo registro de servidor** .  
  
4.  Para **Nombre del servidor**, escriba un valor. El valor que debe especificar variará según el modo de servidor:  
  
    -   Para un servidor de informes en modo nativo, escriba el nombre de la instancia del servidor de informes. Los nombres de instancia del servidor de informes se basan en nombres de instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . De manera predeterminada, el nombre de una instancia del servidor de informes local es únicamente el nombre del equipo. Si ha instalado el servidor de informes como una instancia con nombre, use esta sintaxis para especificar el servidor: *\<nombreDeServidor>[\\<nombreDeInstancia\>]*.  
  
    -   Para un servidor de informes que se ejecuta en el modo integrado con SharePoint, el servidor al que se va a conectar es el sitio de SharePoint con el que el servidor de informes está conectado. La conexión al sitio de SharePoint es necesaria para poder ver los niveles de permiso que controlan el acceso a las operaciones y el contenido del servidor de informes. Puede especificar cualquier sitio de la colección de sitios. El ejemplo siguiente muestra la sintaxis: http://misitiosharepoint.  
  
5.  En **Autenticación**, seleccione qué modo de autenticación desea utilizar para obtener acceso al servidor web. Debe elegir el modo de autenticación que el servidor de informes ya está utilizando.  
  
    -   Si está utilizando seguridad predeterminada, elija **Autenticación de Windows**.  
  
    -   Si ha instalado e implementado una extensión de seguridad personalizada, elija **Autenticación de formularios**.  
  
    -   Si configurara el servidor de informes para usar la autenticación básica, elija **Autenticación básica**.  
  
    -   Si el servidor de informes se configura para el modo integrado con SharePoint, elija **Autenticación de Windows**.  
  
6.  Haga clic en **Probar** para comprobar la conexión.  
  
7.  Cuando se le solicite, haga clic en **Aceptar**y después en **Guardar**.  
  
## Permisos y sintaxis de conexión  
 En la tabla siguiente se resume la sintaxis de conexión, las operaciones y los permisos requeridos para realizar operaciones concretas.  
  
 Al especificar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] como el tipo de servidor en el cuadro de diálogo **Conectar al servidor** , puede especificar un nombre de servidor de informes o un extremo para el servicio web.  
  
|Conectar a|Tareas|Permissions|  
|----------------|-----------|-----------------|  
|Servidor de informes en modo nativo, conectado como la instancia con nombre o predeterminada:<br /><br /> \<nombre de servidor>\<_instancia><br /><br /> La conexión al servidor de informes se realiza a través del proveedor WMI del servidor de informes.|Ver y establecer las propiedades del servidor y los valores predeterminados.<br /><br /> Ver y cancelar trabajos.<br /><br /> Crear y administrar programaciones compartidas.<br /><br /> Crear, modificar o eliminar definiciones de roles.|Se asigna al rol Administrador del sistema.|  
|Servidor de informes en modo nativo, conectado como la instancia con nombre o predeterminada, a través del extremo al servicio web del servidor de informes:<br /><br /> http://\<nombreDelServidor>/ReportServer<br /><br /> La especificación de una dirección URL al servidor de informes ofrece una manera alternativa de conectarse al servidor de informes.|Ver y establecer las propiedades del servidor y los valores predeterminados.<br /><br /> Ver y cancelar trabajos.<br /><br /> Crear y administrar programaciones compartidas.<br /><br /> Crear, modificar o eliminar definiciones de roles.|Se asigna al rol Administrador del sistema.|  
|Servidor de informes en el modo integrado con SharePoint, conectado a través del sitio de SharePoint:<br /><br /> http://\<servidorWeb>/\<sitioDeSharePoint>|Ver y establecer las propiedades del servidor y los valores predeterminados.<br /><br /> Ver y cancelar trabajos.<br /><br /> Crear y administrar programaciones compartidas definidas para el sitio al que está conectado.<br /><br /> Ver los niveles de permisos definidos para el sitio al que está conectado.|Nivel de permiso de Control total en el sitio de SharePoint al que está conectado.|  
|Servidor de informes en el modo con SharePoint, conectado a través del nombre de la instancia del servidor de informes:<br /><br /> \<nombre de servidor>\<_instancia>|Ver y establecer las propiedades del servidor y los valores predeterminados.<br /><br /> Ver y cancelar trabajos.|El nivel de permiso Control total en el sitio de SharePoint que está integrado con el servidor de informes.<br /><br /> Tenga en cuenta que, cuando se conecta al servidor de informes en lugar del sitio de SharePoint, se reduce significativamente el número de tareas que puede realizar. Esto se debe a que el servidor de informes solamente puede devolver datos de aplicación almacenadas o administradas en la base de datos del servidor de informes, y no en la configuración de SharePoint y en las bases de datos de contenido.|  
  
## Vea también  
 [Configurar una conexión a la base de datos del servidor de informes &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [Reporting Services en SQL Server Management Studio &#40;SSRS&#41;](../../reporting-services/tools/reporting-services-in-sql-server-management-studio-ssrs.md)  
  
  