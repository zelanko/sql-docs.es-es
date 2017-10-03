---
title: "Configurar servicios de aprendizaje de máquina de SQL Server (In-Database) | Documentos de Microsoft"
ms.custom: 
ms.date: 09/28/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
keywords:
- "instalación de SQL Server R Services"
ms.assetid: 4d773c74-c779-4fc2-b1b6-ec4b4990950d
caps.latest.revision: 36
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: e76675099ab290d29231d434eb74e92b613185b7
ms.openlocfilehash: 9b3449e8c1f19ee69b36107f3530eac80fae0227
ms.contentlocale: es-es
ms.lasthandoff: 09/29/2017

---
# <a name="set-up-sql-server-machine-learning-services-in-database"></a>Configurar servicios de aprendizaje de máquina de SQL Server (In-Database)

Este tema describe cómo configurar los servicios de aprendizaje de máquina en SQL Server mediante el uso de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Asistente para la instalación.

**Se aplica a:** (solo para R), SQL Server de 2017 Machine Learning Services (R y Python) de servicios de SQL Server 2016 R

## <a name="machine-learning-options-in-sql-server-setup"></a>Opciones de instalación de SQL Server de aprendizaje automático

El programa de instalación de SQL Server proporciona las siguientes opciones para la instalación de aprendizaje automático:

* Instale el aprendizaje automático con la base de datos de SQL Server

  Esta opción le permite ejecutar scripts de R o Python mediante un procedimiento almacenado. También puede usar el equipo de SQL Server como un contexto de proceso remoto para los scripts de R o Python que se ejecutan desde una conexión externa.

  Para instalar esta opción:
  
  * En SQL Server 2016, seleccione **R Services (In-Database)**.
  * En SQL Server 2017, seleccione **Machine Learning Services (In-Database)**.


* Instalar a un servidor independiente de aprendizaje de máquina

  Esta opción crea un entorno de desarrollo de soluciones que no requiere ni usar SQL Server de aprendizaje automático. Por lo tanto, generalmente recomendamos que instale esta opción en un equipo diferente que el servidor de hospedaje de SQL uno. Para obtener más información acerca de esta opción, vea [crear un Standalone R Server](../r/create-a-standalone-r-server.md).

El proceso de instalación requiere varios pasos, algunos de los cuales son opcionales. Los aspectos opcionales dependen de ambos cómo planea usar aprendizaje automático y el estado de su entorno de seguridad. 

## <a name="bkmk_prereqs"></a> Requisitos previos

*  Evitar la instalación de servidor de R y R Services al mismo tiempo. Por lo general, debería instalar a R Server (independiente) para crear un entorno que utiliza un científico de datos o un desarrollador para conectarse a SQL Server e implementar soluciones de R. Por lo tanto, no es necesario instalar ambos en el mismo equipo.

* Si utiliza cualquier versión anterior de paquetes RevoScaleR o el entorno de desarrollo de Revolution Analytics, o bien si instaló las versiones preliminares de SQL Server 2016, debe desinstalarlas. No se admite la instalación en paralelo. Para quitar versiones anteriores, consulte [actualización y p+f sobre la instalación de SQL Server R Services](../r/upgrade-and-installation-faq-sql-server-r-services.md).

* No puede instalar servicios de aprendizaje de máquina en un clúster de conmutación por error. El motivo es que el mecanismo de seguridad que se utiliza para aislar los procesos de script externo no es compatible con un entorno de clúster de conmutación por error de Windows Server. Como alternativa, puede realizar una de las siguientes acciones:
    * Utilice la replicación para copiar tablas necesarias en una instancia de SQL Server independiente con R Services.
    * Instalar [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] en un equipo independiente que usa AlwaysOn y forma parte de un grupo de disponibilidad.

> [!IMPORTANT]
> Una vez completada la instalación, son necesarios algunos pasos adicionales para habilitar la característica de aprendizaje automático. Podría también necesita conceder permisos a los usuarios a bases de datos específicas, cambiar o configurar las cuentas o configurar un cliente de ciencia de datos remotos.

##  <a name="bkmk_installExt"></a>Paso 1: Instalar las características de extensibilidad y elija un lenguaje de aprendizaje automático

Para usar el aprendizaje automático, debe instalar a SQL Server 2016 o posterior. Para usar [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], se requiere al menos una instancia del motor de base de datos. Puede usar una instancia con nombre o una instancia predeterminada.

1. Ejecute el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .
  
    Para obtener información acerca de cómo realizar instalaciones desatendidas, consulte [desatendido la instalación de SQL Server R Services](../r/unattended-installs-of-sql-server-r-services.md).
  
2. En el **instalación** ficha, seleccione **instalación independiente del nuevo servidor SQL Server o agregar características a una instalación existente**.
   
3. En el **selección de características** página, para instalar los servicios de base de datos utilizados por R trabajos e instala las extensiones que admiten scripts y procesos externos, seleccione las opciones siguientes:
   
   **SQL Server 2016**
   - Seleccione **servicios del motor de base de datos**.
   - Seleccione **R Services (en bases de datos)**.

   **SQL Server 2017**
   - Seleccione **servicios del motor de base de datos**.
   - Seleccione **(en bases de datos) de servicios de aprendizaje automático**.
   - Seleccione al menos un idioma para habilitar de aprendizaje de automático. Puede seleccionar solo R, o puede agregar R y Python.
   
   > [!NOTE]
   > Si no selecciona la R o Python la opción de idioma, el Asistente para instalación instala solo el marco de extensibilidad, que incluye el Launchpad de confianza de SQL Server, pero no instala los componentes específicos del idioma. Esta opción es para enlazar la instancia de SQL Server a R o Python como parte de la directiva de ciclo de vida moderna de Microsoft. Para obtener más información, consulte [SqlBindR de uso para actualizar una instancia de servicios de R](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

4.  En el **dar su consentimiento para instalar Microsoft R Open** página, seleccione **Accept**.
  
     Este contrato de licencia se requiere para descargar Microsoft R Open, que incluye una distribución de los paquetes de base de código abierto R y herramientas, junto con los paquetes de R mejorados y proveedores de conectividad desde el equipo de desarrollo de Microsoft R.
  
    > [!NOTE]
    >  Si el equipo que está utilizando no tiene acceso a internet, puede pausar el programa de instalación en este momento para descargar los instaladores por separado, tal como se describe en [componentes instalar R sin acceso a internet](installing-ml-components-without-internet-access.md).
  
5. Seleccione **Siguiente**.

6. En el **preparado para instalar** , comprueba que se incluyen los siguientes elementos y, a continuación, seleccionan **instalar**.

   **SQL Server 2017**
   - Servicios de Motor de base de datos
   - Machine Learning Services (en base de datos)
   - R, Python o ambos

   **SQL Server 2016**
   - Servicios de Motor de base de datos
   - R Services (en bases de datos)

7. Una vez completada la instalación, reinicie el equipo.

##  <a name="bkmk_enableFeature"></a>Paso 2: Habilitar los servicios de script externo

1. Abra [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Si todavía no está instalado, puede volver a ejecutar el Asistente para la instalación de SQL Server para abrir un vínculo de descarga e instalarlo.
  
2. Conéctese a la instancia donde instaló el aprendizaje automático y, a continuación, ejecute el siguiente comando:

   ```SQL
   sp_configure
   ```

    El valor de la **scripts externos habilitados** propiedad debería estar ahora **0**. Eso es porque la característica está desactivada de forma predeterminada para reducir el área expuesta y debe habilitarse explícitamente por un administrador.
     
3. Para habilitar la característica de scripting externo, ejecute la siguiente instrucción:
  
    ```SQL
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
  
4. Reinicie el servicio SQL Server para la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Al reiniciar el servicio SQL Server también automáticamente reinician relacionado [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] servicio.

    Puede reiniciar el servicio mediante el uso de la **servicios** panel en el Panel de Control o mediante el Administrador de configuración de SQL Server.

## <a name="bkmk_TestScript"></a>Paso 3: Comprobar que la ejecución del script funciona localmente

Compruebe que está habilitado el servicio de ejecución de script externo.

1. En SQL Server Management Studio, abra una nueva **consulta** ventana y vuelva a ejecutar el comando siguiente:
  
    ```SQL
    EXEC sp_configure  'external scripts enabled'
    ```
    **run_value** debería estar establecido ahora en 1.
    
2. Abra la **servicios** panel y compruebe que está ejecutando el servicio Launchpad para la instancia. Si instala varias instancias, cada una de ellas tendrá su propio servicio Launchpad.
   
3. Abra una nueva **consulta** ventana en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], y, a continuación, ejecute un script de R simple como el siguiente:
  
    ```SQL
    EXEC sp_execute_external_script  @language =N'R',
    @script=N'
    OutputDataSet <- InputDataSet;
    ',
    @input_data_1 =N'SELECT 1 AS hello'
    WITH RESULT SETS (([hello] int not null));
    GO
    ```
  
    **Resultado**
  
    *Hola* *1*
  
   Si el comando se ejecuta sin errores, vaya a los siguientes pasos. Si se produce un error, para obtener una lista de algunos problemas comunes, consulte [preguntas más frecuentes de actualización e instalación](../r/upgrade-and-installation-faq-sql-server-r-services.md).

## <a name="bkmk_FollowUp"></a>Paso 4: Configuración adicional

Según el caso de uso de R o Python, deberá realizar cambios adicionales en el servidor, el servidor de seguridad, las cuentas utilizadas por el servicio o los permisos de base de datos. Los cambios que debe realizar varían por mayúsculas o minúsculas.

Entre los escenarios comunes que requieren cambios adicionales se incluyen:

* Cambiar las reglas de firewall para permitir conexiones entrantes a SQL Server.
* Habilitar los protocolos de red adicionales.
* Asegurarse de que el servidor admite las conexiones remotas.
* Habilitar *autenticación implícita*, si los usuarios tener acceso a datos de SQL Server desde un terminal de desarrollo de R remoto y ejecutan código R mediante el paquete RODBC u otro proveedor de Microsoft Open Database Connectivity (ODBC).
* Conceder a los usuarios permisos para ejecutar un script de R o usar bases de datos.
* Solucionar problemas de seguridad que impiden la comunicación con el servicio Launchpad.
* Asegurarse de que los usuarios tienen permiso para ejecutar el código de R o instalar paquetes.

> [!NOTE]
> No todos los cambios de la lista pueden ser necesarios. Sin embargo, se recomienda que revise todos los elementos para ver si son aplicables a su escenario.

### <a name="bkmk_configureAccounts"></a>Habilitar la autenticación implícita para el grupo de cuentas de Launchpad

Durante la instalación, se crean algunas cuentas de usuario de Windows para ejecutar tareas en el token de seguridad de la [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] servicio. Cuando un usuario envía un script de R desde un cliente externo, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] activa una cuenta de trabajo disponible, lo asigna a la identidad del usuario que realiza la llamada y ejecuta el script de R en nombre del usuario. Este nuevo servicio del motor de base de datos admite la ejecución segura de scripts externos, denominado *autenticación implícita*.

Puede ver estas cuentas en el grupo de usuarios de Windows **SQLRUserGroup**. De forma predeterminada, se crean 20 cuentas de trabajo, que normalmente es más que suficiente para ejecutar código R trabajos.

Sin embargo, si necesita ejecutar scripts de R desde un cliente de ciencia de datos remotos y usa la autenticación de Windows, debe conceder estas cuentas de trabajo permiso para iniciar sesión en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia en su nombre.

1. En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], en el Explorador de objetos, expanda **Seguridad**, haga clic con el botón derecho en **Inicios de sesión**y seleccione **Nuevo inicio de sesión**.
2. En el **inicio de sesión - nuevo** cuadro de diálogo, seleccione **búsqueda**.
3. Seleccione el **tipos de objeto** y **grupos** casillas de verificación y desactive todas las demás casillas.
4. Haga clic en **avanzadas**, compruebe que la ubicación de búsqueda es el equipo actual y, a continuación, haga clic en **Buscar ahora**.
5. Desplácese por la lista de cuentas de grupo en el servidor hasta que encuentre una que comience con `SQLRUserGroup`.
    
    + El nombre del grupo que esté asociada con el servicio Launchpad para la _instancia predeterminada_ es siempre **SQLRUserGroup**. Seleccione esta cuenta solo para la instancia predeterminada.
    + Si usas un _con el nombre de instancia_, el nombre de instancia se anexa al nombre predeterminado, `SQLRUserGroup`. Por lo tanto, si la instancia se denomina "MLTEST", el nombre del grupo de usuario predeterminada para esta instancia sería **SQLRUserGroupMLTest**.
5. Haga clic en **Aceptar** para cerrar el cuadro de diálogo de búsqueda avanzada y compruebe que ha seleccionado la cuenta correcta para la instancia. Cada instancia puede usar solo su propio servicio de Launchpad y el grupo creado para ese servicio.
6. Haga clic en **Aceptar** otra vez para cerrar el **Seleccionar usuario o grupo** cuadro de diálogo.
7. En el **inicio de sesión - nuevo** cuadro de diálogo, haga clic en **Aceptar**. De forma predeterminada, el inicio de sesión se asigna al rol **público** y tiene permiso para conectarse al motor de base de datos.

### <a name="bkmk_AllowLogon"></a>Proporcionar a los usuarios permiso para ejecutar scripts externos

> [!NOTE]
> Si utiliza un inicio de sesión SQL para ejecutar scripts de R en un contexto de proceso de SQL Server, este paso no es necesario.

Si instaló [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y se ejecutan scripts de R en su propia instancia, normalmente se ejecutan las secuencias de comandos como administrador, o al menos como un propietario de la base de datos, y, por tanto, tienen permisos implícitos para diversas operaciones, todos los datos en la base de datos y la capacidad Para instalar nuevos paquetes de R como sea necesario.

Sin embargo, en un escenario empresarial, la mayoría de los usuarios, incluidos los usuarios que tienen acceso a la base de datos mediante el uso de los inicios de sesión SQL, no tiene estos permisos elevados. Por lo tanto, para cada usuario que vaya a ejecutar scripts de R o Python, debe conceder al usuario permisos para ejecutar scripts en cada base de datos que se usarán los scripts externos.

```SQL
USE <database_name>
GO
GRANT EXECUTE ANY EXTERNAL SCRIPT  TO [UserName]
```

> [!TIP]
> ¿Necesita ayuda con la instalación? ¿No está seguro de haber ejecutado todos los pasos? Use estos informes personalizados para comprobar el estado de instalación de R Services. Para obtener más información, consulte [Supervisar R Services con informes personalizados](monitor-r-services-using-custom-reports-in-management-studio.md).

### <a name="ensure-that-the-sql-server-computer-supports-remote-connections"></a>Asegúrese de que el equipo de SQL Server admite las conexiones remotas

Si no se puede conectar desde un equipo remoto, compruebe si el servidor permite conexiones remotas. Las conexiones remotas se deshabilitan a veces de forma predeterminada.

Compruebe también si el firewall permite el acceso a SQL Server. De forma predeterminada, el puerto utilizado por SQL Server a menudo está bloqueado por el firewall. Si se usa el Firewall de Windows, consulte [configurar Firewall de Windows para obtener acceso al motor de base de datos](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md).

### <a name="give-your-users-read-write-or-ddl-permissions-to-the-database"></a>Proporcionar a los usuarios de lectura, escritura o permisos de DDL para la base de datos

Mientras se está ejecutando scripts de R, la cuenta de usuario o inicio de sesión SQL podría necesario para leer datos de otras bases de datos, crear nuevas tablas para almacenar los resultados y escribir datos en tablas.

Para cada cuenta de usuario o inicio de sesión SQL que se van a ejecutar scripts de R, asegúrese de que la cuenta o inicio de sesión tiene los permisos adecuados en la base de datos: *db_datareader*, *db_datawriter*, o  *db_ddladmin*.

Por ejemplo, la siguiente instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] concede al inicio de sesión de SQL *MySQLLogin* los derechos necesarios para ejecutar consultas de T-SQL en la base de datos *RSamples* . Para ejecutar esta instrucción, el inicio de sesión de SQL debe existir en el contexto de seguridad del servidor.

```SQL
USE RSamples
GO
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'
```

Para obtener más información acerca de los permisos que se incluyen en cada rol, consulte [roles de nivel de base de datos](../../relational-databases/security/authentication-access/database-level-roles.md).

### <a name="use-machine-learning-in-an-azure-vm"></a>Usar aprendizaje automático en una máquina virtual de Azure

Si ha instalado servicios de aprendizaje de máquina (o R Services) en una máquina virtual de Azure, tendrá que cambiar algunos valores predeterminados adicionales. Para obtener más información, consulte [instalar aprendizaje de máquina de SQL Server en una máquina virtual de Azure](installing-sql-server-r-services-on-an-azure-virtual-machine.md).

### <a name="create-an-odbc-data-source-for-the-instance-on-your-data-science-client"></a>Crear un origen de datos de ODBC para la instancia en el cliente de ciencia de datos

Si crea una solución en R en un equipo cliente de ciencia de datos y que necesite ejecutar código con el equipo de SQL Server como el contexto de proceso, puede utilizar un inicio de sesión SQL o la autenticación integrada de Windows.

* En caso de usar un inicio de sesión de SQL: asegúrese de que el inicio de sesión tenga los permisos adecuados en la base de datos donde se van a leer los datos. Puede hacerlo agregando *conectarse a* y *seleccione* permisos, o agregando el inicio de sesión para la *db_datareader* rol. Para los inicios de sesión que necesitan para crear objetos, agregue *funciones DDL_admin* derechos. Para los inicios de sesión que deben guardar los datos en tablas, agregue el inicio de sesión para la *db_datawriter* rol.

* Para la autenticación de Windows: tendrá que configurar un origen de datos ODBC en el cliente de ciencia de datos que especifica el nombre de instancia y otra información de conexión. Para obtener más información, consulte [Administrador de orígenes de datos ODBC](https://docs.microsoft.com/sql/odbc/admin/odbc-data-source-administrator).

## <a name="next-steps"></a>Pasos siguientes

Después de comprobar que funciona la característica de ejecución del script en SQL Server, puede ejecutar comandos de R y Python desde SQL Server Management Studio, código de Visual Studio o cualquier otro cliente que puede enviar instrucciones T-SQL en el servidor.

Sin embargo, puede realizar algunos cambios en la configuración del sistema para admitir un uso intensivo de aprendizaje automático, o agregar nuevos paquetes de R.

Esta sección enumeran algunas modificaciones comunes que puede realizar para admitir el aprendizaje automático.

### <a name="add-more-worker-accounts"></a>Agregue más cuentas de trabajo

Si cree que podría usar R mucho, o si se espera que muchos usuarios pueden ejecutar scripts al mismo tiempo, puede aumentar el número de cuentas de trabajo que están asignadas al servicio Launchpad. Para obtener más información, consulte [modificar el grupo de cuentas de usuario de SQL Server R Services](modify-the-user-account-pool-for-sql-server-r-services.md).

### <a name="bkmk_optimize"></a>Optimizar el servidor para la ejecución de scripts externos

La configuración predeterminada para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el programa de instalación están diseñados para optimizar el equilibrio del servidor para una variedad de servicios que son compatibles con el motor de base de datos, lo que puede incluir de extracción, transformación y carga (ETL) de procesos, creación de informes, auditoría, y las aplicaciones que utilizan [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] datos. Por lo tanto, la configuración predeterminada, es posible que los recursos para el aprendizaje automático a veces se restringido o limitados, especialmente en operaciones con uso intensivo de memoria.

Para garantizar que los trabajos de aprendizaje de máquina están ordenados y asignaron correctamente, se recomienda que use el regulador de recursos de SQL Server para configurar un grupo de recursos externos. También puede cambiar la cantidad de memoria que se asigna a la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] motor de base de datos o aumentar el número de cuentas que se ejecutan en el [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] service.

- Para configurar un grupo de recursos para administrar recursos externos, consulte [crear un grupo de recursos externo](../../t-sql/statements/create-external-resource-pool-transact-sql.md).
  
- Para cambiar la cantidad de memoria reservada para la base de datos, vea [opciones de configuración de memoria de servidor](../../database-engine/configure-windows/server-memory-server-configuration-options.md).
  
- Para cambiar el número de cuentas de R que se puede iniciar por [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], consulte [modificar el grupo de cuentas de usuario para el aprendizaje automático](modify-the-user-account-pool-for-sql-server-r-services.md).

Si está usando Standard Edition y no tiene el regulador de recursos, puede usar vistas de administración dinámica (DMV) y eventos extendidos, así como eventos de Windows de supervisión, para ayudar a administrar los recursos del servidor que usan R. Para obtener más información, consulte [supervisión y administración de servicios de R](managing-and-monitoring-r-solutions.md).

### <a name="install-additional-r-packages"></a>Instalar paquetes de R adicionales

Dedique un minuto a instalar los paquetes de R adicionales que vamos a usar.

Los paquetes que quiera usar de SQL Server deben estar instalados en la biblioteca predeterminada que la instancia usa. Si tiene una instalación independiente de R en el equipo, o si ha instalado los paquetes a las bibliotecas de usuario, no podrá usar esos paquetes de T-SQL. Para obtener más información, consulte [instalar paquetes de R adicionales en SQL Server](../../advanced-analytics/r-services/install-additional-r-packages-on-sql-server.md).

También puede configurar grupos de usuarios para compartir los paquetes en un nivel de cada base de datos, o configurar los roles de base de datos para permitir a los usuarios instalar sus propios paquetes. Para obtener más información, consulte [administración del paquete](r-package-management-for-sql-server-r-services.md).

### <a name="upgrade-the-machine-learning-components"></a>Actualizar los componentes de aprendizaje automático

Al instalar servicios de R mediante SQL Server 2016, obtendrá la versión de los componentes de R que fue actualizada cuando se publicó la versión o service pack. Cada vez que aplicar la revisión o actualiza el servidor, los componentes de aprendizaje de máquina se actualizan también.

Sin embargo, puede actualizar los componentes de forma más rápida que se admite de aprendizaje automático en versiones de SQL Server, mediante la instalación de Microsoft R Server y la instancia de enlace. Cuando se actualiza, también obtendrá las siguientes características nuevas, que se admiten en las versiones recientes de Microsoft R Server:

* Nuevos paquetes de R, incluidos los [sqlrutils](https://docs.microsoft.com/r-server/r-reference/sqlrutils/sqlrutils), [olapR](https://docs.microsoft.com/r-server/r-reference/olapr/olapr), y [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package).
* [Previamente entrenada modelos](https://docs.microsoft.com/r-server/install/microsoftml-install-pretrained-models) para el análisis de clasificación y el texto de la imagen.

Para obtener información sobre cómo actualizar una instancia de SQL Server 2016, consulte [componentes de R actualizar a través del enlace](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

Si no está seguro de qué versión de R está asociado a la instancia, puede ejecutar un comando como el siguiente:

```SQL
EXEC sp_execute_external_script  @language =N'R',
@script=N'
myvar <- version$version.string
OutputDataSet <- as.data.frame(myvar);'
```

> [!NOTE]
> Las actualizaciones a través del proceso de enlace se admitirá para SQL Server 2017 así. Sin embargo, actualmente las actualizaciones solo son compatibles con instancias de SQL Server 2016.

### <a name="tutorials"></a>Tutoriales

Para empezar a trabajar con algunos ejemplos sencillos y conozca los aspectos básicos del funcionamiento de R con SQL Server, vea [código R de uso en Transact-SQL](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md).

Para ver ejemplos de aprendizaje automático que se basan en situaciones del mundo real, vea [máquina tutoriales de aprendizaje](../tutorials/machine-learning-services-tutorials.md).

### <a name="troubleshooting"></a>Solucionar problemas

¿Le ha surgido algún problema? ¿Intentando actualizar? Para obtener respuestas a preguntas comunes y los problemas conocidos, vea el artículo siguiente:

* [Actualización e instalación preguntas más frecuentes: servicios de aprendizaje de máquina](upgrade-and-installation-faq-sql-server-r-services.md)

Para comprobar el estado de instalación de la instancia y solucionar problemas comunes, pruebe estos informes personalizados.

* [Informes personalizados para SQL Server R Services](monitor-r-services-using-custom-reports-in-management-studio.md)

