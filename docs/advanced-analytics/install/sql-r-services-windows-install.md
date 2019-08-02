---
title: Instalar SQL Server 2016 R Services (en bases de datos)
description: Agregue compatibilidad con el lenguaje de programación R a un motor de base de datos en SQL Server 2016 R Services en Windows.
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/03/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: =sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 61dd49191e85d9fd4685904ae01b72d754d43318
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715810"
---
# <a name="install-sql-server-2016-r-services"></a>Instalación de SQL Server R Services de 2016
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo se explica cómo instalar y configurar los **servicios de SQL Server 2016 R**. Si tiene SQL Server 2016, instale esta característica para habilitar la ejecución de código de R en SQL Server.

En SQL Server 2017, la integración de R se ofrece en [Machine Learning Services](../r/r-server-standalone.md), que refleja la adición de Python. Si desea la integración de R y tiene SQL Server medio de instalación 2017, consulte [instalación de SQL Server Machine Learning Services](sql-machine-learning-services-windows-install.md) para agregar la característica. 

<a name="bkmk_prereqs"> </a> 

## <a name="pre-install-checklist"></a>Lista de comprobación previa a la instalación

+ Se requiere una instancia del motor de base de datos. No se puede instalar solo R, aunque se puede Agregar incrementalmente a una instancia existente.

+ Para la continuidad empresarial, se admiten [Always on grupos de disponibilidad](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server) para R Services. Tiene que instalar R Services y configurar paquetes en cada nodo.

+ No instale R Services en un clúster de conmutación por error. El mecanismo de seguridad que se usa para aislar los procesos de R no es compatible con un entorno de clústeres de conmutación por error de Windows Server.

+ No instale R Services en un controlador de dominio. Se producirá un error en la parte de R Services del programa de instalación.

+ No instale **las características** > compartidas**R Server (independiente)** en el mismo equipo que ejecuta una instancia de en la base de datos. 

  La instalación en paralelo con otras versiones de R y Python es posible porque la instancia de SQL Server utiliza sus propias copias de las distribuciones de R y Anaconda de código abierto. Sin embargo, la ejecución de código que usa R y Python en el SQL Server equipo fuera de SQL Server puede provocar varios problemas:
    
  + Se utiliza una biblioteca diferente y un archivo ejecutable diferente, y se obtienen resultados diferentes, que cuando se ejecuta en SQL Server.
  + Los scripts de R y Python que se ejecutan en bibliotecas externas no se pueden administrar mediante SQL Server, lo que conduce a la contención de recursos.
  
Si ha usado cualquier versión anterior del entorno de desarrollo de revolución o de los paquetes RevoScaleR, o si ha instalado alguna versión preliminar de SQL Server 2016, debe desinstalarlas. No se admite la ejecución de versiones anteriores y más recientes de RevoScaleR y otros paquetes de propiedad. Para obtener ayuda con la eliminación de versiones anteriores, consulte [preguntas más frecuentes sobre actualización e instalación de SQL Server Machine Learning Services](../r/upgrade-and-installation-faq-sql-server-r-services.md).

> [!IMPORTANT]
> Una vez finalizada la instalación, asegúrese de completar los pasos adicionales posteriores a la configuración que se describen en este artículo. En estos pasos se incluye la habilitación de la SQL Server para usar scripts externos y la adición de cuentas necesarias para SQL Server ejecutar trabajos de R en su nombre. Normalmente, los cambios de configuración requieren un reinicio de la instancia o un reinicio del servicio Launchpad.

## <a name="get-the-installation-media"></a>Obtener los medios de instalación

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

<a name="bkmk_ga_instalpatch"></a>

 ### <a name="install-patch-requirement"></a>Requisito de instalación de revisión 

Microsoft ha identificado un problema con la versión concreta de los archivos binarios en tiempo de ejecución de Microsoft VC++ 2013 que instala como requisito previo SQL Server. Si esta actualización de los archivos binarios en tiempo de ejecución de VC++ no se instala, puede que SQL Server experimente problemas de estabilidad en determinados escenarios. Antes de instalar SQL Server, siga las instrucciones de [Notas de la versión de SQL Server](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch) para ver si el equipo necesita una revisión para los archivos binarios en tiempo de ejecución de VC.  

<a name="bkmk2016top"></a>

## <a name="run-setup"></a>Ejecutar el programa de instalación

En instalaciones locales, debe ejecutar el programa de instalación como administrador. Si instala [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde un recurso compartido remoto, deberá usar una cuenta de dominio que tenga permisos de lectura y ejecución para dicho recurso.

1. Inicie el Asistente para la instalación de SQL Server 2016.

2. En la pestaña **instalación** , seleccione **nuevo SQL Server instalación independiente o agregar características a una instalación existente**.
    
   ![Instalación de R Services (en bases de datos)](media/2016-setup-installation-rsvcs.png "Iniciar la instalación del motor de base de datos con R Services")
   
3. En la página **selección de características** , seleccione las siguientes opciones:

   - Seleccione **servicios de motor de base de datos**. El motor de base de datos es necesario en cada instancia que usa el aprendizaje automático.
   - Seleccione **R Services (en base de datos)** . Instala compatibilidad con el uso en la base de datos de R.
    
     ![Selección de características de R Services](media/2016setup-rsvcs-features.png "Seleccione estas características para R Services en la base de datos")

    > [!IMPORTANT]
    > No instale R Server y R Services al mismo tiempo. Normalmente, se instala R Server (independiente) para crear un entorno que un desarrollador o científico de datos usa para conectarse a SQL Server e implementar soluciones de R. Por lo tanto, no es necesario instalar ambos en el mismo equipo.

4.  En la página **consentimiento para instalar Microsoft R Open** , haga clic en **Aceptar**.
  
    Este contrato de licencia es necesario para descargar Microsoft R Open, que incluye una distribución de las herramientas y los paquetes base de R de código abierto, junto con los paquetes de R y los proveedores de conectividad mejorados del equipo de desarrollo de Microsoft R.
  
5. Una vez que haya aceptado el contrato de licencia, habrá una breve pausa mientras se prepara el instalador. Haga clic en **siguiente** cuando el botón esté disponible.

6. En la página **listo para instalar** , compruebe que se incluyen los siguientes elementos y, a continuación, seleccione **instalar**.

   + Servicios de Motor de base de datos
   + R Services (en bases de datos)

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

##  <a name="enable-script-execution"></a>Habilitar la ejecución de scripts

1. Abra [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. 

    > [!TIP]
    > Puede descargar e instalar la versión adecuada desde esta página: [Descargue SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).
    > 
    > También puede probar la versión preliminar de [Azure Data Studio](../../azure-data-studio/what-is.md), que admite tareas administrativas y consultas en SQL Server.
  
2. Conéctese a la instancia donde instaló Machine Learning Services, haga clic en **nueva consulta** para abrir una ventana de consulta y ejecute el siguiente comando:

   ```sql
   sp_configure
   ```
    El valor de la propiedad, `external scripts enabled`, debería ser **0** en este momento. Esto se debe a que la característica está desactivada de forma predeterminada. Un administrador debe habilitar explícitamente la característica para poder ejecutar scripts de R o Python.
     
3. Para habilitar la característica de scripting externo, ejecute la siguiente instrucción:
  
    ```sql
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
  
## <a name="restart-the-service"></a>Reinicie el servicio.

Una vez completada la instalación, reinicie el motor de base de datos antes de continuar con el siguiente, habilitando la ejecución del script.

Al reiniciar el servicio, también se reinicia automáticamente el servicio relacionado [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] .

Puede reiniciar el servicio mediante el comando de reinicio con el botón secundario para la instancia en SSMS, o mediante el panel **servicios** del panel de Control, o mediante [Administrador de configuración de SQL Server](../../relational-databases/sql-server-configuration-manager.md).

## <a name="verify-installation"></a>Comprobar la instalación

Compruebe el estado de la instalación de la instancia mediante [informes personalizados](../r/monitor-r-services-using-custom-reports-in-management-studio.md).

Siga los pasos que se indican a continuación para comprobar que se están ejecutando todos los componentes que se usan para iniciar el script externo.

1. En SQL Server Management Studio, abra una nueva ventana de consulta y ejecute el siguiente comando:
    
    ```sql
    EXEC sp_configure  'external scripts enabled'
    ```

    **run_value** debería estar establecido ahora en 1.

2. Abra el panel **servicios** o administrador de configuración de SQL Server y compruebe que **SQL Server Launchpad servicio** se está ejecutando. Debe tener un servicio para cada instancia del motor de base de datos que tenga instalado R o Python. Para obtener más información sobre el servicio, vea [Extensibility Framework](../concepts/extensibility-framework.md).

7. Si Launchpad se está ejecutando, debería poder ejecutar R simple para comprobar que los Runtimes de scripting externos pueden comunicarse con SQL Server. 

    Abra una nueva ventana de consulta [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]en y, a continuación, ejecute un script como el siguiente:
    
    ```sql
    EXEC sp_execute_external_script  @language =N'R',
    @script=N'
    OutputDataSet <- InputDataSet;
    ',
    @input_data_1 =N'SELECT 1 AS hello'
    WITH RESULT SETS (([hello] int not null));
    GO
    ```

    El script puede tardar un poco en ejecutarse, la primera vez que se carga el tiempo de ejecución del script externo. Los resultados deben ser similares a los siguientes:

    | hello |
    |----|
    | 1|

<a name="apply-cu"></a>

## <a name="apply-updates"></a>Aplicar actualizaciones

Se recomienda aplicar la última actualización acumulativa al motor de base de datos y a los componentes de aprendizaje automático.

En los dispositivos conectados a Internet, las actualizaciones acumulativas se aplican normalmente a través de Windows Update, pero también puede usar los pasos siguientes para las actualizaciones controladas. Al aplicar la actualización para el motor de base de datos, el programa de instalación extrae las actualizaciones acumulativas de las bibliotecas de R instaladas en la misma instancia. 

En los servidores desconectados, se requieren pasos adicionales. Para obtener más información, consulte [instalar en equipos sin acceso a internet > aplicar actualizaciones acumulativas](sql-ml-component-install-without-internet-access.md#apply-cu).

1. Comience con una instancia de línea de base ya instalada: SQL Server versión inicial 2016, SQL Server 2016 SP 1 o SQL Server 2016 SP 2.

2. Vaya a la lista de actualizaciones acumulativas: [SQL Server 2016 actualizaciones](https://sqlserverupdates.com/sql-server-2016-updates/)

3. Seleccione la actualización acumulativa más reciente. Un ejecutable se descarga y se extrae automáticamente.

4. Ejecute el programa de instalación. Acepte los términos de licencia y, en la página selección de características, revise las características para las que se aplican las actualizaciones acumulativas. Debería ver todas las características instaladas para la instancia actual, incluido R Services. El programa de instalación descarga los archivos. CAB necesarios para actualizar todas las características.

5. Continúe con el asistente y acepte los términos de licencia de la distribución de R. 

<a name="bkmk_FollowUp"></a> 

## <a name="additional-configuration"></a>Configuración adicional

Si el paso de comprobación del script externo se realizó correctamente, puede ejecutar comandos de Python desde SQL Server Management Studio, Visual Studio Code o cualquier otro cliente que pueda enviar instrucciones T-SQL al servidor.

Si se produjo un error al ejecutar el comando, revise los pasos de configuración adicionales de esta sección. Es posible que tenga que crear configuraciones más adecuadas para el servicio o la base de datos.

En el nivel de instancia, la configuración adicional podría incluir:

* [Configuración del firewall para SQL Server Machine Learning Services](../../advanced-analytics/security/firewall-configuration.md)
* [Habilitar protocolos de red adicionales](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)
* [Habilitar conexiones remotas](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md)
* [Administrar cuotas de disco](https://docs.microsoft.com/windows/desktop/fileio/managing-disk-quotas) para evitar que los scripts externos ejecuten tareas que agotan el espacio en disco

<a name="bkmk_configureAccounts"></a>
<a name="bkmk_AllowLogon"></a>

En la base de datos, puede que necesite las siguientes actualizaciones de configuración:

* [Conceder permiso a los usuarios para SQL Server Machine Learning Services](../../advanced-analytics/security/user-permission.md)
* [Agregar SQLRUserGroup como usuario de base de datos](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md)

> [!NOTE]
> No se requieren todos los cambios enumerados y no es necesario ninguno. Los requisitos dependen del esquema de seguridad, del lugar en el que instaló SQL Server y de cómo espera que los usuarios se conecten a la base de datos y ejecuten scripts externos. Puede encontrar más sugerencias para la solución de problemas aquí: [Preguntas más frecuentes sobre actualización e instalación](../r/upgrade-and-installation-faq-sql-server-r-services.md)

## <a name="suggested-optimizations"></a>Optimizaciones sugeridas

Ahora que todo funciona, puede que también desee optimizar el servidor para admitir el aprendizaje automático o instalar modelos previamente entrenados.

### <a name="add-more-worker-accounts"></a>Agregar más cuentas de trabajo

Si cree que puede usar R de forma intensiva o si espera que muchos usuarios ejecuten scripts simultáneamente, puede aumentar el número de cuentas de trabajo que se asignan al servicio Launchpad. Para obtener más información, vea [modificar el grupo de cuentas de usuario para SQL Server Machine Learning Services](../administration/modify-user-account-pool.md).

<a name="bkmk_optimize"></a>

### <a name="optimize-the-server-for-external-script-execution"></a>Optimizar el servidor para la ejecución de scripts externos

La configuración predeterminada del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] programa de instalación de está diseñada para optimizar el equilibrio del servidor para diversos servicios que son compatibles con el motor de base de datos, que pueden incluir procesos de extracción, transformación y carga (ETL), informes, auditorías y aplicaciones que usan [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] datos. Por lo tanto, en la configuración predeterminada, puede que los recursos del aprendizaje automático a veces se restrinjan o limiten, especialmente en las operaciones que consumen mucha memoria.

Para asegurarse de que los trabajos de machine learning se priorizan y se vuelvan a crear correctamente, se recomienda usar SQL Server Resource Governor para configurar un grupo de recursos externo. También puede cambiar la cantidad de memoria que se asigna al motor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos o aumentar el número de cuentas que se ejecutan en el [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] servicio.

- Para configurar un grupo de recursos para la administración de recursos externos, consulte [crear un grupo de recursos externos](../../t-sql/statements/create-external-resource-pool-transact-sql.md).
  
- Para cambiar la cantidad de memoria reservada para la base de datos, consulte [Opciones de configuración de memoria del servidor](../../database-engine/configure-windows/server-memory-server-configuration-options.md).
  
- Para cambiar el número de cuentas de R que puede iniciar [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], consulte [modificación del grupo de cuentas de usuario para machine learning](../administration/modify-user-account-pool.md).

Si usa la edición Standard y no tiene Resource Governor, puede usar vistas de administración dinámica (DMV) y eventos extendidos, así como la supervisión de eventos de Windows, para ayudar a administrar los recursos de servidor que usa R. Para obtener más información, consulte [supervisión y administración de R Services](../r/managing-and-monitoring-r-solutions.md).

### <a name="install-additional-r-packages"></a>Instalación de paquetes de R adicionales

Las soluciones de R que cree para SQL Server pueden llamar a funciones básicas de R, funciones de los paquetes de propiedad instalados con SQL Server y paquetes de R de terceros compatibles con la versión de R de código abierto instalada por SQL Server.

Los paquetes que quiera usar de SQL Server deben estar instalados en la biblioteca predeterminada que la instancia usa. Si tiene una instalación independiente de R en el equipo, o si instaló paquetes en bibliotecas de usuario, no podrá usar esos paquetes desde T-SQL.

El proceso de instalación y administración de paquetes de R es diferente en SQL Server 2016 y SQL Server 2017. En SQL Server 2016, un administrador de bases de datos debe instalar los paquetes de R que necesitan los usuarios. En SQL Server 2017, puede configurar grupos de usuarios para compartir paquetes en cada nivel de base de datos o configurar roles de base de datos para permitir que los usuarios instalen sus propios paquetes. Para obtener más información, vea [instalar nuevos paquetes de R](../r/install-additional-r-packages-on-sql-server.md).

## <a name="next-steps"></a>Pasos siguientes

Los desarrolladores de r pueden empezar a trabajar con algunos ejemplos sencillos y aprender los aspectos básicos de cómo funciona R con SQL Server. Para el siguiente paso, consulte los vínculos siguientes:

+ [Tutorial: Ejecutar R en T-SQL](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [Tutorial: Análisis en base de datos para desarrolladores de R](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Para ver ejemplos de aprendizaje automático basados en escenarios del mundo real, consulte tutoriales de [machine learning](../tutorials/machine-learning-services-tutorials.md).