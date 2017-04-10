---
title: "Cat&#225;logo de SSIS | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 24bd987e-164a-48fd-b4f2-cbe16a3cd95e
caps.latest.revision: 28
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 26
---
# Cat&#225;logo de SSIS
  El catálogo de **SSISDB** es el eje central cuando se trabaja con proyectos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] (SSIS) que ha implementado en el servidor [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Por ejemplo, establece los parámetros del proyecto y del paquete, configura entornos para especificar los valores en tiempo de ejecución para los paquetes, ejecuta paquetes y soluciona los problemas de los mismos, y administra las operaciones del servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Entre los objetos que se almacenan en el catálogo **SSISDB** se incluyen proyectos, paquetes, parámetros, entornos y el historial de operaciones.  
  
 Inspecciona objetos, valores y los datos operativos que se almacenan en el catálogo de **SSISDB** , consultando las vistas de la base de datos de **SSISDB** . Administra los objetos al llamar a los procedimientos almacenados en la base de datos de **SSISDB** o mediante la interfaz de usuario del catálogo de **SSISDB** . En muchos casos, la misma tarea se puede realizar en la interfaz de usuario o al llamar a un procedimiento almacenado.  
  
 Para mantener la base de datos de **SSISDB** , se recomienda aplicar las directivas corporativas estándar para administrar las bases de datos de usuario. Para obtener información acerca de cómo crear planes de mantenimiento, vea [Maintenance Plans](../../relational-databases/maintenance-plans/maintenance-plans.md).  
  
 El catálogo de **SSISDB** y la base de datos de **SSISDB** admiten Windows PowerShell. Para obtener más información acerca de cómo usar SQL Server con Windows PowerShell, vea [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md). Para obtener ejemplos de cómo usar Windows PowerShell para completar tareas como implementar un proyecto, vea la entrada del blog [SSIS y PowerShell en SQL Server 2012](http://go.microsoft.com/fwlink/?LinkId=242539), en blogs.msdn.com.  
  
 Para más información sobre cómo ver los datos de las operaciones, consulte [Monitor de ejecución de paquetes y otras operaciones](../../integration-services/performance/monitor-running-packages-and-other-operations.md).  
  
 Tiene acceso al catálogo de **SSISDB** en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] al conecta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el motor de base de datos y después expandir el nodo **Catálogos de Integration Services** en el Explorador de objetos. Tiene acceso a la base de datos de **SSISDB** en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] al expandir el nodo Bases de datos en el Explorador de objetos.  
  
> [!NOTE] No puede cambiar el nombre de la base de datos de **SSISDB** .  
  
> [!NOTE] Si la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a la que la base de datos **SSISDB** se adjuntada se detiene o no responde, el proceso de ISServerExec.exe finaliza. Se escribe un mensaje en un registro de eventos de Windows.  
>   
>  Si los recursos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conmutan por error como parte de una conmutación por error de clúster, los paquetes en ejecución no se reinician. Puede usar los puntos de comprobación para reiniciar los paquetes. Para obtener más información, vea [Restart Packages by Using Checkpoints](../../integration-services/packages/restart-packages-by-using-checkpoints.md).  
  
## <a name="in-this-topic"></a>En este tema  
  
-   [Identificadores de objeto de catálogo](../../integration-services/service/ssis-catalog.md#CatalogObjectIdentifiers)  
  
-   [Configuración de catálogo](../../integration-services/service/ssis-catalog.md#Configuration)  
  
-   [Permisos](../../integration-services/service/ssis-catalog.md#Permissions)  
  
-   [Carpetas](../../integration-services/service/ssis-catalog.md#Folders)  
  
-   [Proyectos y paquetes](../../integration-services/service/ssis-catalog.md#ProjectsAndPackages)  
  
-   [Parámetros](../../integration-services/service/ssis-catalog.md#Parameters)  
  
-   [Entornos de servidor, variables de servidor y referencias del entorno de servidor](../../integration-services/service/ssis-catalog.md#ServerEnvironments)  
  
-   [Ejecuciones y validaciones](../../integration-services/service/ssis-catalog.md#Executions)  
  
-   [Compatibilidad con AlwaysOn](../../integration-services/service/ssis-catalog.md#AlwaysOn)  
  
-   [Tareas relacionadas](../../integration-services/service/ssis-catalog.md#RelatedTasks)  
  
-   [Contenido relacionado](../../integration-services/service/ssis-catalog.md#RelatedContent)  
  
##  <a name="a-namecatalogobjectidentifiersa-catalog-object-identifiers"></a><a name="CatalogObjectIdentifiers"></a> Identificadores de objeto de catálogo  
 Cuando cree un nuevo objeto en el catálogo, asígnele un nombre El nombre del objeto es un identificador. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] define las reglas para las que los caracteres se pueden usar en un identificador. Los nombres de los siguientes objetos deben seguir las reglas de identificador.  
  
-   Carpeta  
  
-   Proyecto  
  
-   Entorno  
  
-   Parámetro  
  
-   Variable de entorno  
  
###  <a name="a-namefoldera-folder-project-environment"></a><a name="Folder"></a> Carpeta, proyecto, entorno  
 Tenga en cuenta las reglas siguientes al cambiar el nombre de una carpeta, un proyecto, o un entorno.  
  
-   Los caracteres no válidos incluyen caracteres ASCII/Unicode del 1 al 31, comillas dobles ("), menor que (\<), mayor que (>), barra vertical (|), retroceso (\b), NULL (\0) y tabulación (\t).  
  
-   El nombre no puede contener espacios delante ni detrás.  
  
-   @ no se permite como primer carácter, pero los caracteres siguientes pueden usar @.  
  
-   La longitud del nombre debe ser mayor que 0 y menor o igual que 128.  
  
###  <a name="a-nameparametera-parameter"></a><a name="Parameter"></a> Parámetro  
 Tenga en cuenta las reglas siguientes cuando asigne un nombre a un parámetro.  
  
-   El primer carácter del nombre debe ser una letra, tal como se define en el Estándar Unicode 2.0, o un carácter de subrayado (_).  
  
-   Los caracteres siguientes pueden ser letras o números, tal como se define en el Estándar Unicode 2.0, o un carácter de subrayado (_).  
  
###  <a name="a-nameenvironmentvariablea-environment-variable"></a><a name="EnvironmentVariable"></a> Variable de entorno  
 Tenga en cuenta las reglas siguientes cuando asigne un nombre a una variable de entorno.  
  
-   Los caracteres no válidos incluyen caracteres ASCII/Unicode del 1 al 31, comillas dobles ("), menor que (\<), mayor que (>), barra vertical (|), retroceso (\b), NULL (\0) y tabulación (\t).  
  
-   El nombre no puede contener espacios delante ni detrás.  
  
-   @ no se permite como primer carácter, pero los caracteres siguientes pueden usar @.  
  
-   La longitud del nombre debe ser mayor que 0 y menor o igual que 128.  
  
-   El primer carácter del nombre debe ser una letra, tal como se define en el Estándar Unicode 2.0, o un carácter de subrayado (_).  
  
-   Los caracteres siguientes pueden ser letras o números, tal como se define en el Estándar Unicode 2.0, o un carácter de subrayado (_).  
  
##  <a name="a-nameconfigurationa-catalog-configuration"></a><a name="Configuration"></a> Configuración de catálogo  
 Ajusta con precisión cómo se comporta el catálogo ajustando las propiedades del catálogo. Las propiedades del catálogo definen cómo se cifra la información confidencial y cómo se conservan las operaciones y los datos de versiones del proyecto. Para establecer las propiedades del catálogo, use el cuadro de diálogo **Propiedades del catálogo** o llame al procedimiento almacenado [catalog.configure_catalog &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-configure-catalog-ssisdb-database.md). Para ver las propiedades, use el cuadro de diálogo o la consulta [catalog.catalog_properties &#40;base de datos de SSISDB&#41;](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md). Puede acceder al cuadro de diálogo si hace clic con el botón derecho en **SSISDB** en el Explorador de objetos.  
  
###  <a name="a-namecleanupa-operations-and-project-version-cleanup"></a><a name="Cleanup"></a> Limpieza de las operaciones y los datos de versiones del proyecto  
 Los datos de estado para muchas de las operaciones del catálogo se almacena en tablas de base de datos internas. Por ejemplo, el catálogo realiza el seguimiento del estado de las ejecuciones de paquetes y las implementaciones de proyecto. Para mantener el tamaño de los datos de operaciones, se usa **Tareas de mantenimiento de SSIS Server** de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para quitar los datos antiguos. Este trabajo del agente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se crea al instalar [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Puede actualizar o volver a implementar un proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] implementándolo con el mismo nombre en la misma carpeta en el catálogo. De forma predeterminada, cada vez que vuelve a implementar un proyecto, el catálogo de **SSISDB** conserva la versión anterior del proyecto. Para mantener el tamaño de los datos de las operaciones, se utiliza el **trabajo de mantenimiento del Agente SQL Server** para quitar las versiones anteriores de proyectos.  
 
Para ejecutar el **trabajo de mantenimiento del servidor SSIS**, SSIS crea el inicio de sesión de SQL Server **##MS_SSISServerCleanupJobLogin##**. Este inicio de sesión es solo para uso interno de SSIS.
  
 Las siguientes propiedades del catálogo de **SSISDB** definen cómo se comporta este trabajo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Puede ver y modificar las propiedades mediante el cuadro de diálogo **Propiedades del catálogo** o mediante [catalog.catalog_properties &#40;base de datos de SSISDB&#41;](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md) y [catalog.configure_catalog &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-configure-catalog-ssisdb-database.md).  
  
 **Borrar registros periódicamente**  
 El paso de trabajo de limpieza de operaciones se ejecuta cuando esta propiedad se establece en **True**.  
  
 **Período de retención (días)**  
 Define la antigüedad máxima de los datos permitidos para las operaciones (en días). Se quitan los datos más antiguos.  
  
 El valor mínimo es un día. El valor máximo solo está limitado por el valor máximo de los datos **int** de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para más información sobre este tipo de datos, vea [int, bigint, smallint y tinyint &#40;Transact-SQL&#41;](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md).  
  
 **Quitar periódicamente versiones anteriores**  
 El paso de trabajo de limpieza de versiones del proyecto se ejecuta cuando esta propiedad se establece en **True**.  
  
 **Número máximo de versiones por proyecto**  
 Define cuántas versiones de un proyecto se almacenan en el catálogo. Se quitan las versiones anteriores de proyectos.  
  
###  <a name="a-nameencryptiona-encryption-algorithm"></a><a name="Encryption"></a> Algoritmo de cifrado  
 La propiedad **Algoritmo de cifrado** especifica el tipo de cifrado que se utiliza para cifrar los valores de los parámetros confidenciales. Puede elegir entre los siguientes tipos de cifrado.  
  
-   AES_256 (predeterminado)  
  
-   AES_192  
  
-   AES_128  
  
-   DESX  
  
-   TRIPLE_DES_3KEY  
  
-   TRIPLE_DES  
  
-   DES  
  
 Al implementar un proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en el servidor [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], el catálogo cifra automáticamente los datos del paquete y los valores confidenciales. El catálogo también descifra automáticamente los datos cuando lo recupera. El catálogo de SSISDB emplea el nivel de protección **ServerStorage** . Para más información, consulte [Access Control for Sensitive Data in Packages](../../integration-services/packages/access-control-for-sensitive-data-in-packages.md).  
  
 Cambiar el algoritmo de cifrado es una operación que lleva mucho tiempo. En primer lugar, el servidor tiene que utilizar el algoritmo especificado previamente para descifrar todos los valores de configuración. A continuación, el servidor tiene que utilizar el nuevo algoritmo para volver a cifrar los valores. Durante este tiempo, no puede haber otras operaciones de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en el servidor. Así, para que las operaciones de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] continúen sin interrupción, el algoritmo de cifrado es un valor de solo lectura en el cuadro de diálogo de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
 Para cambiar la configuración de la propiedad **Algoritmo de cifrado** , establezca la base de datos de **SSISDB** en modo de usuario único y, luego, llame al procedimiento almacenado catalog.configure_catalog. Use ENCRYPTION_ALGORITHM para el argumento *property_name*. Para más información sobre los valores de propiedad admitidos, vea [catalog.catalog_properties &#40;base de datos de SSISDB&#41;](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md). Para más información sobre el procedimiento almacenado, vea [catalog.configure_catalog &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-configure-catalog-ssisdb-database.md).  
  
 Para más información sobre el modo de usuario único, vea [Establecer una base de datos en modo de usuario único](../../relational-databases/databases/set-a-database-to-single-user-mode.md). Para más información sobre el cifrado y los algoritmos de cifrado en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea los temas de la sección [Cifrado de SQL Server](../../relational-databases/security/encryption/sql-server-encryption.md).  
  
 Para el cifrado se utiliza una clave maestra de base de datos. La clave se crea al crear el catálogo. Para más información, vea [Crear el catálogo de SSIS](../../integration-services/service/create-the-ssis-catalog.md).  
  
 En la tabla siguiente se muestran los nombres de propiedad que aparecen en el cuadro de diálogo **Propiedades del catálogo** y las propiedades correspondientes de la vista de base de datos.  
  
|Nombre de la propiedad (cuadro de diálogo**Propiedades del catálogo** )|Nombre de la propiedad (vista de base de datos)|  
|---------------------------------------------------------|-------------------------------------|  
|Nombre del algoritmo de cifrado|ENCRYPTION_ALGORITHM|  
|Borrar registros periódicamente|OPERATION_CLEANUP_ENABLED|  
|Período de retención (días)|RETENTION_WINDOW|  
|Quitar periódicamente versiones anteriores|VERSION_CLEANUP_ENABLED|  
|Número máximo de versiones por proyecto|MAX_PROJECT_VERSIONS|  
|Nivel de registro predeterminado de todo el servidor|SERVER_LOGGING_LEVEL|  
  
##  <a name="a-namepermissionsa-permissions"></a><a name="Permissions"></a> Permisos  
 Los proyectos, los entornos y los paquetes se encuentran en carpetas que son objetos protegibles. Puede conceder permisos a una carpeta, incluido el permiso de MANAGE_OBJECT_PERMISSIONS. MANAGE_OBJECT_PERMISSIONS le permite delegar la administración del contenido de la carpeta a un usuario sin tener que conceder la pertenencia del usuario al rol ssis_admin. También puede conceder permisos a los proyectos, entornos y operaciones. Las operaciones incluyen inicializar [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], implementar proyectos, crear e iniciar ejecuciones, validar proyectos y paquetes, y configurar el catálogo de **SSISDB** .  
  
 Para obtener más información sobre los roles de base de datos, vea [Roles de nivel de base de datos](../../relational-databases/security/authentication-access/database-level-roles.md).  
  
 El catálogo de SSISDB usa un desencadenador DDL, ddl_cleanup_object_permissions, para exigir la integridad de la información sobre permisos para elementos de SSIS protegibles. El desencadenador se activa cuando se quita de la base de datos de SSISDB una entidad de seguridad de base de datos, como un usuario de base de datos, un rol de base de datos o un rol de aplicación de base de datos.  
  
 Si la entidad de seguridad ha concedido o denegado los permisos a otras entidades de seguridad, revoque los permisos proporcionados por el otorgante, antes de que la entidad de seguridad se pueda quitar. De lo contrario, se devuelve un mensaje de error cuando el sistema intenta quitar la entidad de seguridad. El desencadenador quita todos los registros de permisos donde la entidad de seguridad de base de datos es un receptor.  
  
 Se recomienda que el desencadenador no se deshabilite porque garantiza que no hay ningún registro de permiso huérfano después de que una entidad de seguridad de base de datos se quita de la base de datos de **SSISDB** .  
  
### <a name="managing-permissions"></a>Administrar permisos  
 Puede administrar permisos mediante la interfaz de usuario de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , los procedimientos almacenados y el espacio de nombres <xref:Microsoft.SqlServer.Management.IntegrationServices> .  
  
 Para administrar permisos con la interfaz de usuario de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , use los cuadros de diálogo siguientes.  
  
-   Para una carpeta, use la página **Permisos** del [Folder Properties Dialog Box](../../integration-services/service/folder-properties-dialog-box.md).  
  
-   Para un proyecto, use la página **Permisos** del [Project Properties Dialog Box](../../integration-services/service/project-properties-dialog-box.md).  
  
-   Para un entorno, utilice la página **Permisos** de [NIB: Environment Properties Dialog Box](http://msdn.microsoft.com/es-es/6a91a8d4-0006-4cfd-9759-3e4295ae452b)(NIB: cuadro de diálogo de propiedades del entorno).  
  
 Para administrar permisos mediante Transact-SQL, llame a [catalog.grant_permission &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-grant-permission-ssisdb-database.md), [catalog.deny_permission &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-deny-permission-ssisdb-database.md) y [catalog.revoke_permission &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-revoke-permission-ssisdb-database.md). Para ver los permisos efectivos de la entidad de seguridad actual para todos los objetos, consulte [catalog.effective_object_permissions &#40;base de datos de SSISDB&#41;](../../integration-services/system-views/catalog-effective-object-permissions-ssisdb-database.md). Este tema proporciona descripciones de los diferentes tipos de permisos. Para ver los permisos asignados explícitamente al usuario, consulte [catalog.explicit_object_permissions &#40;base de datos de SSISDB&#41;](../../integration-services/system-views/catalog-explicit-object-permissions-ssisdb-database.md).  
  
##  <a name="a-namefoldersa-folders"></a><a name="Folders"></a> Carpetas  
 Una carpeta contiene uno o más proyectos y entornos en el catálogo de **SSISDB** . Puede usar la vista [catalog.folders &#40;base de datos de SSISDB&#41;](../../integration-services/system-views/catalog-folders-ssisdb-database.md) para acceder a información sobre las carpetas del catálogo. Puede utilizar los siguientes procedimientos almacenados para administrar carpetas.  
  
-   [catalog.create_folder &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-create-folder-ssisdb-database.md)  
  
-   [catalog.delete_folder &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-delete-folder-ssisdb-database.md)  
  
-   [catalog.rename_folder &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-rename-folder-ssisdb-database.md)  
  
-   [catalog.set_folder_description &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-set-folder-description-ssisdb-database.md)  
  
##  <a name="a-nameprojectsandpackagesa-projects-and-packages"></a><a name="ProjectsAndPackages"></a> Proyectos y paquetes  
 Cada proyecto puede contener varios paquetes. Proyectos y paquetes pueden contener parámetros y referencias a los entornos. Puede tener acceso a los parámetros y referencias del entorno mediante el uso de [Configure Dialog Box](../../integration-services/service/configure-dialog-box.md).  
  
 Puede realizar otras tareas de proyectos llamando a los siguientes procedimientos almacenados.  
  
-   [catalog.delete_project &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-delete-project-ssisdb-database.md)  
  
-   [catalog.deploy_project &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-deploy-project-ssisdb-database.md)  
  
-   [catalog.get_project &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-get-project-ssisdb-database.md)  
  
-   [catalog.move_project &#40;&#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-move-project-ssisdb-database.md)  
  
-   [catalog.restore_project &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-restore-project-ssisdb-database.md)  
  
 Estas vistas proporcionan detalles sobre los paquetes, proyectos y versiones del proyecto.  
  
-   [catalog.projects &#40;base de datos de SSISDB&#41;](../../integration-services/system-views/catalog-projects-ssisdb-database.md)  
  
-   [catalog.packages &#40;base de datos de SSISDB&#41;](../../integration-services/system-views/catalog-packages-ssisdb-database.md)  
  
-   [catalog.object_versions &#40;base de datos de SSISDB&#41;](../../integration-services/system-views/catalog-object-versions-ssisdb-database.md)  
  
##  <a name="a-nameparametersa-parameters"></a><a name="Parameters"></a> Parámetros  
 Use parámetros para asignar valores a las propiedades del paquete en el momento de la ejecución del mismo. Para establecer el valor de un paquete o parámetro de proyecto y borrar el valor, llame a [catalog.set_object_parameter_value &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-set-object-parameter-value-ssisdb-database.md) y [catalog.clear_object_parameter_value &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-clear-object-parameter-value-ssisdb-database.md). Para establecer el valor de un parámetro para una instancia de ejecución, llame a [catalog.set_execution_parameter_value &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md). Puede recuperar los valores de parámetro predeterminados si llama a [catalog.get_parameter_values &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-get-parameter-values-ssisdb-database.md).  
  
 Estas vistas muestran los parámetros de todos los paquetes y proyectos, así como los valores de los parámetros que se usan para una instancia de ejecución.  
  
-   [catalog.object_parameters &#40;base de datos de SSISDB&#41;](../../integration-services/system-views/catalog-object-parameters-ssisdb-database.md)  
  
-   [catalog.execution_parameter_values &#40;base de datos de SSISDB&#41;](../../integration-services/system-views/catalog-execution-parameter-values-ssisdb-database.md)  
  
##  <a name="a-nameserverenvironmentsa-server-environments-server-variables-and-server-environment-references"></a><a name="ServerEnvironments"></a> Entornos de servidor, variables de servidor y referencias del entorno de servidor  
 Los entornos de servidor contienen variables de servidor. Los valores variables se pueden usar cuando un paquete se ejecuta o se valida en el servidor [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Los siguientes procedimientos almacenados permiten realizar muchas otras tareas de administración para entornos y variables.  
  
-   [catalog.create_environment &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-create-environment-ssisdb-database.md)  
  
-   [catalog.delete_environment &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-delete-environment-ssisdb-database.md)  
  
-   [catalog.move_environment &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-move-environment-ssisdb-database.md)  
  
-   [catalog.rename_environment &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-rename-environment-ssisdb-database.md)  
  
-   [catalog.set_environment_property &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-set-environment-property-ssisdb-database.md)  
  
-   [catalog.create_environment_variable &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-create-environment-variable-ssisdb-database.md)  
  
-   [catalog.delete_environment_variable &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-delete-environment-variable-ssisdb-database.md)  
  
-   [catalog.set_environment_variable_property &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-set-environment-variable-property-ssisdb-database.md)  
  
-   [catalog.set_environment_variable_value &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-set-environment-variable-value-ssisdb-database.md)  
  
 Al llamar al procedimiento almacenado [catalog.set_environment_variable_protection &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-set-environment-variable-protection-ssisdb-database.md), puede establecer el bit de sensibilidad de una variable.  
  
 Para utilizar el valor de una variable de servidor, especifique la referencia entre el proyecto y el entorno del servidor. Puede usar los procedimientos almacenados siguientes para crear y eliminar referencias. También puede indicar si el entorno se puede encontrar en la misma carpeta que el proyecto o en una carpeta diferente.  
  
-   [catalog.create_environment_reference &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-create-environment-reference-ssisdb-database.md)  
  
-   [catalog.delete_environment_reference &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-delete-environment-reference-ssisdb-database.md)  
  
-   [catalog.set_environment_reference_type &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-set-environment-reference-type-ssisdb-database.md)  
  
 Para obtener más detalles sobre entornos y variables, consulte estas vistas.  
  
-   [catalog.environments &#40;base de datos de SSISDB&#41;](../../integration-services/system-views/catalog-environments-ssisdb-database.md)  
  
-   [catalog.environment_variables &#40;base de datos de SSISDB&#41;](../../integration-services/system-views/catalog-environment-variables-ssisdb-database.md)  
  
-   [catalog.environment_references &#40;base de datos de SSISDB&#41;](../../integration-services/system-views/catalog-environment-references-ssisdb-database.md)  
  
##  <a name="a-nameexecutionsa-executions-and-validations"></a><a name="Executions"></a> Ejecuciones y validaciones  
 Una ejecución es una instancia de una ejecución del paquete. Llame a [catalog.create_execution &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md) y [catalog.start_execution &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md) para crear e iniciar una ejecución. Para detener una ejecución o una validación de paquete o proyecto, llame a [catalog.stop_operation &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-stop-operation-ssisdb-database.md).  
  
 Para que un paquete en ejecución se ponga en pausa y cree un archivo de volcado, llame al procedimiento almacenado de catalog.create_execution_dump. Un archivo de volcado proporciona información sobre la ejecución de un paquete que puede ayudarle a solucionar problemas de ejecución. Para obtener más información acerca de cómo generar y configurar archivos de volcado, vea [Generating Dump Files for Package Execution](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md).  
  
 Para obtener más información sobre ejecuciones, validaciones, mensajes que se registran durante las operaciones y la información contextual relacionada con errores, consulte estas vistas.  
  
-   [catalog.executions &#40;base de datos de SSISDB&#41;](../../integration-services/system-views/catalog-executions-ssisdb-database.md)  
  
-   [catalog.operations &#40;base de datos de SSISDB&#41;](../../integration-services/system-views/catalog-operations-ssisdb-database.md)  
  
-   [catalog.operation_messages &#40;base de datos de SSISDB&#41;](../../integration-services/system-views/catalog-operation-messages-ssisdb-database.md)  
  
-   [catalog.extended_operation_info &#40;base de datos de SSISDB&#41;](../../integration-services/system-views/catalog-extended-operation-info-ssisdb-database.md)  
  
-   [catalog.event_messages](../../integration-services/system-views/catalog-event-messages.md)  
  
-   [catalog.event_message_context](../../integration-services/system-views/catalog-event-message-context.md)  
  
 Puede validar proyectos y paquetes si llama a los procedimientos almacenados [catalog.validate_project &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-validate-project-ssisdb-database.md) y [catalog.validate_package &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-validate-package-ssisdb-database.md). La vista [catalog.validations &#40;base de datos de SSISDB&#41;](../../integration-services/system-views/catalog-validations-ssisdb-database.md) proporciona detalles sobre validaciones, como las referencias del entorno de servidor que se consideran en la validación, si se trata de una validación de dependencia o de una validación completa, y si para ejecutar el paquete se usa el tiempo de ejecución de 32 bits o el tiempo de ejecución de 64 bits.  
  
##  <a name="a-namealwaysona-alwayson-support"></a><a name="AlwaysOn"></a> Compatibilidad con AlwaysOn  
 La característica Grupos de disponibilidad Always On es una solución de alta disponibilidad y de recuperación ante desastres que proporciona una alternativa empresarial a la creación de reflejo de la base de datos. Un grupo de disponibilidad admite un entorno de conmutación por error para un conjunto discreto de bases de datos de usuario, conocido como bases de datos de disponibilidad, que realizan la conmutación por error conjuntamente. Para más información, consulte [Grupos de disponibilidad AlwaysOn](https://msdn.microsoft.com/library/hh510230.aspx).  
  
 En [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], SQL Server Integration Services (SSIS) presenta nuevas funcionalidades que le permiten realizar implementaciones fácilmente en un catálogo SSIS centralizado (es decir, la base de datos de usuario de SSISDB). Para proporcionar alta disponibilidad de la base de datos SSISDB y su contenido (proyectos, paquetes, registros de ejecución, etc.), puede agregar dicha base de datos (igual que cualquier otra base de datos de usuario) a un grupo de disponibilidad Always On. Cuando se produce una conmutación por error, uno de los nodos secundarios se convierte automáticamente en el nuevo nodo principal.  
  
 Para más información e instrucciones paso a paso sobre cómo habilitar Always On para SSISDB, vea [Always On for SSIS Catalog &#40;SSISDB&#41;](../../integration-services/service/always-on-for-ssis-catalog-ssisdb.md).  
  
##  <a name="a-namerelatedtasksa-related-tasks"></a><a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Crear el catálogo de SSIS](../../integration-services/service/create-the-ssis-catalog.md)  
  
-   [Copia de seguridad, restauración y traslado del catálogo de SSIS](../../integration-services/service/backup-restore-and-move-the-ssis-catalog.md)  
  
##  <a name="a-namerelatedcontenta-related-content"></a><a name="RelatedContent"></a> Contenido relacionado  
  
-   Entrada de blog, [SSIS y PowerShell en SQL Server 2012](http://go.microsoft.com/fwlink/?LinkId=242539), en blogs.msdn.com.  
  
-   Entrada de blog [Sugerencias del control de acceso al catálogo de SSIS](http://go.microsoft.com/fwlink/?LinkId=246669), en blogs.msdn.com.  
  
-   Entrada del blog [A Glimpse of the SSIS Catalog Managed Object Model](http://go.microsoft.com/fwlink/?LinkId=254267), en blogs.msdn.com.  
  
  