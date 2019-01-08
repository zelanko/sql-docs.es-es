---
title: Catálogo de SSIS | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 24bd987e-164a-48fd-b4f2-cbe16a3cd95e
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a9eb4de07ad7bd564578462b053637bb472b22f6
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/13/2018
ms.locfileid: "53353984"
---
# <a name="ssis-catalog"></a>Catálogo de SSIS
  El `SSISDB` catálogo es el punto central para trabajar con [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] (SSIS), proyectos que han implementado en el [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] server. Por ejemplo, establece los parámetros del proyecto y del paquete, configura entornos para especificar los valores en tiempo de ejecución para los paquetes, ejecuta paquetes y soluciona los problemas de los mismos, y administra las operaciones del servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Los objetos que se almacenan en el `SSISDB` catalog incluye proyectos, paquetes, parámetros, entornos e historial de operaciones.  
  
 Inspeccionar objetos, valores y datos operativos que se almacenan en el `SSISDB` catálogo, consultando las vistas en el `SSISDB` base de datos. Administrar los objetos mediante una llamada a procedimientos almacenados el `SSISDB` de base de datos o mediante la interfaz de usuario de la `SSISDB` catálogo. En muchos casos, la misma tarea se puede realizar en la interfaz de usuario o al llamar a un procedimiento almacenado.  
  
 Para mantener la base de datos de `SSISDB`, se recomienda aplicar las directivas corporativas estándar para administrar las bases de datos de usuario. Para obtener información acerca de cómo crear planes de mantenimiento, vea [Maintenance Plans](../../relational-databases/maintenance-plans/maintenance-plans.md).  
  
 El `SSISDB` catálogo y el `SSISDB` database: compatibilidad con Windows PowerShell. Para obtener más información acerca de cómo usar SQL Server con Windows PowerShell, vea [SQL Server PowerShell](../../powershell/sql-server-powershell.md). Para obtener ejemplos de cómo usar Windows PowerShell para completar tareas como implementar un proyecto, vea la entrada del blog [SSIS y PowerShell en SQL Server 2012](https://go.microsoft.com/fwlink/?LinkId=242539), en blogs.msdn.com.  
  
 Para obtener más información acerca de cómo ver los datos de las operaciones, consulte [supervisión de ejecuciones de paquetes y otras operaciones](../performance/monitor-running-packages-and-other-operations.md).  
  
 Obtener acceso a la `SSISDB` de catálogo en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] conectándose a la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] motor de base de datos y, a continuación, expandir el **catálogos de Integration Services** nodo en el Explorador de objetos. Obtener acceso a la `SSISDB` en la base de datos [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] expandiendo el nodo bases de datos en el Explorador de objetos.  
  
> [!NOTE]  
>  No se puede cambiar el nombre de la `SSISDB` base de datos.  
  
> [!NOTE]  
>  Si el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de instancia que el `SSISDB` base de datos se adjunta a, se detiene o no responde, el ISServerExec.exe proceso finaliza. Se escribe un mensaje en un registro de eventos de Windows.  
>   
>  Si los recursos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conmutan por error como parte de una conmutación por error de clúster, los paquetes en ejecución no se reinician. Puede usar los puntos de comprobación para reiniciar los paquetes. Para más información, consulte [Restart Packages by Using Checkpoints](../packages/restart-packages-by-using-checkpoints.md).  
  
## <a name="catalog-object-identifiers"></a>Identificadores de objeto de catálogo  
 Cuando cree un nuevo objeto en el catálogo, asígnele un nombre El nombre del objeto es un identificador. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] define las reglas para las que los caracteres se pueden usar en un identificador. Los nombres de los siguientes objetos deben seguir las reglas de identificador.  
  
-   Carpeta  
  
-   Proyecto  
  
-   Entorno  
  
-   Parámetro  
  
-   Variable de entorno  
  
### <a name="folder-project-environment"></a>Carpeta, proyecto, entorno  
 Tenga en cuenta las reglas siguientes al cambiar el nombre de una carpeta, un proyecto, o un entorno.  
  
-   Entre los caracteres no válidos, se incluyen los caracteres ASCII/Unicode del 1 al 31, comillas dobles ("), menor que (\<), mayor que (>), barra vertical (|), retroceso (\b), NULL (\0) y tabulación (\t).  
  
-   El nombre no puede contener espacios delante ni detrás.  
  
-   \@ no se permite como primer carácter, pero los caracteres subsiguientes pueden utilizar \@.  
  
-   La longitud del nombre debe ser mayor que 0 y menor o igual que 128.  
  
### <a name="parameter"></a>Parámetro  
 Tenga en cuenta las reglas siguientes cuando asigne un nombre a un parámetro.  
  
-   El primer carácter del nombre debe ser una letra, tal como se define en el Estándar Unicode 2.0, o un carácter de subrayado (_).  
  
-   Los caracteres siguientes pueden ser letras o números, tal como se define en el Estándar Unicode 2.0, o un carácter de subrayado (_).  
  
### <a name="environment-variable"></a>Variable de entorno  
 Tenga en cuenta las reglas siguientes cuando asigne un nombre a una variable de entorno.  
  
-   Entre los caracteres no válidos, se incluyen los caracteres ASCII/Unicode del 1 al 31, comillas dobles ("), menor que (\<), mayor que (>), barra vertical (|), retroceso (\b), NULL (\0) y tabulación (\t).  
  
-   El nombre no puede contener espacios delante ni detrás.  
  
-   \@ no se permite como primer carácter, pero los caracteres subsiguientes pueden utilizar \@.  
  
-   La longitud del nombre debe ser mayor que 0 y menor o igual que 128.  
  
-   El primer carácter del nombre debe ser una letra, tal como se define en el Estándar Unicode 2.0, o un carácter de subrayado (_).  
  
-   Los caracteres siguientes pueden ser letras o números, tal como se define en el Estándar Unicode 2.0, o un carácter de subrayado (_).  
  
## <a name="catalog-configuration"></a>Configuración de catálogo  
 Ajusta con precisión cómo se comporta el catálogo ajustando las propiedades del catálogo. Las propiedades del catálogo definen cómo se cifra la información confidencial y cómo se conservan las operaciones y los datos de versiones del proyecto. Para establecer las propiedades del catálogo, use el cuadro de diálogo **Propiedades del catálogo** o llame al procedimiento almacenado [catalog.configure_catalog &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-configure-catalog-ssisdb-database). Para ver las propiedades, use el cuadro de diálogo o la consulta [catalog.catalog_properties &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-views/catalog-catalog-properties-ssisdb-database). Puede tener acceso al cuadro de diálogo haciendo clic con el botón secundario en `SSISDB` en el Explorador de objetos.  
  
### <a name="operations-and-project-version-cleanup"></a>Limpieza de las operaciones y los datos de versiones del proyecto  
 Los datos de estado para muchas de las operaciones del catálogo se almacena en tablas de base de datos internas. Por ejemplo, el catálogo realiza el seguimiento del estado de las ejecuciones de paquetes y las implementaciones de proyecto. Para mantener el tamaño de los datos de operaciones, se usa **Tareas de mantenimiento de SSIS Server** de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para quitar los datos antiguos. Este trabajo del agente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se crea al instalar [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Puede actualizar o volver a implementar un proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] implementándolo con el mismo nombre en la misma carpeta en el catálogo. De forma predeterminada, cada vez vuelva a implementar un proyecto, el `SSISDB` catálogo conserva la versión anterior del proyecto. Para mantener el tamaño de los datos de las operaciones, se utiliza el **trabajo de mantenimiento del Agente SQL Server** para quitar las versiones anteriores de proyectos.  
  
 La siguiente `SSISDB` las propiedades del catálogo definen cómo este [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se comporta el trabajo del agente. Puede ver y modificar las propiedades mediante el cuadro de diálogo **Propiedades del catálogo** o mediante [catalog.catalog_properties &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-views/catalog-catalog-properties-ssisdb-database) y [catalog.configure_catalog &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-configure-catalog-ssisdb-database).  
  
 **Borrar registros periódicamente**  
 El paso de trabajo de limpieza de operaciones se ejecuta cuando esta propiedad se establece en `True`.  
  
 **Período de retención (días)**  
 Define la antigüedad máxima de los datos permitidos para las operaciones (en días). Se quitan los datos más antiguos.  
  
 El valor mínimo es un día. El valor máximo está limitado sólo por el valor máximo de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `int` datos. Para más información sobre este tipo de datos, vea [int, bigint, smallint y tinyint &#40;Transact-SQL&#41;](/sql/t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql).  
  
 **Quitar periódicamente versiones anteriores**  
 El paso de trabajo de limpieza de versiones del proyecto se ejecuta cuando esta propiedad se establece en `True`.  
  
 **Número máximo de versiones por proyecto**  
 Define cuántas versiones de un proyecto se almacenan en el catálogo. Se quitan las versiones anteriores de proyectos.  
  
### <a name="encryption-algorithm"></a>Algoritmo de cifrado  
 La propiedad **Algoritmo de cifrado** especifica el tipo de cifrado que se utiliza para cifrar los valores de los parámetros confidenciales. Puede elegir entre los siguientes tipos de cifrado.  
  
-   AES_256 (predeterminado)  
  
-   AES_192  
  
-   AES_128  
  
-   DESX  
  
-   TRIPLE_DES_3KEY  
  
-   TRIPLE_DES  
  
-   DES  
  
 Al implementar un proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en el servidor [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], el catálogo cifra automáticamente los datos del paquete y los valores confidenciales. El catálogo también descifra automáticamente los datos cuando lo recupera. El catálogo de SSISDB emplea el nivel de protección `ServerStorage`. Para más información, consulte [Access Control for Sensitive Data in Packages](../security/access-control-for-sensitive-data-in-packages.md).  
  
 Cambiar el algoritmo de cifrado es una operación que lleva mucho tiempo. En primer lugar, el servidor tiene que utilizar el algoritmo especificado previamente para descifrar todos los valores de configuración. A continuación, el servidor tiene que utilizar el nuevo algoritmo para volver a cifrar los valores. Durante este tiempo, no puede haber otras operaciones de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en el servidor. Así, para que las operaciones de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] continúen sin interrupción, el algoritmo de cifrado es un valor de solo lectura en el cuadro de diálogo de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
 Para cambiar la **algoritmo de cifrado** establecer la configuración de la propiedad, el `SSISDB` de base de datos para el modo de usuario único y, a continuación, llame al procedimiento almacenado catalog.configure_catalog. Use ENCRYPTION_ALGORITHM para el argumento *property_name* . Para más información sobre los valores de propiedad admitidos, vea [catalog.catalog_properties &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-views/catalog-catalog-properties-ssisdb-database). Para más información sobre el procedimiento almacenado, vea [catalog.configure_catalog &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-configure-catalog-ssisdb-database).  
  
 Para más información sobre el modo de usuario único, vea [Establecer una base de datos en modo de usuario único](../../relational-databases/databases/set-a-database-to-single-user-mode.md). Para más información sobre el cifrado y los algoritmos de cifrado en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea los temas de la sección [Cifrado de SQL Server](../../relational-databases/security/encryption/sql-server-encryption.md).  
  
 Para el cifrado se utiliza una clave maestra de base de datos. La clave se crea al crear el catálogo. Para más información, vea [Crear el catálogo de SSIS](ssis-catalog.md).  
  
 En la tabla siguiente se muestran los nombres de propiedad que aparecen en el cuadro de diálogo **Propiedades del catálogo** y las propiedades correspondientes de la vista de base de datos.  
  
|Nombre de la propiedad (cuadro de diálogo**Propiedades del catálogo** )|Nombre de la propiedad (vista de base de datos)|  
|---------------------------------------------------------|-------------------------------------|  
|Nombre del algoritmo de cifrado|ENCRYPTION_ALGORITHM|  
|Borrar registros periódicamente|OPERATION_CLEANUP_ENABLED|  
|Período de retención (días)|RETENTION_WINDOW|  
|Quitar periódicamente versiones anteriores|VERSION_CLEANUP_ENABLED|  
|Número máximo de versiones por proyecto|MAX_PROJECT_VERSIONS|  
|Nivel de registro predeterminado de todo el servidor|SERVER_LOGGING_LEVEL|  
  
## <a name="permissions"></a>Permisos  
 Los proyectos, los entornos y los paquetes se encuentran en carpetas que son objetos protegibles. Puede conceder permisos a una carpeta, incluido el permiso de MANAGE_OBJECT_PERMISSIONS. MANAGE_OBJECT_PERMISSIONS le permite delegar la administración del contenido de la carpeta a un usuario sin tener que conceder la pertenencia del usuario al rol ssis_admin. También puede conceder permisos a los proyectos, entornos y operaciones. Las operaciones incluyen inicializar [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], implementar proyectos, crear e iniciar ejecuciones, validar proyectos y paquetes y configurar el `SSISDB` catálogo.  
  
 Para obtener más información sobre los roles de base de datos, vea [Roles de nivel de base de datos](../../relational-databases/security/authentication-access/database-level-roles.md).  
  
 El catálogo de SSISDB usa un desencadenador DDL, ddl_cleanup_object_permissions, para exigir la integridad de la información sobre permisos para elementos de SSIS protegibles. El desencadenador se activa cuando se quita de la base de datos de SSISDB una entidad de seguridad de base de datos, como un usuario de base de datos, un rol de base de datos o un rol de aplicación de base de datos.  
  
 Si la entidad de seguridad ha concedido o denegado los permisos a otras entidades de seguridad, revoque los permisos proporcionados por el otorgante, antes de que la entidad de seguridad se pueda quitar. De lo contrario, se devuelve un mensaje de error cuando el sistema intenta quitar la entidad de seguridad. El desencadenador quita todos los registros de permisos donde la entidad de seguridad de base de datos es un receptor.  
  
 Se recomienda que el desencadenador no se deshabilite porque garantiza que no hay ningún registro de permiso huérfano después de quita una entidad de seguridad de base de datos de la `SSISDB` base de datos.  
  
### <a name="managing-permissions"></a>Administrar permisos  
 Puede administrar permisos mediante la interfaz de usuario de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , los procedimientos almacenados y el espacio de nombres <xref:Microsoft.SqlServer.Management.IntegrationServices> .  
  
 Para administrar permisos con la interfaz de usuario de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , use los cuadros de diálogo siguientes.  
  
-   Para una carpeta, use la página **Permisos** del [Folder Properties Dialog Box](folder-properties-dialog-box.md).  
  
-   Para un proyecto, use la página **Permisos** del [Project Properties Dialog Box](project-properties-dialog-box.md).  
  
 Para administrar permisos mediante Transact-SQL, llame a [catalog.grant_permission &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-grant-permission-ssisdb-database), [catalog.deny_permission &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-deny-permission-ssisdb-database) y [catalog.revoke_permission &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-revoke-permission-ssisdb-database). Para ver los permisos efectivos de la entidad de seguridad actual para todos los objetos, consulte [catalog.effective_object_permissions &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-views/catalog-effective-object-permissions-ssisdb-database). Este tema proporciona descripciones de los diferentes tipos de permisos. Para ver los permisos asignados explícitamente al usuario, consulte [catalog.explicit_object_permissions &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-views/catalog-explicit-object-permissions-ssisdb-database).  
  
## <a name="folders"></a>Carpetas  
 Una carpeta contiene uno o varios proyectos y entornos en los `SSISDB` catálogo. Puede usar la vista [catalog.folders &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-views/catalog-folders-ssisdb-database) para acceder a información sobre las carpetas del catálogo. Puede utilizar los siguientes procedimientos almacenados para administrar carpetas.  
  
-   [catalog.create_folder &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-create-folder-ssisdb-database)  
  
-   [catalog.delete_folder &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-delete-folder-ssisdb-database)  
  
-   [catalog.rename_folder &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-rename-folder-ssisdb-database)  
  
-   [catalog.set_folder_description &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-set-folder-description-ssisdb-database)  
  
## <a name="projects-and-packages"></a>Proyectos y paquetes  
 Cada proyecto puede contener varios paquetes. Proyectos y paquetes pueden contener parámetros y referencias a los entornos. Puede tener acceso a los parámetros y referencias del entorno mediante el uso de [Configure Dialog Box](configure-dialog-box.md).  
  
 Puede realizar otras tareas de proyectos llamando a los siguientes procedimientos almacenados.  
  
-   [catalog.delete_project &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-delete-project-ssisdb-database)  
  
-   [catalog.deploy_project &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-deploy-project-ssisdb-database)  
  
-   [catalog.get_project &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-get-project-ssisdb-database)  
  
-   [catalog.move_project &#40;&#40;base de datos de SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-move-project-ssisdb-database)  
  
-   [catalog.restore_project &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-restore-project-ssisdb-database)  
  
 Estas vistas proporcionan detalles sobre los paquetes, proyectos y versiones del proyecto.  
  
-   [catalog.projects &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-views/catalog-projects-ssisdb-database)  
  
-   [catalog.packages &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-views/catalog-packages-ssisdb-database)  
  
-   [catalog.object_versions &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-views/catalog-object-versions-ssisdb-database)  
  
## <a name="parameters"></a>Parámetros  
 Use parámetros para asignar valores a las propiedades del paquete en el momento de la ejecución del mismo. Para establecer el valor de un paquete o parámetro de proyecto y borrar el valor, llame a [catalog.set_object_parameter_value &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-set-object-parameter-value-ssisdb-database) y [catalog.clear_object_parameter_value &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-clear-object-parameter-value-ssisdb-database). Para establecer el valor de un parámetro para una instancia de ejecución, llame a [catalog.set_execution_parameter_value &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database). Puede recuperar los valores de parámetro predeterminados si llama a [catalog.get_parameter_values &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-get-parameter-values-ssisdb-database).  
  
 Estas vistas muestran los parámetros de todos los paquetes y proyectos, así como los valores de los parámetros que se usan para una instancia de ejecución.  
  
-   [catalog.object_parameters &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-views/catalog-object-parameters-ssisdb-database)  
  
-   [catalog.execution_parameter_values &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-views/catalog-execution-parameter-values-ssisdb-database)  
  
## <a name="server-environments-server-variables-and-server-environment-references"></a>Entornos de servidor, variables de servidor y referencias del entorno de servidor  
 Los entornos de servidor contienen variables de servidor. Los valores variables se pueden usar cuando un paquete se ejecuta o se valida en el servidor [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Los siguientes procedimientos almacenados permiten realizar muchas otras tareas de administración para entornos y variables.  
  
-   [catalog.create_environment &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-create-environment-ssisdb-database)  
  
-   [catalog.delete_environment &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-delete-environment-ssisdb-database)  
  
-   [catalog.move_environment &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-move-environment-ssisdb-database)  
  
-   [catalog.rename_environment &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-rename-environment-ssisdb-database)  
  
-   [catalog.set_environment_property &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-set-environment-property-ssisdb-database)  
  
-   [catalog.create_environment_variable &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-create-environment-variable-ssisdb-database)  
  
-   [catalog.delete_environment_variable &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-delete-environment-variable-ssisdb-database)  
  
-   [catalog.set_environment_variable_property &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-set-environment-variable-property-ssisdb-database)  
  
-   [catalog.set_environment_variable_value &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-set-environment-variable-value-ssisdb-database)  
  
 Al llamar al procedimiento almacenado [catalog.set_environment_variable_protection &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-set-environment-variable-protection-ssisdb-database), puede establecer el bit de sensibilidad de una variable.  
  
 Para utilizar el valor de una variable de servidor, especifique la referencia entre el proyecto y el entorno del servidor. Puede usar los procedimientos almacenados siguientes para crear y eliminar referencias. También puede indicar si el entorno se puede encontrar en la misma carpeta que el proyecto o en una carpeta diferente.  
  
-   [catalog.create_environment_reference &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-create-environment-reference-ssisdb-database)  
  
-   [catalog.delete_environment_reference &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-delete-environment-reference-ssisdb-database)  
  
-   [catalog.set_environment_reference_type &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-set-environment-reference-type-ssisdb-database)  
  
 Para obtener más detalles sobre entornos y variables, consulte estas vistas.  
  
-   [catalog.environments &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-views/catalog-environments-ssisdb-database)  
  
-   [catalog.environment_variables &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-views/catalog-environment-variables-ssisdb-database)  
  
-   [catalog.environment_references &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-views/catalog-environment-references-ssisdb-database)  
  
## <a name="executions-and-validations"></a>Ejecuciones y validaciones  
 Una ejecución es una instancia de una ejecución del paquete. Llame a [catalog.create_execution &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database) y [catalog.start_execution &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database) para crear e iniciar una ejecución. Para detener una ejecución o una validación de paquete o proyecto, llame a [catalog.stop_operation &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-stop-operation-ssisdb-database).  
  
 Para que un paquete en ejecución se ponga en pausa y cree un archivo de volcado, llame al procedimiento almacenado de catalog.create_execution_dump. Un archivo de volcado proporciona información sobre la ejecución de un paquete que puede ayudarle a solucionar problemas de ejecución. Para obtener más información acerca de cómo generar y configurar archivos de volcado, vea [Generating Dump Files for Package Execution](../troubleshooting/generating-dump-files-for-package-execution.md).  
  
 Para obtener más información sobre ejecuciones, validaciones, mensajes que se registran durante las operaciones y la información contextual relacionada con errores, consulte estas vistas.  
  
-   [catalog.executions &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-views/catalog-executions-ssisdb-database)  
  
-   [catalog.operations &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-views/catalog-operations-ssisdb-database)  
  
-   [catalog.operation_messages &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-views/catalog-operation-messages-ssisdb-database)  
  
-   [catalog.extended_operation_info &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-views/catalog-extended-operation-info-ssisdb-database)  
  
-   [catalog.event_messages](/sql/integration-services/system-views/catalog-event-messages)  
  
-   [catalog.event_message_context](/sql/integration-services/system-views/catalog-event-message-context)  
  
 Puede validar proyectos y paquetes si llama a los procedimientos almacenados [catalog.validate_project &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-validate-project-ssisdb-database) y [catalog.validate_package &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-validate-package-ssisdb-database). La vista [catalog.validations &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-views/catalog-validations-ssisdb-database) proporciona detalles sobre validaciones, como las referencias del entorno de servidor que se consideran en la validación, si se trata de una validación de dependencia o de una validación completa, y si para ejecutar el paquete se usa el tiempo de ejecución de 32 bits o el tiempo de ejecución de 64 bits.  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [Crear el catálogo de SSIS](ssis-catalog.md)  
  
-   [Copia de seguridad, restauración y traslado del catálogo de SSIS](../backup-restore-and-move-the-ssis-catalog.md)  
  
## <a name="related-content"></a>Contenido relacionado  
  
-   Entrada de blog, [SSIS y PowerShell en SQL Server 2012](https://go.microsoft.com/fwlink/?LinkId=242539), en blogs.msdn.com.  
  
-   Entrada de blog [Sugerencias del control de acceso al catálogo de SSIS](https://go.microsoft.com/fwlink/?LinkId=246669), en blogs.msdn.com.  
  
-   Entrada del blog [A Glimpse of the SSIS Catalog Managed Object Model](https://go.microsoft.com/fwlink/?LinkId=254267), en blogs.msdn.com.  
  
  
