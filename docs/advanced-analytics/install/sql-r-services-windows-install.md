---
title: 'Instalar SQL Server 2016 R Services (en bases de datos): SQL Server Machine Learning'
description: Agregar compatibilidad de idioma a un motor de base de datos en SQL Server 2016 R Services en Windows de programación R.
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/03/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 439ce4388f03422be40c9b35fa4a5d4e3dbf5299
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962842"
---
# <a name="install-sql-server-2016-r-services"></a>Instalar SQL Server 2016 R Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo se explica cómo instalar y configurar **SQL Server 2016 R Services**. Si tiene SQL Server 2016, instale esta característica para habilitar la ejecución del código de R en SQL Server.

En SQL Server 2017, se ofrece la integración de R en [Machine Learning Services](../r/r-server-standalone.md), que refleja la adición de Python. Si desea una integración de R y tiene los medios de instalación de SQL Server 2017, consulte [instalar SQL Server 2017 Machine Learning Services](sql-machine-learning-services-windows-install.md) para agregar la característica. 

<a name="bkmk_prereqs"> </a> 

## <a name="pre-install-checklist"></a>Lista de comprobación previa a la instalación

+ Se requiere una instancia del motor de base de datos. No se puede instalar solo R, aunque se puede agregar gradualmente a una instancia existente.

+ Para la continuidad empresarial, [siempre en grupos de disponibilidad:](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server) son compatibles con R Services. Tendrá que instalar R Services y configurar paquetes, en cada nodo.

+ No instale R Services en un clúster de conmutación por error. El mecanismo de seguridad que se usa para aislar los procesos de R no es compatible con un entorno de clúster de conmutación por error de Windows Server.

+ No instale R Services en un controlador de dominio. Se producirá un error en la parte de los servicios de R del programa de instalación.

+ No instale **características compartidas** > **R Server (independiente)** en el mismo equipo que ejecuta una instancia de base de datos. 

  Instalación en paralelo con otras versiones de R y Python son posibles porque la instancia de SQL Server usa sus propias copias de las distribuciones de R y Anaconda de código abierto. Sin embargo, ejecutar código que usa R y Python en el equipo de SQL Server fuera de SQL Server puede provocar varios problemas:
    
  + Usar un ejecutable diferente y una biblioteca diferente y obtener resultados diferentes, que se obtienen cuando se ejecuta en SQL Server.
  + No puede administrar los scripts de R y Python que se ejecutan en bibliotecas externas de SQL Server, dando lugar a la contención de recursos.
  
Si usa las versiones anteriores de los paquetes RevoScaleR o el entorno de desarrollo Revolution Analytics, o si ha instalado todas las versiones preliminares de SQL Server 2016, debe desinstalarlas. No se admite la ejecución de las versiones anteriores y recientes de RevoScaleR y otros paquetes de propiedad. Para obtener ayuda con la eliminación de las versiones anteriores, consulte [actualización y p+f sobre la instalación de SQL Server Machine Learning Services](../r/upgrade-and-installation-faq-sql-server-r-services.md).

> [!IMPORTANT]
> Una vez completada la instalación, asegúrese de completar los pasos posteriores a la configuración adicionales que se describe en este artículo. Estos pasos incluyen habilitar SQL Server puede utilizar scripts externos y cómo agregar cuentas necesarias para que SQL Server ejecutar trabajos de R en su nombre. Los cambios de configuración generalmente requieren un reinicio de la instancia o un reinicio del servicio Launchpad.

## <a name="get-the-installation-media"></a>Obtener los medios de instalación

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

<a name="bkmk_ga_instalpatch"></a>

 ### <a name="install-patch-requirement"></a>Instale el requisito de revisión 

Microsoft ha identificado un problema con la versión concreta de los archivos binarios en tiempo de ejecución de Microsoft VC++ 2013 que instala como requisito previo SQL Server. Si esta actualización de los archivos binarios en tiempo de ejecución de VC++ no se instala, puede que SQL Server experimente problemas de estabilidad en determinados escenarios. Antes de instalar SQL Server, siga las instrucciones de [Notas de la versión de SQL Server](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch) para ver si el equipo necesita una revisión para los archivos binarios en tiempo de ejecución de VC.  

<a name="bkmk2016top"></a>

## <a name="run-setup"></a>Ejecute el programa de instalación

En instalaciones locales, debe ejecutar el programa de instalación como administrador. Si instala [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde un recurso compartido remoto, deberá usar una cuenta de dominio que tenga permisos de lectura y ejecución para dicho recurso.

1. Iniciar al Asistente para la instalación de SQL Server 2016.

2. En el **instalación** ficha, seleccione **instalación independiente del nuevo servidor SQL Server o agregar características a una instalación existente**.
    
   ![Instalar R Services (In-Database)](media/2016-setup-installation-rsvcs.png "Iniciar instalación del motor de base de datos con R Services")
   
3. En el **selección de características** página, seleccione las opciones siguientes:

   - Seleccione **servicios de motor de base de datos**. Se requiere el motor de base de datos en cada instancia que utiliza aprendizaje automático.
   - Seleccione **R Services (en bases de datos)** . Instala compatibilidad para su uso en bases de datos de R.
    
     ![Selección de características de R Services](media/2016setup-rsvcs-features.png "seleccione estas características para R Services en bases de datos")

    > [!IMPORTANT]
    > No instale el servidor de R y R Services al mismo tiempo. Normalmente, podría instalar a R Server (independiente) para crear un entorno que un desarrollador o científico de datos que se usa para conectarse a SQL Server e implementar soluciones de R. Por lo tanto, no es necesario instalar ambos en el mismo equipo.

4.  En el **da su consentimiento para instalar Microsoft R Open** página, haga clic en **Accept**.
  
    Este contrato de licencia es necesario para descargar Microsoft R Open, que incluye una distribución de los paquetes base de código abierto R y herramientas, junto con los paquetes de R mejorados y proveedores de conectividad desde el equipo de desarrollo de Microsoft R.
  
5. Una vez que ha aceptado el contrato de licencia, hay una breve pausa mientras se prepara el instalador. Haga clic en **siguiente** cuando esté disponible el botón.

6. En el **preparado para instalar** , comprueba que se incluyen los siguientes elementos y, a continuación, seleccione **instalar**.

   + Servicios de Motor de base de datos
   + R Services (en bases de datos)

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

##  <a name="enable-script-execution"></a>Habilitar la ejecución del script

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
     
3. Para habilitar la característica de scripting externo, ejecute la siguiente instrucción:
  
    ```sql
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
  
## <a name="restart-the-service"></a>Reinicie el servicio.

Una vez completada la instalación, reinicie el motor de base de datos antes de continuar con la siguiente, habilitar la ejecución del script.

Reiniciar automáticamente el servicio reinicia relacionado [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] service.

Puede reiniciar el servicio con el botón secundario **reiniciar** comando de la instancia en SSMS o mediante el uso de la **servicios** panel en el Panel de Control o mediante el uso de [Administrador de configuración de SQL Server ](../../relational-databases/sql-server-configuration-manager.md).

## <a name="verify-installation"></a>Comprobar la instalación

Comprobar el estado de instalación de la instancia mediante [informes personalizados](../r/monitor-r-services-using-custom-reports-in-management-studio.md).

Use los pasos siguientes para comprobar que se están ejecutando todos los componentes utilizados para iniciar scripts externos.

1. En SQL Server Management Studio, abra una nueva ventana de consulta y ejecute el siguiente comando:
    
    ```sql
    EXEC sp_configure  'external scripts enabled'
    ```

    **run_value** debería estar establecido ahora en 1.

2. Abra el **servicios** panel o el Administrador de configuración de SQL Server y compruebe **servicio Launchpad de SQL Server** se está ejecutando. Debe tener un servicio para cada instancia del motor de base de datos que tenga R o Python instalado. Para obtener más información sobre el servicio, consulte [Extensibility framework](../concepts/extensibility-framework.md).

7. Si Launchpad se está ejecutando, debe ser capaz de ejecutar R simple para comprobar que los tiempos de ejecución de secuencias de comandos externos pueden comunicarse con SQL Server. 

    Abra una nueva **consulta** ventana en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], y, a continuación, ejecute una secuencia de comandos como la siguiente:
    
    ```sql
    EXEC sp_execute_external_script  @language =N'R',
    @script=N'
    OutputDataSet <- InputDataSet;
    ',
    @input_data_1 =N'SELECT 1 AS hello'
    WITH RESULT SETS (([hello] int not null));
    GO
    ```

    El script puede tardar unos instantes para ejecutar la primera vez que se carga el tiempo de ejecución de scripts externos. Los resultados deben ser algo parecido a esto:

    | hello |
    |----|
    | 1|

<a name="apply-cu"></a>

## <a name="apply-updates"></a>Aplicar actualizaciones

Se recomienda que aplique la actualización acumulativa más reciente para el motor de base de datos y los componentes de aprendizaje automático.

En los dispositivos conectados a internet, normalmente se aplican las actualizaciones acumulativas a través de Windows Update, pero también puede usar los pasos siguientes para las actualizaciones controladas. Al aplicar la actualización para el motor de base de datos, el programa de instalación extrae las actualizaciones acumulativas para bibliotecas de R que instaló en la misma instancia. 

En los servidores sin conexión, se necesitan pasos adicionales. Para obtener más información, consulte [instalar en equipos sin acceso a internet > aplicar actualizaciones acumulativas](sql-ml-component-install-without-internet-access.md#apply-cu).

1. Comience con una instancia de la línea base ya instalada: Versión inicial de SQL Server 2016, SQL Server 2016 Service Pack 1 o SQL Server 2016 Service Pack 2.

2. Vaya a la lista de actualización acumulativa: [Actualizaciones de SQL Server 2016](https://sqlserverupdates.com/sql-server-2016-updates/)

3. Seleccione la actualización acumulativa más reciente. Un archivo ejecutable se descargan y extraen automáticamente.

4. Ejecute el programa de instalación. Acepte los términos de licencia y, en la página de selección de características, revise las características para el que se aplican las actualizaciones acumulativas. Debería ver todas las características instaladas para la instancia actual, incluidos los servicios de R. Programa de instalación descarga los archivos CAB necesarios para actualizar todas las características.

5. Continúe con el asistente, acepte los términos de licencia para la distribución de R. 

<a name="bkmk_FollowUp"></a> 

## <a name="additional-configuration"></a>Configuración adicional

Si el paso de comprobación de script externo se realizó correctamente, puede ejecutar comandos de Python de SQL Server Management Studio, Visual Studio Code o cualquier otro cliente que puede enviar instrucciones T-SQL al servidor.

Si recibe un error al ejecutar el comando, revise los pasos de configuración adicionales en esta sección. Es posible que deba realizar configuraciones adecuadas adicionales en el servicio o la base de datos.

En el nivel de instancia, podría incluir una configuración adicional:

* [Configuración de Firewall para SQL Server Machine Learning Services](../../advanced-analytics/security/firewall-configuration.md)
* [Habilitar los protocolos de red adicionales](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)
* [Habilitar conexiones remotas](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md)
* [Administrar las cuotas de disco](https://docs.microsoft.com/windows/desktop/fileio/managing-disk-quotas) para evitar scripts externos que se ejecutan las tareas que se agote el espacio en disco

<a name="bkmk_configureAccounts"></a>
<a name="bkmk_AllowLogon"></a>

En la base de datos, puede que necesite las actualizaciones de configuración siguientes:

* [Proporcionar a los usuarios permiso para SQL Server Machine Learning Services](../../advanced-analytics/security/user-permission.md)
* [Agregar SQLRUserGroup como usuario de base de datos](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md)

> [!NOTE]
> No todos los cambios enumerados son necesarios, y ninguno puede ser necesario. Requisitos dependen de su esquema de seguridad, donde instaló SQL Server y cómo se espera que los usuarios conectarse a la base de datos y ejecutar scripts externos. Sugerencias de solución de problemas adicionales pueden encontrarse aquí: [Preguntas más frecuentes sobre actualización e instalación](../r/upgrade-and-installation-faq-sql-server-r-services.md)

## <a name="suggested-optimizations"></a>Optimizaciones sugeridas

Ahora que tiene todo funcione, es posible que también desea optimizar el servidor para admitir el aprendizaje automático o modelos previamente aprendidos install.

### <a name="add-more-worker-accounts"></a>Agregar más cuentas de trabajo

Si piensa que es posible que uso intensivo de R, o si se prevé que muchos usuarios van a ejecutar scripts al mismo tiempo, puede aumentar el número de cuentas de trabajo que están asignadas al servicio Launchpad. Para obtener más información, consulte [modificar el grupo de cuentas de usuario de SQL Server Machine Learning Services](../administration/modify-user-account-pool.md).

<a name="bkmk_optimize"></a>

### <a name="optimize-the-server-for-external-script-execution"></a>Optimizar el servidor para la ejecución de scripts externos

La configuración predeterminada para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el programa de instalación está diseñada para optimizar el equilibrio entre el servidor para una variedad de servicios que son compatibles con el motor de base de datos, lo que puede incluir la extracción, transformación y carga (ETL) de procesos, generación de informes, auditoría, y las aplicaciones que usan [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] datos. Por lo tanto, en la configuración predeterminada, es posible que los recursos para el aprendizaje automático son a veces restringidos o limitados, especialmente en operaciones de gran cantidad de memoria.

Para asegurarse de que los trabajos de machine learning son prioridades y recursos correctos, se recomienda que use el regulador de recursos de SQL Server para configurar un grupo de recursos externos. También puede cambiar la cantidad de memoria que se asigna a la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] motor de base de datos o aumentar el número de cuentas que se ejecutan bajo el [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] service.

- Para configurar un grupo de recursos para administrar los recursos externos, consulte [crear un grupo de recursos externos](../../t-sql/statements/create-external-resource-pool-transact-sql.md).
  
- Para cambiar la cantidad de memoria reservada para la base de datos, vea [opciones de configuración de memoria de servidor](../../database-engine/configure-windows/server-memory-server-configuration-options.md).
  
- Para cambiar el número de cuentas de R que se pueda iniciar por [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], consulte [modificar el grupo de cuentas de usuario para el aprendizaje automático](../administration/modify-user-account-pool.md).

Si está utilizando Standard Edition y no tiene el regulador de recursos, puede usar vistas de administración dinámica (DMV) y eventos extendidos, así como supervisión, para ayudar a administrar los recursos del servidor que usan R. de eventos de Windows Para obtener más información, consulte [supervisión y administración de servicios de R](../r/managing-and-monitoring-r-solutions.md).

### <a name="install-additional-r-packages"></a>Instalar paquetes de R adicionales

Las soluciones de R que se crea para SQL Server pueden llamar a funciones de R básicas, las funciones de la propiedad paquetes instalados con SQL Server y paquetes de R de terceros compatible con la versión de R de código abierto que se instala con SQL Server.

Los paquetes que quiera usar de SQL Server deben estar instalados en la biblioteca predeterminada que la instancia usa. Si tiene una instalación independiente de R en el equipo, o si ha instalado paquetes en bibliotecas de usuario, no podrá usar esos paquetes desde T-SQL.

El proceso para instalar y administrar paquetes de R es diferente en SQL Server 2016 y SQL Server 2017. En SQL Server 2016, un administrador de base de datos debe instalar los paquetes de R que necesitan los usuarios. En SQL Server 2017, puede configurar grupos de usuarios para compartir paquetes en un nivel por base de datos, o configurar roles de base de datos para permitir que los usuarios instalar sus propios paquetes. Para obtener más información, consulte [instalar nuevos paquetes de R](../r/install-additional-r-packages-on-sql-server.md).

## <a name="next-steps"></a>Pasos siguientes

Los desarrolladores de R pueden empezar a trabajar con algunos ejemplos sencillos y conozca los aspectos básicos del funcionamiento de R con SQL Server. Para el siguiente paso, vea los siguientes vínculos:

+ [Tutorial: Ejecutar R en T-SQL](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [Tutorial: Análisis en bases de datos para los desarrolladores de R](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Para ver ejemplos de aprendizaje automático que se basan en escenarios del mundo real, consulte [tutoriales de aprendizaje automático](../tutorials/machine-learning-services-tutorials.md).