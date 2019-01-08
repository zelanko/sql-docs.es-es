---
title: 'Instalar SQL Server Machine Learning Services (en bases de datos) en Windows: SQL Server Machine Learning'
description: R en SQL Server o Python en los pasos de instalación de SQL Server para SQL Server 2017 Machine Learning Services en Windows.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/01/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 9118edd1ab25cf13cbb6d10212b50f7e7428fe9f
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/20/2018
ms.locfileid: "53645354"
---
# <a name="install-sql-server-machine-learning-services-on-windows"></a>Instalar SQL Server Machine Learning Services en Windows
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

A partir de SQL Server 2017, R y Python ofrece compatibilidad para análisis en bases de datos están en **SQL Server Machine Learning Services**, el sucesor de [SQL Server R Services](../r/sql-server-r-services.md) introducidas en SQL Server 2016. Bibliotecas de funciones están disponibles en R y Python y de identificación de script externo en una instancia del motor de base de datos. 

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

   ![Nueva instalación independiente de SQL Server](media/2017setup-installation-page-mlsvcs.PNG)
   
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

## <a name="set-environment-variables"></a>Establezca variables de entorno

Para solo integración de características de R, se debe establecer el **MKL_CBWR** variable de entorno [garantizar resultados coherentes](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr) de cálculos de Intel Math Kernel Library (MKL).

1. En el Panel de Control, haga clic en **sistema y seguridad** > **sistema** > **configuración avanzada del sistema**  >   **Las Variables de entorno**.

2. Crear una nueva variable de usuario o del sistema. 

  + Establezca el nombre de variable en `MKL_CBWR`
  + Establece el valor de la variable en `AUTO`

Este paso requiere un reinicio del servidor. Si va a habilitar la ejecución del script, puede contener en el reinicio hasta que se hace todo el trabajo de configuración.

<a name="bkmk_enableFeature"></a>

## <a name="enable-script-execution"></a>Habilitar la ejecución del script

1. Abra [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. 

    > [!TIP]
    > Puede descargar e instalar la versión adecuada de esta página: [Descargue SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).
    > 
    > También puede probar la versión preliminar de [Azure Data Studio](../../azure-data-studio/what-is.md), que es compatible con las tareas administrativas y las consultas en SQL Server.
  
2. Conéctese a la instancia donde instaló Servicios Machine Learning, haga clic en **nueva consulta** para abrir una ventana de consulta y ejecute el siguiente comando:

   ```sql
   sp_configure
   ```

    El valor de la propiedad, `external scripts enabled`, debería ser **0** en este momento. Eso es porque la característica está desactivada de forma predeterminada. La característica debe habilitarse explícitamente por un administrador para poder ejecutar scripts de R o Python.
    
3.  Para habilitar la característica de scripting externo, ejecute la siguiente instrucción:
    
    ```sql
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
    
    ```sql
    EXEC sp_configure  'external scripts enabled'
    ```

    **run_value** debería estar establecido ahora en 1.
    
2. Abra el **servicios** panel o el Administrador de configuración de SQL Server y compruebe **servicio Launchpad de SQL Server** se está ejecutando. Debe tener un servicio para cada instancia del motor de base de datos que tenga R o Python instalado. Para obtener más información sobre el servicio, consulte [Extensibility framework](../concepts/extensibility-framework.md). 
   
3. Si Launchpad se está ejecutando, debe ser capaz de ejecutar scripts de R y Python para comprobar que los tiempos de ejecución de secuencias de comandos externos pueden comunicarse con SQL Server.

   Abra una nueva **consulta** ventana en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], y, a continuación, ejecute una secuencia de comandos como la siguiente:
    
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

1. Comience con una instancia de la línea base ya instalada: Versión inicial de SQL Server 2017

2. Vaya a la lista de actualización acumulativa: [Actualizaciones de SQL Server 2017](https://sqlserverupdates.com/sql-server-2017-updates/)

3. Seleccione la actualización acumulativa más reciente. Un archivo ejecutable se descargan y extraen automáticamente.

4. Ejecute el programa de instalación. Acepte los términos de licencia y, en la página de selección de características, revise las características para el que se aplican las actualizaciones acumulativas. Debería ver todas las características instaladas para la instancia actual, incluidas características de aprendizaje automático. Programa de instalación descarga los archivos CAB necesarios para actualizar todas las características.

  ![Resumen de las características instaladas](media/cumulative-update-feature-selection.png)

5. Continúe con el asistente, acepte los términos de licencia para las distribuciones de R y Python. 

## <a name="additional-configuration"></a>Configuración adicional

Si el paso de comprobación de script externo se realizó correctamente, puede ejecutar comandos de R o Python de SQL Server Management Studio, Visual Studio Code o cualquier otro cliente que puede enviar instrucciones T-SQL al servidor.

Si recibe un error al ejecutar el comando, revise los pasos de configuración adicionales en esta sección. Es posible que deba realizar configuraciones adecuadas adicionales en el servicio o la base de datos.

En el nivel de instancia, podría incluir una configuración adicional:

* [Configuración de Firewall para SQL Server Machine Learning Services](../../advanced-analytics/security/firewall-configuration.md)
* [Habilitar los protocolos de red adicionales](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)
* [Habilitar conexiones remotas](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md)

<a name="bkmk_configureAccounts"></a> 
<a name="permissions-external-script"></a> 

En la base de datos, puede que necesite las actualizaciones de configuración siguientes:

* [Proporcionar a los usuarios permiso para SQL Server Machine Learning Services](../../advanced-analytics/security/user-permission.md)
* [Agregar SQLRUserGroup como usuario de base de datos](../../advanced-analytics/security/add-sqlrusergroup-to-database.md)

> [!NOTE]
> Si se requiere configuración adicional depende del esquema de seguridad, que se instaló SQL Server y cómo se espera que los usuarios conectarse a la base de datos y ejecutar scripts externos.

## <a name="suggested-optimizations"></a>Optimizaciones sugeridas

Ahora que tiene todo funcione, es posible que también desea optimizar el servidor para admitir el aprendizaje automático o modelos previamente aprendidos install.

### <a name="add-more-worker-accounts"></a>Agregar más cuentas de trabajo

Si espera que muchos usuarios para ejecutar scripts al mismo tiempo, puede aumentar el número de cuentas de trabajo que están asignadas al servicio Launchpad. Para obtener más información, consulte [modificar el grupo de cuentas de usuario de SQL Server Machine Learning Services](../administration/modify-user-account-pool.md).

### <a name="optimize-the-server-for-script-execution"></a>Optimizar el servidor para la ejecución del script

La configuración predeterminada para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el programa de instalación está diseñada para optimizar el equilibrio entre el servidor para una variedad de servicios que son compatibles con el motor de base de datos, lo que puede incluir la extracción, transformación y carga (ETL) de procesos, generación de informes, auditoría, y las aplicaciones que usan [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] datos. Por lo tanto, en la configuración predeterminada, es posible que los recursos para el aprendizaje automático son a veces restringidos o limitados, especialmente en operaciones de gran cantidad de memoria.

Para asegurarse de que los trabajos de machine learning son prioridades y recursos correctos, se recomienda que use el regulador de recursos de SQL Server para configurar un grupo de recursos externos. También puede cambiar la cantidad de memoria que se asigna a la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] motor de base de datos o aumentar el número de cuentas que se ejecutan bajo el [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] service.

- Para configurar un grupo de recursos para administrar los recursos externos, consulte [crear un grupo de recursos externos](../../t-sql/statements/create-external-resource-pool-transact-sql.md).
  
- Para cambiar la cantidad de memoria reservada para la base de datos, vea [opciones de configuración de memoria de servidor](../../database-engine/configure-windows/server-memory-server-configuration-options.md).
  
- Para cambiar el número de cuentas de R que se pueda iniciar por [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], consulte [modificar el grupo de cuentas de usuario para el aprendizaje automático](../administration/modify-user-account-pool.md).

Si está utilizando Standard Edition y no tiene el regulador de recursos, puede usar vistas de administración dinámica (DMV) y eventos extendidos, así como supervisión, para ayudar a administrar los recursos del servidor de eventos de Windows. Para obtener más información, consulte [supervisión y administración de servicios de R](../r/managing-and-monitoring-r-solutions.md) y [supervisión y administración de servicios de Python](../python/managing-and-monitoring-python-solutions.md).

### <a name="install-additional-r-packages"></a>Instalar paquetes de R adicionales

Las soluciones de R que se crea para SQL Server pueden llamar a funciones de R básicas, las funciones de la propiedad paquetes instalados con SQL Server y paquetes de R de terceros compatible con la versión de R de código abierto que se instala con SQL Server.

Los paquetes que quiera usar de SQL Server deben estar instalados en la biblioteca predeterminada que la instancia usa. Si tiene una instalación independiente de R en el equipo, o si ha instalado paquetes en bibliotecas de usuario, no podrá usar esos paquetes desde T-SQL.

El proceso para instalar y administrar paquetes de R es diferente en SQL Server 2016 y SQL Server 2017. En SQL Server 2016, un administrador de base de datos debe instalar los paquetes de R que necesitan los usuarios. En SQL Server 2017, puede configurar grupos de usuarios para compartir paquetes en un nivel por base de datos, o configurar roles de base de datos para permitir que los usuarios instalar sus propios paquetes. Para obtener más información, consulte [instalar nuevos paquetes de R en SQL Server](../r/install-additional-r-packages-on-sql-server.md).


## <a name="next-steps"></a>Pasos siguientes

Los desarrolladores de R pueden empezar a trabajar con algunos ejemplos sencillos y conozca los aspectos básicos del funcionamiento de R con SQL Server. Para el siguiente paso, vea los siguientes vínculos:

+ [Tutorial: Ejecutar R en T-SQL](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [Tutorial: Análisis en bases de datos para los desarrolladores de R](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Los desarrolladores de Python pueden aprender a usar Python con SQL Server, siga estos tutoriales:

+ [Tutorial: Ejecución de Python en T-SQL](../tutorials/run-python-using-t-sql.md)
+ [Tutorial: Análisis en bases de datos para desarrolladores de Python](../tutorials/sqldev-in-database-python-for-sql-developers.md)

Para ver ejemplos de aprendizaje automático que se basan en escenarios del mundo real, consulte [tutoriales de aprendizaje automático](../tutorials/machine-learning-services-tutorials.md).
