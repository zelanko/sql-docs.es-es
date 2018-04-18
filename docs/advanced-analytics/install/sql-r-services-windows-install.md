---
title: Instalar SQL Server 2016 R Services (In-Database) | Documentos de Microsoft
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 86263158581b92af42a7ad1ce9b538b2c1cdbfa7
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="install-sql-server-2016-r-services-in-database"></a>Instalar SQL Server 2016 R Services (en bases de datos) 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artículo explica cómo instalar y configurar **SQL Server 2016 R Services (In-Database)**. Si tiene SQL Server 2016, instale esta característica para habilitar la ejecución del código de R en SQL Server.

## <a name="bkmk_prereqs"> </a> Lista de comprobación previa a la instalación

+ El programa de instalación de SQL Server 2016 es necesaria si desea instalar R Services. Si en su lugar tiene los medios de instalación de SQL Server 2017, debe instalar [Machine Learning Services (In-Database) de SQL Server de 2017](sql-machine-learning-services-windows-install.md) para obtener la integración de R para esa versión de SQL Server.

+ Se requiere una instancia del motor de base de datos. No se puede instalar solo R, a pesar de que puede agregar de forma incremental a una instancia existente.

+ No instale Servicios de R en un clúster de conmutación por error. El mecanismo de seguridad utilizado para aislar los procesos de R no es compatible con un entorno de clúster de conmutación por error de Windows Server.

+ No instale Servicios de R en un controlador de dominio. Se producirá un error en la parte de servicios de R del programa de instalación.

+ No instale **características compartidas** > **R Server (independiente)** en el mismo equipo que ejecuta una instancia de base de datos. 

+ Instalación en paralelo con otras versiones de R y Python son posibles porque la instancia de SQL Server utiliza sus propias copias de las distribuciones de R y Anaconda de código abierto. Sin embargo, ejecutar código que usa R y Python en el equipo de SQL Server fuera de SQL Server puede producir varios problemas:
    
  + Usar una biblioteca diferente y un ejecutable diferente y obtener resultados diferentes, que se obtienen cuando se ejecuta en SQL Server.
  + Scripts de R y Python que se ejecutan en bibliotecas externas no se puede administrar por SQL Server, dando lugar a la contención de recursos.
  
Si utiliza cualquier versión anterior de paquetes RevoScaleR o el entorno de desarrollo de Revolution Analytics, o bien si instaló las versiones preliminares de SQL Server 2016, debe desinstalarlas. No se admite la ejecución de versiones anteriores y recientes de RevoScaleR y otros paquetes propietarios. Para quitar versiones anteriores, consulte [actualización y p+f sobre la instalación de servicios de aprendizaje de máquina de SQL Server](../r/upgrade-and-installation-faq-sql-server-r-services.md).

> [!IMPORTANT]
> Una vez completada la instalación, asegúrese de completar los pasos adicionales de configuración posterior a la descrita en este artículo. Estos pasos incluyen la habilitación de SQL Server puede utilizar scripts externos y agregar cuentas necesarias para que SQL Server ejecutar trabajos de R en su nombre. Cambios de configuración suele ser necesitan un reinicio de la instancia o un reinicio del servicio Launchpad.

## <a name="get-the-installation-media"></a>Obtener los medios de instalación

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

 ###  <a name="bkmk_ga_instalpatch"></a> Requisito de instalación de revisión 

Microsoft ha identificado un problema con la versión concreta de los archivos binarios en tiempo de ejecución de Microsoft VC++ 2013 que instala como requisito previo SQL Server. Si esta actualización de los archivos binarios en tiempo de ejecución de VC++ no se instala, puede que SQL Server experimente problemas de estabilidad en determinados escenarios. Antes de instalar SQL Server, siga las instrucciones de [Notas de la versión de SQL Server](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch) para ver si el equipo necesita una revisión para los archivos binarios en tiempo de ejecución de VC.  

## <a name="bkmk2016top"></a>Ejecute el programa de instalación

En instalaciones locales, debe ejecutar el programa de instalación como administrador. Si instala [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde un recurso compartido remoto, deberá usar una cuenta de dominio que tenga permisos de lectura y ejecución para dicho recurso.

1. Inicie al Asistente para la instalación de SQL Server 2016.

2. En el **instalación** ficha, seleccione **instalación independiente del nuevo servidor SQL Server o agregar características a una instalación existente**.
    
   ![Instalar R Services (In-Database)](media/2016-setup-installation-rsvcs.png "Iniciar instalación del motor de base de datos con R Services")
   
3. En el **selección de características** página, seleccione las opciones siguientes:

   - Seleccione **servicios del motor de base de datos**. Se requiere el motor de base de datos en cada instancia que usa el aprendizaje automático.
   - Seleccione **R Services (en bases de datos)**. Instala compatibilidad para su uso en bases de datos de R.
    
     ![Selección de características de servicios de R](media/2016setup-rsvcs-features.png "seleccione estas características para R Services en bases de datos")

    > [!IMPORTANT]
    > No instale Servicios de R y R Server al mismo tiempo. Por lo general, debería instalar a R Server (independiente) para crear un entorno que utiliza un científico de datos o un desarrollador para conectarse a SQL Server e implementar soluciones de R. Por lo tanto, no es necesario instalar ambos en el mismo equipo.

4.  En el **dar su consentimiento para instalar Microsoft R Open** página, haga clic en **Accept**.
  
    Este contrato de licencia se requiere para descargar Microsoft R Open, que incluye una distribución de los paquetes de base de código abierto R y herramientas, junto con los paquetes de R mejorados y proveedores de conectividad desde el equipo de desarrollo de Microsoft R.
  
5. Después de que ha aceptado el contrato de licencia, no hay una breve pausa mientras el programa de instalación se prepara. Haga clic en **siguiente** cuando el botón esté disponible.

6. En el **preparado para instalar** , comprueba que se incluyen los siguientes elementos y, a continuación, seleccionan **instalar**.

   + Servicios de Motor de base de datos
   + R Services (en bases de datos)

    Tenga en cuenta la ubicación de la carpeta en la ruta de acceso `..\Setup Bootstrap\Log` donde se almacenan los archivos de configuración. Cuando finalice la instalación, puede revisar los componentes instalados en el archivo de resumen.

7. Una vez completada la instalación, reinicie el equipo.

##  <a name="bkmk_enableFeature"></a>Habilitar la ejecución de scripts externos

1. Abra [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. 

    > [!TIP]
    > Puede descargar e instalar la versión adecuada de esta página: [descargar SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).
    > 
    > También puede probar la versión preliminar de [Studio de operaciones SQL](https://docs.microsoft.com/sql/sql-operations-studio/what-is), que es compatible con las tareas administrativas y las consultas en SQL Server.
  
2. Conectarse a la instancia donde haya instalado servicios de aprendizaje de máquina, haga clic en **nueva consulta** para abrir una ventana de consulta y ejecute el siguiente comando:

   ```SQL
   sp_configure
   ```
    El valor de la propiedad, `external scripts enabled`, debería ser **0** en este momento. Esto ocurre porque la característica está desactivada de forma predeterminada. La característica debe habilitarse explícitamente por un administrador para poder ejecutar scripts de R o Python.
     
3. Para habilitar la característica de scripting externo, ejecute la siguiente instrucción:
  
    ```SQL
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
  
## <a name="restart-the-service"></a>Reinicie el servicio.

Una vez completada la instalación, reinicie el motor de base de datos antes de continuar con la siguiente, habilitar la ejecución del script.

Al reiniciar el ombre también automáticamente reinician relacionado [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] servicio.

Puede reiniciar el servicio mediante el menú contextual **reiniciar** comando para la instancia de SSMS o mediante el **servicios** en el Panel de Control, o mediante el panel [Administrador de configuración de SQL Server ](../../relational-databases/sql-server-configuration-manager.md).

## <a name="verify-installation"></a>Comprobar la instalación

Use los pasos siguientes para comprobar que se están ejecutando todos los componentes utilizados para iniciar scripts externos.

1. En SQL Server Management Studio, abra una nueva ventana de consulta y ejecute el siguiente comando:
    
    ```SQL
    EXEC sp_configure  'external scripts enabled'
    ```

    **run_value** debería estar establecido ahora en 1.

2. Abra la **servicios** panel o administrador de configuración de SQL Server y compruebe **servicio SQL Server Launchpad** está ejecutando. Debe tener un servicio para cada instancia de motor de base de datos que tenga R o Python instalado. Si no se está ejecutando, reinicie el servicio. Para obtener más información, consulte [componentes para la integración de Python](../python/new-components-in-sql-server-to-support-python-integration.md).

7. Si está ejecutando Launchpad, debe ser capaz de ejecutar R simple para comprobar que los tiempos de ejecución de secuencias de comandos externos pueden comunicarse con SQL Server. 

    Abra una nueva **consulta** ventana en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], y, a continuación, ejecute una secuencia de comandos como la siguiente:
    
    ```SQL
    EXEC sp_execute_external_script  @language =N'R',
    @script=N'
    OutputDataSet <- InputDataSet;
    ',
    @input_data_1 =N'SELECT 1 AS hello'
    WITH RESULT SETS (([hello] int not null));
    GO
    ```

    La secuencia de comandos puede tardar un poco para que se ejecute, la primera vez que se carga en tiempo de ejecución de script externo. Los resultados deben ser algo parecido a esto:

    | hello |
    |----|
    | 1|

## <a name="bkmk_FollowUp"></a> Configuración adicional

Si el paso de comprobación de script externo fue correcto, puede ejecutar comandos de Python desde SQL Server Management Studio, código de Visual Studio o cualquier otro cliente que puede enviar instrucciones T-SQL en el servidor.

Si recibe un error al ejecutar el comando, revise los pasos de configuración adicionales en esta sección. Debe realizar configuraciones adecuadas adicionales en el servicio o la base de datos.

Entre los escenarios comunes que requieren cambios adicionales se incluyen:

* [Configurar firewall de Windows para las conexiones de entrada](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)
* [Habilitar otros protocolos de red](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)
* [Habilitar las conexiones remotas](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md)
* [Ampliar los permisos integrados a los usuarios remotos](#bkmk_configureAccounts)
* [Conceder permiso para ejecutar scripts externos](#bkmk_AllowLogon)
* [Conceder acceso a bases de datos individuales](#permissions-db)

> [!NOTE]
> No todos los cambios mostrados son necesarios y ninguno puede ser necesario. Requisitos dependen de un esquema de seguridad, que se instaló SQL Server y cómo esperar a los usuarios conectarse a la base de datos y ejecutar scripts externos. Sugerencias de solución de problemas adicionales se pueden encontrar aquí: [preguntas más frecuentes de actualización e instalación](../r/upgrade-and-installation-faq-sql-server-r-services.md)

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

Si instaló [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en su propia instancia, normalmente se ejecutan las secuencias de comandos como administrador, o al menos como un propietario de la base de datos, y, por tanto, tienen permisos implícitos para diversas operaciones, todos los datos en la base de datos y la capacidad para instalar nuevos paquetes según sea necesario.

Sin embargo, en un escenario empresarial, la mayoría de los usuarios, incluidos los usuarios que tienen acceso a la base de datos mediante el uso de los inicios de sesión SQL, no tiene estos permisos elevados. Por lo tanto, para cada usuario que vaya a ejecutar scripts de R, debe conceder al usuario permisos para ejecutar scripts en cada base de datos que se usarán los scripts externos.

```SQL
USE <database_name>
GO
GRANT EXECUTE ANY EXTERNAL SCRIPT  TO [UserName]
```

> [!TIP]
> ¿Necesita ayuda con la instalación? ¿No está seguro de haber ejecutado todos los pasos? Usar estos informes personalizados para comprobar el estado de la instalación y ejecutar pasos adicionales. 
> 
> [Supervisar servicios de aprendizaje de máquina con informes personalizados](../r/monitor-r-services-using-custom-reports-in-management-studio.md).

### <a name="permissions-db"></a> Proporcionar a los usuarios de lectura, escritura o permisos de DDL para la base de datos

La cuenta de usuario que se usa para ejecutar R podría necesario para leer datos de otras bases de datos, crear nuevas tablas para almacenar los resultados y escribir datos en tablas. Por lo tanto, para cada usuario que se van a ejecutar scripts de R, asegúrese de que el usuario tiene los permisos adecuados en la base de datos: *db_datareader*, *db_datawriter*, o *db_ddladmin*.

Por ejemplo, la siguiente instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] concede al inicio de sesión de SQL *MySQLLogin* los derechos necesarios para ejecutar consultas de T-SQL en la base de datos *RSamples* . Para ejecutar esta instrucción, el inicio de sesión de SQL debe existir en el contexto de seguridad del servidor.

```SQL
USE RSamples
GO
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'
```

Para obtener más información acerca de los permisos que se incluyen en cada rol, consulte [roles de nivel de base de datos](../../relational-databases/security/authentication-access/database-level-roles.md).


### <a name="create-an-odbc-data-source-for-the-instance-on-your-data-science-client"></a>Crear un origen de datos de ODBC para la instancia en el cliente de ciencia de datos

Si crea una solución en R en un equipo cliente de ciencia de datos y que necesite ejecutar código con el equipo de SQL Server como el contexto de proceso, puede utilizar un inicio de sesión SQL o la autenticación integrada de Windows.

* En caso de usar un inicio de sesión de SQL: asegúrese de que el inicio de sesión tenga los permisos adecuados en la base de datos donde se van a leer los datos. Puede hacerlo agregando *conectarse a* y *seleccione* permisos, o agregando el inicio de sesión para la *db_datareader* rol. Para los inicios de sesión que necesitan para crear objetos, agregue *funciones DDL_admin* derechos. Para los inicios de sesión que deben guardar los datos en tablas, agregue el inicio de sesión para la *db_datawriter* rol.

* Para la autenticación de Windows: tendrá que configurar un origen de datos ODBC en el cliente de ciencia de datos que especifica el nombre de instancia y otra información de conexión. Para obtener más información, consulte [Administrador de orígenes de datos ODBC](https://docs.microsoft.com/sql/odbc/admin/odbc-data-source-administrator).

## <a name="suggested-optimizations"></a>Optimizaciones sugeridas

Ahora que tiene todo en funcionamiento, que le interese optimizar el servidor para admitir el aprendizaje automático o instalar previamente entrenada modelos.

### <a name="add-more-worker-accounts"></a>Agregue más cuentas de trabajo

Si cree que podría usar R mucho, o si se espera que muchos usuarios pueden ejecutar scripts al mismo tiempo, puede aumentar el número de cuentas de trabajo que están asignadas al servicio Launchpad. Para obtener más información, consulte [modificar el grupo de cuentas de usuario para servicios de aprendizaje de máquina de SQL Server](../r/modify-the-user-account-pool-for-sql-server-r-services.md).

### <a name="bkmk_optimize"></a>Optimizar el servidor para la ejecución de scripts externos

La configuración predeterminada para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el programa de instalación están diseñados para optimizar el equilibrio del servidor para una variedad de servicios que son compatibles con el motor de base de datos, lo que puede incluir de extracción, transformación y carga (ETL) de procesos, creación de informes, auditoría, y las aplicaciones que utilizan [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] datos. Por lo tanto, la configuración predeterminada, es posible que los recursos para el aprendizaje automático a veces se restringido o limitados, especialmente en operaciones con uso intensivo de memoria.

Para garantizar que los trabajos de aprendizaje de máquina están ordenados y asignaron correctamente, se recomienda que use el regulador de recursos de SQL Server para configurar un grupo de recursos externos. También puede cambiar la cantidad de memoria que se asigna a la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] motor de base de datos o aumentar el número de cuentas que se ejecutan en el [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] service.

- Para configurar un grupo de recursos para administrar recursos externos, consulte [crear un grupo de recursos externo](../../t-sql/statements/create-external-resource-pool-transact-sql.md).
  
- Para cambiar la cantidad de memoria reservada para la base de datos, vea [opciones de configuración de memoria de servidor](../../database-engine/configure-windows/server-memory-server-configuration-options.md).
  
- Para cambiar el número de cuentas de R que se puede iniciar por [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], consulte [modificar el grupo de cuentas de usuario para el aprendizaje automático](../r/modify-the-user-account-pool-for-sql-server-r-services.md).

Si está usando Standard Edition y no tiene el regulador de recursos, puede usar vistas de administración dinámica (DMV) y eventos extendidos, así como eventos de Windows de supervisión, para ayudar a administrar los recursos del servidor que usan R. Para obtener más información, consulte [supervisión y administración de servicios de R](../r/managing-and-monitoring-r-solutions.md).

### <a name="install-additional-r-packages"></a>Instalar paquetes de R adicionales

Las soluciones de R que se crean para SQL Server pueden llamar a funciones básicas de R, las funciones de la packes properietary instalado con SQL Server y paquetes de R de terceros compatibles con la versión de R de código abierto instalado por SQL Server.

Los paquetes que quiera usar de SQL Server deben estar instalados en la biblioteca predeterminada que la instancia usa. Si tiene una instalación independiente de R en el equipo, o si ha instalado los paquetes a las bibliotecas de usuario, no podrá usar esos paquetes de T-SQL.

El proceso para instalar y administrar paquetes de R es diferente de SQL Server 2016 y 2017 de SQL Server. En SQL Server 2016, un administrador de base de datos debe instalar paquetes de R que necesitan los usuarios. En SQL Server 2017, puede configurar grupos de usuarios para compartir los paquetes en un nivel de cada base de datos o configurar los roles de base de datos para permitir a los usuarios instalar sus propios paquetes. Para obtener más información, consulte [administración del paquete](../r/r-package-management-for-sql-server-r-services.md).


## <a name="get-help"></a>Obtener ayuda

¿Necesita ayuda con la instalación o actualización? Para obtener respuestas a preguntas comunes y los problemas conocidos, vea el artículo siguiente:

* [Actualización e instalación preguntas más frecuentes: servicios de aprendizaje de máquina](../r/upgrade-and-installation-faq-sql-server-r-services.md)

Para comprobar el estado de instalación de la instancia y solucionar problemas comunes, pruebe estos informes personalizados.

* [Informes personalizados para SQL Server R Services](../r/monitor-r-services-using-custom-reports-in-management-studio.md)

## <a name="next-steps"></a>Pasos siguientes

Los desarrolladores de R pueden empezar a trabajar con algunos ejemplos sencillos y conozca los aspectos básicos del funcionamiento de R con SQL Server. Para el siguiente paso, vea los siguientes vínculos:

+ [Tutorial: Ejecutar R en T-SQL](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [Tutorial: Análisis de en bases de datos para los desarrolladores de R](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Para ver ejemplos de aprendizaje automático que se basan en situaciones del mundo real, vea [máquina tutoriales de aprendizaje](../tutorials/machine-learning-services-tutorials.md).


