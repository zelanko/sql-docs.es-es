---
title: 'Solución de problemas de recopilación de datos para machine learning: SQL Server Machine Learning Services'
ms.prod: sql
ms.technology: machine-learning
ms.date: 02/28/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 3c9d8d6cc8c0a5cfdc697c5daaa3b56631d74116
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67963027"
---
# <a name="troubleshoot-data-collection-for-machine-learning"></a>Solución de problemas de recopilación de datos para el aprendizaje automático

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo se describe los métodos de recopilación de datos con que debe usar al intentar resolver los problemas por su cuenta o con la Ayuda de cliente de Microsoft son compatibles.

**Se aplica a:** SQL Server 2016 R Services, SQL Server 2017 Machine Learning Services (R y Python)

## <a name="sql-server-version-and-edition"></a>Edición y versión de SQL Server

SQL Server 2016 R Services es la primera versión de SQL Server para incluir compatibilidad integrada con R. SQL Server 2016 Service Pack 1 (SP1) incluye varias mejoras importantes, incluida la capacidad para ejecutar scripts externos. Si es un cliente de SQL Server 2016, considere la posibilidad de instalar SP1 o posterior.

SQL Server 2017 agrega integración de lenguaje Python. No se puede obtener la característica de integración de Python en las versiones anteriores.

Para obtener edition y versiones, ayuda, consulte este artículo, que se enumera los números de compilación para cada uno de los [versiones de SQL Server](https://social.technet.microsoft.com/wiki/contents/articles/783.sql-server-versions.aspx#Service_Pack_editions).

Dependiendo de la edición de SQL Server que está usando, algunas funciones de aprendizaje automático podría ser limitada o no está disponible. La siguiente lista de artículos de características de aprendizaje automático en las ediciones Enterprise, Developer, Standard y Express.

* [Ediciones y características admitidas de SQL Server](https://docs.microsoft.com/sql/sql-server/editions-and-components-of-sql-server-2016)
* [Características de R y Python con las ediciones de SQL Server](r/differences-in-r-features-between-editions-of-sql-server.md)

## <a name="r-language-and-tool-versions"></a>Versiones de idioma y herramientas de R

En general, la versión de R de Microsoft que se instala cuando se selecciona la característica R Services o la función de Machine Learning Services viene determinada por el número de compilación de SQL Server. Si actualizar o aplicar revisiones de SQL Server, también debe actualizar o aplicar revisiones a sus componentes de R.

Para obtener una lista de versiones y vínculos a descargas de componentes de R, consulte [instalar componentes de aprendizaje automático sin acceso a internet](https://docs.microsoft.com/sql/advanced-analytics/r/installing-ml-components-without-internet-access). En los equipos con acceso a internet, la versión necesaria de R se identifican y se instala automáticamente.

Es posible actualizar los componentes de R Server por separado desde el motor de base de datos de SQL Server en un proceso conocido como enlace. Por lo tanto, la versión de R que usa al ejecutar código R en SQL Server puede diferir dependiendo de la versión instalada de SQL Server y si ha migrado el servidor a la versión más reciente de R.

### <a name="determine-the-r-version"></a>Determinar la versión de R

Es la manera más fácil de determinar la versión de R obtener las propiedades de tiempo de ejecución mediante la ejecución de una instrucción como la siguiente:

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

Como último recurso, puede abrir archivos en el servidor para determinar la versión instalada. Para ello, busque el archivo rlauncher.config para obtener la ubicación de la ejecución de R y el directorio de trabajo actual. Se recomienda que haga y abrir una copia del archivo para que accidentalmente no cambie las propiedades.

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name\MSSQL\Binn\rlauncher.config`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\MSSQL\Binn\rlauncher.config`

Para obtener la versión de R y las versiones de RevoScaleR, abra un símbolo del sistema de R, o abra el RGui asociado a la instancia.

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.<instancename>\R_SERVICES\bin\x64\RGui.exe`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\R_SERVICES\bin\x64\RGui.exe`

La consola de R muestra la información de versión en el inicio. Por ejemplo, la versión siguiente representa la configuración predeterminada de SQL Server 2017:

    *Microsoft R Open 3.3.3*

    *The enhanced R distribution from Microsoft*

    *Microsoft packages Copyright (C) 2017 Microsoft*

    *Loading Microsoft R Server packages, version 9.1.0.*

## <a name="python-versions"></a>Versiones de Python

Hay varias maneras de obtener la versión de Python. La forma más sencilla es ejecutar esta instrucción desde Management Studio o cualquier otra herramienta de consulta SQL:

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

Si no se está ejecutando servicios Machine Learning, puede determinar la versión de Python instalada examinando el archivo pythonlauncher.config. Se recomienda que haga y abrir una copia del archivo para que accidentalmente no cambie las propiedades.

1. Para SQL Server 2017 solo: `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\MSSQL\Log\ExtensibilityLog\pythonlauncher.config`
2. Obtener el valor de **PYTHONHOME**.
3. Obtiene el valor del directorio de trabajo actual.

> [!NOTE]
> Si ha instalado Python y R en SQL Server 2017, el directorio de trabajo y el grupo de cuentas de trabajo se comparten para los lenguajes R y Python.

## <a name="are-multiple-instances-of-r-or-python-installed"></a>¿Son varias instancias de R o Python instalado?

Compruebe si más de una copia de las bibliotecas de R está instalada en el equipo. Esta duplicación puede ocurrir si:

* Durante la instalación seleccione R Services (In-Database) y R Server (independiente).
* Instale a Microsoft R Client además de SQL Server.
* Un conjunto diferente de las bibliotecas de R se instaló mediante herramientas de R para Visual Studio, R Studio, Microsoft R Client u otro IDE de R.
* El equipo hospeda varias instancias de SQL Server y más de una instancia utiliza el aprendizaje automático.

Las mismas condiciones se aplican a Python.

Si encuentra que se instalan varias bibliotecas o tiempos de ejecución, asegúrese de que obtiene solo los errores asociados con los tiempos de ejecución de Python o R que se usan por la instancia de SQL Server.

## <a name="origin-of-errors"></a>Origen de errores

Los errores que se ven cuando se intenta ejecutar código de R pueden proceder de cualquiera de los orígenes siguientes:

* Motor de base de datos de SQL Server, incluido el procedimiento almacenado sp_execute_external_script
* El servidor SQL Server Launchpad de confianza
* Otros componentes del marco de extensibilidad, incluidos los iniciadores de R y Python y los procesos satélite
* Los proveedores, como Microsoft Open de base de datos ODBC (conectividad)
* Lenguaje R

Cuando se trabaja con el servicio por primera vez, puede ser difícil saber qué mensajes se originan en los servicios. Se recomienda que capturar el texto exacto de los mensajes, pero no solo el contexto en el que ha visto el mensaje. Tenga en cuenta el software cliente que esté usando para ejecutar el código de machine learning:

* ¿Usa Management Studio? ¿Una aplicación externa?
* ¿Se está ejecutando código de R en un cliente remoto, o directamente en un procedimiento almacenado?

## <a name="sql-server-log-files"></a>Archivos de registro de SQL Server

Obtenga la versión más reciente de SQL Server ERRORLOG. El conjunto completo de los registros de error consta de los archivos del directorio de registro de forma predeterminada siguiente:

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.SQL2016\MSSQL\Log\ExtensibilityLog`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.SQL2016\MSSQL\Log\ExtensibilityLog`

> [!NOTE]
> El nombre de la carpeta exacta varía según el nombre de instancia.

## <a name="errors-returned-by-spexecuteexternalscript"></a>Errores devueltos por sp_execute_external_script

Obtiene el texto completo de los errores que se devuelven, si hay alguno, al ejecutar el comando de sp_execute_external_script.

Para evitar problemas de R o Python en cuenta, puede ejecutar este script, que se inicia el tiempo de ejecución de R o Python y pasa los datos y hacia atrás.

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

SQL Server genera registros independientes para los tiempos de ejecución de lenguaje de script externo. Estos errores no se generan el lenguaje Python o R. Generó desde los componentes de extensibilidad en SQL Server, incluidos los iniciadores específicos del lenguaje y sus procesos satélite.

Puede obtener estos registros desde las siguientes ubicaciones predeterminadas:

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\MSSQL\Log\ExtensibilityLog`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\MSSQL\Log\ExtensibilityLog`

> [!NOTE]
> El nombre de carpeta exacto es diferente según el nombre de instancia. Según la configuración, la carpeta puede estar en una unidad diferente.

Por ejemplo, los mensajes de registro siguientes están relacionados con el marco de extensibilidad:

* *Error de LogonUser para el usuario MSSQLSERVER01*
  
  Esto podría indicar que las cuentas de trabajo que se ejecutan los scripts externos no pueden tener acceso a la instancia.

* *Error de InitializePhysicalUsersPool*
  
  Este mensaje podría significar que la configuración de seguridad impide que el programa de instalación cree el grupo de cuentas de trabajo que se necesitan para ejecutar scripts externos.

* *Error de inicialización de administrador de contexto de seguridad*

* *No se pudo inicializar el Administrador de sesión de satélite*

## <a name="system-events"></a>Eventos del sistema

1. Abra el Visor de eventos de Windows y buscar el **evento del sistema** registro para los mensajes que contienen la cadena *Launchpad*.
2. Abra el archivo ExtLaunchErrorlog y busque la cadena *ErrorCode*. Revise el mensaje que está asociado con el código de error.

Por ejemplo, los mensajes siguientes son errores comunes del sistema que están relacionados con el marco de extensibilidad de SQL Server:

* *El servicio Launchpad de SQL Server (MSSQLSERVER) no pudo iniciarse debido al error siguiente:  <text>*

* *El servicio no respondió a la solicitud de inicio o control de manera oportuna.*

* *Un tiempo de espera se ha alcanzado (120000 milisegundos) mientras se espera que el servicio Launchpad de SQL Server (MSSQLSERVER) para conectarse.*

## <a name="dump-files"></a>Archivos de volcado de memoria

Si está familiarizado con la depuración, puede usar los archivos de volcado de memoria para analizar un error en el Launchpad.

1. Busque la carpeta que contiene los registros de arranque de instalación de SQL Server. Por ejemplo, en SQL Server 2016, la ruta de acceso predeterminada era C:\Program Files\Microsoft SQL Server\130\Setup Bootstrap\Log.
2. Abra la subcarpeta de registro de arranque que es específica de extensibilidad.
3. Si tiene que enviar una solicitud de soporte técnico, agregar todo el contenido de esta carpeta a un archivo comprimido. Por ejemplo, C:\Program Files\Microsoft SQL Server\130\Setup Bootstrap\Log\LOG\ExtensibilityLog.
  
La ubicación exacta puede diferir en su sistema y es posible en una unidad distinta de la unidad C. Asegúrese de obtener los registros para la instancia donde está instalado el aprendizaje automático.

## <a name="configuration-settings"></a>Parámetros de configuración

Esta sección enumeran los componentes adicionales o proveedores que pueden ser una fuente de errores al ejecutar scripts de R o Python.

### <a name="what-network-protocols-are-available"></a>¿Qué protocolos de red están disponibles?

Servicios Machine Learning requiere los siguientes protocolos de red para la comunicación interna entre los componentes de extensibilidad y para la comunicación con clientes externos de R o Python.

* Canalizaciones con nombre
* TCP/IP

Abra el Administrador de configuración de SQL Server para determinar si se instala un protocolo y, si está instalado, para determinar si está habilitada.

### <a name="security-configuration-and-permissions"></a>Permisos y la configuración de seguridad

Para las cuentas de trabajo:

1. En el Panel de Control, abra **usuarios y grupos**y busque el grupo que se usa para ejecutar trabajos de script externo. De forma predeterminada, el grupo es **SQLRUserGroup**.
2. Compruebe que el grupo existe y que contiene al menos una cuenta de trabajo.
3. En SQL Server Management Studio, seleccione la instancia donde se ejecutará los trabajos de R o Python, seleccione **seguridad**y, a continuación, determine si hay un inicio de sesión SQLRUserGroup.
4. Revise los permisos para el grupo de usuarios.

Para las cuentas de usuario individual:

1. Determinar si la instancia admite únicamente la autenticación de Windows, solo inicios de sesión SQL o autenticación de modo mixto. Esta configuración afecta a su R o Python code requisitos.
2. Para cada usuario que necesite ejecutar código R, determinar el nivel necesario de permisos en cada base de datos donde se escribirán los objetos de R, se accederá a datos o los objetos se crearán.
3. Para habilitar la ejecución del script, crear roles o agregar usuarios a los roles siguientes, según sea necesario:

   - Todos excepto *db_owner*: Necesita ejecutar cualquier SCRIPT externo.
   - *db_datawriter*: Para escribir los resultados de R o Python.
   - *db_ddladmin*: Para crear nuevos objetos.
   - *db_datareader*: Para leer datos que utilizan el código de R o Python.
4. Tenga en cuenta que si cambia las cuentas de inicio de forma predeterminada al instalar SQL Server 2016.
5. Si un usuario necesita instalar nuevos paquetes de R o usar los paquetes de R que se instalaron por otros usuarios, es posible que deba habilitar la administración de paquetes en la instancia y, a continuación, asignar permisos adicionales. Para obtener más información, consulte [habilitar o deshabilitar la administración de paquetes de R](r/r-package-how-to-enable-or-disable.md).

### <a name="what-folders-are-subject-to-locking-by-antivirus-software"></a>¿Cuáles son las carpetas sujetos a un bloqueo al software antivirus?

El software antivirus puede bloquear carpetas, lo que impide que el programa de instalación de la ejecución correcta de la secuencia de comandos y características de aprendizaje automático. Determinar si las carpetas en el árbol de SQL Server están sujetos a la detección de virus.

Sin embargo, cuando se instalan varios servicios o características en una instancia, puede ser difícil enumerar todas las carpetas posibles que son utilizadas por la instancia. Por ejemplo, cuando se agregan nuevas características, las nuevas carpetas deben identificadas y excluidas.

Además, algunas características de creación nuevas carpetas dinámicamente en tiempo de ejecución. Por ejemplo, tablas OLTP en memoria, procedimientos almacenados y funciones de creación de nuevos directorios en tiempo de ejecución. A menudo, estos nombres de carpeta contienen GUID y no se puede predecir. Trusted Launchpad de SQL Server crea nuevos directorios de trabajo de R y Python script los trabajos.

Porque no sería posible excluir todas las carpetas que son necesarios para el proceso de SQL Server y sus características, se recomienda que excluya el árbol de directorio de instancia completo de SQL Server.

### <a name="is-the-firewall-open-for-sql-server-does-the-instance-support-remote-connections"></a>¿Es el firewall abierto para SQL Server? ¿La instancia admite conexiones remotas?

1. Para determinar si SQL Server admite las conexiones remotas, consulte [configurar conexiones a servidores remotos](../database-engine/configure-windows/view-or-configure-remote-server-connection-options-sql-server.md).

2. Determinar si se ha creado una regla de firewall para SQL Server. Por motivos de seguridad en una instalación predeterminada, no sería posible para el cliente remoto de R o Python para conectarse a la instancia. Para obtener más información, consulte [solución de problemas de conexión a SQL Server](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md).

## <a name="see-also"></a>Vea también

[Solución de problemas de aprendizaje automático en SQL Server](machine-learning-troubleshooting-faq.md)
