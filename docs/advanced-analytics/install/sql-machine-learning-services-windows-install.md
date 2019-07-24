---
title: Instalación de SQL Server Machine Learning Services (en bases de datos) en Windows
description: R en SQL Server o Python en SQL Server pasos de instalación de SQL Server 2017 Machine Learning Services en Windows.
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/22/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 6e4d1eace0be8d00d536d1ab3782685da9512ab5
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344173"
---
# <a name="install-sql-server-machine-learning-services-on-windows"></a>Instalación de Machine Learning Services de SQL Server en Windows

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

A partir de SQL Server 2017, la compatibilidad con R y Python para el análisis en base de datos se proporciona en **SQL Server Machine Learning Services**, el sucesor de [SQL Server R Services](../r/sql-server-r-services.md) introducido en SQL Server 2016. Las bibliotecas de funciones están disponibles en R y Python y se ejecutan como scripts externos en una instancia del motor de base de datos. 

En este artículo se explica cómo instalar el componente de machine learning mediante [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] la ejecución del Asistente para la instalación de y después de los mensajes en pantalla.

## <a name="bkmk_prereqs"></a> Lista de comprobación previa a la instalación

+ Se requiere SQL Server el programa de instalación 2017 (o superior) Si desea instalar Machine Learning Services con compatibilidad con el lenguaje R o Python. Si en su lugar tiene SQL Server medio de instalación 2016, puede instalar [SQL Server 2016 R Services (en base de datos)](sql-r-services-windows-install.md) para obtener compatibilidad con el lenguaje r.

+ Se requiere una instancia del motor de base de datos. No se pueden instalar solo las características de R o Python, aunque se pueden agregar incrementalmente a una instancia existente.

+ Para la continuidad empresarial, se admiten [Always on grupos de disponibilidad](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server) para Machine Learning Services. Tiene que instalar Machine Learning Services y configurar paquetes en cada nodo.

+ La instalación de Machine Learning Services *no se admite* en un clúster de conmutación por error en SQL Server 2017. Sin embargo, *se admite* con SQL Server 2019. 
 
+ No instale Machine Learning Services en un controlador de dominio. Se producirá un error en la parte Machine Learning Services del programa de instalación.

+ No instale **las características** > compartidas**machine learning Server (independiente)** en el mismo equipo que ejecuta una instancia de en la base de datos. Un servidor independiente competirá por los mismos recursos, con lo que se descargará el rendimiento de ambas instalaciones.

+ Se admite la instalación en paralelo con otras versiones de R y Python, pero no se recomienda. Se admite porque SQL Server instancia utiliza sus propias copias de las distribuciones de R y Anaconda de código abierto. Pero no se recomienda porque la ejecución de código que usa R y Python en el SQL Server equipo fuera de SQL Server puede provocar varios problemas:
    
  + Se utiliza una biblioteca diferente y un archivo ejecutable diferente, y se obtienen resultados diferentes, que cuando se ejecuta en SQL Server.
  + Los scripts de R y Python que se ejecutan en bibliotecas externas no se pueden administrar mediante SQL Server, lo que conduce a la contención de recursos.
  
> [!IMPORTANT]
> Una vez finalizada la instalación, asegúrese de completar los pasos posteriores a la configuración que se describen en este artículo. En estos pasos se incluye la habilitación de la SQL Server para usar scripts externos y la adición de cuentas necesarias para SQL Server ejecutar trabajos de R y Python en su nombre. Normalmente, los cambios de configuración requieren un reinicio de la instancia o un reinicio del servicio Launchpad.

## <a name="get-the-installation-media"></a>Obtener los medios de instalación

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

## <a name="run-setup"></a>Ejecutar el programa de instalación

En instalaciones locales, debe ejecutar el programa de instalación como administrador. Si instala [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde un recurso compartido remoto, deberá usar una cuenta de dominio que tenga permisos de lectura y ejecución para dicho recurso.

1. Inicie el Asistente para la instalación de SQL Server 2017. 
  
2. En la pestaña **instalación** , seleccione **nuevo SQL Server instalación independiente o agregar características a una instalación existente**.

   ![Nueva instalación independiente de SQL Server](media/2017setup-installation-page-mlsvcs.PNG)
   
3. En la página **Selección de características** , seleccione estas opciones:
  
    -   **Servicios de Motor de base de datos**
  
         Para usar R y Python con SQL Server, debe instalar una instancia del motor de base de datos. Puede usar una instancia predeterminada o una instancia con nombre.
  
    -   **Machine Learning Services (en base de datos)**
  
         Esta opción instala los servicios de base de datos que admiten la ejecución de scripts de R y Python.

    -   **R**

        Active esta opción para agregar los paquetes de Microsoft R, intérprete y R de código abierto. 

    -   **Python**

        Active esta opción para agregar los paquetes de Microsoft Python, el archivo ejecutable de Python 3,5 y seleccione bibliotecas de la distribución de anaconda.
        
        ![Opciones de características para R y Python](media/2017setup-features-page-mls-rpy.png "Opciones de configuración de Python")

        > [!NOTE]
        > 
        > No seleccione la opción para **machine learning Server (independiente)** . La opción para instalar Machine Learning Server en **características** compartidas está pensada para su uso en un equipo independiente.

4. En la página **consentimiento para instalar R** , seleccione **Aceptar**. Este contrato de licencia abarca Microsoft R Open, que incluye una distribución de las herramientas y los paquetes base de R de código abierto, junto con los paquetes de R y los proveedores de conectividad mejorados del equipo de desarrollo de Microsoft.

5. En la página **consentimiento para instalar Python** , seleccione **Aceptar**. El contrato de licencia de código abierto de Python también incluye Anaconda y herramientas relacionadas, además de algunas bibliotecas de Python nuevas del equipo de desarrollo de Microsoft.
     
     ![Contrato a la licencia de Python](media/2017setup-python-license.png "Contrato de licencia para Python")
  
    > [!NOTE]
    >  Si el equipo que está usando no tiene acceso a Internet, puede pausar el programa de instalación en este momento para descargar los instaladores por separado. Para obtener más información, consulte [instalación de componentes de machine learning sin acceso a Internet](../install/sql-ml-component-install-without-internet-access.md).
  
     Seleccione **Aceptar**, espere hasta que se active el botón **siguiente** y, a continuación, seleccione **siguiente**.
  
6. En la página **listo para instalar** , compruebe que están incluidas estas selecciones y seleccione **instalar**.
  
    + Servicios de Motor de base de datos
    + Machine Learning Services (en base de datos)
    + R o Python, o ambos

    Tenga en cuenta la ubicación de la carpeta en la `..\Setup Bootstrap\Log` ruta de acceso donde se almacenan los archivos de configuración. Una vez completada la instalación, puede revisar los componentes instalados en el archivo de resumen.

7. Una vez completada la instalación, si se le indica que reinicie el equipo, hágalo ahora. Es importante leer el mensaje del Asistente para la instalación tras finalizar el programa de instalación. Para obtener más información, vea [View and Read SQL Server Setup Log Files](https://docs.microsoft.com/sql/database-engine/install-windows/view-and-read-sql-server-setup-log-files).

## <a name="set-environment-variables"></a>Establecer variables de entorno

Solo para la integración de características de R, debe establecer la variable de entorno **MKL_CBWR** para [garantizar una salida coherente](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr) de los cálculos de la biblioteca de kernels matemáticos (MKL) de Intel.

1. En el panel de control, haga clic en sistema **y seguridad** >  > **configuración** > avanzada del sistema**variables de entorno**.

2. Cree una nueva variable de usuario o del sistema. 

  + Establezca el nombre de la variable en`MKL_CBWR`
  + Establezca el valor de la variable en`AUTO`

Este paso requiere un reinicio del servidor. Si va a habilitar la ejecución de scripts, puede mantener el reinicio hasta que se realice todo el trabajo de configuración.

<a name="bkmk_enableFeature"></a>

## <a name="enable-script-execution"></a>Habilitar la ejecución de scripts

1. Abra [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. 

    > [!TIP]
    > Puede descargar e instalar la versión adecuada desde esta página: [Descargue SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).
    > 
    > También puede usar [Azure Data Studio](../../azure-data-studio/what-is.md), que admite tareas administrativas y consultas en SQL Server.
  
2. Conéctese a la instancia donde instaló Machine Learning Services, haga clic en **nueva consulta** para abrir una ventana de consulta y ejecute el siguiente comando:

    ```sql
    sp_configure
    ```

    El valor de la propiedad, `external scripts enabled`, debería ser **0** en este momento. Esto se debe a que la característica está desactivada de forma predeterminada. Un administrador debe habilitar explícitamente la característica para poder ejecutar scripts de R o Python.
    
3.  Para habilitar la característica de scripting externo, ejecute la siguiente instrucción:
    
    ```sql
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
    
    Si ya ha habilitado la característica para el lenguaje R, no ejecute volver a configurar una segunda vez para Python. La plataforma de extensibilidad subyacente es compatible con ambos lenguajes.

## <a name="restart-the-service"></a>Reinicie el servicio.

Una vez completada la instalación, reinicie el motor de base de datos antes de continuar con el siguiente, habilitando la ejecución del script.

Al reiniciar el servicio, también se reinicia automáticamente el servicio relacionado [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] .

Puede reiniciar el servicio mediante el comando de reinicio  con el botón secundario para la instancia en SSMS, o mediante el panel **servicios** del panel de Control, o mediante [Administrador de configuración de SQL Server](../../relational-databases/sql-server-configuration-manager.md).

## <a name="verify-installation"></a>Comprobar la instalación

Compruebe el estado de la instalación de la instancia en [informes personalizados](../r/monitor-r-services-using-custom-reports-in-management-studio.md) o registros de instalación.

Siga los pasos que se indican a continuación para comprobar que se están ejecutando todos los componentes que se usan para iniciar el script externo.

1. En SQL Server Management Studio, abra una nueva ventana de consulta y ejecute el siguiente comando:
    
    ```sql
    EXEC sp_configure  'external scripts enabled'
    ```

    **run_value** debería estar establecido ahora en 1.
    
2. Abra el panel **servicios** o administrador de configuración de SQL Server y compruebe que **SQL Server Launchpad servicio** se está ejecutando. Debe tener un servicio para cada instancia del motor de base de datos que tenga instalado R o Python. Para obtener más información sobre el servicio, vea [Extensibility Framework](../concepts/extensibility-framework.md). 
   
3. Si Launchpad se está ejecutando, debería poder ejecutar scripts sencillos de R y Python para comprobar que los tiempos de ejecución de scripting externos pueden comunicarse con SQL Server.

   Abra una nueva  ventana de consulta [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]en y, a continuación, ejecute un script como el siguiente:
    
    + Para R
    
    ```sql
    EXEC sp_execute_external_script  @language =N'R',
    @script=N'
    OutputDataSet <- InputDataSet;
    ',
    @input_data_1 =N'SELECT 1 AS hello'
    WITH RESULT SETS (([hello] int not null));
    GO
    ```

    + Para Python
    
    ```sql
    EXEC sp_execute_external_script  @language =N'Python',
    @script=N'
    OutputDataSet = InputDataSet;
    ',
    @input_data_1 =N'SELECT 1 AS hello'
    WITH RESULT SETS (([hello] int not null));
    GO
    ```

 **Resultado**

    El script puede tardar un poco en ejecutarse, la primera vez que se carga el tiempo de ejecución del script externo. Los resultados deben ser similares a los siguientes:

    | hello |
    |----|
    | 1|


<!--  The preceding 'hello' table is NOT rendering properly on live Docs.
Instead, the RAW markdown for the table is being displayed.  Probable bug in this markdown source,
due to stricter rules imposed by 'markdig' engine (replaced 'DFM').
I will inform HeidiSteen  [GeneMi, 2019/01/17]
-->


> [!NOTE]
> Las columnas o los encabezados usados en el script de Python no se devuelven, por diseño. Para agregar nombres de columna para la salida, debe especificar el esquema para el conjunto de datos devuelto. Para ello, use el parámetro WITH RESULTs del procedimiento almacenado, asigne un nombre a las columnas y especifique el tipo de datos SQL.
> 
> Por ejemplo, puede Agregar la siguiente línea para generar un nombre de columna arbitrario:`WITH RESULT SETS ((Col1 AS int))`

<a name="apply-cu"></a>

## <a name="apply-updates"></a>Aplicar actualizaciones

Se recomienda aplicar la última actualización acumulativa al motor de base de datos y a los componentes de aprendizaje automático.

En los dispositivos conectados a Internet, las actualizaciones acumulativas se aplican normalmente a través de Windows Update, pero también puede usar los pasos siguientes para las actualizaciones controladas. Al aplicar la actualización para el motor de base de datos, el programa de instalación extrae las actualizaciones acumulativas de las características de R o Python instaladas en la misma instancia. 

En los servidores desconectados, se requieren pasos adicionales. Para obtener más información, consulte [instalar en equipos sin acceso a internet > aplicar actualizaciones acumulativas](sql-ml-component-install-without-internet-access.md#apply-cu).

1. Comience con una instancia de línea de base ya instalada: SQL Server versión inicial 2017

2. Vaya a la lista de actualizaciones acumulativas: [SQL Server 2017 actualizaciones](https://sqlserverupdates.com/sql-server-2017-updates/)

3. Seleccione la actualización acumulativa más reciente. Un ejecutable se descarga y se extrae automáticamente.

4. Ejecute el programa de instalación. Acepte los términos de licencia y, en la página selección de características, revise las características para las que se aplican las actualizaciones acumulativas. Debería ver todas las características instaladas para la instancia actual, incluidas las características de aprendizaje automático. El programa de instalación descarga los archivos. CAB necesarios para actualizar todas las características.

  ![Resumen de las características instaladas](media/cumulative-update-feature-selection.png)

5. Continúe con el asistente y acepte los términos de licencia para las distribuciones de R y Python. 

## <a name="additional-configuration"></a>Configuración adicional

Si el paso de comprobación del script externo se realizó correctamente, puede ejecutar comandos de R o Python desde SQL Server Management Studio, Visual Studio Code o cualquier otro cliente que pueda enviar instrucciones T-SQL al servidor.

Si se produjo un error al ejecutar el comando, revise los pasos de configuración adicionales de esta sección. Es posible que tenga que crear configuraciones más adecuadas para el servicio o la base de datos.

En el nivel de instancia, la configuración adicional podría incluir:

* [Configuración del firewall para SQL Server Machine Learning Services](../../advanced-analytics/security/firewall-configuration.md)
* [Habilitar protocolos de red adicionales](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)
* [Habilitar conexiones remotas](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md)
* [Creación de un inicio de sesión para SQLRUserGroup](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md)
* [Administrar cuotas de disco](https://docs.microsoft.com/windows/desktop/fileio/managing-disk-quotas) para evitar que los scripts externos ejecuten tareas que agotan el espacio en disco

<a name="bkmk_configureAccounts"></a> 
<a name="permissions-external-script"></a> 

En la base de datos, puede que necesite las siguientes actualizaciones de configuración:

* [Conceder permiso a los usuarios para SQL Server Machine Learning Services](../../advanced-analytics/security/user-permission.md)

> [!NOTE]
> El hecho de que se requiera una configuración adicional depende del esquema de seguridad, del lugar en el que haya instalado SQL Server y de cómo espera que los usuarios se conecten a la base de datos y ejecuten scripts externos.

## <a name="suggested-optimizations"></a>Optimizaciones sugeridas

Ahora que todo funciona, puede que también desee optimizar el servidor para admitir el aprendizaje automático o instalar modelos previamente entrenados.

### <a name="add-more-worker-accounts"></a>Agregar más cuentas de trabajo

Si espera que muchos usuarios ejecuten scripts simultáneamente, puede aumentar el número de cuentas de trabajo que se asignan al servicio Launchpad. Para obtener más información, vea [modificar el grupo de cuentas de usuario para SQL Server Machine Learning Services](../administration/modify-user-account-pool.md).

### <a name="optimize-the-server-for-script-execution"></a>Optimizar el servidor para la ejecución de scripts

La configuración predeterminada del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] programa de instalación de está diseñada para optimizar el equilibrio del servidor para diversos servicios que son compatibles con el motor de base de datos, que pueden incluir procesos de extracción, transformación y carga (ETL), informes, auditorías y aplicaciones que usan [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] datos. Por lo tanto, en la configuración predeterminada, puede que los recursos del aprendizaje automático a veces se restrinjan o limiten, especialmente en las operaciones que consumen mucha memoria.

Para asegurarse de que los trabajos de machine learning se priorizan y se vuelvan a crear correctamente, se recomienda usar SQL Server Resource Governor para configurar un grupo de recursos externo. También puede cambiar la cantidad de memoria que se asigna al motor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos o aumentar el número de cuentas que se ejecutan en el [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] servicio.

- Para configurar un grupo de recursos para la administración de recursos externos, consulte [crear un grupo de recursos externos](../../t-sql/statements/create-external-resource-pool-transact-sql.md).
  
- Para cambiar la cantidad de memoria reservada para la base de datos, consulte [Opciones de configuración de memoria del servidor](../../database-engine/configure-windows/server-memory-server-configuration-options.md).
  
- Para cambiar el número de cuentas de R que puede iniciar [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], consulte [modificación del grupo de cuentas de usuario para machine learning](../administration/modify-user-account-pool.md).

Si usa la edición Standard y no tiene Resource Governor, puede usar vistas de administración dinámica (DMV) y eventos extendidos, así como la supervisión de eventos de Windows, para ayudar a administrar los recursos del servidor. Para obtener más información, consulte [supervisión y administración de R Services](../r/managing-and-monitoring-r-solutions.md) y [supervisión y administración de servicios de Python](../python/managing-and-monitoring-python-solutions.md).

### <a name="install-additional-r-packages"></a>Instalación de paquetes de R adicionales

Las soluciones de R que cree para SQL Server pueden llamar a funciones básicas de R, funciones de los paquetes de propiedad instalados con SQL Server y paquetes de R de terceros compatibles con la versión de R de código abierto instalada por SQL Server.

Los paquetes que quiera usar de SQL Server deben estar instalados en la biblioteca predeterminada que la instancia usa. Si tiene una instalación independiente de R en el equipo, o si instaló paquetes en bibliotecas de usuario, no podrá usar esos paquetes desde T-SQL.

El proceso de instalación y administración de paquetes de R es diferente en SQL Server 2016 y SQL Server 2017. En SQL Server 2016, un administrador de bases de datos debe instalar los paquetes de R que necesitan los usuarios. En SQL Server 2017, puede configurar grupos de usuarios para compartir paquetes en cada nivel de base de datos o configurar roles de base de datos para permitir que los usuarios instalen sus propios paquetes. Para obtener más información, vea [instalar nuevos paquetes de R en SQL Server](../r/install-additional-r-packages-on-sql-server.md).


## <a name="next-steps"></a>Pasos siguientes

Los desarrolladores de r pueden empezar a trabajar con algunos ejemplos sencillos y aprender los aspectos básicos de cómo funciona R con SQL Server. Para el siguiente paso, consulte los vínculos siguientes:

+ [Tutorial: Ejecutar R en T-SQL](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [Tutorial: Análisis en base de datos para desarrolladores de R](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Los desarrolladores de Python pueden aprender a usar Python con SQL Server siguiendo estos tutoriales:

+ [Tutorial: Ejecución de Python en T-SQL](../tutorials/run-python-using-t-sql.md)
+ [Tutorial: Análisis en base de datos para desarrolladores de Python](../tutorials/sqldev-in-database-python-for-sql-developers.md)

Para ver ejemplos de aprendizaje automático basados en escenarios del mundo real, consulte tutoriales de [machine learning](../tutorials/machine-learning-services-tutorials.md).
