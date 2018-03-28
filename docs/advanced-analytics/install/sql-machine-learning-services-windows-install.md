---
title: Instalar equipo con SQL Server de 2017 aprendizaje Services (en bases de datos) en Windows | Documentos de Microsoft
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: python
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.workload: On Demand
ms.openlocfilehash: a620e7ede1976fbbc50c0c81a595f002410403c8
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
---
# <a name="install-sql-server-2017-machine-learning-services-in-database-on-windows"></a>Instalar equipo con SQL Server de 2017 aprendizaje Services (en bases de datos) en Windows 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

El componente de servicios de máquinas de aprendizaje de SQL Server agrega análisis predictivos en bases de datos, realizar análisis estadísticos, visualización y algoritmos de aprendizaje automático. Bibliotecas de funciones están disponibles en R y Python y ejecutan como script externo en una instancia del motor de base de datos. 

Este artículo explica cómo instalar el componente de aprendizaje de máquina mediante la ejecución de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Asistente para la instalación y, a continuación las indicaciones en pantalla.

## <a name="bkmk_prereqs"> </a> Lista de comprobación previa a la instalación

+ El programa de instalación de SQL Server 2017 es necesario si va a instalar servicios de aprendizaje de máquina con compatibilidad con idiomas de R, Python o ambos. Si en su lugar tiene los medios de instalación de SQL Server 2016, puede instalar [SQL Server 2016 R Services (In-Database)](sql-r-services-windows-install.md) para obtener compatibilidad con idiomas de R.

+ Se requiere una instancia del motor de base de datos. No se puede instalar solo R o características de Python, a pesar de que puede agregarlos incrementalmente a una instancia existente.

+ No instale Servicios de aprendizaje de máquina en un clúster de conmutación por error. El mecanismo de seguridad utilizado para aislar los procesos de R y Python no es compatible con un entorno de clúster de conmutación por error de Windows Server.

+ No instale Servicios de aprendizaje de máquina en un controlador de dominio. Se producirá un error en la parte de servicios de aprendizaje de máquina del programa de instalación.

+ No instale **características compartidas** > **Server de aprendizaje de máquina (independiente)** en el mismo equipo que ejecuta una instancia de base de datos. Un servidor independiente competirán por los mismos recursos, lo que puede perjudicar el rendimiento de las instalaciones.

+ Instalación en paralelo con otras versiones de R y Python es compatible pero no se recomienda. Se admite porque la instancia de SQL Server utiliza sus propias copias de las distribuciones de R y Anaconda de código abierto. Pero no se recomienda porque ejecuta código que usa R y Python en el equipo de SQL Server fuera de SQL Server puede provocar varios problemas:
    
  + Usar una biblioteca diferente y un ejecutable diferente y obtener resultados diferentes, que se obtienen cuando se ejecuta en SQL Server.
  + Scripts de R y Python que se ejecutan en bibliotecas externas no se puede administrar por SQL Server, dando lugar a la contención de recursos.
  
> [!IMPORTANT]
> Una vez completada la instalación, asegúrese de completar los pasos posteriores a la configuración descritos en este artículo. Estos pasos incluyen la habilitación de SQL Server puede utilizar scripts externos y agregar cuentas necesarias para que SQL Server ejecutar trabajos de R y Python en su nombre. Cambios de configuración suele ser necesitan un reinicio de la instancia o un reinicio del servicio Launchpad.

## <a name="get-the-installation-media"></a>Obtener los medios de instalación

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

## <a name="run-setup"></a>Ejecute el programa de instalación

En instalaciones locales, debe ejecutar el programa de instalación como administrador. Si instala [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde un recurso compartido remoto, deberá usar una cuenta de dominio que tenga permisos de lectura y ejecución para dicho recurso.

1. Inicie al Asistente para la instalación de SQL Server 2017. Puede descargar 
  
2. En el **instalación** ficha, seleccione **instalación independiente del nuevo servidor SQL Server o agregar características a una instalación existente**.

   ![Instalar servicios de bases de datos de aprendizaje automático](media/2017setup-installation-page-mlsvcs.PNG)
   
3. En la página **Selección de características** , seleccione estas opciones:
  
    -   **Servicios de Motor de base de datos**
  
         Para usar R y Python con SQL Server, debe instalar una instancia del motor de base de datos. Puede usar el valor predeterminado o una instancia con nombre.
  
    -   **Machine Learning Services (en base de datos)**
  
         Esta opción instala los servicios de base de datos que admiten R y la ejecución del script de Python.

    -   **R**

        Seleccione esta opción para agregar los paquetes de Microsoft R, intérprete y r de código abierto. 

    -   **Python**

        Active esta opción para agregar los paquetes de Microsoft Python, el ejecutable de Python 3.5 y seleccione las bibliotecas de la distribución de Anaconda.
        
        ![Característica de opciones de R y Python](media/2017setup-features-page-mls-rpy.png "configurar opciones de Python")

        > [!NOTE]
        > 
        > No seleccione la opción para **Server de aprendizaje de máquina (independiente)**. La opción para instalar el servidor de aprendizaje de máquina en **características compartidas** está diseñado para su uso en un equipo independiente.

4. En el **dar su consentimiento para instalar R** página, seleccione **Accept**. Este contrato de licencia cubre Microsoft R Open, que incluye una distribución de los paquetes de base de código abierto R y herramientas, junto con los paquetes de R mejorados y proveedores de conectividad desde el equipo de desarrollo de Microsoft.

5. En el **dar su consentimiento para instalar Python** página, seleccione **Accept**. El contrato de licencia de código abierto de Python también cubre la Anaconda y herramientas relacionadas, además de algunas nuevas bibliotecas de Python desde el equipo de desarrollo de Microsoft.
     
     ![Contrato de licencia de Python](media/2017setup-python-license.png "del acuerdo para Python de licencia")
  
    > [!NOTE]
    >  Si el equipo que está utilizando no tiene acceso a internet, puede pausar el programa de instalación en este momento para descargar a los instaladores por separado. Para obtener más información, consulte [instalar componentes de aprendizaje de máquina sin acceso a internet](../install/sql-ml-component-install-without-internet-access.md).
  
     Seleccione **Accept**, espere hasta que el **siguiente** botón se convierte en activa y, a continuación, seleccione **siguiente**.
  
6. En el **preparado para instalar** , comprueba que las selecciones se incluyen y seleccione **instalar**.
  
    + Servicios de Motor de base de datos
    + Machine Learning Services (en base de datos)
    + R, Python o ambos

    Tenga en cuenta la ubicación de la carpeta en la ruta de acceso `..\Setup Bootstrap\Log` donde se almacenan los archivos de configuración. Cuando finalice la instalación, puede revisar los componentes instalados en el archivo de resumen.

## <a name="restart-the-service"></a>Reinicie el servicio.

Una vez completada la instalación, reinicie el motor de base de datos antes de continuar con la siguiente, habilitar la ejecución del script.

Al reiniciar el ombre también automáticamente reinician relacionado [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] servicio.

Puede reiniciar el servicio mediante el menú contextual **reiniciar** comando para la instancia de SSMS o mediante el **servicios** en el Panel de Control, o mediante el panel [Administrador de configuración de SQL Server ](../../relational-databases/sql-server-configuration-manager.md).

## <a name="bkmk_enableFeature"></a>Habilitar la ejecución de scripts externos

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
    
3.  Para habilitar la característica de scripting externo, ejecute la siguiente instrucción:
    
    ```SQL
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
    
    No se ejecutan si ya ha habilitado la característica del lenguaje R, volver a configurar una segunda vez para Python. La plataforma de extensibilidad subyacente admite ambos lenguajes.

4. Reinicie el servicio SQL Server para la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Al reiniciar el servicio SQL Server también automáticamente reinician relacionado [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] servicio.

    Puede reiniciar el servicio mediante el menú contextual **reiniciar** comando para la instancia de SSMS o mediante el **servicios** en el Panel de Control, o mediante el panel [Administrador de configuración de SQL Server ](../../relational-databases/sql-server-configuration-manager.md).

## <a name="verify-installation"></a>Comprobar la instalación

Use los pasos siguientes para comprobar que se están ejecutando todos los componentes utilizados para iniciar scripts externos.

1. En SQL Server Management Studio, abra una nueva ventana de consulta y ejecute el siguiente comando:
    
    ```SQL
    EXEC sp_configure  'external scripts enabled'
    ```

    **run_value** debería estar establecido ahora en 1.
    
2. Abra la **servicios** panel o administrador de configuración de SQL Server y compruebe **servicio SQL Server Launchpad** está ejecutando. Debe tener un servicio para cada instancia de motor de base de datos que tenga R o Python instalado. Si no se está ejecutando, reinicie el servicio. Para obtener más información, consulte [componentes para la integración de Python](../python/new-components-in-sql-server-to-support-python-integration.md). 
   
3. Si está ejecutando Launchpad, debe ser capaz de ejecutar scripts de R y Python para comprobar que los tiempos de ejecución de secuencias de comandos externos pueden comunicarse con SQL Server.

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

    La secuencia de comandos puede tardar un poco para que se ejecute, la primera vez que se carga en tiempo de ejecución de script externo. Los resultados deben ser algo parecido a esto:

    | hello |
    |----|
    | 1|


> [!NOTE]
> Encabezados que se usa en el script de Python o columnas no se devuelven, por diseño. Para agregar nombres de columna para la salida, debe especificar el esquema para el conjunto de datos devuelto. Esto se hace mediante el parámetro con resultados del procedimiento almacenado, nombres de las columnas y especificar el tipo de datos SQL.
> 
> Por ejemplo, puede agregar la línea siguiente para generar un nombre de columna arbitrario: `WITH RESULT SETS ((Col1 AS int))`

## <a name="additional-configuration"></a>Configuración adicional

Si el paso de comprobación de script externo fue correcto, puede ejecutar comandos de Python desde SQL Server Management Studio, código de Visual Studio o cualquier otro cliente que puede enviar instrucciones T-SQL en el servidor.

Si recibe un error al ejecutar el comando, revise los pasos de configuración adicionales en esta sección. Debe realizar configuraciones adecuadas adicionales en el servicio o la base de datos.

Entre los escenarios comunes que requieren cambios adicionales se incluyen:

* [Configurar firewall de Windows para las conexiones de entrada](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)
* [Habilitar otros protocolos de red](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)
* [Habilitar las conexiones remotas](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md)
* [Ampliar los permisos integrados a los usuarios remotos](#bkmk_configureAccounts)
* [Conceder permiso para ejecutar scripts externos](#permissions-external-script)
* [Conceder acceso a bases de datos individuales](#permissions-db)

> [!NOTE]
> No todos los cambios mostrados son necesarios y ninguno puede ser necesario. Requisitos dependen de un esquema de seguridad, que se instaló SQL Server y cómo esperar a los usuarios conectarse a la base de datos y ejecutar scripts externos. Sugerencias de solución de problemas adicionales se pueden encontrar aquí: [preguntas más frecuentes de actualización e instalación](../r/upgrade-and-installation-faq-sql-server-r-services.md)

###  <a name="bkmk_configureAccounts"></a> Habilitar la autenticación implícita para el grupo de cuentas de Launchpad

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

### <a name="permissions-external-script"></a> Proporcionar a los usuarios permiso para ejecutar scripts externos

Si instaló [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usted mismo y ejecuta scripts de R o Python en su propia instancia, normalmente ejecutar secuencias de comandos como administrador. Por lo tanto, tiene permiso implícito en varias operaciones y todos los datos en la base de datos.

Sin embargo, la mayoría de los usuarios, no tiene estos permisos elevados. Por ejemplo, los usuarios de una organización que usan inicios de sesión SQL para tener acceso a la base de datos generalmente no tiene permisos elevados. Por lo tanto, para cada usuario que usa R o Python, debe conceder a los usuarios de servicios de aprendizaje de máquina el permiso para ejecutar scripts externos en cada base de datos donde se utiliza el idioma. A continuación, se indica cómo puede hacerlo.

```SQL
USE <database_name>
GO
GRANT EXECUTE ANY EXTERNAL SCRIPT  TO [UserName]
```

> [!NOTE]
> Permisos no son específicos del lenguaje de secuencia de comandos compatible. En otras palabras, no hay niveles de permisos distintos para un script de R en comparación con el script de Python. Si necesita mantener permisos independientes para estos idiomas, instalar R y Python en instancias independientes.

### <a name="permissions-db"></a> Conceder permisos de DDL (lenguaje) para las bases de datos a la definición de lectura, escritura o datos de los usuarios

Mientras un usuario ejecuta las secuencias de comandos, el usuario deba leer datos de otras bases de datos. El usuario necesite también crear nuevas tablas para almacenar los resultados y escribir datos en tablas.

Para cada cuenta de usuario de Windows o inicio de sesión SQL que ejecuta scripts de R o Python, asegúrese de que tiene los permisos adecuados en la base de datos específica: `db_datareader`, `db_datawriter`, o `db_ddladmin`.

Por ejemplo, la siguiente [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción proporciona el inicio de sesión SQL *MySQLLogin* los derechos para ejecutar consultas de T-SQL la *ML_Samples* base de datos. Para ejecutar esta instrucción, el inicio de sesión de SQL debe existir en el contexto de seguridad del servidor.

```SQL
USE ML_Samples
GO
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'
```

Para obtener más información acerca de los permisos que se incluyen en cada rol, consulte [roles de nivel de base de datos](../../relational-databases/security/authentication-access/database-level-roles.md).


### <a name="create-an-odbc-data-source-for-the-instance-on-your-data-science-client"></a>Crear un origen de datos de ODBC para la instancia en el cliente de ciencia de datos

Puede crear un solución en un equipo cliente de ciencia de datos de aprendizaje automático. Si tiene que ejecutar código con el equipo de SQL Server como el contexto de proceso, tiene dos opciones: tener acceso a la instancia mediante un inicio de sesión SQL o mediante el uso de una ventana de la cuenta.

+ Para los inicios de sesión SQL: asegúrese de que el inicio de sesión tiene los permisos adecuados en la base de datos donde está leyendo datos. Puede hacerlo agregando *conectarse a* y *seleccione* permisos, o agregando el inicio de sesión para el `db_datareader` rol. Para crear objetos, asignar `DDL_admin` derechos. Si debe guardar los datos en tablas, agregar a la `db_datawriter` rol.

+ Para la autenticación de Windows: deberá crear un origen de datos ODBC en el cliente de ciencia de datos que especifica el nombre de instancia y otra información de conexión. Para obtener más información, consulte [Administrador de orígenes de datos ODBC](https://docs.microsoft.com/sql/odbc/admin/odbc-data-source-administrator).

## <a name="suggested-optimizations"></a>Optimizaciones sugeridas

Ahora que tiene todo en funcionamiento, que le interese optimizar el servidor para admitir el aprendizaje automático o instalar previamente entrenada modelos.

### <a name="add-more-worker-accounts"></a>Agregue más cuentas de trabajo

Si se espera que muchos usuarios que se esté ejecutando secuencias de comandos al mismo tiempo, puede aumentar el número de cuentas de trabajo que están asignadas al servicio Launchpad. Para obtener más información, consulte [modificar el grupo de cuentas de usuario para servicios de aprendizaje de máquina de SQL Server](../r/modify-the-user-account-pool-for-sql-server-r-services.md).

### <a name="optimize-the-server-for-script-execution"></a>Optimizar el servidor para la ejecución de secuencias de comandos

La configuración predeterminada para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el programa de instalación están diseñados para optimizar el equilibrio del servidor para una variedad de servicios que son compatibles con el motor de base de datos, lo que puede incluir de extracción, transformación y carga (ETL) de procesos, creación de informes, auditoría, y las aplicaciones que utilizan [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] datos. Por lo tanto, la configuración predeterminada, es posible que los recursos para el aprendizaje automático a veces se restringido o limitados, especialmente en operaciones con uso intensivo de memoria.

Para garantizar que los trabajos de aprendizaje de máquina están ordenados y asignaron correctamente, se recomienda que use el regulador de recursos de SQL Server para configurar un grupo de recursos externos. También puede cambiar la cantidad de memoria que se asigna a la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] motor de base de datos o aumentar el número de cuentas que se ejecutan en el [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] service.

- Para configurar un grupo de recursos para administrar recursos externos, consulte [crear un grupo de recursos externo](../../t-sql/statements/create-external-resource-pool-transact-sql.md).
  
- Para cambiar la cantidad de memoria reservada para la base de datos, vea [opciones de configuración de memoria de servidor](../../database-engine/configure-windows/server-memory-server-configuration-options.md).
  
- Para cambiar el número de cuentas de R que se puede iniciar por [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], consulte [modificar el grupo de cuentas de usuario para el aprendizaje automático](../r/modify-the-user-account-pool-for-sql-server-r-services.md).

Si está usando Standard Edition y no tiene el regulador de recursos, puede usar vistas de administración dinámica (DMV) y eventos extendidos, así como supervisión, para ayudar a administrar los recursos del servidor de eventos de Windows. Para obtener más información, consulte [supervisión y administración de servicios de R](../r/managing-and-monitoring-r-solutions.md) y [supervisión y administración de servicios de Python](../python/managing-and-monitoring-python-solutions.md).

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

Los desarrolladores de Python pueden aprender a usar Python con SQL Server, siga estos tutoriales:

+ [Tutorial: Ejecutar Python en T-SQL](../tutorials/run-python-using-t-sql.md)
+ [Tutorial: Análisis de en bases de datos para los desarrolladores de Python](../tutorials/sqldev-in-database-python-for-sql-developers.md)

Para ver ejemplos de aprendizaje automático que se basan en situaciones del mundo real, vea [máquina tutoriales de aprendizaje](../tutorials/machine-learning-services-tutorials.md).
