---
title: "Preguntas m&#225;s frecuentes sobre actualizaci&#243;n e instalaci&#243;n (SQL Server R Services) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 001e66b9-6c3f-41b3-81b7-46541e15f9ea
caps.latest.revision: 58
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 47
---
# Preguntas m&#225;s frecuentes sobre actualizaci&#243;n e instalaci&#243;n (SQL Server R Services)
  En este tema encontrará respuesta a preguntas habituales sobre la instalación y sobre cómo actualizar versiones preliminares de [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)].  
  
 Si va a instalar [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] por primera vez, siga los procedimientos para instalar [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y los componentes de R descritos aquí: [Configurar SQL Server R Services &#40;en bases de datos&#41;](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md).  

   
## <a name="important-changes-from-pre-releae-versions"></a>Cambios importantes de versiones preliminares  
 Si ha instalado cualquier versión preliminar de SQL Server 2016 o si está usando las instrucciones de configuración que se publicaron antes del lanzamiento público de SQL Server 2016, es importante que sepa que el proceso de instalación es completamente diferente en las versiones preliminar y RTM. Estos cambios afectan a las opciones disponibles en el Asistente para la instalación de SQL Server y a los pasos posteriores a la instalación. 
   
> [!WARNING] Ya no se admite la instalación nueva de ninguna versión preliminar de [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]. Se recomienda que actualice lo antes posible.  
+ Si instaló [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] en CTP3, CTP3.1, CTP3.2, RC0 o RC1, deberá volver a ejecutar el script de instalación posterior a la configuración para desinstalar las versiones anteriores de los componentes de R y de R Services. 
+ El script de instalación posterior a la configuración se proporciona únicamente para ayudar a los clientes a desinstalar versiones preliminares.  No ejecute el script al instalar una versión más reciente.

## <a name="how-to-uninstall-previous-versions-of-r-services"></a>Cómo desinstalar versiones anteriores de R Services

Es importante que desinstale las versiones anteriores de [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] y sus componentes de R relacionados en el orden correcto.

### <a name="1-run-script-to-deregister-windows-user-group-and-components-before-uninstalling-previous-components"></a>1. Ejecute el script para anular el registro de los componentes y del grupo de usuarios de Windows antes de desinstalar los componentes anteriores.
Si ha instalado una versión preliminar de [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], debe ejecutar primero el script `RegisteREext.exe` con el argumento `/uninstall`.

Al hacerlo, anula el registro de componentes antiguos y quita el grupo de usuarios de Windows asociado a Launchpad. Si no lo hace, no podrá crear el grupo de usuarios de Windows necesario para instalar instancias nuevas.
  
Por ejemplo, si instaló R Services en la instancia predeterminada, ejecute este comando desde el directorio donde está instalado el script:  
  
~~~~
    RegisterRExt.exe /UNINSTALL  
~~~~ 
  
Si instaló R Services en una instancia con nombre, especifique el nombre de esa instancia después de *INSTANCE:*  
  
~~~~ 
RegisterRExt.exe /UNINSTALL /INSTANCE:<instancename>   
~~~~  

Es posible que deba ejecutar el script más de una vez para quitar todos los componentes.

> [!NOTE]
> La ubicación predeterminada de este script es diferente, en función de la versión preliminar que haya instalado. Si intenta ejecutar una versión incorrecta del script, podría obtener un error. 
> 
>  + Si tiene la versión CTP 3.1, 3.2 o 3.3, para poder desinstalar componentes, debe descargar una versión actualizada del script de configuración posterior a la instalación desde el [Centro de descarga de Microsoft](http://go.microsoft.com/fwlink/?LinkId=723194). El script actualizado admite la eliminación del registro de los componentes anteriores. Haga clic en el vínculo y seleccione **Guardar como** para guardar el script en una carpeta local. Cambie el nombre del script existente y, después, copie el nuevo en la carpeta donde se ejecutará. 
>  + En el caso de RC0, se instaló el archivo de script correcto, que se encuentra en esta carpeta: `C:\Program Files\Microsoft\MRO-for-RRE\8.0\R-3.2.2\library\RevoScaleR\rxLibs\x64`  
>  + En el caso de versiones de lanzamiento (13.0.1601.5 o posteriores), no se necesita ningún script para instalar o configurar componentes. El script debe usarse únicamente para quitar componentes anteriores. 


### <a name="2-uninstall-any-older-versions-of-the-revolution-enterprise-tools-including-components-installed-with-ctp-releases"></a>2. Desinstale las versiones anteriores de las herramientas de Revolution R Enterprise, incluidos los componentes instalados con versiones de CTP.

El orden de desinstalación de los componentes de R es fundamental. Siempre desinstale primero [!INCLUDE[rsql_rre-noversion](../../includes/rsql-rre-noversion-md.md)]. Después, desinstale [!INCLUDE[rsql_rro-noversion](../../includes/rsql-rro-noversion-md.md)].  

 Si desinstala R Open primero por error y, a raíz de eso, obtiene un error al intentar desinstalar Revolution R Enterprise, una solución provisional sería volver a instalar Revolution R Open o Microsoft R Open y después desinstalar ambos componentes en el orden correcto.  

### <a name="3-uninstall-any-other-version-of-microsoft-r-open"></a>3. Desinstale todas las demás versiones de Microsoft R Open.

Por último, desinstale todas las demás versiones de Microsoft R Open.
 
### <a name="4-upgrade-sql-server"></a>4. Actualizar SQL Server  
  
Después de que se hayan desinstalado todos los componentes preliminares, reinicie el equipo. Este es un requisito del programa de instalación de SQL Server y no podrá continuar con una instalación actualizada hasta que no se complete el reinicio.     

Una vez hecho esto, ejecute el programa de instalación de SQL Server y siga estas instrucciones para instalar [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]: [Configurar SQL Server R Services](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md).  
  
No se necesitan componentes adicionales. Los paquetes de R y de conectividad se instalan con el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 


## <a name="upgrading-r-components"></a>Actualización de componentes de R

A medida que se publiquen revisiones o mejoras de SQL Server 2016, los componentes de R también se actualizarán, si la instancia ya incluye la característica R Services. 

Pero cuando actualice o aplique revisiones a servidores que no están conectados a Internet, debe descargar manualmente una versión actualizada de los componentes de R para poder comenzar la actualización. Para obtener más información, consulte [Instalación de componentes de R sin acceso a Internet](../../advanced-analytics/r-services/installing-r-components-without-internet-access.md).

## <a name="problems-uninstalling-older-versions-of-r"></a>Problemas al desinstalar versiones anteriores de R  
En algunos casos, el proceso de desinstalación no quita completamente las versiones anteriores de Revolution R Open o Revolution R Enterprise.  
  
 Si tiene problemas para quitar una versión anterior, también puede editar el Registro para quitar las claves relacionadas.  
  
 Abra el Registro de Windows y busque esta clave: `HKLM\Software\Microsoft\Windows\CurrentVersion\Uninstall`.  
  
 Elimine todas las entradas siguientes, si están presentes, y si la clave solo contiene un único valor `sEstimatedSize2`:  
  
-   E0B2C29E-B8FC-490B-A043-2CAE75634972        (para 8.0.2)  
  
-   46695879-954E-4072-9D32-1CC84D4158F4        (para 8.0.1)  
  
-   2DF16DF8-A2DB-4EC6-808B-CB5A302DA91B        (para 8.0.0)  
  
-   5A2A1571-B8CD-4AAF-9303-8DF463DABE5A        (para 7.5.0)  


## <a name="new-license-agreement-for-r-components-required-for-unattended-installs"></a>Nuevo contrato de licencia para los componentes de R necesarios para las instalaciones desatendidas  
 Si usa la línea de comandos para actualizar una instancia de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] que ya tiene instalado [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], debe modificar la línea de comandos para usar el nuevo parámetro de contrato de licencia */IACCEPTROPENLICENSEAGREEMENT*. 
 
 Puede producirse un error en la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si no se usa el argumento correcto.  
  
## <a name="after-running-setup-includersqlproductnametokenrsqlproductnamemdmd-is-still-not-enabled"></a>Después de ejecutar el programa de instalación, [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] todavía no está habilitado  
 La característica que admite la ejecución de scripts externos está deshabilitada de forma predeterminada, aunque se haya instalado. Esto es así por diseño, para reducir el área expuesta.  
  
 Para habilitar los scripts de R, un administrador puede ejecutar la instrucción siguiente en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]:  
  
1.  En la instancia de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] donde quiera usar R, ejecute esta instrucción.  
  
    ```  
    sp_configure 'external scripts enabled',1 
    reconfigure with override  
    ```  
  
2.  Reinicie la instancia.  
  
3.  Una vez que se haya reiniciado la instancia, abra el **Administrador de configuración de SQL Server** o el panel **Servicios** y compruebe que el servicio [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] se está ejecutando.  

> [!TIP] Para instalar una instancia de R Services preconfigurada, use la imagen de máquina virtual de Azure que incluye Enterprise Edition con R Services habilitado. Para obtener más información, consulte [Instalación de SQL Server R Services en una máquina virtual de Azure](../../advanced-analytics/r-services/installing-sql-server-r-services-on-an-azure-virtual-machine.md).
 

## <a name="setup-of-includersqlproductnametokenrsqlproductnamemdmd-not-available-in-a-failover-cluster"></a>La configuración de [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] no está disponible en un clúster de conmutación por error  
 Actualmente, no es posible instalar [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] en un clúster de conmutación por error.  
    
 Pero puede instalar [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] en un equipo independiente que use Always On y forme parte de un grupo de disponibilidad. Para obtener más información sobre el uso de R Services en un grupo de disponibilidad Always On, vea [Grupos de disponibilidad AlwaysOn: interoperabilidad](../../database-engine/availability-groups/windows/always-on-availability-groups-interoperability-sql-server.md).  

Otra opción es configurar una réplica en una instancia diferente de SQL Server a fin de ejecutar scripts de R. La réplica puede crearse mediante replicación o trasvase de registros.
 
## <a name="launchpad-service-cannot-be-started"></a>No se puede iniciar el servicio Launchpad  

Hay varios problemas que pueden impedir que se inicie Launchpad.
+ **La notación 8.3 no está habilitada**.  Para instalar R Services (en bases de datos), la unidad donde está instalada la característica debe admitir la creación de nombres de archivo cortos mediante la notación **8.3**.  Un nombre de archivo 8.3 también se denomina nombre de archivo corto, y se usa para que sea compatible con versiones anteriores de Microsoft Windows o como nombre de archivo alternativo al nombre de archivo largo. 

  Si el volumen donde está instalando [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] no admite nombres de archivo cortos, los procesos que inicien R desde SQL Server podrían no encontrar el ejecutable correcto y [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] no se iniciará.  
  
   Como solución alternativa, debe habilitar la notación 8.3 en el volumen donde estén instalados SQL Server y R Services. Después, debe proporcionar el nombre corto del directorio de trabajo en el archivo de configuración de R Services. 

    1. Para habilitar la notación 8.3, ejecute la utilidad **fsutil** con el argumento *8dot3name*, como se muestra aquí: [fsutil 8dot3name](https://technet.microsoft.com/library/ff621566(v=ws.11).aspx).
    2. Una vez que se haya habilitado la notación 8.3, abra el archivo RLauncher.config. En una instalación predeterminada, el archivo RLauncher.config se encuentra en C:\Archivos de programa\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn.
    3. Tome nota de la propiedad de WORKING_DIRECTORY.
    4. Use la utilidad fsutil con el argumento *file* para especificar una ruta de acceso del archivo corta para la carpeta especificada en WORKING_DIRECTORY.
    5. Edite el archivo de configuración de modo que use el nombre corto de WORKING_DIRECTORY.   
     
También puede especificar un directorio diferente para WORKING_DIRECTORY que tenga una ruta de acceso compatible con la notación 8.3.     
   
   > [!NOTE] Esta restricción se quitará en una versión posterior. 
 
+ **Se ha cambiado la cuenta que ejecuta Launchpad o se han eliminado los permisos necesarios.** De forma predeterminada, [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] usa la cuenta siguiente al iniciar, que el programa de instalación de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] configura para que tenga todos los permisos necesarios: NT Service\MSSQLLaunchpad.

  Por lo tanto, si asigna una cuenta diferente a Launchpad o si una directiva de la máquina con SQL Server quita el derecho, la cuenta podría no tener los permisos necesarios y podría ver este error: *ERROR_LOGON_TYPE_NOT_GRANTED 1385 (0x569) Error de inicio de sesión: el usuario no tiene permisos para el tipo de inicio de sesión solicitado en el equipo.*

  Para conceder los permisos necesarios a la nueva cuenta de servicio, use la aplicación **Directiva de seguridad local** y actualice los permisos de la cuenta para incluir estos permisos:
  + Ajustar las cuotas de memoria de un proceso (SeIncreaseQuotaPrivilege)
  + Omitir la comprobación transversal (SeChangeNotifyPrivilege)
  + Iniciar sesión como servicio (SeServiceLogonRight)
  + Reemplazar un token de nivel de proceso (SeAssignPrimaryTokenPrivilege)

  Para obtener más información sobre los permisos para ejecutar servicios de SQL Server, consulte [Configurar los permisos y las cuentas de servicio de Windows](https://msdn.microsoft.com/library/ms143504.aspx#Windows).
  
## <a name="side-by-side-installation-not-supported"></a>No se admite la instalación en paralelo  
 No cree una instalación en paralelo con otra versión de R ni con otras versiones de Revolution Analytics.  

## <a name="offline-installation-of-r-components-for-localized-version-of-sql-server"></a>Instalación sin conexión de los componentes de R para una versión localizada de SQL Server 
Si va a instalar R Services en un equipo que no tiene acceso a Internet, debe realizar dos pasos adicionales: debe descargar el instalador de componentes de R en una carpeta local antes de ejecutar el programa de instalación de SQL Server y debe editar el archivo instalador para asegurarse de que se instale el idioma correcto. 

El identificador de idioma que se usa para los componentes de R debe coincidir con el idioma del programa de instalación de SQL Server que se está instalando. De lo contrario, el botón **Siguiente** estará deshabilitado y no se podrá completar la instalación.

Para obtener más información, consulte [Instalación de componentes de R sin acceso a Internet](../../advanced-analytics/r-services/installing-r-components-without-internet-access.md). 
  
## <a name="unable-to-launch-runtime-for-r-script"></a>No se puede iniciar el tiempo de ejecución para el script de R
[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] crea un grupo de usuarios de Windows que [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] usa para ejecutar trabajos de R. Este grupo de usuarios debe poder iniciar sesión en la instancia que ejecuta R Services para ejecutar R en nombre de los usuarios remotos que usan la autenticación integrada de Windows.
  
 En un entorno en el que el grupo de Windows para los usuarios de R (**SQLRUsers**) no tiene este permiso, pueden aparecer los errores siguientes:  
  
-   Al intentar ejecutar scripts de R:  
  
     *No se puede iniciar el tiempo de ejecución para el script 'R'. Compruebe la configuración del tiempo de ejecución 'R'.*  
  
     *An external script error occurred. Unable to launch the runtime.* (Error en el script externo. No se puede iniciar el tiempo de ejecución).  
  
-   Errores generados por el servicio de [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] :  
  
     *Failed to initialize the launcher RLauncher.dll* (No se pudo inicializar el iniciador RLauncher.dll)  
  
     *No launcher dlls were registered!* (No se registraron .dll de iniciador)  
  
-   Los registros de seguridad indican que la cuenta NT SERVICE\MSSQLLAUNCHPAD no pudo iniciar sesión.  
  
Para obtener información sobre cómo asignar a este grupo de usuarios los permisos necesarios, consulte [Configurar SQL Server R Services ](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md). 

> [!NOTE]
> 
> Esta limitación no se aplica si usa inicios de sesión de SQL para ejecutar scripts de R desde una estación de trabajo remota. 

  
## <a name="remote-execution-via-odbc"></a>Ejecución remota a través de ODBC   
 Si usa una estación de trabajo de ciencia de datos y se conecta al equipo con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para ejecutar comandos de R mediante las funciones **RevoScaleR**, puede aparecer un error al usar llamadas ODBC que escriben datos en el servidor. 
 
 El motivo es el mismo que se describe en la sección anterior: durante la instalación, R Services crea un grupo de cuentas de trabajo que se usan para ejecutar tareas de R. Pero si estas cuentas no se pueden conectar al servidor, no se pueden ejecutar llamadas ODBC en su nombre. 
 
 Tenga en cuenta que esta limitación no se aplica si usa inicios de sesión de SQL para ejecutar scripts de R desde una estación de trabajo remota, ya que las credenciales de inicio de sesión de SQL se pasan explícitamente desde el cliente de R a la instancia de SQL Server y, después, a ODBC.
  
Para habilitar la autenticación implícita, debe conceder permisos a este grupo de cuentas de trabajo como se indica a continuación:  
    
1. Abra [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] como administrador en la instancia donde se ejecutará código de R. 

2. Ejecute el script siguiente. Asegúrese de editar el nombre del grupo de usuario, si ha cambiado el valor predeterminado, y el nombre de equipo y de instancia.
    ```sql
    USE [master]
    GO
    
    CREATE LOGIN [computername\SQLRUserGroup] FROM WINDOWS WITH DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[language]
    GO  
    ```

Para obtener más información y conocer los pasos necesarios para hacerlo mediante la interfaz de usuario de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], consulte [Configurar SQL Server R Services ](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md).

    
## <a name="errors-during-setup-because-r-components-cannot-be-installed"></a>Errores durante la instalación debido a que no se pueden instalar componentes de R  
 Cuando se instala R Services (en bases de datos) mediante el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], al hacer clic en **Aceptar** en la página que contiene los términos de licencia de Microsoft R Open, el programa de instalación debe localizar los componentes y empezar la instalación cuando se instalen otros componentes. Pero en estos casos, es posible que se produzcan errores en la instalación de los componentes:  
  
-   Realiza una instalación sin conexión y no se pueden descargar los componentes.  
  
     [Instalación de componentes de R sin acceso a Internet](../../advanced-analytics/r-services/installing-r-components-without-internet-access.md)  
  
-   Usa la opción de comprobar las actualizaciones y el servicio de actualización devuelve un error porque no puede encontrar la versión correcta del componente.  
  
  Este es un problema conocido que se ha corregido en RC3.  
  
 
  
## <a name="upgrade-of-r-server-standalone-to-rc3-requires-uninstallation-using-the-rc2-setup-utility"></a>La actualización de R Server (independiente) a RC3 requiere la desinstalación mediante la utilidad de configuración de RC2
 Microsoft R Server (independiente) está disponible a partir de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] RC2. Para actualizar a la versión RC3 de Microsoft R Server, primero debe realizar la desinstalación mediante el programa de instalación de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] RC2 y, después, volver a instalar mediante el programa de instalación de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] RC3.  
  
1.  Desinstale R Server (independiente) para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] RC2 mediante el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
2.  Actualice [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] a RC3 y seleccione la opción para instalar R Services (en bases de datos). Esto actualiza la instancia de [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] a RC3. No es necesaria ninguna configuración adicional.  
  
3.  Ejecute el programa de instalación de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para RC3 otra vez e instale Microsoft R Server (independiente).  

Esta solución alternativa no es necesaria cuando se actualiza a la versión RTM de Microsoft R Server.

## <a name="see-also"></a>Vea también  
 [Introducción a SQL Server R Services](../../advanced-analytics/r-services/getting-started-with-sql-server-r-services.md)   
 [Introducción a Microsoft R Server &#40;independiente&#41;](../../advanced-analytics/r-services/getting-started-with-microsoft-r-server-standalone.md)  
  
  