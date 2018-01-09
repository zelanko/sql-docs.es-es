---
title: "Configurar servicios de aprendizaje de máquina de SQL Server (In-Database) | Documentos de Microsoft"
ms.custom: 
ms.date: 11/15/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
keywords:
- "instalación de SQL Server R Services"
- "instalar servicios de aprendizaje de máquina de SQL Server"
- Configurar los servicios de R
- "instalar el aprendizaje automático SQL"
ms.assetid: 4d773c74-c779-4fc2-b1b6-ec4b4990950d
caps.latest.revision: "36"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Active
ms.openlocfilehash: 04f2502853e21968f2edaac927247eb45730d000
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="set-up-sql-server-machine-learning-services-in-database"></a>Configurar servicios de aprendizaje de máquina de SQL Server (In-Database)

Este tema describe cómo instalar y configurar la siguiente máquina aprendizaje de las características que admiten los análisis de en bases de datos en SQL Server:

+ **SQL Server 2016 R Services (In-Database)**. Si tiene SQL Server 2016, instale esta característica para habilitar la ejecución del código de R en SQL Server. Requiere el motor de base de datos.

    [Configurar el aprendizaje automático en SQL Server 2016](#bkmk_2016top)

+ **Servicios de aprendizaje de máquina (en bases de datos) de SQL Server de 2017**. Si tiene SQL Server 2017, instale esta versión para ejecutar código R (o Python) en SQL Server. Requiere el motor de base de datos. 

    [Configurar el aprendizaje automático en SQL Server 2017](#bkmk_2017top)

+ Un servidor de aprendizaje de máquina con **sin** SQL Server

    [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]el programa de instalación también incluye la opción para instalar una versión "independiente" de los componentes de aprendizaje automático que no requieren el motor de base de datos y no se ejecutan en SQL Server.  Por lo general, le recomendamos que instale esta opción en un equipo diferente que el equipo que hospeda SQL Server.
    
    [Configurar un servidor de aprendizaje automático de independiente](create-a-standalone-r-server.md).

En este artículo se describe el proceso de instalación que utiliza la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Asistente para la instalación. Para la instalación de línea de comandos, o para descargar los instaladores para usar en servidores sin conexión, vea estos artículos:

+ [Instalar R para SQL Server desde la línea de comandos](unattended-installs-of-sql-server-r-services.md)
+ [Instalar Python para SQL Server desde la línea de comandos](../python/unattended-installs-of-sql-server-python-services.md)
+ [Instalar a un servidor de aprendizaje de máquina independiente desde la línea de comandos](install-microsoft-r-server-from-the-command-line.md)
+ [Instalar componentes de aprendizaje de máquina en un servidor con ninguna ACE de internet](installing-ml-components-without-internet-access.md)

**Se aplica a:** SQL Server 2016, SQL Server de 2017

## <a name="bkmk_prereqs"></a> Lista de comprobación de preinstalación

+ Máquina aprendizaje en bases de datos requiere que SQL Server 2016 o posterior. 

+ Idiomas admitidos: 

    + SQL Server 2016 solo admite R. 

    + R también está disponible como una característica de vista previa de la base de datos de SQL Azure, con algunas limitaciones. Para obtener más información, vea [usar R en la base de datos de SQL Azure](using-r-in-azure-sql-database.md)

    + Para utilizar Python requiere SQL Server 2017 o posterior.

+ Si utiliza cualquier versión anterior de paquetes RevoScaleR o el entorno de desarrollo de Revolution Analytics, o bien si instaló las versiones preliminares de SQL Server 2016, debe desinstalarlas. No se admite la instalación en paralelo. Para quitar versiones anteriores, consulte [actualización y p+f sobre la instalación de servicios de aprendizaje de máquina de SQL Server](../r/upgrade-and-installation-faq-sql-server-r-services.md).

+ No puede instalar SQL Server 2016 R Services o servicios de aprendizaje de SQL Server de 2017 máquinas en un controlador de dominio. Se producirá un error en la parte del programa de instalación R Services o servicios de aprendizaje de máquina.

+ No puede instalar el características en un clúster de conmutación por error de aprendizaje automático. El mecanismo de seguridad que se utiliza para aislar los procesos de script externo no es compatible con un entorno de clúster de conmutación por error de Windows Server. Como alternativa, puede realizar una de las siguientes acciones:
    * Utilice la replicación para copiar tablas necesarias en una instancia de SQL Server con aprendizaje automático habilitado.
    * Instale el aprendizaje automático en un equipo independiente que usa AlwaysOn y forma parte de un grupo de disponibilidad.

+ El marco de aprendizaje automático requiere configuración adicional después de que el programa de instalación se completa. Los pasos exactos dependen de su organización y las directivas de seguridad, configuración del servidor y el usuario. Se recomienda que revise todos los pasos y determinar la configuración adicional que podría ser necesario en su entorno.

## <a name="bkmk2016top"></a>Instalar SQL Server 2016 R Services (en bases de datos)

> [!div class="checklist"]
> * Instalar el motor de base de datos y características de aprendizaje automático
> * Requiere los pasos posteriores a la instalación: habilitar el aprendizaje automático y reiniciar
> * Pasos posteriores a la instalación opcionales: agregar reglas de firewall, agregar usuarios, cambiar o configurar las cuentas de servicio, configurar un cliente de ciencia de datos remotos

**Con el Asistente para la instalación de SQL Server 2016**

1. Ejecute el Asistente para la instalación de SQL Server.

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
  
    Si el equipo que está utilizando no tiene acceso a internet, puede pausar el programa de instalación en este momento para descargar los instaladores por separado, tal como se describe en [componentes instalar R sin acceso a internet](installing-ml-components-without-internet-access.md).
  
5. Después de que ha aceptado el contrato de licencia, no hay una breve pausa mientras el programa de instalación se prepara. Haga clic en **siguiente** cuando el botón esté disponible.

6. En el **preparado para instalar** , comprueba que se incluyen los siguientes elementos y, a continuación, seleccionan **instalar**.

   + Servicios de Motor de base de datos
   + R Services (en bases de datos)

7. Cuando una vez completada la instalación, reinicie el equipo.


## <a name="bkmk2017top"></a>Instalar servicios de aprendizaje automático SQL Server de 2017 (en bases de datos)

> [!div class="checklist"]
> * Instalar el motor de base de datos y características de aprendizaje automático
> * Requiere los pasos posteriores a la instalación: habilitar el aprendizaje automático y reiniciar
> * Pasos posteriores a la instalación opcionales: agregar reglas de firewall, agregar usuarios, cambiar o configurar las cuentas de servicio, configurar un cliente de ciencia de datos remotos.

**Introducción**

1. Ejecute el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .
  
2. En el **instalación** ficha, seleccione **instalación independiente del nuevo servidor SQL Server o agregar características a una instalación existente**.

     ![Instalar servicios de aprendizaje de máquina (In-Database)](media/2017setup-installation-page-mlsvcs.png "Iniciar instalación del motor de base de datos con servicios de aprendizaje de máquina")

3. En el **selección de características** página, seleccione las opciones siguientes:
   
    + Seleccione **servicios del motor de base de datos**. Se requiere el motor de base de datos en cada instancia que usa el aprendizaje automático.

    + Seleccione **(en bases de datos) de servicios de aprendizaje automático**. Esta opción instala la compatibilidad para su uso en bases de datos de R. Después de seleccionar esta opción, puede seleccionar el idioma de aprendizaje automático. Puede seleccionar solo R, o puede agregar R y Python.
   
    ![Selección de características de servicios de aprendizaje de máquina](media/2017setup-features-page-mls-rpy.png "seleccione estas características para R Services en bases de datos")

    Si no selecciona la R o Python la opción de idioma, el Asistente para instalación instala sólo el marco de extensibilidad, que incluye el Launchpad de confianza de SQL Server y no instala los componentes específicos del idioma.  Por lo general se recomienda que instale al menos un idioma que se inicie con. Sin embargo, puede usar esta opción si piensa utilizar inmediatamente el proceso de enlace para actualizar los componentes de aprendizaje automático. Para obtener más información, consulte [SqlBindR de uso para actualizar una instancia de servicios de R](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

    Se recomienda **no** instalar las características independientes y en bases de datos en el mismo equipo y nunca se instalan al mismo tiempo. Normalmente se instalan a Server de aprendizaje de máquina (independiente) para crear un entorno que utiliza un científico de datos o un desarrollador para conectarse a SQL Server al implementar soluciones. Por lo tanto, no es necesario instalar ambos en el mismo equipo.

4.  Contratos para el aprendizaje automático de licencia: dependiendo de los idiomas que se va a instalar, debe aceptar los contratos de licencia de R, Python o ambos.

    + Términos de licencia para este contrato de licencia R: cubre Microsoft R Open, que incluye una distribución de los paquetes de base de código abierto R y herramientas, junto con los paquetes de R mejorados y proveedores de conectividad desde el equipo de desarrollo de Microsoft.
  
    + Términos de licencia para Python. El contrato de licencia de código abierto de Python también cubre la Anaconda y herramientas relacionadas, además de algunas nuevas bibliotecas de Python desde el equipo de desarrollo de Microsoft.

    Haga clic en **Accept** para indicar su contrato. Hay una breve pausa mientras los componentes estén preparados, la **siguiente** botón esté disponible.

    Si el equipo que está utilizando no tiene acceso a internet, puede pausar el programa de instalación en este momento para descargar los instaladores por separado, como se describe aquí: [instalar componentes de aprendizaje de máquina sin acceso a internet](installing-ml-components-without-internet-access.md).

6. En el **preparado para instalar** , comprueba que se incluyen los siguientes elementos y, a continuación, seleccionan **instalar**.

   - Servicios de Motor de base de datos
   - Machine Learning Services (en base de datos)
   - R, Python o ambos

7. Una vez completada la instalación, tome nota de la ubicación del registro de instalación y, a continuación, reinicie el equipo.

###  <a name="bkmk_enableFeature"></a>Necesario después de la instalación

Por motivos de seguridad, la característica de aprendizaje de máquina no está habilitada de forma predeterminada incluso si ha instalado la característica. Un administrador del servidor debe habilitar la característica y reiniciar la instancia. 

En esta sección se describe cómo volver a configurar la instancia para el aprendizaje automático. Configuración configura cuentas de servicio externo e inicia el servicio Launchpad.

1. Abra [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Si todavía no está instalado, puede volver a ejecutar el Asistente para la instalación de SQL Server para abrir un vínculo de descarga e instalarlo.
  
2. Conéctese a la instancia donde instaló el aprendizaje automático y, a continuación, ejecute el siguiente comando:

   ```SQL
   sp_configure
   ```

    Busque el valor de la **scripts externos habilitados** propiedad, que debería ser **0**. Esto ocurre porque la característica está desactivada de forma predeterminada para reducir el área expuesta.
     
3. Para habilitar la característica de scripting externo, ejecute la siguiente instrucción:
  
    ```SQL
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
  
4. Reinicie el servicio SQL Server para la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Al reiniciar el servicio SQL Server también automáticamente reinician relacionado [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] servicio.

    Puede reiniciar el servicio mediante el uso de la **servicios** panel en el Panel de Control o mediante el Administrador de configuración de SQL Server.

5. Para comprobar que el servicio de ejecución de script externo está habilitado, en SQL Server Management Studio, abra una nueva **consulta** ventana y vuelva a ejecutar el comando siguiente:
  
    ```SQL
    EXEC sp_configure  'external scripts enabled'
    ```
    **run_value** debería estar establecido ahora en 1.
    
6. Abra la **servicios** panel y compruebe que está ejecutando el servicio Launchpad para la instancia. Si instala varias instancias, cada una de ellas tendrá su propio servicio Launchpad.

7. Es una buena idea para ejecutar un script sencillo para comprobar que los tiempos de ejecución de secuencias de comandos externos pueden comunicarse con SQL Server. 

    Abra una nueva **consulta** ventana en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], y, a continuación, ejecute una secuencia de comandos como la siguiente:
    
    + Para R
    
    ```SQL
    EXEC sp_execute_external_script  @language =N'R',
    @script=N'
    OutputDataSet <- InputDataSet;
    ',
    @input_data_1 =N'SELECT 1 AS hello'
    WITH RESULT SETS (([hello] int not null));
    GO
    ```

    + Para Python
    
    ```SQL
    EXEC sp_execute_external_script  @language =N'Python',
    @script=N'
    OutputDataSet = InputDataSet;
    ',
    @input_data_1 =N'SELECT 1 AS hello'
    WITH RESULT SETS (([hello] int not null));
    GO
    ```

    La secuencia de comandos puede tardar un poco para que se ejecute, la primera vez que se carga en tiempo de ejecución de script externo. Los resultados deben ser algo parecido a esto:

    | hello |
    |----|
    | 1|


8. Si recibe algún error, continúe con la sección que describe los cambios de otros, opcionales que necesite para realizar una vez completada la instalación o consulte a la Guía de solución de problemas:

    + [Pasos posteriores a la instalación opcionales: configurar los permisos y servicio](#bkmk_FollowUp) 
    + [Solución de problemas de aprendizaje automático en SQL Server](upgrade-and-installation-faq-sql-server-r-services.md)

## <a name="bkmk_FollowUp"></a>Pasos posteriores a la instalación opcionales

Dependiendo del caso de uso para el aprendizaje automático, deberá realizar cambios adicionales en el servidor, el servidor de seguridad, las cuentas utilizadas por el servicio o los permisos de base de datos. Los cambios que debe realizar varían por mayúsculas o minúsculas.

Entre los escenarios comunes que requieren cambios adicionales se incluyen:

* Cambiar las reglas de firewall para permitir conexiones entrantes a SQL Server.
* Habilitar los protocolos de red adicionales.
* Asegurarse de que el servidor admite las conexiones remotas.
* Habilitar *autenticación implícita*, si los usuarios tener acceso a datos de SQL Server desde un cliente de ciencia de datos remoto y ejecutan el código mediante el paquete RODBC u otro proveedor ODBC.
* Proporciona a los usuarios acceso a bases de datos individuales.
* Solucionar problemas de seguridad que impiden la comunicación con el servicio Launchpad.
* Asegurarse de que los usuarios tienen permiso para ejecutar el código o instalar paquetes.

> [!NOTE]
> No todos los cambios de la lista pueden ser necesarios. Sin embargo, se recomienda que revise todos los elementos para ver si son aplicables a su escenario.

Sugerencias de solución de problemas adicionales se pueden encontrar aquí: [preguntas más frecuentes de actualización e instalación](../r/upgrade-and-installation-faq-sql-server-r-services.md)

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

Sin embargo, en un escenario empresarial, la mayoría de los usuarios, incluidos los usuarios que tienen acceso a la base de datos mediante el uso de los inicios de sesión SQL, no tiene estos permisos elevados. Por lo tanto, para cada usuario que vaya a ejecutar scripts de R o Python, debe conceder al usuario permisos para ejecutar scripts en cada base de datos que se usarán los scripts externos.

```SQL
USE <database_name>
GO
GRANT EXECUTE ANY EXTERNAL SCRIPT  TO [UserName]
```

> [!TIP]
> ¿Necesita ayuda con la instalación? ¿No está seguro de haber ejecutado todos los pasos? Usar estos informes personalizados para comprobar el estado de la instalación y ejecutar pasos adicionales. 
> 
> [Supervisar servicios de aprendizaje de máquina con informes personalizados](monitor-r-services-using-custom-reports-in-management-studio.md).

### <a name="ensure-that-the-sql-server-computer-supports-remote-connections"></a>Asegúrese de que el equipo de SQL Server admite las conexiones remotas

Si no se puede conectar desde un equipo remoto, compruebe si el servidor permite conexiones remotas. Las conexiones remotas se deshabilitan a veces de forma predeterminada.

Compruebe también si el firewall permite el acceso a SQL Server. De forma predeterminada, el puerto utilizado por SQL Server a menudo está bloqueado por el firewall. Si se usa el Firewall de Windows, consulte [configurar Firewall de Windows para obtener acceso al motor de base de datos](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md).

### <a name="give-your-users-read-write-or-ddl-permissions-to-the-database"></a>Proporcionar a los usuarios de lectura, escritura o permisos de DDL para la base de datos

La cuenta de usuario que se usa para ejecutar R o Python podría necesario para leer datos de otras bases de datos, crear nuevas tablas para almacenar los resultados y escribir datos en tablas. Por lo tanto, para cada usuario que se van a ejecutar los scripts de R o Python, asegúrese de que el usuario tiene los permisos adecuados en la base de datos: *db_datareader*, *db_datawriter*, o *db_ ddladmin*.

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

Después de comprobar que funciona la característica de ejecución del script en SQL Server, puede ejecutar comandos de R y Python desde SQL Server Management Studio, código de Visual Studio o cualquier otro cliente que puede enviar instrucciones T-SQL en el servidor. Antes de hacerlo, debe realizar algunos cambios en la configuración del sistema para admitir un uso intensivo de aprendizaje automático, o agregar nuevos paquetes de R.

Esta sección enumeran algunas optimizaciones comunes y las actividades de aprendizaje para el aprendizaje automático.

### <a name="add-more-worker-accounts"></a>Agregue más cuentas de trabajo

Si cree que podría usar R mucho, o si se espera que muchos usuarios pueden ejecutar scripts al mismo tiempo, puede aumentar el número de cuentas de trabajo que están asignadas al servicio Launchpad. Para obtener más información, consulte [modificar el grupo de cuentas de usuario para servicios de aprendizaje de máquina de SQL Server](modify-the-user-account-pool-for-sql-server-r-services.md).

### <a name="bkmk_optimize"></a>Optimizar el servidor para la ejecución de scripts externos

La configuración predeterminada para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el programa de instalación están diseñados para optimizar el equilibrio del servidor para una variedad de servicios que son compatibles con el motor de base de datos, lo que puede incluir de extracción, transformación y carga (ETL) de procesos, creación de informes, auditoría, y las aplicaciones que utilizan [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] datos. Por lo tanto, la configuración predeterminada, es posible que los recursos para el aprendizaje automático a veces se restringido o limitados, especialmente en operaciones con uso intensivo de memoria.

Para garantizar que los trabajos de aprendizaje de máquina están ordenados y asignaron correctamente, se recomienda que use el regulador de recursos de SQL Server para configurar un grupo de recursos externos. También puede cambiar la cantidad de memoria que se asigna a la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] motor de base de datos o aumentar el número de cuentas que se ejecutan en el [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] service.

- Para configurar un grupo de recursos para administrar recursos externos, consulte [crear un grupo de recursos externo](../../t-sql/statements/create-external-resource-pool-transact-sql.md).
  
- Para cambiar la cantidad de memoria reservada para la base de datos, vea [opciones de configuración de memoria de servidor](../../database-engine/configure-windows/server-memory-server-configuration-options.md).
  
- Para cambiar el número de cuentas de R que se puede iniciar por [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], consulte [modificar el grupo de cuentas de usuario para el aprendizaje automático](modify-the-user-account-pool-for-sql-server-r-services.md).

Si está usando Standard Edition y no tiene el regulador de recursos, puede usar vistas de administración dinámica (DMV) y eventos extendidos, así como eventos de Windows de supervisión, para ayudar a administrar los recursos del servidor que usan R. Para obtener más información, consulte [supervisión y administración de servicios de R](managing-and-monitoring-r-solutions.md).

### <a name="install-additional-r-packages"></a>Instalar paquetes de R adicionales

Dedique un minuto a instalar los paquetes de R adicionales que vamos a usar.

Los paquetes que quiera usar de SQL Server deben estar instalados en la biblioteca predeterminada que la instancia usa. Si tiene una instalación independiente de R en el equipo, o si ha instalado los paquetes a las bibliotecas de usuario, no podrá usar esos paquetes de T-SQL.

El proceso para instalar y administrar paquetes de R es diferente de SQL Server 2016 y 2017 de SQL Server. Por ejemplo, en SQL Server 2017, puede configurar grupos de usuarios para compartir los paquetes en un nivel de cada base de datos o configurar los roles de base de datos para permitir a los usuarios instalar sus propios paquetes. Para obtener más información, consulte [administración del paquete](r-package-management-for-sql-server-r-services.md).

En SQL Server 2016, un administrador de base de datos debe instalar paquetes de R que necesitan los usuarios.

Acceso administrativo también es necesario para instalar paquetes adicionales de Python en la biblioteca de la instancia.

### <a name="upgrade-the-machine-learning-components"></a>Actualizar los componentes de aprendizaje automático

Al instalar características de aprendizaje de máquina en SQL Server, obtendrá la versión de los componentes de R o Python que era más actualizada cuando se publicó la versión o service pack. Cada vez que aplicar la revisión o actualiza el servidor, los componentes de aprendizaje de máquina se actualizan también.

Sin embargo, puede actualizar los componentes de forma más rápida que se admite de aprendizaje automático en versiones de SQL Server, mediante el uso de un proceso conocido como _enlace_. Al enlazar una instancia de SQL Server, actualiza las versiones de R o Python tanto cambia a una directiva de soporte técnico diferente que es compatible con las actualizaciones más frecuentes. 

Estas actualizaciones podrían incluir:

* Nuevos paquetes de R
+ Nuevas API de Microsoft como paquetes [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package).
* [Previamente entrenada modelos](https://docs.microsoft.com/r-server/install/microsoftml-install-pretrained-models) para el análisis de clasificación y el texto de la imagen.

Para obtener información sobre cómo actualizar una instancia de SQL Server, vea [actualizar componentes de aprendizaje de máquina a través del enlace](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).


### <a name="tutorials"></a>Tutoriales

Para empezar a trabajar con algunos ejemplos sencillos y conozca los aspectos básicos del funcionamiento de R con SQL Server, vea [código R de uso en Transact-SQL](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md).

Para ver ejemplos de aprendizaje automático que se basan en situaciones del mundo real, vea [máquina tutoriales de aprendizaje](../tutorials/machine-learning-services-tutorials.md).

### <a name="troubleshooting"></a>Solucionar problemas

¿Le ha surgido algún problema? ¿Intentando actualizar? Para obtener respuestas a preguntas comunes y los problemas conocidos, vea el artículo siguiente:

* [Actualización e instalación preguntas más frecuentes: servicios de aprendizaje de máquina](upgrade-and-installation-faq-sql-server-r-services.md)

Para comprobar el estado de instalación de la instancia y solucionar problemas comunes, pruebe estos informes personalizados.

* [Informes personalizados para SQL Server R Services](\r\monitor-r-services-using-custom-reports-in-management-studio.md)
