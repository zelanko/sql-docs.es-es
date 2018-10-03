---
title: Instalar SQL Server Machine Learning Services (en bases de datos) en Windows | Microsoft Docs
description: R en SQL Server o Python en SQL Server está disponible al instalar SQL Server 2017 Machine Learning Services en Windows.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/01/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 330c21e6eb256bfe398bc707852eb9a66a183fb7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48142665"
---
# <a name="install-sql-server-machine-learning-services-on-windows"></a>Instalar SQL Server Machine Learning Services en Windows
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

A partir de SQL Server 2017, R y Python ofrece compatibilidad para análisis en bases de datos están en SQL Server Machine Learning Services, el sucesor de [SQL Server R Services](../r/sql-server-r-services.md) introducidas en SQL Server 2016. Bibliotecas de funciones están disponibles en R y Python y de identificación de script externo en una instancia del motor de base de datos. 

En este artículo se explica cómo instalar el componente de machine learning mediante la ejecución de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Asistente para la instalación y seguir las indicaciones en pantalla.

## <a name="bkmk_prereqs"> </a> Lista de comprobación previa a la instalación

+ Instalación de 2017 (o superior) de SQL Server es necesario si va a instalar servicios de Machine Learning con compatibilidad con el lenguaje R, Python o Java. Si en su lugar tiene los medios de instalación de SQL Server 2016, puede instalar [SQL Server 2016 R Services (In-Database)](sql-r-services-windows-install.md) para obtener compatibilidad con el lenguaje R.

+ Se requiere una instancia del motor de base de datos. No se puede instalar solo características R o Python, aunque se puede agregar gradualmente a una instancia existente.

- La instalación de Machine Learning Services es *no admite* en un clúster de conmutación por error de SQL Server 2017. Sin embargo, lo *es compatible con* con SQL Server 2019. 
 
+ No instale Machine Learning Services en un controlador de dominio. Se producirá un error en la parte de Machine Learning Services del programa de instalación.

+ No instale **características compartidas** > **Machine Learning Server (independiente)** en el mismo equipo que ejecuta una instancia de base de datos. Un servidor independiente competirán por los mismos recursos, lo cual puede perjudicar el rendimiento de ambas instalaciones.

+ Instalación en paralelo con otras versiones de R y Python es compatible, pero no se recomienda. Se admite porque la instancia de SQL Server usa sus propias copias de las distribuciones de R y Anaconda de código abierto. Pero no se recomienda porque ejecuta código que usa R y Python en el equipo de SQL Server fuera de SQL Server puede provocar varios problemas:
    
  + Usar un ejecutable diferente y una biblioteca diferente y obtener resultados diferentes, que se obtienen cuando se ejecuta en SQL Server.
  + No puede administrar los scripts de R y Python que se ejecutan en bibliotecas externas de SQL Server, dando lugar a la contención de recursos.
  
> [!IMPORTANT]
> Una vez completada la instalación, asegúrese de completar los pasos posteriores a la configuración descritos en este artículo. Estos pasos incluyen habilitar SQL Server puede utilizar scripts externos y cómo agregar cuentas necesarias para que SQL Server ejecutar trabajos de R y Python en su nombre. Los cambios de configuración generalmente requieren un reinicio de la instancia o un reinicio del servicio Launchpad.

## <a name="get-the-installation-media"></a>Obtener los medios de instalación

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

## <a name="run-setup"></a>Ejecute el programa de instalación

En instalaciones locales, debe ejecutar el programa de instalación como administrador. Si instala [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde un recurso compartido remoto, deberá usar una cuenta de dominio que tenga permisos de lectura y ejecución para dicho recurso.

1. Iniciar al Asistente para la instalación de SQL Server 2017. Puede descargar 
  
2. En el **instalación** ficha, seleccione **instalación independiente del nuevo servidor SQL Server o agregar características a una instalación existente**.

   ![Instalar servicios de base de datos de aprendizaje automático](media/2017setup-installation-page-mlsvcs.PNG)
   
3. En la página **Selección de características** , seleccione estas opciones:
  
    -   **Servicios de Motor de base de datos**
  
         Para usar R y Python con SQL Server, debe instalar una instancia del motor de base de datos. Puede usar un valor predeterminado o una instancia con nombre.
  
    -   **Machine Learning Services (en base de datos)**
  
         Esta opción instala los servicios de base de datos que sea compatible con R y la ejecución del script de Python.

    -   **R**

        Active esta opción para agregar los paquetes de Microsoft R, intérprete y r de código abierto. 

    -   **Python**

        Active esta opción para agregar los paquetes de Python de Microsoft, el archivo ejecutable de Python 3.5 y seleccione las bibliotecas de la distribución de Anaconda.
        
        ![Características de las opciones de R y Python](media/2017setup-features-page-mls-rpy.png "configurar opciones de Python")

        > [!NOTE]
        > 
        > No seleccione la opción para **Machine Learning Server (independiente)**. La opción para instalar el servidor de Machine Learning en **características compartidas** está pensado para su uso en un equipo independiente.

4. En el **da su consentimiento para instalar R** página, seleccione **Accept**. Este contrato de licencia cubre Microsoft R Open, que incluye una distribución de los paquetes base de código abierto R y herramientas, junto con los paquetes de R mejorados y proveedores de conectividad desde el equipo de desarrollo de Microsoft.

5. En el **da su consentimiento para instalar Python** página, seleccione **Accept**. El contrato de licencia de código abierto de Python también cubre Anaconda y herramientas relacionadas, además de algunas bibliotecas de Python nuevo desde el equipo de desarrollo de Microsoft.
     
     ![Contrato de licencia de Python](media/2017setup-python-license.png "contrato para Python de licencia")
  
    > [!NOTE]
    >  Si el equipo que está utilizando no tiene acceso a internet, puede pausar el programa de instalación en este momento para descargar a los instaladores por separado. Para obtener más información, consulte [instalar componentes de aprendizaje automático sin acceso a internet](../install/sql-ml-component-install-without-internet-access.md).
  
     Seleccione **Accept**, espere hasta que el **siguiente** botón se convierte en activa y, a continuación, seleccione **siguiente**.
  
6. En el **preparado para instalar** , comprueba que estas selecciones se incluyen y seleccione **instalar**.
  
    + Servicios de Motor de base de datos
    + Machine Learning Services (en base de datos)
    + R, Python o ambos

    Tenga en cuenta la ubicación de la carpeta en la ruta de acceso `..\Setup Bootstrap\Log` donde se almacenan los archivos de configuración. Cuando se completa la instalación, puede revisar los componentes instalados en el archivo de resumen.

7. Una vez completada la instalación, si se indica que reinicie el equipo, hágalo ahora. Es importante leer el mensaje del Asistente para la instalación tras finalizar el programa de instalación. Para obtener más información, vea [View and Read SQL Server Setup Log Files](https://docs.microsoft.com/sql/database-engine/install-windows/view-and-read-sql-server-setup-log-files).

<a name="bkmk_enableFeature"></a>

## <a name="enable-script-execution"></a>Habilitar la ejecución del script

1. Abra [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. 

    > [!TIP]
    > Puede descargar e instalar la versión adecuada desde esta página: [descargar SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).
    > 
    > También puede probar la versión preliminar de [Azure Data Studio](../../azure-data-studio/what-is.md), que es compatible con las tareas administrativas y las consultas en SQL Server.
  
2. Conéctese a la instancia donde instaló Servicios Machine Learning, haga clic en **nueva consulta** para abrir una ventana de consulta y ejecute el siguiente comando:

   ```SQL
   sp_configure
   ```

    El valor de la propiedad, `external scripts enabled`, debería ser **0** en este momento. Eso es porque la característica está desactivada de forma predeterminada. La característica debe habilitarse explícitamente por un administrador para poder ejecutar scripts de R o Python.
    
3.  Para habilitar la característica de scripting externo, ejecute la siguiente instrucción:
    
    ```SQL
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
    
    No se ejecutan si ya ha habilitado la característica del lenguaje R, volver a configurar una segunda vez para Python. La plataforma de extensibilidad subyacente admite ambos lenguajes.

## <a name="restart-the-service"></a>Reinicie el servicio.

Una vez completada la instalación, reinicie el motor de base de datos antes de continuar con la siguiente, habilitar la ejecución del script.

Reiniciar automáticamente el servicio reinicia relacionado [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] service.

Puede reiniciar el servicio con el botón secundario **reiniciar** comando de la instancia en SSMS o mediante el uso de la **servicios** panel en el Panel de Control o mediante el uso de [Administrador de configuración de SQL Server ](../../relational-databases/sql-server-configuration-manager.md).

## <a name="verify-installation"></a>Comprobar la instalación

Comprobar el estado de instalación de la instancia en [informes personalizados](../r/monitor-r-services-using-custom-reports-in-management-studio.md) o registros de instalación.

Use los pasos siguientes para comprobar que se están ejecutando todos los componentes utilizados para iniciar scripts externos.

1. En SQL Server Management Studio, abra una nueva ventana de consulta y ejecute el siguiente comando:
    
    ```SQL
    EXEC sp_configure  'external scripts enabled'
    ```

    **run_value** debería estar establecido ahora en 1.
    
2. Abra el **servicios** panel o el Administrador de configuración de SQL Server y compruebe **servicio Launchpad de SQL Server** se está ejecutando. Debe tener un servicio para cada instancia del motor de base de datos que tenga R o Python instalado. Para obtener más información sobre el servicio, consulte [Extensibility framework](../concepts/extensibility-framework.md). 
   
3. Si Launchpad se está ejecutando, debe ser capaz de ejecutar scripts de R y Python para comprobar que los tiempos de ejecución de secuencias de comandos externos pueden comunicarse con SQL Server.

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

 **Resultado**

    El script puede tardar unos instantes para ejecutar la primera vez que se carga el tiempo de ejecución de scripts externos. Los resultados deben ser algo parecido a esto:

    | hello |
    |----|
    | 1|


> [!NOTE]
> Las columnas o los encabezados que se usa en el script de Python no se devuelven, por diseño. Para agregar nombres de columna para la salida, debe especificar el esquema para el conjunto de datos devuelto. Hacer esto con el parámetro con resultados del procedimiento almacenado, nombres de las columnas y especificar el tipo de datos SQL.
> 
> Por ejemplo, puede agregar la línea siguiente para generar un nombre de columna arbitraria: `WITH RESULT SETS ((Col1 AS int))`

<a name="apply-cu"></a>

## <a name="apply-updates"></a>Aplicar actualizaciones

Se recomienda que aplique la actualización acumulativa más reciente para el motor de base de datos y los componentes de aprendizaje automático.

En los dispositivos conectados a internet, normalmente se aplican las actualizaciones acumulativas a través de Windows Update, pero también puede usar los pasos siguientes para las actualizaciones controladas. Al aplicar la actualización para el motor de base de datos, el programa de instalación extrae las actualizaciones acumulativas para las características de R o Python que instala en la misma instancia. 

En los servidores sin conexión, se necesitan pasos adicionales. Para obtener más información, consulte [instalar en equipos sin acceso a internet > aplicar actualizaciones acumulativas](sql-ml-component-install-without-internet-access.md#apply-cu).

1. Comience con una instancia de la línea base ya instalada: versión inicial de SQL Server 2017

2. Vaya a la lista de actualizaciones acumulativas: [actualiza SQL Server 2017](https://sqlserverupdates.com/sql-server-2017-updates/)

3. Seleccione la actualización acumulativa más reciente. Un archivo ejecutable se descargan y extraen automáticamente.

4. Ejecute el programa de instalación. Acepte los términos de licencia y, en la página de selección de características, revise las características para el que se aplican las actualizaciones acumulativas. Debería ver todas las características instaladas para la instancia actual, incluidas características de aprendizaje automático. Programa de instalación descarga los archivos CAB necesarios para actualizar todas las características.

  ![](media/cumulative-update-feature-selection.png)

5. Continúe con el asistente, acepte los términos de licencia para las distribuciones de R y Python. 

## <a name="additional-configuration"></a>Configuración adicional

Si el paso de comprobación de script externo se realizó correctamente, puede ejecutar comandos de R o Python de SQL Server Management Studio, Visual Studio Code o cualquier otro cliente que puede enviar instrucciones T-SQL al servidor.

Si recibe un error al ejecutar el comando, revise los pasos de configuración adicionales en esta sección. Es posible que deba realizar configuraciones adecuadas adicionales en el servicio o la base de datos.

En el nivel de instancia, podría incluir una configuración adicional:

* [Configurar firewall de Windows para las conexiones entrantes](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)
* [Habilitar los protocolos de red adicionales](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)
* [Habilitar conexiones remotas](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md)

En la base de datos, puede que necesite las actualizaciones de configuración siguientes:

* [Ampliar los permisos integrados a los usuarios remotos](#bkmk_configureAccounts)
* [Conceder permiso para ejecutar scripts externos](#permissions-external-script)
* [Conceder acceso a bases de datos individuales](#permissions-db)

> [!NOTE]
> Si se requiere configuración adicional depende del esquema de seguridad, que se instaló SQL Server y cómo se espera que los usuarios conectarse a la base de datos y ejecutar scripts externos. 

<a name="bkmk_configureAccounts"></a> 

###  <a name="enable-implied-authentication-for-sql-restricted-user-group-sqlrusergroup-account-group"></a>Habilitar la autenticación implícita para el grupo de cuentas de grupo de usuarios restringidos (SQLRUserGroup) de SQL

Si necesita ejecutar scripts desde un cliente de ciencia de datos remoto y utiliza la autenticación de Windows, configuración adicional es necesaria para proporcionar a las cuentas de trabajo ejecuta R y Python procesa permiso para iniciar sesión en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia en su nombre. Este comportamiento se denomina *autenticación implícita*y se implementa mediante el motor de base de datos para admitir la ejecución segura de scripts externos en SQL Server 2016 y SQL Server 2017.

> [!NOTE]
> Si usa un **inicio de sesión SQL** para ejecutar scripts en un contexto de proceso de SQL Server, no es necesario este paso adicional.

1. En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], en el Explorador de objetos, expanda **seguridad**. A continuación, haga clic en **inicios de sesión**y seleccione **nuevo inicio de sesión**.
2. En el **inicio de sesión - nuevo** cuadro de diálogo, seleccione **búsqueda**.
3. Seleccione **tipos de objeto**y seleccione **grupos**. Borrar todo lo demás.
4. En **escriba el nombre de objeto a seleccionar**, tipo *SQLRUserGroup*y seleccione **comprobar nombres**.
5. El nombre del grupo local asociado al servicio Launchpad de la instancia se debe resolver como algo parecido a *instancename\SQLRUserGroup*. Seleccione **Aceptar**.
6. De forma predeterminada, el grupo se asigna a la **pública** rol, y tiene permiso para conectarse al motor de base de datos.
7. Seleccione **Aceptar**.

En SQL Server 2017 y versiones anteriores, se crea un número de cuentas de usuario de Windows locales con el fin de ejecutar tareas en el token de seguridad de la [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] service. Puede ver estas cuentas en el grupo de usuarios de Windows **SQLRUserGroup**. De forma predeterminada, se crean 20 cuentas de trabajo, que normalmente es más que suficiente para ejecutar scripts externos de los trabajos. 

Estas cuentas se usan como sigue. Cuando un usuario envía un script de Python o R desde un cliente externo, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] activa una cuenta de trabajo disponible, lo asigna a la identidad del usuario que realiza la llamada y ejecuta la secuencia de comandos en nombre del usuario. Si la secuencia de comandos, que se está ejecutando externos a SQL Server, tiene que recuperar datos o recursos de SQL Server, la conexión a SQL Server requiere un inicio de sesión. Crear un inicio de sesión de base de datos para **SQLRUserGroup** también la conexión se realice correctamente.

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
En SQL Server 2019, cuentas de trabajo se reemplazan con AppContainers, con procesos que se ejecutan en el servicio Launchpad de SQL Server. Aunque ya no se utilizan las cuentas de trabajo, siguen siendo necesarios para agregar un inicio de sesión de base de datos para **SQLRUsergroup** si implícito es necesaria la autenticación. Igual que las cuentas de trabajo no tiene permiso de inicio de sesión, la identidad del servicio Launchpad no uno hace. Crear un inicio de sesión para **SQLRUserGroup**, que consta del servicio Launchpad en esta versión, permite que funcione la autenticación implícita.
::: moniker-end

<a name="permissions-external-script"></a> 

### <a name="give-users-permission-to-run-external-scripts"></a>Proporcionar a los usuarios permiso para ejecutar scripts externos

Si instaló [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usted mismo y ejecuta scripts de R o Python en su propia instancia, normalmente ejecutar secuencias de comandos como administrador. Por lo tanto, tendrá permiso implícito en varias operaciones y todos los datos de la base de datos.

Sin embargo, la mayoría de los usuarios, no tiene estos permisos elevados. Por ejemplo, los usuarios de una organización que usa inicios de sesión SQL para tener acceso a la base de datos generalmente no tiene permisos elevados. Por lo tanto, para cada usuario que usa R o Python, debe conceder a los usuarios de Machine Learning Services el permiso para ejecutar scripts externos en cada base de datos donde se usa el idioma. A continuación, se indica cómo puede hacerlo.

```SQL
USE <database_name>
GO
GRANT EXECUTE ANY EXTERNAL SCRIPT  TO [UserName]
```

> [!NOTE]
> Permisos no son específicos del lenguaje de secuencia de comandos compatible. En otras palabras, no hay niveles de permisos independientes para el script de R en comparación con el script de Python. Si necesita mantener permisos independientes para estos idiomas, instalar R y Python en instancias independientes.

<a name="permissions-db"></a> 

### <a name="give-your-users-read-write-or-data-definition-language-ddl-permissions-to-databases"></a>Conceder permisos de DDL (lenguaje) para las bases de datos de la definición de datos, escritura o lectura de los usuarios

Mientras que un usuario ejecuta secuencias de comandos, el usuario deba leer datos de otras bases de datos. El usuario también podría necesitar crear nuevas tablas para almacenar resultados y escribir datos en tablas.

Para cada cuenta de usuario de Windows o inicio de sesión SQL que ejecuta scripts de R o Python, asegúrese de que tiene los permisos adecuados en la base de datos específica: `db_datareader`, `db_datawriter`, o `db_ddladmin`.

Por ejemplo, la siguiente [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción proporciona el inicio de sesión SQL *MySQLLogin* los derechos para ejecutar consultas de T-SQL en la *ML_Samples* base de datos. Para ejecutar esta instrucción, el inicio de sesión de SQL debe existir en el contexto de seguridad del servidor.

```SQL
USE ML_Samples
GO
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'
```

Para obtener más información acerca de los permisos incluidos en cada rol, consulte [roles de nivel de base de datos](../../relational-databases/security/authentication-access/database-level-roles.md).


### <a name="create-an-odbc-data-source-for-the-instance-on-your-data-science-client"></a>Crear un origen de datos de ODBC para la instancia en el cliente de ciencia de datos

Puede crear una solución en un equipo cliente de ciencia de datos de aprendizaje automático. Si necesita ejecutar código con el equipo de SQL Server como contexto de proceso, tiene dos opciones: tener acceso a la instancia mediante un inicio de sesión SQL o mediante el uso de un Windows de la cuenta.

+ Para los inicios de sesión SQL: asegúrese de que el inicio de sesión tiene los permisos adecuados en la base de datos donde estén leyendo los datos. Puede hacerlo agregando *conectarse a* y *seleccione* permisos, o agregando el inicio de sesión para el `db_datareader` rol. Para crear objetos, asigne `DDL_admin` derechos. Si se debe guardar datos en tablas, agregar a la `db_datawriter` rol.

+ Para la autenticación de Windows: es posible que deba crear un origen de datos ODBC en el cliente de ciencia de datos que especifica el nombre de instancia y otra información de conexión. Para obtener más información, consulte [Administrador de orígenes de datos ODBC](https://docs.microsoft.com/sql/odbc/admin/odbc-data-source-administrator).

## <a name="suggested-optimizations"></a>Optimizaciones sugeridas

Ahora que tiene todo funcione, es posible que también desea optimizar el servidor para admitir el aprendizaje automático o modelos previamente aprendidos install.

### <a name="add-more-worker-accounts"></a>Agregar más cuentas de trabajo

Si espera que muchos usuarios para ejecutar scripts al mismo tiempo, puede aumentar el número de cuentas de trabajo que están asignadas al servicio Launchpad. Para obtener más información, consulte [modificar el grupo de cuentas de usuario de SQL Server Machine Learning Services](../r/modify-the-user-account-pool-for-sql-server-r-services.md).

### <a name="optimize-the-server-for-script-execution"></a>Optimizar el servidor para la ejecución del script

La configuración predeterminada para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el programa de instalación está diseñada para optimizar el equilibrio entre el servidor para una variedad de servicios que son compatibles con el motor de base de datos, lo que puede incluir la extracción, transformación y carga (ETL) de procesos, generación de informes, auditoría, y las aplicaciones que usan [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] datos. Por lo tanto, en la configuración predeterminada, es posible que los recursos para el aprendizaje automático son a veces restringidos o limitados, especialmente en operaciones de gran cantidad de memoria.

Para asegurarse de que los trabajos de machine learning son prioridades y recursos correctos, se recomienda que use el regulador de recursos de SQL Server para configurar un grupo de recursos externos. También puede cambiar la cantidad de memoria que se asigna a la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] motor de base de datos o aumentar el número de cuentas que se ejecutan bajo el [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] service.

- Para configurar un grupo de recursos para administrar los recursos externos, consulte [crear un grupo de recursos externos](../../t-sql/statements/create-external-resource-pool-transact-sql.md).
  
- Para cambiar la cantidad de memoria reservada para la base de datos, vea [opciones de configuración de memoria de servidor](../../database-engine/configure-windows/server-memory-server-configuration-options.md).
  
- Para cambiar el número de cuentas de R que se pueda iniciar por [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], consulte [modificar el grupo de cuentas de usuario para el aprendizaje automático](../r/modify-the-user-account-pool-for-sql-server-r-services.md).

Si está utilizando Standard Edition y no tiene el regulador de recursos, puede usar vistas de administración dinámica (DMV) y eventos extendidos, así como supervisión, para ayudar a administrar los recursos del servidor de eventos de Windows. Para obtener más información, consulte [supervisión y administración de servicios de R](../r/managing-and-monitoring-r-solutions.md) y [supervisión y administración de servicios de Python](../python/managing-and-monitoring-python-solutions.md).

### <a name="install-additional-r-packages"></a>Instalar paquetes de R adicionales

Las soluciones de R que se crea para SQL Server pueden llamar a funciones de R básicas, las funciones de la propiedad paquetes instalados con SQL Server y paquetes de R de terceros compatible con la versión de R de código abierto que se instala con SQL Server.

Los paquetes que quiera usar de SQL Server deben estar instalados en la biblioteca predeterminada que la instancia usa. Si tiene una instalación independiente de R en el equipo, o si ha instalado paquetes en bibliotecas de usuario, no podrá usar esos paquetes desde T-SQL.

El proceso para instalar y administrar paquetes de R es diferente en SQL Server 2016 y SQL Server 2017. En SQL Server 2016, un administrador de base de datos debe instalar los paquetes de R que necesitan los usuarios. En SQL Server 2017, puede configurar grupos de usuarios para compartir paquetes en un nivel por base de datos, o configurar roles de base de datos para permitir que los usuarios instalar sus propios paquetes. Para obtener más información, consulte [instalar nuevos paquetes de R en SQL Server](../r/install-additional-r-packages-on-sql-server.md).


## <a name="next-steps"></a>Pasos siguientes

Los desarrolladores de R pueden empezar a trabajar con algunos ejemplos sencillos y conozca los aspectos básicos del funcionamiento de R con SQL Server. Para el siguiente paso, vea los siguientes vínculos:

+ [Tutorial: Ejecución de R en T-SQL](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [Tutorial: Análisis de en bases de datos para los desarrolladores de R](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Los desarrolladores de Python pueden aprender a usar Python con SQL Server, siga estos tutoriales:

+ [Tutorial: Ejecución de Python en T-SQL](../tutorials/run-python-using-t-sql.md)
+ [Tutorial: Análisis de en bases de datos para desarrolladores de Python](../tutorials/sqldev-in-database-python-for-sql-developers.md)

Para ver ejemplos de aprendizaje automático que se basan en escenarios del mundo real, consulte [tutoriales de aprendizaje automático](../tutorials/machine-learning-services-tutorials.md).
