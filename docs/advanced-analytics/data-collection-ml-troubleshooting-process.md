---
title: Solución de problemas de recopilación de datos para machine learning
ms.prod: sql
ms.technology: machine-learning
ms.date: 02/28/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: f7d5e39d0ca0a89312a6fefd261eff950859d0a2
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/19/2019
ms.locfileid: "68343389"
---
# <a name="troubleshoot-data-collection-for-machine-learning"></a>Solución de problemas de recopilación de datos para machine learning

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo se describen los métodos de recopilación de datos que debe usar al intentar resolver problemas por su cuenta o con la ayuda del servicio de soporte al cliente de Microsoft.

**Se aplica a:** SQL Server 2016 R Services, SQL Server 2017 Machine Learning Services (R y Python)

## <a name="sql-server-version-and-edition"></a>Versión y edición de SQL Server

SQL Server 2016 R Services es la primera versión de SQL Server para incluir compatibilidad integrada con R. SQL Server 2016 Service Pack 1 (SP1) incluye varias mejoras importantes, incluida la capacidad de ejecutar scripts externos. Si es un cliente de SQL Server 2016, considere la posibilidad de instalar SP1 o posterior.

SQL Server 2017 agregó la integración del lenguaje Python. No se puede obtener la integración de características de Python en versiones anteriores.

Para obtener ayuda para obtener ediciones y versiones, consulte este artículo, donde se enumeran los números de compilación de cada una de las [versiones SQL Server](https://social.technet.microsoft.com/wiki/contents/articles/783.sql-server-versions.aspx#Service_Pack_editions).

En función de la edición de SQL Server esté usando, es posible que algunas funciones de aprendizaje automático no estén disponibles o estén limitadas. En los artículos siguientes se muestra una lista de características de machine learning en las ediciones Enterprise, Developer, Standard y Express.

* [Ediciones y características admitidas de SQL Server](https://docs.microsoft.com/sql/sql-server/editions-and-components-of-sql-server-2016)
* [Características de R y Python por ediciones de SQL Server](r/differences-in-r-features-between-editions-of-sql-server.md)

## <a name="r-language-and-tool-versions"></a>Versiones del lenguaje y las herramientas de R

En general, la versión de Microsoft R que se instala al seleccionar la característica R Services o la característica Machine Learning Services está determinada por el número de compilación SQL Server. Si actualiza SQL Server, también debe actualizar o aplicar revisiones a sus componentes de R.

Para obtener una lista de las versiones y vínculos a las descargas de componentes de R, consulte [instalación de componentes de machine learning sin acceso a Internet](https://docs.microsoft.com/sql/advanced-analytics/r/installing-ml-components-without-internet-access). En los equipos con acceso a Internet, la versión necesaria de R se identifica y se instala automáticamente.

Es posible actualizar los componentes de R Server de forma independiente del motor de base de datos de SQL Server, en un proceso conocido como enlace. Por lo tanto, la versión de R que use al ejecutar el código de R en SQL Server podría variar en función de la versión instalada de SQL Server y de si migró el servidor a la versión más reciente de R.

### <a name="determine-the-r-version"></a>Determinar la versión de R

La forma más fácil de determinar la versión de R es obtener las propiedades en tiempo de ejecución mediante la ejecución de una instrucción como la siguiente:

```sql
exec sp_execute_external_script
       @language = N'R'
       , @script = N'
# Transform R version properties to data.frame
OutputDataSet <- data.frame(
  property_name = c("R.version", "Revo.version"),
  property_value = c(R.Version()$version.string, Revo.version$version.string),
  stringsAsFactors = FALSE)
# Retrieve properties like R.home, libPath & default packages
OutputDataSet <- rbind(OutputDataSet, data.frame(
  property_name = c("R.home", "libPaths", "defaultPackages"),
  property_value = c(R.home(), .libPaths(), paste(getOption("defaultPackages"), collapse=", ")),
  stringsAsFactors = FALSE)
)
'
WITH RESULT SETS ((PropertyName nvarchar(100), PropertyValue nvarchar(4000)));

```

> [!TIP]
> Si R Services no funciona, intente ejecutar solo la parte del script de R desde RGui.

Como último recurso, puede abrir archivos en el servidor para determinar la versión instalada. Para ello, busque el archivo rlauncher. config para obtener la ubicación del tiempo de ejecución de R y el directorio de trabajo actual. Se recomienda que cree y abra una copia del archivo para que no cambie accidentalmente ninguna propiedad.

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name\MSSQL\Binn\rlauncher.config`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\MSSQL\Binn\rlauncher.config`

Para obtener la versión de R y las versiones de RevoScaleR, abra un símbolo del sistema de R o abra el RGui asociado a la instancia.

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.<instancename>\R_SERVICES\bin\x64\RGui.exe`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\R_SERVICES\bin\x64\RGui.exe`

La consola de R muestra la información de versión en el inicio. Por ejemplo, la siguiente versión representa la configuración predeterminada para SQL Server 2017:

    *Microsoft R Open 3.3.3*

    *The enhanced R distribution from Microsoft*

    *Microsoft packages Copyright (C) 2017 Microsoft*

    *Loading Microsoft R Server packages, version 9.1.0.*

## <a name="python-versions"></a>Versiones de Python

Hay varias maneras de obtener la versión de Python. La manera más fácil es ejecutar esta instrucción desde Management Studio o cualquier otra herramienta de consulta SQL:

```sql
-- Get Python runtime properties:
exec sp_execute_external_script
       @language = N'Python'
       , @script = N'
import sys
import pkg_resources
OutputDataSet = pandas.DataFrame(
                    {"property_name": ["Python.home", "Python.version", "Revo.version", "libpaths"],
                    "property_value": [sys.executable[:-10], sys.version, pkg_resources.get_distribution("revoscalepy").version, str(sys.path)]}
)
'
with WITH RESULT SETS (SQL keywords) ((PropertyName nvarchar(100), PropertyValue nvarchar(4000)));
```

Si Machine Learning Services no se está ejecutando, puede determinar la versión de Python instalada examinando el archivo pythonlauncher. config. Se recomienda que cree y abra una copia del archivo para que no cambie accidentalmente ninguna propiedad.

1. Solo para SQL Server 2017:`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\MSSQL\Log\ExtensibilityLog\pythonlauncher.config`
2. Obtiene el valor de **PYTHONHOME**.
3. Obtiene el valor del directorio de trabajo actual.

> [!NOTE]
> Si ha instalado Python y R en SQL Server 2017, el directorio de trabajo y el grupo de cuentas de trabajo se comparten para los idiomas R y Python.

## <a name="are-multiple-instances-of-r-or-python-installed"></a>¿Hay varias instancias de R o Python instaladas?

Compruebe si hay más de una copia de las bibliotecas de R instalada en el equipo. Esta duplicación puede producirse si:

* Durante la instalación, seleccione R Services (en base de datos) y R Server (independiente).
* Instale Microsoft R Client además de SQL Server.
* Se instaló un conjunto diferente de bibliotecas de R mediante Herramientas de R para Visual Studio, R Studio, Microsoft R Client u otro IDE de R.
* El equipo hospeda varias instancias de SQL Server y más de una instancia usa el aprendizaje automático.

Se aplican las mismas condiciones a Python.

Si observa que hay instaladas varias bibliotecas o tiempos de ejecución, asegúrese de que obtiene solo los errores asociados a los tiempos de ejecución de Python o R utilizados por la instancia de SQL Server.

## <a name="origin-of-errors"></a>Origen de los errores

Los errores que se ven al intentar ejecutar el código de R pueden provienen de cualquiera de los orígenes siguientes:

* SQL Server motor de base de datos, incluido el procedimiento almacenado sp_execute_external_script
* SQL Server Launchpad de confianza
* Otros componentes de la plataforma de extensibilidad, incluidos los iniciadores de R y Python y los procesos satélite
* Proveedores, como Microsoft Open Database Connectivity (ODBC)
* Lenguaje R

Cuando se trabaja con el servicio por primera vez, puede resultar difícil saber qué mensajes proceden de los servicios. Se recomienda capturar no solo el texto exacto del mensaje, sino el contexto en el que vio el mensaje. Anote el software cliente que está usando para ejecutar el código de aprendizaje automático:

* ¿Usa Management Studio? ¿Una aplicación externa?
* ¿Está ejecutando código R en un cliente remoto o directamente en un procedimiento almacenado?

## <a name="sql-server-log-files"></a>Archivos de registro de SQL Server

Obtiene el SQL Server de errores más reciente. El conjunto completo de registros de errores consta de los archivos del siguiente directorio de registro predeterminado:

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.SQL2016\MSSQL\Log\ExtensibilityLog`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.SQL2016\MSSQL\Log\ExtensibilityLog`

> [!NOTE]
> El nombre exacto de la carpeta varía en función del nombre de la instancia.

## <a name="errors-returned-by-spexecuteexternalscript"></a>Errores devueltos por sp_execute_external_script

Obtiene el texto completo de los errores que se devuelven, si los hay, al ejecutar el comando sp_execute_external_script.

Para quitar los problemas de R o Python de tener en cuenta, puede ejecutar este script, que inicia el tiempo de ejecución de R o Python y pasa los datos de un y otro.

**Para R**

```sql
exec sp_execute_external_script @language =N'R',  
@script=N'OutputDataSet<-InputDataSet',  
@input_data_1 =N'select 1 as hello'  
with result sets (([hello] int not null));  
go
```

**Para Python**

```sql
exec sp_execute_external_script @language =N'Python',  
@script=N'OutputDataSet= InputDataSet',  
@input_data_1 =N'select 1 as hello'  
with result sets (([hello] int not null));  
go
```

## <a name="errors-generated-by-the-extensibility-framework"></a>Errores generados por el marco de extensibilidad

SQL Server genera registros independientes para los tiempos de ejecución del lenguaje de script externo. Estos errores no se generan con el lenguaje Python o R. Se generan a partir de los componentes de extensibilidad en SQL Server, incluidos los iniciadores específicos del idioma y sus procesos satélite.

Puede obtener estos registros desde las siguientes ubicaciones predeterminadas:

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\MSSQL\Log\ExtensibilityLog`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\MSSQL\Log\ExtensibilityLog`

> [!NOTE]
> El nombre exacto de la carpeta difiere en función del nombre de la instancia. En función de la configuración, la carpeta podría estar en una unidad diferente.

Por ejemplo, los siguientes mensajes de registro están relacionados con el marco de extensibilidad:

* *Error de LogonUser para el usuario MSSQLSERVER01*
  
  Esto podría indicar que las cuentas de trabajo que ejecutan scripts externos no pueden tener acceso a la instancia.

* *Error de InitializePhysicalUsersPool*
  
  Este mensaje podría significar que la configuración de seguridad impide que el programa de instalación cree el grupo de cuentas de trabajo necesarias para ejecutar scripts externos.

* *Error de inicialización del administrador de contexto de seguridad*

* *Error de inicialización del administrador de sesión satélite*

## <a name="system-events"></a>Eventos del sistema

1. Abra Windows Visor de eventos y busque en el registro de **eventos del sistema** los mensajes que incluyan la cadena *Launchpad*.
2. Abra el archivo ExtLaunchErrorlog y busque la cadena *ErrorCode*. Revise el mensaje asociado al código de error.

Por ejemplo, los siguientes mensajes son errores comunes del sistema relacionados con el marco de extensibilidad de SQL Server:

* *No se pudo iniciar el servicio SQL Server Launchpad (MSSQLSERVER) debido al siguiente error:<text>*

* *El servicio no respondió a tiempo a la solicitud de inicio o de control.*

* *Se alcanzó el tiempo de espera (120000 milisegundos) mientras se esperaba a que se conectara el servicio SQL Server Launchpad (MSSQLSERVER).*

## <a name="dump-files"></a>Archivos de volcado de memoria

Si tiene conocimientos sobre la depuración, puede utilizar los archivos de volcado para analizar un error en Launchpad.

1. Busque la carpeta que contiene los registros de arranque del programa de instalación de SQL Server. Por ejemplo, en SQL Server 2016, la ruta de acceso predeterminada es C:\Archivos de Programa\microsoft SQL Server\130\Setup Bootstrap\Log.
2. Abra la subcarpeta de registro de bootstrap que es específica de la extensibilidad.
3. Si necesita enviar una solicitud de soporte técnico, agregue todo el contenido de esta carpeta a un archivo comprimido. Por ejemplo, C:\Archivos de Programa\microsoft SQL Server\130\Setup Bootstrap\Log\LOG\ExtensibilityLog.
  
La ubicación exacta podría diferir en el sistema y podría estar en una unidad distinta de la unidad C. Asegúrese de obtener los registros de la instancia en la que está instalado el aprendizaje automático.

## <a name="configuration-settings"></a>Parámetros de configuración

En esta sección se enumeran los componentes o proveedores adicionales que pueden ser un origen de errores al ejecutar scripts de R o Python.

### <a name="what-network-protocols-are-available"></a>¿Qué protocolos de red están disponibles?

Machine Learning Services requiere los siguientes protocolos de red para la comunicación interna entre los componentes de extensibilidad y para la comunicación con clientes de R o Python externos.

* Canalizaciones con nombre
* TCP/IP

Abra Administrador de configuración de SQL Server para determinar si un protocolo está instalado y, si está instalado, para determinar si está habilitado.

### <a name="security-configuration-and-permissions"></a>Configuración de seguridad y permisos

Para las cuentas de trabajo:

1. En el panel de control, Abra **usuarios y grupos**y busque el grupo que se usa para ejecutar trabajos de script externos. De forma predeterminada, el grupo es **SQLRUserGroup**.
2. Compruebe que el grupo existe y que contiene al menos una cuenta de trabajo.
3. En SQL Server Management Studio, seleccione la instancia en la que se ejecutarán los trabajos de R o Python, seleccione **seguridad**y, a continuación, determine si hay un inicio de sesión para SQLRUserGroup.
4. Revise los permisos del grupo de usuarios.

Para cuentas de usuario individuales:

1. Determine si la instancia admite solo la autenticación de modo mixto, los inicios de sesión de SQL o la autenticación de Windows. Esta configuración afecta a los requisitos de código de R o Python.
2. Para cada usuario que necesite ejecutar código de R, determine el nivel de permisos necesario en cada base de datos donde se escribirán los objetos desde R, se tendrá acceso a los datos o se crearán los objetos.
3. Para habilitar la ejecución de scripts, cree roles o agregue usuarios a los siguientes roles, según sea necesario:

   - Todo pero *db_owner*: Requerir ejecutar cualquier SCRIPT externo.
   - *db_datawriter*: Para escribir los resultados de R o Python.
   - *db_ddladmin*: Para crear nuevos objetos.
   - *db_datareader*: Para leer los datos que usa el código de R o Python.
4. Tenga en cuenta si cambió alguna cuenta de inicio predeterminada al instalar SQL Server 2016.
5. Si un usuario necesita instalar nuevos paquetes de R o usar paquetes de R instalados por otros usuarios, es posible que tenga que habilitar la administración de paquetes en la instancia de y, a continuación, asignar permisos adicionales. Para obtener más información, vea [habilitar o deshabilitar la administración de paquetes de R](r/r-package-how-to-enable-or-disable.md).

### <a name="what-folders-are-subject-to-locking-by-antivirus-software"></a>¿Qué carpetas están sujetas a bloqueos por software antivirus?

El software antivirus puede bloquear carpetas, lo que impide la configuración de las características de aprendizaje automático y la ejecución correcta del script. Determine si alguna carpeta del árbol de SQL Server está sujeta a la detección de virus.

Sin embargo, cuando se instalan varios servicios o características en una instancia de, puede ser difícil enumerar todas las carpetas posibles que utiliza la instancia de. Por ejemplo, cuando se agregan nuevas características, se deben identificar y excluir las nuevas carpetas.

Además, algunas características crean dinámicamente nuevas carpetas en tiempo de ejecución. Por ejemplo, las tablas, los procedimientos almacenados y las funciones de OLTP en memoria crean nuevos directorios en tiempo de ejecución. Estos nombres de carpeta suelen contener GUID y no se pueden predecir. El SQL Server Launchpad de confianza crea nuevos directorios de trabajo para los trabajos de scripts de R y Python.

Dado que es posible que no sea posible excluir todas las carpetas que necesita el proceso de SQL Server y sus características, se recomienda excluir todo el árbol de directorio de instancia de SQL Server.

### <a name="is-the-firewall-open-for-sql-server-does-the-instance-support-remote-connections"></a>¿Está abierto el firewall para SQL Server? ¿Admite la instancia conexiones remotas?

1. Para determinar si SQL Server admite conexiones remotas, consulte [configuración de conexiones de servidor remoto](../database-engine/configure-windows/view-or-configure-remote-server-connection-options-sql-server.md).

2. Determine si se ha creado una regla de Firewall para SQL Server. Por motivos de seguridad, en una instalación predeterminada, es posible que no sea posible que el cliente R o Python remoto se conecte a la instancia. Para obtener más información, consulte [solución de problemas de conexión a SQL Server](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md).

## <a name="see-also"></a>Vea también

[Solución de problemas de machine learning en SQL Server](machine-learning-troubleshooting-faq.md)
