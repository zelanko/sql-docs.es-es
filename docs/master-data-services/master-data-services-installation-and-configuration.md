---
title: "Configuración e instalación de Master Data Services | Documentos de Microsoft"
ms.custom:
- SQL2016_New_Updated
ms.date: 07/28/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
ms.assetid: f6cd850f-b01b-491f-972c-f966b9fe4190
caps.latest.revision: 44
author: sabotta
ms.author: carlasab
manager: craigg
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 25e5dc869efd2417c47b72c70ede7ba19ab54b46
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="master-data-services-installation-and-configuration"></a>Instalación y configuración de Master Data Services
  En este artículo se describe cómo instalar [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] en una máquina con Windows Server 2012 R2, configurar la base de datos y el sitio web de MDS e implementar los modelos y datos de ejemplo. [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] (MDS) le permite a su organización administrar una versión de datos de confianza.   
  
> [!NOTE] 
> Puede instalar [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] en Windows 10 máquina cuando se usa la edición Developer que ahora es compatible con [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]. 
>>Para obtener más información sobre el sistema operativo admite para diferentes [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)] ediciones, vea [requisitos de Hardware y Software para instalar SQL Server 2016](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md). 

Para obtener información general sobre cómo organizar los datos en [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)], consulte [Introducción a Master Data Services (MDS)](../master-data-services/master-data-services-overview-mds.md).     
  
 Para obtener información sobre las nuevas características de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)], consulte [Novedades en Master Data Services &#40;MDS&#41;](../master-data-services/what-s-new-in-master-data-services-mds.md).  
 
Para obtener vínculos a los vídeos y a otros recursos de aprendizaje de [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)], consulte [Información sobre SQL Server Master Data Services](../master-data-services/learn-sql-server-master-data-services.md). 
  
> **Descargar**  
>-   Para descargar [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)], vaya al  **[Centro de evaluación](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2017-ctp/)**.  
>-   ¿Tiene una cuenta de Azure?  A continuación, vaya  **[aquí](https://azure.microsoft.com/en-us/services/virtual-machines/sql-server/?wt.mc_id=sqL16_vm)**  para poner en marcha una máquina Virtual con SQL Server ya instalado.  
 
> **¿No puede crear un sitio web de MDS?**
>>Consulte este artículo de soporte técnico de Microsoft para obtener instrucciones sobre cómo resolver este problema.
[No se puede crear un sitio web de MDS mediante una cuenta con pocos privilegios en SQL Server 2016](https://aka.ms/mdssupport) 

## <a name="internet-explorer-and-silverlight"></a>Silverlight e Internet Explorer
- Cuando se instala [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] en un equipo Windows Server 2012, tendrá que configurar la seguridad mejorada en el Explorador de Internet para permitir el scripting para el sitio Web de la aplicación. De lo contrario, se producirá exploración al sitio en el equipo del servidor.
- Para trabajar en la aplicación Web, Silverlight 5 debe instalarse en el equipo cliente. Si no tiene la versión necesaria de Silverlight, se le pedirá que la instale cuando navegue a un área de la aplicación Web que lo requiera. Puede instalar Silverlight 5 desde  **[aquí](https://www.microsoft.com/silverlight/)**.

## <a name="includessmdsshortmdincludesssmdsshort-mdmd-on-an-azure-virtual-machine"></a>[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]en una máquina Virtual de Azure
De forma predeterminada, cuando el número de una máquina Virtual de Azure con [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)] ya instalado, [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] también está instalado. 

Es el siguiente paso consiste en instalar Internet Information Services (IIS). Consulte la [instalar y configurar IIS](#InstallIIS) sección. 

Si está interesado en realizar cambios en la instalación de [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)], encontrará el archivo setup.exe en la ubicación predeterminada, `<drive>`: \SQLServer_13.0_Full.
  
## <a name="InstallMDS"></a>Instalar Master Data Services  
 Use el asistente para la instalación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o un símbolo del sistema para instalar [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)].  
  
 **Para instalar [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] con Instalación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en una máquina con Windows Server 2012 R2**  
  
1.  Haga doble clic en Setup.exe y siga los pasos del asistente para la instalación.  
  
2.  Seleccione [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] en la página **Selección de características** en **Características compartidas**.  
  
     Esto instala [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)], ensamblados, un complemento de Windows PowerShell y carpetas y archivos para las aplicaciones y los servicios web.  
  
     ![mds_SQLServer2016Setup_FeatureSelection](../master-data-services/media/mds-sqlserver2016setup-featureselection.png "mds_SQLServer2016Setup_FeatureSelection")  
  
3.  Complete el asistente para la instalación.  

## <a name="InstallIIS"></a>Instalación y configuración de IIS
  
1.  En [!INCLUDE[winblue_server_2](../includes/winblue-server-2-md.md)], haga clic en el icono **Administrador del servidor** de la barra de tareas en el **Escritorio**.  
  
     ![Icono para el administrador del servidor en la barra de tareas de Windows Server 2012](../master-data-services/media/mds-windowsservertaskbar-servermanagericon.png "icono para el administrador del servidor en la barra de tareas de Windows Server 2012")  
  
5.  En **Administrador del servidor**, haga clic en **Agregar roles y características** en el menú **Administrar** .  
   
     ![En administración del servidor, el agregar Roles y características de comando de menú](../master-data-services/media/mds-servermanagerdashboard-addrolesfeaturesmenu.png "en Administrar servidor, agregar Roles y características de comando de menú")  
  
6.  En la página **Tipo de instalación** del **Asistente para agregar roles y características**, acepte el valor predeterminado (**Instalación basada en características o en roles**) y haga clic en **Siguiente**.  
  
7.  Haga clic en **Seleccionar un servidor del grupo de servidores**y, después, haga clic en el servidor en el que ha instalado [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)].  
  
     ![mds_AddRolesFeaturesWizard_ServerSelectionPage](../master-data-services/media/mds-addrolesfeatureswizard-serverselectionpage.png) 
  
8. En el **Roles de servidor** página, haga clic en **servidor Web** y, a continuación, haga clic en **siguiente**. 

   ![mds_AddRolesFeaturesWizard_ServerRolesPage](../master-data-services/media/mds-addrolesfeatureswizard-serverrolespage.png)
   
9. En el **características** página, confirme que las siguientes características están seleccionadas y, a continuación, haga clic en **siguiente**. Estas características son necesarias para [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] en [!INCLUDE[winblue_server_2_md](../includes/winblue-server-2-md.md)].
  
    |Características|Características|  
    |--------------|--------------|  
    |![mds_AddRolesFeaturesWizard_FeaturesPage](../master-data-services/media/mds-addrolesfeatureswizard-featurespage.png)|![mds_AddRolesFeaturesWizard_FeaturesPage_WindowsProcActive](../master-data-services/media/mds-addrolesfeatureswizard-featurespage-windowsprocactive.png)|  

10. En el panel izquierdo, haga clic en **rol de servidor Web (IIS)** y, a continuación, haga clic en **servicios de rol**.
11. En el **servicios de rol** página, confirme que los siguientes servicios están seleccionados y, a continuación, haga clic en **siguiente**. Estos servicios son necesarios para [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] en [!INCLUDE[winblue_server_2](../includes/winblue-server-2-md.md)].

    > [!WARNING]  
    >  No instale el servicio de rol Publicación en WebDAV. Publicación en WebDAV no es compatible con [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)].  
  
     |Servicios de rol|Servicios de rol|  
    |-----------------------------|-----------------------------|  
    |![mds_AddRolesFeaturesWizard_RoleServicesPage](../master-data-services/media/mds-addrolesfeatureswizard-roleservicespage.png)|![mds_AddRolesFeaturesWizard_RoleServicesPage_PerformSecurity](../master-data-services/media/mds-addrolesfeatureswizard-roleservicespage-performsecurity.png)|  
    |![mds_AddRolesFeaturesWizard_RoleServicesPage_AppDevsection](../master-data-services/media/mds-addrolesfeatureswizard-roleservicespage-appdevsection.png)|![mds_AddRolesFeaturesWizard_RoleServicesPage_ManageToolssection](../master-data-services/media/mds-addrolesfeatureswizard-roleservicespage-managetoolssection.png)|  
    |||  
  
     Para obtener una lista de las características y los servicios de rol en otros sistemas operativos, consulte [requisitos de la aplicación Web &#40; Master Data Services &#41; ](../master-data-services/install-windows/web-application-requirements-master-data-services.md) .   
  
 Para obtener más información sobre la instalación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] con el programa de instalación, consulte [Instalación de SQL Server 2016 desde el Asistente para la instalación &#40;programa de instalación&#41;](../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md).  
  
 Para obtener más información sobre la instalación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mediante un símbolo del sistema, consulte [Instalar SQL Server 2016 desde el símbolo del sistema](../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md). Si se usa un símbolo del sistema, [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] está disponible como parámetro de característica.  
  
 Para obtener una descripción breve con vínculos a información adicional sobre las tareas previas a la instalación, consulte [Instalar Master Data Services](../master-data-services/install-windows/install-master-data-services.md).  
  
##  <a name="SetUpWeb"></a> Configurar la base de datos y el sitio web  
 **Configurar la base de datos y el sitio web mediante el**  de [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]  

 
> [!WARNING]  
    >  Debe [instalar IIS](#InstallIIS) antes de iniciar la [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] Configuration Manager. De lo contrario, el Administrador de configuración mostrará un error de servicios de información de información y no podrá crear el [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] aplicación web.  
    
> **Requisitos del explorador**
>>El [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] aplicación web funciona únicamente en Internet Explorer (IE) 9 o posterior. No se admiten IE 8 ni versiones anteriores, así como Microsoft Edge ni Chrome.    
  
1.  Inicie el [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]y haga clic en **Configuración de base de datos** en el panel izquierdo.  
  
2.  Haga clic en **Crear base de datos**y, después, haga clic en **Siguiente** en el **Asistente para crear bases de datos**.  
  
3.  En la página **Servidor de base de datos** , seleccione el **Tipo de autenticación** y, después, haga clic en **Probar conexión** para confirmar que puede conectarse a la base de datos con las credenciales del tipo de autenticación seleccionado. Haga clic en **Siguiente**.
  
    > [!NOTE]  
    >  Al seleccionar **Usuario actual: Seguridad integrada** como el tipo de autenticación, el cuadro **Nombre de usuario** es de solo lectura y muestra el nombre de la cuenta de usuario de Windows con la que se ha iniciado sesión en el equipo. Si está ejecutando [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)] [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] en una máquina Virtual de Azure (VM), el **nombre de usuario** cuadro muestra el nombre de la máquina virtual y el nombre de usuario para la cuenta de administrador local en la máquina virtual. 

    ![mds_2016ConfigManager_CreateDatabaseWizard_ServerPage](../master-data-services/media/mds-2016configmanager-createdatabasewizard-serverpage.png)  
  
4.  Escriba un nombre en el campo **Nombre de la base de datos** . Si lo desea, para seleccionar una intercalación de Windows, desactive la **intercalación predeterminada de SQL Server** casilla de verificación y haga clic en una o varias de las opciones disponibles como **entre mayúsculas y minúsculas**. Haga clic en **Siguiente**.

    ![mds_2016ConfigManager_CreateDatabaseWizard_DatabasePage](../master-data-services/media/mds-2016configmanager-createdatabasewizard-databasepage.png)  
  
     Para obtener más información sobre la intercalación de Windows, consulte [Nombre de intercalación de Windows (Transact-SQL)](https://msdn.microsoft.com/library/ms188046.aspx).  
  
5.  En el campo **Nombre de usuario** , especifique la cuenta de Windows del usuario que será el superusuario predeterminado de Master Data Services. Un superusuario tiene acceso a todas las áreas funcionales y puede agregar, eliminar y actualizar todos los modelos.  

    ![mds_2016ConfigManager_CreateDatabaseWizard_AdminPage](../master-data-services/media/mds-2016configmanager-createdatabasewizard-adminpage.png)  
  
6.  Haga clic en **Siguiente** para ver un resumen de la configuración de la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] y, luego, haga clic en **Siguiente** para crear la base de datos. El **del progreso y finalizar** aparecerá la página.

7. Cuando se crea y configura la base de datos, haga clic en **finalizar**.  
  
     Para obtener información sobre la configuración del **Asistente para crear bases de datos**, consulte [Asistente para crear bases de datos &#40;Administrador de configuración de Master Data Services&#41;](../master-data-services/create-database-wizard-master-data-services-configuration-manager.md).  
  
7.  En el **configuración de base de datos** página en el [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)], haga clic en **Seleccionar base de datos**.  
  
8.  Haga clic en **conectar**, seleccione la [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] base de datos que creó en el paso 7 y, a continuación, haga clic en **Aceptar**. 

    ![mds_2016ConfigManager_SelectDatabaseButton_ConnectToDatabaseDialog](../master-data-services/media/mds-2016configmanager-selectdatabasebutton-connecttodatabasedialog.png)  
  
     Ha terminado de configurar la base de datos. En la página **Configuración de base de datos** se muestra ahora la instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a la que está conectado para [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], la base de datos que ha creado y la versión actual de la base de datos.  

    ![mds_2016ConfigManager_DatabaseConfig_Completed](../master-data-services/media/mds-2016configmanager-databaseconfig-completed.png)   
  
9. En [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)], haga clic en **Configuración web** en el panel izquierdo.  
  
10. En el cuadro de lista **Sitio web** , haga clic en **Sitio web predeterminado**y, luego, haga clic en **Crear** para crear una aplicación web.  
  
    > [!NOTE]  
    >  Al seleccionar **Sitio web predeterminado**, debe crear una aplicación web. Si selecciona **Crear nuevo sitio web** en el cuadro de lista, la aplicación se crea de forma automática.  

     ![mds_2016ConfigManager_WebConfig](../master-data-services/media/mds-2016configmanager-webconfig.png)  
  
11. En la sección **Grupo de aplicaciones** , realice una de las siguientes acciones.  
  
    -   Escriba el mismo nombre de usuario que ha escrito en el paso 5 para la **Cuenta de administrador**de la base de datos, escriba la contraseña y, después, haga clic en **Aceptar**.  
  
         **O bien**  
  
    -   Seleccione otro nombre de usuario, escriba la contraseña y, luego, haga clic en Aceptar.  
  
         No tiene que usar la misma cuenta al crear la base de datos y la aplicación web.  

        ![mds_2016ConfigManager_WebConfig_CreateWebApplication](../master-data-services/media/mds-2016configmanager-webconfig-createwebapplication.png)   
  
     Para obtener más información sobre el cuadro de diálogo **Crear aplicación web**, consulte [Cuadro de diálogo Crear aplicación web &#40;Administrador de configuración de Master Data Services&#41;](../master-data-services/create-web-application-dialog-box-master-data-services-configuration-manager.md).  
  
12. En la página **Configuración web** en el cuadro **Aplicación web**, haga clic en la aplicación que ha creado y, luego, haga clic en **Seleccionar** en la sección **Asociar aplicación a base de datos**.  
  
13. Haga clic en **Conectar**, seleccione la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] que quiera asociar a la aplicación web y, después, haga clic en **Aceptar**.  
  
     Ha terminado de configurar el sitio web. En la página **Configuración web** se muestra ahora el sitio web que ha seleccionado, la aplicación web que ha creado y la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] asociada a la aplicación.  

     ![mds_2016ConfigManager_WebConfig_Completed](../master-data-services/media/mds-2016configmanager-webconfig-completed.png)  
 
     
15. Haga clic en **Aplicar**. El **configuración finalizada** muestra de cuadro de mensaje. Haga clic en **Aceptar** en el cuadro de mensaje para iniciar la aplicación web. La dirección del sitio web es http://*nombre del servidor*/*aplicación web*/. 


![mds_2016ConfigurationComplete_MessageBox](../master-data-services/media/mds-2016configurationcomplete-messagebox.png) 
  
     For more information about the settings on the Web Configuration page, see [Web Configuration Page &#40;Master Data Services Configuration Manager&#41;](../master-data-services/web-configuration-page-master-data-services-configuration-manager.md)  
  
 También puede usar [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] para especificar otra configuración de las aplicaciones web y servicios asociados a la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Por ejemplo, puede especificar la frecuencia con la que se cargan los datos o con la que se envían correos electrónico de validación. Para obtener más información, vea [Configuración del sistema &#40;Master Data Services&#41;](../master-data-services/system-settings-master-data-services.md).  
  
##  <a name="deploySample"></a> Implementar modelos y datos de ejemplo  
 Los siguientes tres paquetes de modelo de ejemplo se incluyen con  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)].   Estos modelos de ejemplo incluyen datos. **La ubicación predeterminada de los paquetes de modelo de ejemplo es %programfiles%\Microsoft SQL Server\140\Master Data Services\Samples\Packages.**
  
-   chartofaccounts_en.pkg  
  
-   customer_en.pkg  
  
-   product_en.pkg  
  
 Implemente estos paquetes mediante la herramienta MDSModelDeploy. Es la ubicación predeterminada de la herramienta MDSModelDeploy *unidad*\Program SQL Server\ 140\Master Data Services\Configuration.  
  
 Para obtener información sobre los requisitos previos para ejecutar esta herramienta, consulte [Implementar un paquete de implementación de modelo mediante MDSModelDeploy](../master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md).  
  
 Para obtener información acerca de las actualizaciones realizadas en los datos para admitir nuevas características en [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], consulte [ejemplos de SQL Server: paquetes de implementación de modelo (MDS)](../master-data-services/sql-server-samples-model-deployment-packages-mds.md).  
  
 **Para implementar los modelos de ejemplo**  
  
1.  Copie los paquetes de modelo de ejemplo para *unidad*\Program SQL Server\140\Master Data Services\Configuration.  
  
2.  Abra un símbolo del sistema de administrador y ejecute el siguiente comando para ir a MDSModelDeploy.exe.  
  
    ```  
    cd c:\Program Files\Microsoft SQL Server\140\Master Data Services\Configuration  
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
    >
    > [!NOTE]
    > Para obtener más información acerca de la información de metadatos de los modelos de ejemplo, consulte el archivo Léame disponible en esta ubicación "c:\Program Files\Microsoft SQL Server\140\Master Data Services\Configuration"
    >
   
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
  
     ![Línea de comandos para implementar el modelo de producto de ejemplo](../master-data-services/media/mds-commandprompt-deployingsamplemodel-product.png "línea de comandos para implementar el modelo de producto de ejemplo")  
  
4.  Para ver los modelos de ejemplo, haga lo siguiente.  
  
    1.  Vaya al sitio web de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] que ha configurado. Consulte la sección [Configurar la base de datos y el sitio web](#SetUpWeb) .  
  
         La dirección del sitio web es http://*nombre del servidor*/*aplicación web*/.  
  
    2.  Seleccione un modelo del cuadro de lista **Modelo** y haga clic en **Explorador**.  
  
         ![Sitio Web de MDS, página principal. ] (../master-data-services/media/mds-mdswebsite-homepage-selectsamplemodel.png "Sitio Web de MDS, página principal.")  
  
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
  
  

