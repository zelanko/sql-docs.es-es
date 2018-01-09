---
title: "El programa de instalación y configuración de servicios de aprendizaje de máquina de Python | Documentos de Microsoft"
ms.custom: 
ms.date: 12/20/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: python
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: abc79124569635f3aafaaa309e25e2c827fa5d9b
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="set-up-python-machine-learning-services-in-database"></a>Configurar los servicios de aprendizaje de máquina de Python (In-Database)

  Este artículo describe cómo instalar los componentes necesarios para Python mediante la ejecución de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Asistente para la instalación y siguiendo las indicaciones interactivas.

## <a name="machine-learning-options-in-sql-server-setup"></a>Opciones de instalación de SQL Server de aprendizaje automático

Elija la **Machine Learning Services** de características y seleccione **Python** como el idioma.

El **características compartidas** sección contiene una opción de instalación independiente, **Server de aprendizaje de máquina (independiente)**. Esta opción admite la puesta en marcha del código de Python en un servidor que no tiene SQL Server, o que no requiere el uso de contextos de proceso de SQL Server. Por lo tanto, se recomienda *no* se debe instalar en el mismo equipo que una instancia de SQL Server. En su lugar, instalar a servidor de aprendizaje de máquina (independiente) en un equipo independiente.

Una vez completada la instalación, vuelva a configurar la instancia para permitir la ejecución de scripts que usan un ejecutable externo. Debe realizar cambios adicionales en el servidor para admitir cargas de trabajo de aprendizaje de máquina. Cambios de configuración suele ser necesitan un reinicio de la instancia o un reinicio del servicio Launchpad.

### <a name="prerequisites"></a>Prerequisites

+ Se requiere SQL Server 2017. Integración de Python no se admite en versiones anteriores de SQL Server.
+ Asegúrese de instalar el motor de base de datos. Una instancia de SQL Server es necesario para ejecutar scripts de Python en database.
+ Requisitos previos se instalan como parte de la instalación del componente de Python.
+ No puede instalar el aprendizaje automático con los servicios de Python en un clúster de conmutación por error. El mecanismo de seguridad utilizado para aislar los procesos de Python no es compatible con un entorno de clúster de conmutación por error de Windows Server.
   
  Como alternativa, puede utilizar la replicación para copiar tablas necesarias para una instancia de SQL Server independiente que usa los servicios de Python. Como alternativa, puede instalar el aprendizaje automático con los servicios de Python en un equipo independiente que se usa la configuración de AlwaysOn y forma parte de un grupo de disponibilidad.

+ Instalación en paralelo con otras versiones de Python es posible, porque la instancia de SQL Server utiliza su propia copia de la distribución de Anaconda. Sin embargo, ejecutar código que usa Python en el equipo de SQL Server fuera de SQL Server puede producir varios problemas:
    
    - Usar una biblioteca diferente y un ejecutable diferente y obtener resultados diferentes, que se obtienen cuando se ejecuta en SQL Server.
    - Scripts de Python que se ejecutan en bibliotecas externas no pueden administrarse mediante SQL Server, dando lugar a la contención de recursos.
  
> [!IMPORTANT]
> Una vez completada la instalación, asegúrese de completar los pasos adicionales de configuración posterior a la descrita en este artículo. Estos pasos incluyen la habilitación de SQL Server puede utilizar scripts externos y agregar cuentas necesarias para que SQL Server ejecutar trabajos de Python en su nombre.

### <a name="unattended-installation"></a>Instalación desatendida

Para llevar a cabo una instalación desatendida, use las opciones de línea de comandos para el programa de instalación de SQL Server y los argumentos específicos de Python. Para obtener más información, consulte [desatendido se instala de SQL Server con servicios de aprendizaje de máquina de Python](unattended-installs-of-sql-server-python-services.md).

##  <a name="bkmk_installPythonInDatabase"></a>Paso 1: Instalar servicios (en bases de datos) en SQL Server de aprendizaje automático

1. Ejecute al Asistente para la instalación de SQL Server 2017.
  
2. En el **instalación** ficha, seleccione **instalación independiente del nuevo servidor SQL Server o agregar características a una instalación existente**.

    ![Instalar Python en bases de datos](media/2017setup-installation-page-mlsvcs.PNG)
   
3. En la página **Selección de características** , seleccione estas opciones:
  
    -   **Servicios de Motor de base de datos**
  
         Para usar Python con SQL Server, debe instalar una instancia del motor de base de datos. Puede usar el valor predeterminado o una instancia con nombre.
  
    -   **Servicios (en bases de datos) de aprendizaje automático**
  
         Esta opción instala los servicios de base de datos que admite la ejecución del script de Python.

    -   **Python** Active esta opción para ver el archivo ejecutable de Python 3.5 y seleccione las bibliotecas de la distribución de Anaconda. Instale un solo idioma por cada instancia.
        
        ![Característica opciones para Python](media/ml-svcs-features-python-highlight.png "configurar opciones de Python")

        > [!NOTE]
        > 
        > No seleccione la opción para **Server de aprendizaje de máquina (independiente)**. La opción para instalar el servidor de aprendizaje de máquina en **características compartidas** está diseñado para su uso en un equipo independiente. Por ejemplo, puede instalar la misma versión de los componentes en un equipo diferente que se utiliza para el desarrollo del proyecto, como equipos portátiles de los científicos de datos de aprendizaje automático.

4. En el **dar su consentimiento para instalar Python** página, seleccione **Accept**.
  
     Este contrato de licencia se requiere para descargar el archivo ejecutable, Python paquetes de Python desde Anaconda.
     
     ![Contrato de licencia de Python](media/ml-svcs-license-python.png "del acuerdo para Python de licencia")
  
    > [!NOTE]
    >  Si el equipo que está utilizando no tiene acceso a internet, puede pausar el programa de instalación en este momento para descargar a los instaladores por separado. Para obtener más información, consulte [instalación de componentes sin acceso a internet](../r/installing-ml-components-without-internet-access.md).
  
     Seleccione **Accept**, espere hasta que el **siguiente** botón se convierte en activa y, a continuación, seleccione **siguiente**.
  
5. En el **preparado para instalar** , comprueba que las selecciones se incluyen y seleccione **instalar**.
  
     + Servicios de Motor de base de datos
     + Machine Learning Services (en base de datos)
     + Python
  
    Estas selecciones representan la configuración mínima necesaria para utilizar Python con [!INCLUDE[ssnoversion](../../includes/ssnoversion.md)].
    
    ![Preparado para instalar Python](media/ready-to-install-python.png "componentes necesarios para la instalación de Python")

    Si lo desea, tome nota de la ubicación de la carpeta en la ruta de acceso `..\Setup Bootstrap\Log` donde se almacenan los archivos de configuración. Cuando finalice la instalación, puede revisar los componentes instalados en el archivo de resumen.

6. Cuando se complete la instalación, reinicie el equipo.

##  <a name="bkmk_enableFeature"></a>Paso 2: Habilitar la ejecución del script de Python

1. Abra [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. 

    > [!TIP]
    > Puede descargar e instalar la versión adecuada de esta página: [descargar SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).
    > 
    > También puede probar la versión preliminar de [Studio de operaciones SQL](https://docs.microsoft.com/sql/sql-operations-studio/what-is), que es compatible con las tareas administrativas y las consultas en SQL Server.
  
2. Conéctese a la instancia donde haya instalado servicios de aprendizaje de máquina y ejecute el siguiente comando:

   ```SQL
   sp_configure
   ```

    El valor de la propiedad, `external scripts enabled`, debería ser **0** en este momento. Esto ocurre porque la característica está desactivada de forma predeterminada. La característica debe habilitarse explícitamente por un administrador para poder ejecutar scripts de R o Python.
    
3.  Para habilitar la característica de scripting externo que admita Python, ejecute la siguiente instrucción:
    
    ```SQL
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
    
    No se ejecutan si ya ha habilitado la característica del lenguaje R, volver a configurar una segunda vez para Python. La plataforma de extensibilidad subyacente admite ambos lenguajes.

4. Reinicie el servicio SQL Server para la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Al reiniciar el servicio SQL Server también automáticamente reinician relacionado [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] servicio.

    Puede reiniciar el servicio mediante el uso de la **servicios** en el Panel de Control, o mediante el panel [Administrador de configuración de SQL Server](../../relational-databases/sql-server-configuration-manager.md).

## <a name="step-3-verify-that-the-external-script-execution-feature-is-running"></a>Paso 3: Comprobar que se está ejecutando la característica de ejecución de scripts externos

Tómese un momento para comprobar que se están ejecutando todos los componentes utilizados para iniciar el script de Python.

1. En SQL Server Management Studio, abra una nueva ventana de consulta y ejecute el siguiente comando:
    
    ```SQL
    EXEC sp_configure  'external scripts enabled'
    ```

    **run_value** debería estar establecido ahora en 1.
    
2. Abra la **servicios** panel o administrador de configuración de SQL Server y compruebe que está ejecutando el servicio Launchpad para la instancia. Si no se está ejecutando el Launchpad, reinicie el servicio.
  
    Si tiene instaladas varias instancias de SQL Server, cualquier instancia con R o Python habilitado tiene su propio servicio Launchpad.

    Si instala R y Python en una sola instancia, solo un Launchpad se instala. Se agrega un selector de DLL independiente, específicos del idioma para cada idioma. Para obtener más información, consulte [componentes para la integración de Python](new-components-in-sql-server-to-support-python-integration.md). 
   
3. Si está ejecutando Launchpad, podrá ejecutar scripts de Python simples similar al siguiente en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]:
    
    ```SQL
    EXEC sp_execute_external_script  @language =N'Python',
    @script=N'OutputDataSet = InputDataSet',
    @input_data_1 = N'SELECT 1 AS col'
    ```
    
    **Resultado**
    
    *<code>&nbsp;&nbsp;</code>* *1*

> [!NOTE]
> Encabezados que se usa en el script de Python o columnas no se devuelven, por diseño. Para agregar nombres de columna para la salida, debe especificar el esquema para el conjunto de datos devuelto. Esto se hace mediante el parámetro con resultados del procedimiento almacenado, nombres de las columnas y especificar el tipo de datos SQL.
> 
> Por ejemplo, puede agregar la línea siguiente para generar un nombre de columna arbitrario:`WITH RESULT SETS ((Col1 AS int))`

## <a name="step-4-additional-configuration"></a>Paso 4: Configuración adicional

Si el comando anterior se realizó correctamente, puede ejecutar comandos de Python desde SQL Server Management Studio, código de Visual Studio o cualquier otro cliente que puede enviar instrucciones T-SQL en el servidor.

Si recibe un error al ejecutar el comando, revise la lista siguiente. Debe realizar configuraciones adecuadas adicionales en el servicio o la base de datos.

> [!NOTE]
> 
> No todos los cambios mostrados son necesarios y ninguno puede ser necesario. Requisitos dependen de un esquema de seguridad, que se instaló SQL Server y cómo esperar a los usuarios conectarse a la base de datos y ejecutar scripts externos.

###  <a name="bkmk_configureAccounts"></a>Habilitar la autenticación implícita para el grupo de cuentas de Launchpad

Durante la instalación, se crean una serie de cuentas de usuario de Windows para ejecutar tareas en el token de seguridad del servicio [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]. Cuando un usuario envía un script de Python o R desde un cliente externo, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] activa una cuenta de trabajo disponibles. A continuación, se asigna a la identidad del usuario que realiza la llamada y se ejecuta la secuencia de comandos en nombre del usuario.

Esto se denomina *autenticación implícita*, y es un servicio del motor de base de datos. Este servicio admite la ejecución segura de scripts externos en SQL Server 2016 y 2017 de SQL Server.

Puede ver estas cuentas en el grupo de usuarios de Windows **SQLRUserGroup**. De forma predeterminada, se crean 20 cuentas de trabajo, que normalmente es más que suficiente para ejecutar el script externo trabajos.

> [!IMPORTANT]
> El grupo de trabajo se denomina **SQLRUserGroup** independientemente de si ha instalado R o Python. Hay un único grupo para cada instancia.

Si necesita ejecutar scripts desde un cliente de ciencia de datos remoto y está usando la autenticación de Windows, hay consideraciones adicionales. Estas cuentas de trabajo se le deben conceder permiso para iniciar sesión en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia en su nombre.

1. En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], en el Explorador de objetos, expanda **seguridad**. A continuación, haga clic en **inicios de sesión**y seleccione **nuevo inicio de sesión**.
2. En el **inicio de sesión - nuevo** cuadro de diálogo, seleccione **búsqueda**.
3. Seleccione **tipos de objeto**y seleccione **grupos**. Borrar todo lo demás.
4. En **escriba el nombre de objeto a seleccionar**, tipo *SQLRUserGroup*y seleccione **comprobar nombres**.
5. El nombre del grupo local asociado al servicio Launchpad de la instancia se debe resolver como algo parecido a *instancename\SQLRUserGroup*. Seleccione **Aceptar**.
6. De forma predeterminada, el grupo se asigna a la **público** rol, y tenga permiso para conectarse al motor de base de datos.
7. Seleccione **Aceptar**.

> [!NOTE]
> Si utiliza un **inicio de sesión SQL** para ejecutar scripts en un contexto de proceso de SQL Server, no es necesario el paso adicional.

### <a name="give-users-permission-to-run-external-scripts"></a>Proporcionar a los usuarios permiso para ejecutar scripts externos

Si instaló [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usted mismo y se ejecuta scripts de Python en su propia instancia, normalmente ejecutar secuencias de comandos como administrador. Por lo tanto, tiene permiso implícito en varias operaciones y todos los datos en la base de datos.

Sin embargo, la mayoría de los usuarios, no tiene estos permisos elevados. Por ejemplo, los usuarios de una organización que usan inicios de sesión SQL para tener acceso a la base de datos generalmente no tiene permisos elevados. Por lo tanto, para cada usuario que se usa Python, debe conceder a los usuarios de servicios de aprendizaje de máquina el permiso para ejecutar scripts externos en cada base de datos donde se usa Python. A continuación, se indica cómo puede hacerlo.

```SQL
USE <database_name>
GO
GRANT EXECUTE ANY EXTERNAL SCRIPT  TO [UserName]
```

> [!NOTE]
> Permisos no son específicos del lenguaje de secuencia de comandos compatible. En otras palabras, no hay niveles de permisos distintos para un script de R en comparación con el script de Python. Si necesita mantener permisos independientes para estos idiomas, instalar R y Python en instancias independientes.

### <a name="give-your-users-read-write-or-data-definition-language-ddl-permissions-to-databases"></a>Conceder permisos de DDL (lenguaje) para las bases de datos a la definición de lectura, escritura o datos de los usuarios

Mientras un usuario ejecuta las secuencias de comandos, el usuario deba leer datos de otras bases de datos. El usuario necesite también crear nuevas tablas para almacenar los resultados y escribir datos en tablas.

Para cada cuenta de usuario de Windows o inicio de sesión SQL que ejecuta scripts de R o Python, asegúrese de que tiene los permisos adecuados en la base de datos específica: `db_datareader`, `db_datawriter`, o `db_ddladmin`.

Por ejemplo, la siguiente [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción proporciona el inicio de sesión SQL *MySQLLogin* los derechos para ejecutar consultas de T-SQL la *ML_Samples* base de datos. Para ejecutar esta instrucción, el inicio de sesión de SQL debe existir en el contexto de seguridad del servidor.

```SQL
USE ML_Samples
GO
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'
```

Para obtener más información acerca de los permisos que se incluyen en cada rol, consulte [roles de nivel de base de datos](../../relational-databases/security/authentication-access/database-level-roles.md).

### <a name="ensure-that-the-sql-server-installation-supports-remote-connections"></a>Asegúrese de que la instalación de SQL Server admite las conexiones remotas

Si no se puede conectar desde un equipo remoto, compruebe si el firewall permite el acceso a SQL Server. En una instalación predeterminada, se podrían deshabilitar las conexiones remotas o el puerto específico utilizado por SQL Server puede estar bloqueado por el firewall. Para obtener más información, consulte [configurar Firewall de Windows para obtener acceso al motor de base de datos](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md).

### <a name="create-an-odbc-data-source-for-the-instance-on-your-data-science-client"></a>Crear un origen de datos de ODBC para la instancia en el cliente de ciencia de datos

Puede crear un solución en un equipo cliente de ciencia de datos de aprendizaje automático. Si tiene que ejecutar código con el equipo de SQL Server como el contexto de proceso, tiene dos opciones: tener acceso a la instancia mediante un inicio de sesión SQL o mediante el uso de una ventana de la cuenta.

+ Para los inicios de sesión SQL: asegúrese de que el inicio de sesión tiene los permisos adecuados en la base de datos donde está leyendo datos. Puede hacerlo agregando *conectarse a* y *seleccione* permisos, o agregando el inicio de sesión para el `db_datareader` rol. Para crear objetos, asignar `DDL_admin` derechos. Si debe guardar los datos en tablas, agregar a la `db_datawriter` rol.

+ Para la autenticación de Windows: deberá crear un origen de datos ODBC en el cliente de ciencia de datos que especifica el nombre de instancia y otra información de conexión. Para obtener más información, consulte [Administrador de orígenes de datos ODBC](https://docs.microsoft.com/sql/odbc/admin/odbc-data-source-administrator).

## <a name="additional-optimizations"></a>Optimizaciones adicionales

Ahora que tiene todo en funcionamiento, que le interese optimizar el servidor para admitir el aprendizaje automático o instalar previamente entrenada modelos.

### <a name="add-more-worker-accounts"></a>Agregue más cuentas de trabajo

Si se espera que muchos usuarios que se esté ejecutando secuencias de comandos al mismo tiempo, puede aumentar el número de cuentas de trabajo que están asignadas al servicio Launchpad. Para obtener más información, consulte [modificar el grupo de cuentas de usuario para servicios de aprendizaje de máquina de SQL Server](../r/modify-the-user-account-pool-for-sql-server-r-services.md).

### <a name="optimize-the-server-for-script-execution"></a>Optimizar el servidor para la ejecución de secuencias de comandos

La configuración predeterminada para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el programa de instalación optimizar el equilibrio del servidor para una variedad de servicios. Estos servicios incluyen ETL procesos, informes, auditoría y las aplicaciones que utilizan [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] datos.

Si utiliza la configuración predeterminada, es posible que los recursos para ejecutar scripts externos están restringidos o limitados, especialmente en operaciones con uso intensivo de memoria. Si el aprendizaje automático es una prioridad, cambiar la configuración de base de datos predeterminada para garantizar que los trabajos de script externo son un nivel de prioridad y con los recursos apropiadamente. Estos cambios incluyen:

+ Reducir la cantidad de memoria asignada a la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] motor de base de datos.
+ Aumentar el número de cuentas de ejecución en el [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] service. Esto no aumenta el número de recursos, pero aumenta el número de secuencias de comandos que pueden ejecutarse simultáneamente.

Si tiene SQL Server Enterprise Edition, use el regulador de recursos para configurar un grupo de recursos externos para Python. Para obtener más información, vea los siguientes artículos:

-   Configurar un grupo de recursos para administrar recursos externos
  
     [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)
  
-   Cambiar la cantidad de memoria reservada para el motor de base de datos
  
     [Opciones de configuración de servidor de memoria de servidor](../../database-engine/configure-windows/server-memory-server-configuration-options.md)
  
-   Cambiar el número de cuentas de trabajo que se pueden iniciar mediante[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]
  
     [Modificar el grupo de cuentas de usuario de SQL Server R Services](../r/modify-the-user-account-pool-for-sql-server-r-services.md)

Si está usando SQL Server Standard Edition y no tiene el regulador de recursos, puede usar vistas de administración dinámica y eventos extendidos para ayudarle a administrar los recursos de servidor. También puede usar la supervisión de eventos de Windows para este propósito. Para obtener más información, consulte [supervisión y administración de servicios de R](../r/managing-and-monitoring-r-solutions.md).

### <a name="upgrade-the-machine-learning-components"></a>Actualizar los componentes de aprendizaje automático

Al instalar servicios de aprendizaje de máquina mediante SQL Server 2017, obtendrá la versión de los componentes en el momento en que se publicó la versión. Cada vez que aplicar la revisión o actualiza la instancia de SQL Server, los componentes de aprendizaje de máquina se actualizan también.

Puede actualizar los componentes de forma más rápida que se admite de aprendizaje automático en versiones de SQL Server, al instalar servidor de aprendizaje de máquina de Microsoft. Si lo hace, también obtendrá las nuevas características que se admite en la versión más reciente del servidor de aprendizaje de máquina, como:

+ Las actualizaciones de paquetes de Python para [revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package) y [microsoftml para Python](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package).
+ [Previamente entrenada modelos](https://docs.microsoft.com/r-server/install/microsoftml-install-pretrained-models) para el análisis de clasificación y el texto de la imagen.

Para obtener información acerca de cómo actualizar una instancia, vea [componentes de R actualizar a través del enlace](..\r\use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

### <a name="tutorials"></a>Tutoriales

Vea los siguientes tutoriales para algunos ejemplos de cómo utilizar Python con SQL Server para crear e implementar soluciones de aprendizaje de máquina:

[Uso de Python en T-SQL](../tutorials/run-python-using-t-sql.md)

[Crear un modelo de Python con revoscalepy](../tutorials/use-python-revoscalepy-to-create-model.md)
