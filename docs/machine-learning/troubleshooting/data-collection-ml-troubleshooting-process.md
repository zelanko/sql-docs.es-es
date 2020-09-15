---
title: Recopilación de datos para la solución de problemas de aprendizaje automático en SQL
description: Obtenga información sobre cómo recopilar los datos que necesita para intentar resolver problemas por su cuenta o con la ayuda del servicio de asistencia al cliente de Microsoft.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 07/01/2020
ms.topic: troubleshooting
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e0f7cf6f904768f8394b690c1a45d3cfb4c9bd71
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/13/2020
ms.locfileid: "88173476"
---
# <a name="collect-data-to-troubleshoot-sql-machine-learning"></a>Recopilación de datos para la solución de problemas de aprendizaje automático en SQL

[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

En este artículo se describe cómo recopilar los datos que necesita cuando intenta resolver problemas de aprendizaje automático de SQL. Estos datos pueden ser útiles si está resolviendo problemas por su cuenta o con la ayuda del servicio de atención al cliente de Microsoft.

## <a name="sql-server-version-and-edition"></a>Versión y edición de SQL Server

SQL Server 2016 R Services es la primera versión de SQL Server que incluye compatibilidad integrada con R. SQL Server 2016 Service Pack 1 (SP1) incluye varias mejoras importantes, incluida la capacidad de ejecutar scripts externos. Si usa SQL Server 2016, considere la posibilidad de instalar la versión SP1 o posterior.

SQL Server 2017 y las versiones posteriores tienen integración con el lenguaje Python. La integración de características de Python no es posible en versiones anteriores.

Para obtener ayuda para conseguir una edición y una versión, vea este artículo, donde encontrará los números de compilación de cada una de las [versiones de SQL Server](https://social.technet.microsoft.com/wiki/contents/articles/783.sql-server-versions.aspx#Service_Pack_editions).

Según cuál sea la edición de SQL Server que use, es posible que algunas funciones de Machine Learning no estén disponibles o estén limitadas. 

## <a name="r-language-and-tool-versions"></a>Versiones de herramientas y lenguaje R

En general, la versión de Microsoft R que se instala al seleccionar la característica R Services o la característica Machine Learning Services viene determinada por el número de compilación de SQL Server. Si aplica una actualización o una revisión en SQL Server, deberá hacer lo propio también con sus componentes de R.

Para obtener una lista de las versiones y vínculos a las descargas de componentes de R, vea [Instalación de componentes de Machine Learning en equipos sin acceso a Internet](/sql/machine-learning/install/sql-ml-component-install-without-internet-access). En los equipos con acceso a Internet, la versión de R que se necesita se identifica e instala automáticamente.

Los componentes de R Server se pueden actualizar de forma independiente del motor de base de datos de SQL Server, en un proceso conocido como enlace. Por lo tanto, la versión de R que use al ejecutar el código de R en SQL Server podría variar en función de la versión instalada de SQL Server y, también, de si migró el servidor a la versión más reciente de R.

### <a name="determine-the-r-version"></a>Determinar la versión de R

La forma más fácil de determinar la versión de R es obtener las propiedades del runtime ejecutando una instrucción como la siguiente:

```sql
EXECUTE sp_execute_external_script
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
> Si R Services no funciona, pruebe a ejecutar solo la parte del script de R desde RGui.

Como último recurso, puede abrir archivos en el servidor para determinar la versión instalada. Para ello, busque el archivo rlauncher.config para obtener la ubicación del runtime de R y el directorio de trabajo actual. Se recomienda crear y abrir una copia del archivo para no cambiar ninguna de las propiedades por error.

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name\MSSQL\Binn\rlauncher.config`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\MSSQL\Binn\rlauncher.config`

Para obtener la versión de R y las versiones de RevoScaleR, abra un símbolo del sistema de R o abra la RGui asociada a la instancia.

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.<instancename>\R_SERVICES\bin\x64\RGui.exe`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\R_SERVICES\bin\x64\RGui.exe`

La consola de R muestra información de la versión en el inicio. Por ejemplo, la siguiente versión representa la configuración predeterminada de SQL Server 2017:

```console
*Microsoft R Open 3.3.3*

*The enhanced R distribution from Microsoft*

*Microsoft packages Copyright (C) 2017 Microsoft*

*Loading Microsoft R Server packages, version 9.1.0.*
```

## <a name="python-versions"></a>Versiones de Python

Hay varias maneras de obtener la versión de Python. La más sencilla consiste en ejecutar esta instrucción desde Management Studio o cualquier otra herramienta de consulta SQL:

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

Si Machine Learning Services no se está ejecutando, puede determinar la versión de Python instalada examinando el archivo pythonlauncher.config. Se recomienda crear y abrir una copia del archivo para no cambiar ninguna de las propiedades por error.

1. Solo en SQL Server 2017: `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\MSSQL\Log\ExtensibilityLog\pythonlauncher.config`
2. Obtenga el valor de **PYTHONHOME**.
3. Obtenga el valor del directorio de trabajo actual.

> [!NOTE]
> Si ha instalado tanto Python como R en SQL Server 2017, el directorio de trabajo y el grupo de cuentas de trabajo serán comunes a ambos lenguajes.

## <a name="are-multiple-instances-of-r-or-python-installed"></a>¿Existen varias instancias de R o de Python instaladas?

Compruebe si hay más de una copia de las bibliotecas de R instaladas en el equipo. Esta duplicación puede producirse en los siguientes casos:

* Durante la instalación, seleccionó R Services (en base de datos) y R Server (independiente).
* Tiene instalado Microsoft R Client aparte de SQL Server.
* Se ha instalado un conjunto de bibliotecas de R distinto mediante Herramientas de R para Visual Studio, R Studio, Microsoft R Client u otro IDE de R.
* El equipo hospeda varias instancias de SQL Server, y más de una instancia usa Machine Learning.

Estas condiciones son igualmente válidas para Python.

Si ve que hay varias bibliotecas o runtimes instalados, asegúrese de que obtiene solo los errores relativos a los runtimes de Python o de R que la instancia de SQL Server usa.

## <a name="origin-of-errors"></a>Origen de los errores

Los errores que aparecen al intentar ejecutar código de R pueden provenir de cualquiera de los siguientes orígenes:

* Motor de base de datos de SQL Server, incluido el procedimiento almacenado sp_execute_external_script
* SQL Server Trusted Launchpad
* Otros componentes del marco de extensibilidad, incluidos los procesos satélite y los iniciadores de R y Python
* Proveedores como Microsoft Open Database Connectivity (ODBC)
* Lenguaje R

Cuando se trabaja con el servicio por primera vez, puede resultar difícil saber qué mensajes proceden de qué servicios. Se recomienda capturar no solo el texto exacto del mensaje, sino el contexto en el que el mensaje se ha mostrado. Anote el software cliente que esté usando para ejecutar el código de Machine Learning:

* ¿Usa Management Studio? ¿Una aplicación externa?
* ¿Está ejecutando código R en un cliente remoto o directamente en un procedimiento almacenado?

## <a name="sql-server-log-files"></a>Archivos de registro de SQL Server

Obtenga el registro de errores de SQL Server más reciente. El conjunto completo de registros de errores se compone de los archivos del siguiente directorio de registro predeterminado:

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.SQL2016\MSSQL\Log\ExtensibilityLog`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.SQL2016\MSSQL\Log\ExtensibilityLog`

> [!NOTE]
> El nombre exacto de la carpeta varía en función del nombre de la instancia.

## <a name="errors-returned-by-sp_execute_external_script"></a>Errores devueltos por sp_execute_external_script

Obtenga el texto completo de los errores que se devuelven (si los hay) al ejecutar el comando sp_execute_external_script.

Para no tener en cuenta los problemas de R o Python, puede ejecutar este script, que inicia el runtime de R o Python y pasa los datos, intercambiándolos.

**R**

```sql
exec sp_execute_external_script @language =N'R',  
@script=N'OutputDataSet<-InputDataSet',  
@input_data_1 =N'select 1 as hello'  
with result sets (([hello] int not null));  
go
```

**Python**

```sql
exec sp_execute_external_script @language =N'Python',  
@script=N'OutputDataSet= InputDataSet',  
@input_data_1 =N'select 1 as hello'  
with result sets (([hello] int not null));  
go
```

## <a name="errors-generated-by-the-extensibility-framework"></a>Errores generados por el marco de extensibilidad

SQL Server genera registros aparte para los runtimes de lenguaje de scripts externos. Estos errores no proceden de los lenguajes Python o R, sino que se generan a partir de los componentes de extensibilidad de SQL Server, incluidos iniciadores específicos de lenguaje y sus procesos satélite.

Estos registros se pueden obtener de las siguientes ubicaciones predeterminadas:

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\MSSQL\Log\ExtensibilityLog`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\MSSQL\Log\ExtensibilityLog`

> [!NOTE]
> El nombre exacto de la carpeta varía en función del nombre de la instancia. Según la configuración, la carpeta podría estar en otra unidad.

Por ejemplo, los siguientes mensajes de registro tienen que ver con el marco de extensibilidad:

* *Error de LogonUser para el usuario MSSQLSERVER01*
  
  Podría indicar que las cuentas de trabajo que ejecutan scripts externos no pueden acceder a la instancia.

* *Error de InitializePhysicalUsersPool*
  
  Este mensaje podría significar que la configuración de seguridad impide que el programa de instalación cree el grupo de cuentas de trabajo necesarias para ejecutar scripts externos.

* *Security Context Manager initialization failed* (Error de inicialización del administrador de contextos de seguridad)

* *Satellite Session Manager initialization failed* (Error de inicialización del administrador de sesiones satélite)

## <a name="system-events"></a>Eventos del sistema

1. Abra el Visor de eventos de Windows y busque en el registro de **eventos del sistema** mensajes que incluyan la cadena *Launchpad*.
2. Abra el archivo ExtLaunchErrorlog y busque la cadena *ErrorCode*. Revise el mensaje asociado al código de error.

Por ejemplo, los siguientes mensajes son errores del sistema comunes relacionados con el marco de extensibilidad de SQL Server:

* *El servicio SQL Server Launchpad (MSSQLSERVER) no pudo iniciarse debido al siguiente error: <text>*

* *El servicio no respondió a tiempo a la solicitud de inicio o de control.*

* *Se agotó el tiempo de espera (120000 milisegundos) para la conexión con el servicio SQL Server Launchpad (MSSQLSERVER).*

## <a name="dump-files"></a>Archivos de volcado de memoria

Si posee conocimientos de depuración, puede usar los archivos de volcado de memoria para analizar un error en Launchpad.

1. Busque la carpeta que contenga los registros de arranque del programa de instalación de SQL Server. Por ejemplo, en SQL Server 2016, la ruta de acceso predeterminada es C:\Archivos de programa\Microsoft SQL Server\130\Setup Bootstrap\Log.
2. Abra la subcarpeta de registros de arranque específica de la extensibilidad.
3. Si necesita enviar una solicitud de soporte técnico, agregue todo el contenido de esta carpeta a un archivo comprimido. Por ejemplo, C:\Archivos de programa\Microsoft SQL Server\130\Setup Bootstrap\Log\LOG\ExtensibilityLog.
  
La ubicación exacta podría diferir en el sistema y podría estar en una unidad distinta de la unidad C. Asegúrese de obtener los registros de la instancia en la que Machine Learning está instalado.

## <a name="configuration-settings"></a>Parámetros de configuración

En esta sección se enumeran otros componentes o proveedores que pueden ser origen de errores al ejecutar scripts de R o Python.

### <a name="what-network-protocols-are-available"></a>¿Qué protocolos de red hay disponibles?

Machine Learning Services requiere los siguientes protocolos de red para la comunicación interna entre los componentes de extensibilidad y para la comunicación con clientes de R o de Python externos.

* Canalizaciones con nombre
* TCP/IP

Abra el Administrador de configuración de SQL Server para saber si un protocolo está instalado y, si lo está, para saber si está habilitado.

### <a name="security-configuration-and-permissions"></a>Permisos y configuración de seguridad

En cuentas de trabajo:

1. En el Panel de control, abra **Usuarios y grupos** y busque el grupo usado para ejecutar trabajos de script externos. Ese grupo es **SQLRUserGroup** de forma predeterminada.
2. Compruebe que el grupo existe y que contiene al menos una cuenta de trabajo.
3. En SQL Server Management Studio, seleccione la instancia en la que se van a ejecutar trabajos de R o Python, seleccione **Seguridad** y, después, determine si hay un inicio de sesión para SQLRUserGroup.
4. Revise los permisos del grupo de usuarios.

En cuentas de usuario individuales:

1. Determine si la instancia admite solo la autenticación de modo mixto, solo inicios de sesión de SQL o solo la autenticación de Windows. Esta configuración afecta a los requisitos de código de R o de Python.
2. Por cada usuario que necesite ejecutar código de R, determine el nivel de permisos necesario en cada base de datos donde se van a escribir objetos desde R, donde se va a acceder a los datos o donde se van a crear objetos.
3. Para habilitar la ejecución de scripts, cree roles o agregue usuarios a los siguientes roles, según sea necesario:

   - Todos excepto *db_owner*: se requiere EXECUTE ANY EXTERNAL SCRIPT.
   - *db_datawriter*: para escribir resultados de R o de Python.
   - *db_ddladmin*: para crear objetos.
   - *db_datareader*: para leer los datos que el código de R o de Python usa.
4. Tenga en cuenta si cambió alguna cuenta de inicio predeterminada al instalar SQL Server 2016.
5. Si un usuario necesita instalar nuevos paquetes de R o usar paquetes de R instalados por otros usuarios, puede que tenga que habilitar la administración de paquetes en la instancia y, luego, asignar más permisos. 

### <a name="what-folders-are-subject-to-locking-by-antivirus-software"></a>¿Qué carpetas están sujetas a bloqueos del software antivirus?

El software antivirus puede bloquear carpetas, lo que impide que se instalen las características de Machine Learning y los scripts se ejecuten correctamente. Determine si alguna carpeta del árbol de SQL Server está sujeta a la detección de virus.

Cuando se instalan varios servicios o características en una instancia, puede resultar complicado enumerar todas las carpetas posibles que esa instancia usa. Por ejemplo, cuando se agregan nuevas características, se deben identificar y excluir las nuevas carpetas.

Además, algunas características crean carpetas dinámicamente en tiempo de ejecución. Es el caso de las tablas OLTP en memoria, los procedimientos almacenados y las funciones: todos ellos crean directorios en tiempo de ejecución. Estos nombres de carpeta suelen contener GUID y no se pueden predecir. SQL Server Trusted Launchpad crea directorios de trabajo para los trabajos de script de R y de Python.

Dado que existe la posibilidad de que no se puedan excluir todas las carpetas que el proceso de SQL Server y sus características necesitan, se recomienda excluir todo el árbol de directorio de instancias de SQL Server.

### <a name="is-the-firewall-open-for-sql-server-does-the-instance-support-remote-connections"></a>¿Está abierto el firewall para SQL Server? ¿Admite la instancia conexiones remotas?

1. Para saber si SQL Server admite conexiones remotas, vea [Configurar conexiones de servidor remoto](../../database-engine/configure-windows/view-or-configure-remote-server-connection-options-sql-server.md).

2. Averigüe si se ha creado una regla de firewall para SQL Server. Por motivos de seguridad, en una instalación predeterminada es posible que el cliente de R o de Python remoto no pueda conectarse a la instancia. Para más información, vea [Solucionar problemas de conexión a SQL Server](../../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md).

## <a name="see-also"></a>Consulte también

[Solución de problemas de Machine Learning en SQL Server](machine-learning-troubleshooting-overview.md)
