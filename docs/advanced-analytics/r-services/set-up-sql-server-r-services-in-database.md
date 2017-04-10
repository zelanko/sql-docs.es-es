---
title: "Configurar SQL Server R Services (en bases de datos) | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
keywords: 
  - "instalación de SQL Server R Services"
ms.assetid: 4d773c74-c779-4fc2-b1b6-ec4b4990950d
caps.latest.revision: 35
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 30
---
# Configurar SQL Server R Services (en bases de datos)
  En [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y versiones posteriores, puede instalar todos los componentes relacionados con [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] mediante el Asistente para la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
 
 
 Una vez completada la instalación, puede que sea necesario llevar a cabo algunos pasos adicionales para habilitar la característica R Services, configurar cuentas y conceder a los usuarios permisos para bases de datos específicas.   
  
Si experimenta problemas con el acceso a bases de datos después de completar la instalación o si necesita desinstalar versiones anteriores, consulte [Preguntas más frecuentes sobre actualización e instalación &#40;SQL Server R Services&#41;](../../advanced-analytics/r-services/upgrade-and-installation-faq-sql-server-r-services.md).  

> [!NOTE]
> Para instalar R Services (en bases de datos), la unidad donde está instalada la característica debe admitir la creación de nombres de archivo cortos mediante la notación 8.3. En caso contrario, los procesos que R inicie desde SQL Server podrían no iniciarse. Asegúrese de habilitar la notación 8.3 en el volumen antes de instalar R Services. Esta restricción se quitará en una versión posterior.

  
##  <a name="a-namebkmkinstallrservicesindatabasea-step-1-install-r-services-in-database-on-sql-server-2016-or-later"></a><a name="bkmk_installRServicesInDatabase"></a> Paso 1: instalar R Services (en bases de datos) en SQL Server 2016 o posterior  
   
  
1.  Ejecute el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
    Para obtener más información sobre cómo realizar instalaciones desatendidas, consulte [Unattended Installs of SQL Server R Services](../../advanced-analytics/r-services/unattended-installs-of-sql-server-r-services.md).  
  
2.  En la pestaña **Instalación** , haga clic en **Nueva instalación independiente de SQL Server o agregar características a una instalación existente**.  
  
    > [!NOTE]  
    >  No se puede instalar [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] en un clúster de conmutación por error. Pero puede instalar [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] en un equipo independiente que use Always On y forme parte de un grupo de disponibilidad. Para obtener más información sobre el uso de R Services en un grupo de disponibilidad Always On, vea [Grupos de disponibilidad AlwaysOn: interoperabilidad](../../database-engine/availability-groups/windows/always-on-availability-groups-interoperability-sql-server.md).  
  
3.  En la página **Selección de características** , seleccione estas opciones:  
  
    -   **Servicios de Motor de base de datos**  
  
         Se requiere al menos una instancia del motor de base de datos para usar [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]. Puede usar una instancia con nombre o una instancia predeterminada.  
  
    -   **R Services (en bases de datos)**  
  
         Esta opción configura los servicios de base de datos que usan los trabajos de R e instala las extensiones que admiten scripts y procesos externos.  
    > [!NOTE]
    > 
    > Si necesita ejecutar código de R en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], asegúrese de instalar **[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]**. 
    > 
    > En cambio, Microsoft R Server (independiente) es una opción que le permite usar las bibliotecas de Scale R en un equipo de Windows que no ejecuta SQL Server. Se recomienda que instale Microsoft R Server (independiente) en un equipo portátil o en otro equipo que se use para el desarrollo en R, para crear soluciones de R que después se puedan implementar en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que ejecute R Services (en bases de datos).
 
  
4.  En la página **Consentimiento para instalar Microsoft R Open**, haga clic en **Aceptar**.  
  
     Es necesario aceptar este contrato de licencia para descargar Microsoft R Open, que incluye una distribución de las herramientas y paquetes base de R de código abierto, junto con proveedores de conectividad y paquetes de R mejorados de Revolution Analytics.  
  
    > [!NOTE]  
    >  Si el equipo que está usando no tiene acceso a Internet, puede pausar la instalación en este momento y descargar los instaladores por separado tal y como se describe aquí: [Instalación de componentes de R sin acceso a Internet](../../advanced-analytics/r-services/installing-r-components-without-internet-access.md).  
  
     Haga clic en **Aceptar**, espere hasta que se active el botón **Siguiente** y, después, haga clic en **Siguiente**.  
  
5.  En la página **Listo para instalar**, compruebe que están incluidas estas selecciones y haga clic en **Instalar**.  
  
     **Características**  
  
     Servicios de Motor de base de datos  
  
     R Services (en bases de datos)  
  
6.  Cuando se complete la instalación, reinicie el equipo.   
  
  
##  <a name="a-namebkmkenablefeaturea-step-2-enable-r-services-and-verify-that-local-r-script-execution-works"></a><a name="bkmk_enableFeature"></a> Paso 2: habilitar R Services y comprobar que la ejecución del script de R local funciona  
  
  
1. Abra [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Si todavía no está instalado, puede volver a ejecutar el Asistente para la instalación de SQL Server para abrir un vínculo de descarga e instalarlo.  
  
2. Conéctese a la instancia donde instaló R Services (en bases de datos) y ejecute el comando siguiente para habilitar explícitamente la característica R Services. De lo contrario, no será posible invocar scripts de R aunque el programa de instalación haya instalado la característica.  
  
   ```    
   Exec sp_configure  'external scripts enabled', 1  
   Reconfigure  with override    
   ```  
  
10. Reinicie el servicio SQL Server para la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esto también reiniciará automáticamente el servicio relacionado de [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] . Puede reiniciar el servicio mediante el panel Servicios del Panel de control o mediante el Administrador de configuración de SQL Server.  
  
9. Una vez que el servicio SQL Server esté disponible, compruebe que la característica R está habilitada. Para ello, ejecute el comando siguiente y compruebe que *run_value* está establecido en 1:  
  
    ```    
    Exec sp_configure  'external scripts enabled'    
    ```  
   También puede abrir el panel **Servicios** y comprobar que el servicio Launchpad de su instancia se está ejecutando. Cada instancia tiene su propio servicio Launchpad.
   
10. Ahora debería poder ejecutar scripts de R sencillos parecidos al siguiente en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]:  
  
    ```  
    exec sp_execute_external_script  @language =N'R',  
    @script=N'OutputDataSet<-InputDataSet',    
    @input_data_1 =N'select 1 as hello'  
    with result sets (([hello] int not null));  
    go  
    ```  
  
    **Resultados**  
  
    *hello*  
    *1*   
  
> [!IMPORTANT]  Si necesita tener acceso a datos de SQL Server o ejecutar comandos de R desde un cliente de ciencia de datos remoto, debe llevar a cabo algunos pasos adicionales. En los pasos siguientes se describen en detalle estos requisitos adicionales.
 
  
##  <a name="a-namebkmkconfigureaccountsa-step-3-enable-implied-authentication-for-launchpad-accounts"></a><a name="bkmk_configureAccounts"></a> Paso 3: habilitar la autenticación implícita para cuentas de Launchpad  
   
  
Durante la instalación, se crean 20 cuentas de usuario de Windows para ejecutar tareas en el token de seguridad del servicio [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]. Cuando un usuario envía un script de R desde un cliente externo, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] activa una cuenta de trabajo disponible, la asigna a la identidad del usuario que realiza la llamada y ejecuta el script de R en nombre del usuario. Se trata de un nuevo servicio del motor de base de datos que admite la ejecución segura de scripts externos, denominada *autenticación implícita*. 

Puede ver estas cuentas en el grupo de usuarios de Windows **SQLRUserGroup**.  Si necesita ejecutar scripts de R desde un cliente de ciencia de datos remoto y usa la autenticación de Windows, es necesario conceder permiso a estas cuentas de trabajo para iniciar sesión en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en su nombre.  
  
1. En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], en el Explorador de objetos, expanda **Seguridad**, haga clic con el botón derecho en **Inicios de sesión** y seleccione **Nuevo inicio de sesión**.  
2. En el cuadro de diálogo **Inicio de sesión - Nuevo**, haga clic en **Buscar**.  
3. Haga clic en **Tipos de objeto** y seleccione **Grupos**. Anule la selección de todo lo demás.  
4. En Escriba el nombre del objeto que desea seleccionar, escriba *SQLRUserGroup* y haga clic en **Comprobar nombres**.  
5. El nombre del grupo local asociado al servicio Launchpad de la instancia se debe resolver como algo parecido a *instancename\SQLRUserGroup*. Haga clic en **Aceptar**.  
6. De forma predeterminada, el inicio de sesión se asigna al rol **público** y tiene permiso para conectarse al motor de base de datos. 
7. Haga clic en **Aceptar**.  
  
> [!NOTE] Si usa un inicio de sesión de SQL para ejecutar scripts de R en un contexto de proceso de SQL Server, no es necesario llevar a cabo este paso adicional.
  
  
## <a name="step-4-give-non-admin-users-r-script-permissions"></a>Paso 4: conceder permisos para ejecutar scripts de R a los usuarios que no son administradores  
  
Si ha instalado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usted mismo y ejecuta scripts de R en su propia instancia, normalmente ejecutará los scripts como administrador y, por lo tanto, tendrá permiso implícito en varias operaciones y en todos los datos de la base de datos. Además, podrá instalar paquetes de R nuevos cuando sea necesario.  
  
Pero en un escenario empresarial, la mayoría de los usuarios, incluidos los que obtienen acceso a la base de datos mediante inicios de sesión de SQL, no tienen estos permisos elevados. Por lo tanto, a cada usuario que vaya a ejecutar scripts externos, debe concederle permisos para ejecutar scripts de R en cada base de datos en la que se usará R.   
  
  
```  
USE <database_name>  
GO  
GRANT EXECUTE ANY EXTERNAL SCRIPT  TO [UserName]  
```  

> [!TIP] ¿Necesita ayuda con la instalación? ¿No está seguro de haber ejecutado todos los pasos?
>
> Use estos informes personalizados para comprobar el estado de instalación de R Services. Para obtener más información, consulte [Supervisar R Services con informes personalizados](../../advanced-analytics/r-services/monitor-r-services-using-custom-reports-in-management-studio.md).    
  
##  <a name="a-namebkmkadditionala-optional-modifications"></a><a name="bkmk_Additional"></a> Modificaciones opcionales  
  
En esta sección se describen los cambios adicionales que puede realizar en la configuración de la instancia o del cliente de ciencia de datos para que admita la ejecución de scripts de R.
  
### <a name="modify-the-number-of-worker-accounts-used-by-includersqllaunchpadtokenrsqllaunchpadmdmd"></a>Modificar el número de cuentas de trabajo que usa [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]
  
Si cree que va a hacer un uso intensivo de R, o si prevé que muchos usuarios van a ejecutar scripts al mismo tiempo, puede aumentar el número de cuentas de trabajo que están asignadas al servicio Launchpad. Para obtener más información, consulte [Modify the User Account Pool for SQL Server R Services](../../advanced-analytics/r-services/modify-the-user-account-pool-for-sql-server-r-services.md).  
  
  
### <a name="give-your-r-users-or-logins-read-write-or-ddl-permissions-as-needed-in-additional-databases"></a>Asignar a los inicios de sesión o los usuarios de R permisos de lectura, escritura o DDL según sea necesario en las bases de datos adicionales  
  
Mientras ejecuta scripts de R, la cuenta de usuario podría tener que leer datos de otras bases de datos, crear tablas para almacenar resultados y escribir datos en tablas. 
     
Para cada usuario que vaya a ejecutar scripts de R, asegúrese de que la cuenta de usuario tenga permisos **db_datareader**, **db_datawriter** o **db_ddladmin** en la base de datos específica.   
       
Por ejemplo, la siguiente instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] concede al inicio de sesión de SQL *MySQLLogin* los derechos necesarios para ejecutar consultas de T-SQL en la base de datos *RSamples*. Para ejecutar esta instrucción, el inicio de sesión de SQL debe existir en el contexto de seguridad del servidor.  
  
```  
USE RSamples  
GO  
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'  
```  
  
Para obtener más información sobre los permisos incluidos en cada rol, consulte [Roles de nivel de base de datos](../../relational-databases/security/authentication-access/database-level-roles.md).  
  
  
### <a name="create-an-odbc-data-source-for-the-instance-on-your-data-science-client"></a>Crear un origen de datos de ODBC para la instancia en el cliente de ciencia de datos  
  
Si crea una solución de R en un equipo cliente de ciencia de datos y necesita conectarse al equipo con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como contexto de proceso, puede usar un inicio de sesión de SQL o la autenticación integrada de Windows.  
  
Si usa un inicio de sesión de SQL, asegúrese de que el inicio de sesión tenga los permisos adecuados en la base de datos donde se leerán los datos. Para hacerlo, agregue permisos *Connect to* y *SELECT*, o bien agregue el inicio de sesión al rol **db_datareader**. Si necesita crear objetos, deberá tener derechos **DDL_admin**.  Para guardar datos en tablas, agregue el inicio de sesión al rol **db_datawriter**.  
  
Si usa la autenticación de Windows, debe configurar un origen de datos de ODBC en el cliente de ciencia de datos que especifica ese nombre de instancia y otra información de conexión.  
  
Para obtener más información, consulte [Usar el Administrador de orígenes de datos ODBC](http://windows.microsoft.com/windows/using-odbc-data-source-administrator).  
  
### <a name="optimize-the-server-for-r"></a>Optimizar el servidor para R  

La configuración predeterminada del programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está diseñada para optimizar el equilibrio del servidor para diversos servicios que admite el motor de base de datos, entre ellos procesos ETL, creación de informes, auditoría y aplicaciones que usan datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por lo tanto, en la configuración predeterminada podría ver que los recursos para operaciones de R están restringidos, especialmente en operaciones que usan mucha memoria.  
  
 Para asegurarse de que se asignen a las tareas de R la prioridad y los recursos correctos, se recomienda usar el regulador de recursos para configurar un grupo de recursos externos específico para el funcionamiento de R. Puede que también le interese cambiar la cantidad de memoria asignada al motor de base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o aumentar el número de cuentas que se ejecutan en el servicio [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)].  
  
-   Configurar un grupo de recursos para administrar recursos externos  
  
     [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)  
  
-   Cambiar la cantidad de memoria reservada para el motor de base de datos  
  
     [Opciones de configuración de memoria del servidor](../../database-engine/configure-windows/server-memory-server-configuration-options.md)  
  
-   Cambiar el número de cuentas de R que puede iniciar [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]  
  
     [Modificar el grupo de cuentas de usuario de SQL Server R Services](../../advanced-analytics/r-services/modify-the-user-account-pool-for-sql-server-r-services.md)  
  
### <a name="get-the-r-source-code-optional"></a>Obtener el código fuente de R (opcional)  

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] incluye una distribución de los paquetes base de R de código abierto.  
  
También puede hacer clic en uno de estos vínculos para empezar a descargar de inmediato el código fuente GPL/LGPL modificado. El código fuente se pone a disposición de todos los usuarios de acuerdo con la licencia pública general de GNU, pero no se requiere para instalar o usar [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)].  
  
-   Compatible con RC2: descargue el archivo [rre-gpl-src.8.0.2.tar.gz](http://go.microsoft.com/fwlink/?LinkId=786770) 
  
-   Compatible con RC3: descargue el archivo [rre-gpl-src.8.0.3.tar.gz](http://go.microsoft.com/fwlink/?LinkId=786771) 

-   Compatible con RTM: descargue el archivo [rre-gpl-src.8.0.3.tar.gz](http://go.microsoft.com/fwlink/?LinkID=786771)
  
## <a name="troubleshooting"></a>Solucionar problemas  
 ¿Le ha surgido algún problema? Consulte la lista de problemas habituales al instalar versiones preliminares de [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)].  
  
 [Preguntas más frecuentes sobre actualización e instalación &#40;SQL Server R Services&#41;](../../advanced-analytics/r-services/upgrade-and-installation-faq-sql-server-r-services.md)  
  
## <a name="see-also"></a>Vea también  
 [Configurar un cliente de ciencia de datos](../../advanced-analytics/r-services/set-up-a-data-science-client.md)   
 [Crear un R Server independiente](../../advanced-analytics/r-services/create-a-standalone-r-server.md)  
  
  