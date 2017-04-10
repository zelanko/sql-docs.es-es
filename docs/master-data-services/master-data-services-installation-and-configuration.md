---
title: "Instalaci&#243;n y configuraci&#243;n de Master Data Services | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
ms.assetid: f6cd850f-b01b-491f-972c-f966b9fe4190
caps.latest.revision: 44
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 37
---
# Instalaci&#243;n y configuraci&#243;n de Master Data Services
  En este artículo se describe cómo instalar [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] en una máquina con Windows Server 2012 R2, configurar la base de datos y el sitio web de MDS e implementar los modelos y datos de ejemplo. [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] (MDS) le permite a su organización administrar una versión de datos de confianza.   
   
Para obtener información general sobre cómo organizar los datos en [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)], consulte [Introducción a Master Data Services (MDS)](../master-data-services/master-data-services-overview-mds.md).     
  
 Para obtener información sobre las nuevas características de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)], consulte [Novedades en Master Data Services &#40;MDS&#41;](../master-data-services/what-s-new-in-master-data-services-mds.md).  
 
Para obtener vínculos a los vídeos y a otros recursos de aprendizaje de [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)], consulte [Información sobre SQL Server Master Data Services](../master-data-services/learn-sql-server-master-data-services.md). 
  
> **Descargar**  
>-   Para descargar [!INCLUDE[ssSQL15](../includes/sssql15-md.md)], vaya al  **[Centro de evaluación](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016)**.  
>-   ¿Tiene una cuenta de Azure?  Si es así, haga clic **[aquí](https://azure.microsoft.com/en-us/marketplace/partners/microsoft/sqlserver2016rtmenterprisewindowsserver2012r2/?wt.mc_id=sqL16_vm)** para poner en marcha una máquina virtual con [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]  ya instalado.  
 
> **¿No puede crear un sitio web de MDS?**
>>Consulte este artículo de soporte técnico de Microsoft para obtener instrucciones sobre cómo resolver este problema.
[No se puede crear un sitio web de MDS mediante una cuenta con pocos privilegios en SQL Server 2016](https://aka.ms/mdssupport) 
  
## <a name="installing-master-data-services-and-iis-roles-and-features"></a>Instalar roles y características de Master Data Services e IIS  
 Use el asistente para la instalación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o un símbolo del sistema para instalar [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)].  
  
 **Para instalar [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] con Instalación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en una máquina con Windows Server 2012 R2**  
  
1.  Haga doble clic en Setup.exe y siga los pasos del asistente para la instalación.  
  
2.  Seleccione [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] en la página **Selección de características** en **Características compartidas**.  
  
     Esto instala [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)], ensamblados, un complemento de Windows PowerShell y carpetas y archivos para las aplicaciones y los servicios web.  
  
     ![mds_SQLServer2016Setup_FeatureSelection](../master-data-services/media/mds-sqlserver2016setup-featureselection.png "mds_SQLServer2016Setup_FeatureSelection")  
  
3.  Complete el asistente para la instalación.  
  
4.  En [!INCLUDE[winblue_server_2](../includes/winblue-server-2-md.md)], haga clic en el icono **Administrador del servidor** de la barra de tareas en el **Escritorio**.  
  
     ![Icon for the Server Manager in Windows Server 2012 taskbar](../master-data-services/media/mds-windowsservertaskbar-servermanagericon.png "Icon for the Server Manager in Windows Server 2012 taskbar")  
  
5.  En **Administrador del servidor**, haga clic en **Agregar roles y características** en el menú **Administrar** .  
  
     ![In Server Manage, the Add Roles and Features menu command](../master-data-services/media/mds-servermanagerdashboard-addrolesfeaturesmenu.png "In Server Manage, the Add Roles and Features menu command")  
  
6.  En la página **Tipo de instalación** del **Asistente para agregar roles y características**, acepte el valor predeterminado (**Instalación basada en características o en roles**) y haga clic en **Siguiente**.  
  
7.  Haga clic en **Seleccionar un servidor del grupo de servidores**y, después, haga clic en el servidor en el que ha instalado [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)].  
  
     ![Server Selection page on the Add Roles and Features Wizard](../master-data-services/media/mds-servermanagerdashboard-addrolesandfeatureswizard-serverselection.png "Server Selection page on the Add Roles and Features Wizard")  
  
8.  En el cuadro **Roles** , haga clic en los roles y en los servicios de rol que se necesitan para [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] en [!INCLUDE[winblue_server_2](../includes/winblue-server-2-md.md)]y, luego, haga clic en **Siguiente**. En las siguientes imágenes se muestran los roles y servicios de rol necesarios seleccionados.  
  
    > [!WARNING]  
    >  No instale el servicio de rol Publicación en WebDAV. Publicación en WebDAV no es compatible con [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)].  
  
    > [!IMPORTANT]  
    > La **compresión de contenido dinámico** está habilitada de manera predeterminada. Esto disminuye considerablemente el tamaño de la respuesta xml y reduce la E/S de red, aunque el uso de CPU aumenta.  Para obtener más información, vea **[CTP 2.0] Rendimiento mejorado** in [What's New in Master Data Services &#40;MDS&#41;](../master-data-services/what-s-new-in-master-data-services-mds.md).  
  
    |Roles y servicios de rol|Roles y servicios de rol|  
    |-----------------------------|-----------------------------|  
    |![Common HTTP Features](../master-data-services/media/mds-servermanagerdashboard-commonhttpfeaturesroles.png "Common HTTP Features")|![Health Diagnostics Roles](../master-data-services/media/mds-servermanagerdashboard-healthdiagnosticsroles.png "Health Diagnostics Roles")|  
    |![Performance Roles](../master-data-services/media/mds-servermanagerdashboard-performanceroles.png "Performance Roles")|![Security Roles](../master-data-services/media/mds-servermanagerdashboard-securityroles.png "Security Roles")|  
    |![WebServer Application Development Roles](../master-data-services/media/mds-servermanagerdashboard-webserverapplicationdevelopmentroles.png "WebServer Application Development Roles")|![Management Tools](../master-data-services/media/mds-servermanagerdashboard-managementtoolsroles.png "Management Tools")|  
  
     Para obtener una lista de los roles y servicios de roles necesarios en otros sistemas operativos, consulte [Requisitos de la aplicación web &#40;Master Data Services&#41;](../master-data-services/install-windows/web-application-requirements-master-data-services.md).  
  
9. En el cuadro **Características** , haga clic en las características necesarias para [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] en [!INCLUDE[winblue_server_2](../includes/winblue-server-2-md.md)]y, luego, haga clic en **Siguiente**. En las siguientes imágenes se muestran las características necesarias seleccionadas.  
  
    |Características|Características|  
    |--------------|--------------|  
    |![Net Framework Features](../master-data-services/media/mds-servermanagerdashboard-netframeworkfeatures.png "Net Framework Features")|![Windows Process Features](../master-data-services/media/mds-servermanagerdashboard-windowsprocessfeatures.png "Windows Process Features")|  
  
     Para obtener una lista de las características necesarias en otros sistemas operativos, consulte [Requisitos de la aplicación web &#40;Master Data Services&#41;](../master-data-services/install-windows/web-application-requirements-master-data-services.md).  
  
 Para obtener más información sobre la instalación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] con el programa de instalación, consulte [Instalación de SQL Server 2016 desde el Asistente para la instalación &#40;programa de instalación&#41;](../database-engine/install-windows/install-sql-server-2016-from-the-installation-wizard-setup.md).  
  
 Para obtener más información sobre la instalación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mediante un símbolo del sistema, consulte [Instalar SQL Server 2016 desde el símbolo del sistema](../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md). Si se usa un símbolo del sistema, [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] está disponible como parámetro de característica.  
  
 Para obtener una descripción breve con vínculos a información adicional sobre las tareas previas a la instalación, consulte [Instalar Master Data Services](../master-data-services/install-windows/install-master-data-services.md).  
  
##  <a name="a-namesetupweba-setting-up-the-database-and-website"></a><a name="SetUpWeb"></a> Configurar la base de datos y el sitio web  
 **Configurar la base de datos y el sitio web mediante el ** de [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]  
  
1.  Inicie el [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]y haga clic en **Configuración de base de datos** en el panel izquierdo.  
  
2.  Haga clic en **Crear base de datos**y, después, haga clic en **Siguiente** en el **Asistente para crear bases de datos**.  
  
3.  En la página **Servidor de base de datos** , seleccione el **Tipo de autenticación** y, después, haga clic en **Probar conexión** para confirmar que puede conectarse a la base de datos con las credenciales del tipo de autenticación seleccionado.  
  
    > [!NOTE]  
    >  Al seleccionar **Usuario actual: Seguridad integrada** como el tipo de autenticación, el cuadro **Nombre de usuario** es de solo lectura y muestra el nombre de la cuenta de usuario de Windows con la que se ha iniciado sesión en el equipo.  
  
     ![The Database server page in the Create Database Wizard](../master-data-services/media/mds-configurationmanager-createdatabasewizard-serverpage.png "The Database server page in the Create Database Wizard")  
  
4.  Escriba un nombre en el campo **Nombre de la base de datos** . Opcionalmente, para seleccionar una intercalación de Windows y especificar una o varias de los opciones disponibles, como **Distinguir mayúsculas de minúsculas**, desactive la casilla **Intercalación predeterminada de SQL Server** .  
  
     ![The Database page in the Create Database Wizard](../master-data-services/media/mds-configurationmanager-createdatabasewizard-databasepage.png "The Database page in the Create Database Wizard")  
  
     Para obtener más información sobre la intercalación de Windows, consulte [Nombre de intercalación de Windows (Transact-SQL)](https://msdn.microsoft.com/library/ms188046.aspx).  
  
5.  En el campo **Nombre de usuario** , especifique la cuenta de Windows del usuario que será el superusuario predeterminado de Master Data Services. Un superusuario tiene acceso a todas las áreas funcionales y puede agregar, eliminar y actualizar todos los modelos.  
  
     ![The Administrator Account page in the Create Database Wizard.](../master-data-services/media/mds-configurationmanager-createdatabasewizard-adminpage.png "The Administrator Account page in the Create Database Wizard.")  
  
6.  Haga clic en **Siguiente** para ver un resumen de la configuración de la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] y, luego, haga clic en **Siguiente** para crear la base de datos.  
  
     Para obtener información sobre la configuración del **Asistente para crear bases de datos**, consulte [Asistente para crear bases de datos &#40;Administrador de configuración de Master Data Services&#41;](../master-data-services/create-database-wizard-master-data-services-configuration-manager.md).  
  
7.  En la página Configuración de base de datos en el [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)], haga clic en Seleccionar base de datos.  
  
8.  Haga clic en **Conectar**y, después, seleccione la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] que ha creado en el paso 6.  
  
     ![Connect to Database dialog box for the Database Configuration page](../master-data-services/media/mds-configurationmanager-selectdatabasebutton-connecttodatabasedialog.png "Connect to Database dialog box for the Database Configuration page")  
  
     Ha terminado de configurar la base de datos. En la página **Configuración de base de datos** se muestra ahora la instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a la que está conectado para [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], la base de datos que ha creado y la versión actual de la base de datos.  
  
     ![Database Configuration page in the Configuration Manager shows a completed database setup.](../master-data-services/media/mds-configurationmanager-databaseconfig-completed.png "Database Configuration page in the Configuration Manager shows a completed database setup.")  
  
9. En [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)], haga clic en **Configuración web** en el panel izquierdo.  
  
10. En el cuadro de lista **Sitio web** , haga clic en **Sitio web predeterminado**y, luego, haga clic en **Crear** para crear una aplicación web.  
  
    > [!NOTE]  
    >  Al seleccionar **Sitio web predeterminado**, debe crear una aplicación web. Si selecciona **Crear nuevo sitio web** en el cuadro de lista, la aplicación se crea de forma automática.  
  
     ![Web Configuration page in the Configuration Manager](../master-data-services/media/mds-configurationmanager-webconfig.png "Web Configuration page in the Configuration Manager")  
  
11. En la sección **Grupo de aplicaciones** , realice una de las siguientes acciones.  
  
    -   Escriba el mismo nombre de usuario que ha escrito en el paso 5 para la **Cuenta de administrador**de la base de datos, escriba la contraseña y, después, haga clic en **Aceptar**.  
  
         ** O bien **  
  
    -   Seleccione otro nombre de usuario, escriba la contraseña y, luego, haga clic en Aceptar.  
  
         No tiene que usar la misma cuenta al crear la base de datos y la aplicación web.  
  
     ![Create Web Application dialog box, Web Configuration page](../master-data-services/media/mds-configurationmanager-webconfig-createwebapplication.png "Create Web Application dialog box, Web Configuration page")  
  
     Para obtener más información sobre el cuadro de diálogo **Crear aplicación web**, consulte [Cuadro de diálogo Crear aplicación web &#40;Administrador de configuración de Master Data Services&#41;](../master-data-services/create-web-application-dialog-box-master-data-services-configuration-manager.md).  
  
12. En la página **Configuración web** en el cuadro **Aplicación web**, haga clic en la aplicación que ha creado y, luego, haga clic en **Seleccionar** en la sección **Asociar aplicación a base de datos**.  
  
13. Haga clic en **Conectar**, seleccione la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] que quiera asociar a la aplicación web y, después, haga clic en **Aceptar**.  
  
     Ha terminado de configurar el sitio web. En la página **Configuración web** se muestra ahora el sitio web que ha seleccionado, la aplicación web que ha creado y la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] asociada a la aplicación.  
  
     ![The completed Web site configuration](../master-data-services/media/mds-configurationmanager-webconfig-completed.png "The completed Web site configuration")  
  
     Para obtener más información sobre la configuración de la página Configuración web, consulte [Página Configuración web &#40;Administrador de configuración de Master Data Services&#41;](../master-data-services/web-configuration-page-master-data-services-configuration-manager.md)  
  
 También puede usar [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] para especificar otra configuración de las aplicaciones web y servicios asociados a la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]. Por ejemplo, puede especificar la frecuencia con la que se cargan los datos o con la que se envían correos electrónico de validación. Para obtener más información, vea [Configuración del sistema &#40;Master Data Services&#41;](../master-data-services/system-settings-master-data-services.md).  
  
##  <a name="a-namedeploysamplea-deploying-sample-models-and-data"></a><a name="deploySample"></a> Implementar modelos y datos de ejemplo  
 Los siguientes tres paquetes de modelo de ejemplo se incluyen con  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)].   Estos modelos de ejemplo incluyen datos. **La ubicación predeterminada de los paquetes de modelo de ejemplo es %programfiles%\Microsoft SQL Server\130\Master Data Services\Samples\Packages.**
  
-   chartofaccounts_en.pkg  
  
-   customer_en.pkg  
  
-   product_en.pkg  
  
 Implemente estos paquetes mediante la herramienta MDSModelDeploy. La ubicación predeterminada de la herramienta MDSModelDeploy es *unidad*\Archivos de programa\Microsoft SQL Server\130\Master Data Services\Configuration.  
  
 Para obtener información sobre los requisitos previos para ejecutar esta herramienta, consulte [Implementar un paquete de implementación de modelo mediante MDSModelDeploy](../master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md).  
  
 Para información sobre las actualizaciones realizadas a los datos para admitir nuevas características de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)][!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], consulte [Ejemplos: paquetes de implementación de modelos &#40;Master Data Services&#41;](../Topic/Samples:%20Model%20Deployment%20Packages%20\(Master%20Data%20Services\).md).  
  
 **Para implementar los modelos de ejemplo**  
  
1.  Copie los paquetes de modelo de ejemplo en *unidad*\Archivos de programa\Microsoft SQL Server\130\Master Data Services\Configuration.  
  
2.  Abra un símbolo del sistema de administrador y ejecute el siguiente comando para ir a MDSModelDeploy.exe.  
  
    ```  
    cd c:\Program Files\Microsoft SQL Server\130\Master Data Services\Configuration  
    ```  
  
3.  Implemente todos los modelos de ejemplo en [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] ; para ello, ejecute los siguientes comandos.  
  
    > [!IMPORTANT]  
    >  En los ejemplos siguientes, se especifica el valor de servicio de `MDS1` . Use este valor si ha seleccionado  **Sitio web predeterminado** al configurar el sitio web de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .  Consulte la sección [Configurar la base de datos y el sitio web](#SetUpWeb) .  
    >   
    >  Si ha creado un sitio web nuevo o ha seleccionado otro sitio web existente, ejecute primero el comando siguiente para determinar el valor de servicio correcto.  
    >   
    >  `MDSModelDeploy listservices`  
    >   
    >  El primer valor de servicio de la lista de valores devueltos es el que especifica para implementar un modelo.  
  
     **Para implementar el modelo de ejemplo chartofaccounts_en.pkg**  
  
    ```  
    MDSModelDeploy deploynew -package chartofaccounts_en.pkg -model ChartofAccounts -service MDS1  
    ```  
  
     **Para implementar el modelo de ejemplo customer_en.pkg**  
  
    ```  
    MDSModelDeploy deploynew -package customer_en.pkg -model Customer -service MDS1  
    ```  
  
     **Para implementar el modelo de ejemplo product_en.pkg**  
  
    ```  
    MDSModelDeploy deploynew -package product_en.pkg -model Product -service MDS1  
  
    ```  
  
     Al implementar correctamente un modelo, se muestra el mensaje **MDSModelDeploy finalizó correctamente** .  
  
     En la siguiente imagen se muestra el comando para implementar el modelo de ejemplo product_en.pkg.  
  
     ![Command line for deploying the Product sample model](../master-data-services/media/mds-commandprompt-deployingsamplemodel-product.png "Command line for deploying the Product sample model")  
  
4.  Para ver los modelos de ejemplo, haga lo siguiente.  
  
    1.  Vaya al sitio web de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] que ha configurado. Consulte la sección [Configurar la base de datos y el sitio web](#SetUpWeb) .  
  
         La dirección del sitio web es http://*nombre del servidor*/*aplicación web*/.  
  
    2.  Seleccione un modelo del cuadro de lista **Modelo** y haga clic en **Explorador**.  
  
         ![MDS Web site, home page.](../master-data-services/media/mds-mdswebsite-homepage-selectsamplemodel.png "MDS Web site, home page.")  
  
## <a name="next-step"></a>Paso siguiente  
 Cree un nuevo modelo y entidades para los datos. Consulte [Crear un modelo &#40;Master Data Services&#41;](../master-data-services/create-a-model-master-data-services.md) y [Crear una entidad &#40;Master Data Services&#41;](../master-data-services/create-an-entity-master-data-services.md).  
  
 Para obtener información general sobre cómo usar un modelo y entidades para crear una estructura para los datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], consulte [Introducción a Master Data Services &#40;MDS&#41;](../master-data-services/master-data-services-overview-mds.md)  
  
## <a name="did-this-article-help-you-were-listening"></a>¿Le ayudó este artículo? Le escuchamos  
 ¿Qué información está buscando? ¿La encontró? Escuchamos sus comentarios para mejorar el contenido. Envíe sus comentarios a [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Get%20Started%20with%20Master%20Data%20Services)  
  
## <a name="see-also"></a>Vea también  
 [Base de datos de Master Data Services](../master-data-services/master-data-services-database.md)   
 [Aplicación web Master Data Services](../master-data-services/master-data-manager-web-application.md)   
 [Página Configuración de base de datos &#40;Administrador de configuración de Master Data Services&#41;](../master-data-services/database-configuration-page-master-data-services-configuration-manager.md)   
 [Novedades en Master Data Services &#40;MDS&#41;](../master-data-services/what-s-new-in-master-data-services-mds.md)  
  
  