---
title: 'Solucionar problemas de recopilación de datos para el aprendizaje automático: SQL Server'
ms.custom: ''
ms.date: 06/16/2017
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- R
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.workload: Inactive
ms.openlocfilehash: bb4c8d097cd548ad256f84d513e597e934873e69
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/04/2018
---
# <a name="troubleshoot-data-collection-for-machine-learning"></a>Solucionar problemas de recopilación de datos para el aprendizaje automático
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artículo describe el tipo de datos que se deben recopilar cuando intenta resolver los problemas con el programa de instalación, la configuración o el rendimiento de SQL Server de aprendizaje automático. Estos datos incluyen información del sistema, registros y mensajes de error.

El artículo describen las fuentes de información que son las más útiles al realizar diagnósticos en forma de autoayuda. Recopilación de esta información también es útil cuando se solicita soporte técnico para problemas relacionados con las características de aprendizaje de máquina de SQL Server.

**Se aplica a:** Services (R y Python) de aprendizaje de automático de SQL Server 2016 R Services, SQL Server de 2017

## <a name="sql-server-and-r-versions"></a>Versiones de SQL Server y R

Tenga en cuenta si la versión es una nueva instalación o una actualización. Si es una actualización, determine cómo se haya ejecutado:

- ¿Qué versión se actualiza desde? 
- ¿Ha quitado todos los componentes anteriores, o se actualiza en su lugar?
- ¿Cambiar cualquier selección de características durante la actualización? 

### <a name="which-edition-of-sql-server-is-installed-and-which-version"></a>¿La edición de SQL Server está instalada y en qué versión? 

SQL Server R Services se introdujo en SQL Server 2016. Las versiones anteriores no son compatibles con el aprendizaje automático. Además, los service packs para la versión de 2016 incluyen muchas correcciones de errores y mejoras. Como primer paso, considere la posibilidad de instalar el Service Pack 1 o posterior.

En SQL Server 2017, soporte técnico se extiende para el lenguaje de Python. No se proporciona soporte técnico para Python en versiones anteriores.

Si necesita ayuda para determinar qué edición y versión tiene, consulte este artículo, que enumera los números de compilación para cada uno de los [versiones de SQL Server](https://social.technet.microsoft.com/wiki/contents/articles/783.sql-server-versions.aspx#Service_Pack_editions).

Según la edición de SQL Server que está utilizando, podría ser alguna funcionalidad de aprendizaje de automático no está disponible, o es limitada.

Consulte los artículos siguientes para obtener una lista de características de aprendizaje de máquina en las ediciones Enterprise, Developer, Standard y Express.

* [Ediciones y las características admitidas de SQL Server](https://docs.microsoft.com/sql/sql-server/editions-and-components-of-sql-server-2016)
* [Diferencias en las características de R entre las ediciones de SQL Server](https://docs.microsoft.com/sql/advanced-analytics/r/differences-in-r-features-between-editions-of-sql-server)

### <a name="which-version-of-microsoft-r-is-installed"></a>¿La versión de Microsoft R está instalada?

En general, la versión de Microsoft R que se instalan al seleccionar la característica de R Services o la característica Servicios de aprendizaje de máquina se determina por el número de compilación de SQL Server. Si actualiza o revisión de SQL Server, también debe actualizar o patch sus componentes de R.

Para obtener una lista de versiones y vínculos a las descargas de componentes de R, consulte [instalar componentes de aprendizaje de máquina sin acceso a internet](https://docs.microsoft.com/sql/advanced-analytics/r/installing-ml-components-without-internet-access). En equipos que tienen acceso a internet, la versión necesaria de R se identifican y se instala automáticamente.

Es posible actualizar los componentes de R Server por separado desde el motor de base de datos de SQL Server, en un proceso conocido como enlace. Por lo tanto, la versión de R que utiliza al ejecutar código R en SQL Server puede diferir dependiendo de la versión instalada de SQL Server y si ha migrado el servidor a la última versión de R.

#### <a name="determine-the-r-version"></a>Determinar la versión de R

Es la manera más fácil de determinar la versión de R obtener las propiedades en tiempo de ejecución mediante la ejecución de una instrucción como la siguiente:

```SQL
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
> Si R Services no funciona, intente ejecutar solo la parte de la secuencia de comandos de R desde RGui.

Como último recurso, puede abrir archivos en el servidor para determinar la versión instalada. Para ello, busque el archivo rlauncher.config para obtener la ubicación del runtime de R y el directorio de trabajo actual. Se recomienda hacer y abrir una copia del archivo para que accidentalmente no cambie las propiedades.

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name\MSSQL\Binn\rlauncher.config`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\MSSQL\Binn\rlauncher.config`

Para obtener la versión de R y RevoScaleR, abra un símbolo del sistema de R, o abra el RGui que esté asociada con la instancia.

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.<instancename>\R_SERVICES\bin\x64\RGui.exe`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\R_SERVICES\bin\x64\RGui.exe`


La consola de R, muestra la información de versión en el inicio. Por ejemplo, la versión siguiente representa la configuración predeterminada de SQL Server de 2017 CTP 2.0:

    *Microsoft R Open 3.3.3*
    
    *The enhanced R distribution from Microsoft*
    
    *Microsoft packages Copyright (C) 2017 Microsoft*
    
    *Loading Microsoft R Server packages, version 9.1.0.*


### <a name="what-version-of-python-is-installed"></a>¿Versión de Python que está instalada?

Compatibilidad con Python está disponible solo en SQL Server 2017 Community Technology Preview (CTP) 2.0 y versiones posteriores.

Hay varias maneras de obtener la versión de Python. La forma más sencilla consiste en ejecutar esta instrucción desde Management Studio o cualquier otra herramienta de consulta SQL:

```SQL
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

Si no se está ejecutando servicios de aprendizaje de máquina, puede determinar la versión instalada de Python examinando el archivo pythonlauncher.config. Se recomienda hacer y abrir una copia del archivo para que accidentalmente no cambie las propiedades.

1. Para SQL Server de 2017 solo: `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\MSSQL\Log\ExtensibilityLog\pythonlauncher.config `
2. Obtener el valor de **PYTHONHOME**.
3. Obtiene el valor del directorio de trabajo actual.


> [!NOTE]
> Si ha instalado Python y R en SQL Server 2017, el directorio de trabajo y el grupo de cuentas de trabajadores se comparten para los lenguajes R y Python.

### <a name="are-multiple-instances-of-r-or-python-installed"></a>¿Son varias instancias de R o Python instalado?

Compruebe si más de una copia de las bibliotecas de R está instalada en el equipo. Esta duplicación puede suceder si:

* Durante la instalación seleccione R Services (In-Database) y R Server (independiente). 
* Instalar a Microsoft R cliente además de SQL Server.
* Un conjunto diferente de bibliotecas de R se instaló mediante herramientas de R para Visual Studio, R Studio, Microsoft R cliente u otro IDE de R.
* El equipo hospeda varias instancias de SQL Server y más de una instancia usa el aprendizaje automático.

Se aplican las mismas condiciones para Python.

Si encuentra que se instalan varias bibliotecas o tiempos de ejecución, asegúrese de que obtiene solo los errores relacionados con los tiempos de ejecución de Python o R utilizados por la instancia de SQL Server.

## <a name="errors-and-messages"></a>Errores y mensajes

Los errores que se ven al intentar ejecutar código R pueden proceder de alguno de los siguientes orígenes:

- Motor de base de datos de SQL Server, incluido el procedimiento almacenado sp_execute_external_script
- El servidor SQL Server de confianza Launchpad 
- Otros componentes de framework extensibilidad, incluidos los iniciadores de R y Python y los procesos satélite
- Base de datos de proveedores, como Microsoft Open conectividad (ODBC)
- Lenguaje R

Cuando se trabaja con el servicio por primera vez, puede resultar difícil saber qué mensajes se originan desde los servicios. Se recomienda que capture no sólo el texto exacto de los mensajes, pero el contexto en el que ha visto el mensaje. Tenga en cuenta el software de cliente que esté usando para ejecutar código de aprendizaje de máquina:

- ¿Está usando Management Studio? ¿Una aplicación externa?
- ¿Se está ejecutando código R en un cliente remoto, o directamente en un procedimiento almacenado?

### <a name="what-errors-has-sql-server-logged"></a>¿Qué errores se registran SQL Server?

Obtener la versión más reciente de SQL Server ERRORLOG. El conjunto completo de registros de error consta de los archivos del directorio de registro predeterminada siguiente:

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.SQL2016\MSSQL\Log\ExtensibilityLog`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.SQL2016\MSSQL\Log\ExtensibilityLog`

> [!NOTE] 
> El nombre de la carpeta exacta varía según el nombre de instancia.


### <a name="what-errors-were-returned-by-the-spexecuteexternalscript-command"></a>¿Los errores devueltos por el comando sp_execute_external_script?

Obtener el texto completo de errores que se devuelven, si los hay, al ejecutar el comando sp_execute_external_script. 

Para evitar problemas de R o Python debe tener en cuenta, puede ejecutar este script, que inicia el runtime de R o Python y pasa los datos y hacia atrás.

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

### <a name="what-errors-are-generated-by-the-extensibility-framework"></a>¿Qué errores se generan mediante el marco de extensibilidad?

SQL Server genera registros independientes para los tiempos de ejecución de lenguaje de script externo. Estos errores no se generan mediante el lenguaje de Python o R. Se generan a partir de los componentes de extensibilidad en SQL Server, incluidos los iniciadores específicos del idioma y sus procesos de satélite.

Puede obtener estos registros desde las siguientes ubicaciones predeterminadas:

* SQL Server 2016
  
  `C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\MSSQL\Log\ExtensibilityLog`

* SQL Server 2017
  
  `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\MSSQL\Log\ExtensibilityLog `

> [!NOTE] 
> El nombre de carpeta exacto es diferente según el nombre de instancia. Según la configuración, la carpeta puede estar en una unidad diferente.

Por ejemplo, los siguientes mensajes de registro están relacionadas con el marco de extensibilidad:

* *Error de LogonUser para el usuario MSSQLSERVER01*
  
  Esto podría indicar que las cuentas de trabajo que ejecutan scripts externos no pueden tener acceso a la instancia.

* *Error de InitializePhysicalUsersPool* 
  
  Este mensaje podría significar que la configuración de seguridad impiden que el programa de instalación crea el grupo de cuentas de trabajo que son necesarios para ejecutar scripts externos.

* *Error al inicializar el Administrador de contexto de seguridad* 

* *Error al inicializar el Administrador de la sesión de satélite*

### <a name="are-there-any-related-system-events"></a>¿Hay algún evento de sistema relacionados?

1. Abra el Visor de eventos de Windows y busque la **eventos del sistema** registro para los mensajes que contienen la cadena *Launchpad*. 
2. Abra el archivo ExtLaunchErrorlog y busque la cadena *ErrorCode*. Revise el mensaje que está asociada a la propiedad ErrorCode.

Por ejemplo, los mensajes siguientes son los errores de sistema comunes que están relacionados con el marco de extensibilidad de SQL Server: 

* *El servicio Launchpad de SQL Server (MSSQLSERVER) no pudo iniciarse debido al siguiente error:  <text>*

* *El servicio no respondió a la solicitud de inicio o control de manera oportuna.* 

* *Un tiempo de espera ha alcanzado (120000 milisegundos) mientras se espera para que el servicio Launchpad de SQL Server (MSSQLSERVER) para conectarse.* 

### <a name="did-any-components-start-and-then-crash"></a>¿Todos los componentes de inicio y, a continuación, se bloqueará?

Si está familiarizado con la depuración, puede usar los archivos de volcado de memoria para analizar un error en Launchpad.

1. Busque la carpeta que contiene los registros de arranque en el programa de instalación de SQL Server. Por ejemplo, en SQL Server 2016, la ruta predeterminada era C:\Program Files\Microsoft SQL Server\130\Setup Bootstrap\Log.
2. Abra la subcarpeta de registro de arranque que es específica de extensibilidad.
3. Si tiene que enviar una solicitud de soporte técnico, agregar todo el contenido de esta carpeta a un archivo comprimido. Por ejemplo, C:\Program Files\Microsoft SQL Server\130\Setup Bootstrap\Log\LOG\ExtensibilityLog.
  
La ubicación exacta puede diferir en su sistema y que resulte en una unidad distinta de la unidad C. Asegúrese de obtener los registros para la instancia donde está instalado el aprendizaje automático. 


## <a name="related-tools-and-configuration"></a>Configuración y herramientas relacionadas

Esta sección enumeran los componentes adicionales o proveedores que pueden ser un origen de errores cuando se ejecutan scripts de R o Python.

### <a name="what-network-protocols-are-available"></a>¿Qué protocolos de red están disponibles?

Servicios de aprendizaje de máquina requiere los siguientes protocolos de red para la comunicación interna entre los componentes de extensibilidad y para la comunicación con clientes externos de R o Python.

* Canalizaciones con nombre
* TCP/IP

Abra el Administrador de configuración de SQL Server para determinar si se instala un protocolo y, si está instalado, para determinar si está habilitado.

### <a name="security-configuration-and-permissions"></a>Permisos y la configuración de seguridad

Para las cuentas de trabajo:

1. En el Panel de Control, abra **usuarios y grupos**y busque el grupo se usa para ejecutar trabajos de script externo. De forma predeterminada, el grupo es **SQLRUserGroup**.
2. Compruebe que el grupo existe y que contiene al menos un trabajo cuenta.
3. En SQL Server Management Studio, seleccione la instancia donde se ejecuta trabajos de R o Python, seleccione **seguridad**y, a continuación, determine si hay un inicio de sesión para SQLRUserGroup.
4. Revise los permisos para el grupo de usuarios.

Para las cuentas de usuario individual:

1. Determinar si la instancia es compatible con la autenticación de modo mixto, solo inicios de sesión SQL o autenticación de Windows únicamente. Esta configuración afecta a la R o requisitos de código de Python.
2. Para cada usuario que necesite ejecutar código R, determine el nivel de permisos en cada base de datos donde se escribirán los objetos de R, se accederá a datos o se creará objetos necesario.
3. Para habilitar la ejecución del script, crear roles o agregar usuarios a los roles siguientes, según sea necesario:

   - Todos menos *db_owner*: requerir EXECUTE ANY EXTERNAL SCRIPT.
   - *db_datawriter*: para escribir los resultados de R o Python. 
   - *db_ddladmin*: para crear objetos nuevos. 
   - *db_datareader*: para leer los datos que se usan código R o Python. 
4. Tenga en cuenta si cambia las cuentas de inicio de forma predeterminada al instalar SQL Server 2016.
5. Si un usuario necesita instalar nuevos paquetes de R o usar paquetes de R que se instalaron por otros usuarios, tendrá que habilitar la administración de paquetes en la instancia y, a continuación, asignar permisos adicionales. Para obtener más información, consulte [habilitar o deshabilitar la administración de paquetes de R](r\r-package-how-to-enable-or-disable.md).

### <a name="what-folders-are-subject-to-locking-by-antivirus-software"></a>¿Cuáles son carpetas sujeto a un bloqueo al software antivirus?

El software antivirus puede bloquear carpetas, lo que impide que el programa de instalación de la máquina de aprendizaje características y la ejecución del script correcta. Determinar si las carpetas en el árbol de SQL Server están sujetos a la detección de virus.

Sin embargo, cuando se instalan varios servicios o características en una instancia, puede ser difícil enumerar todas las carpetas posibles que son utilizadas por la instancia. Por ejemplo, cuando se agregan nuevas características, las nuevas carpetas deben identificadas y excluidas.

Además, algunas características de crear nuevas carpetas dinámicamente en tiempo de ejecución. Por ejemplo, tablas OLTP en memoria, procedimientos almacenados y funciones crear nuevos directorios en tiempo de ejecución. A menudo, estos nombres de carpeta contienen los GUID y no se puede predecir. El Launchpad de confianza de SQL Server crea los directorios de trabajo nuevo para R y trabajos de script de Python.

Dado que podría no ser posible excluir todas las carpetas que son necesarios para el proceso de SQL Server y sus características, se recomienda que excluya el árbol completo de directorio de instancia de SQL Server.

### <a name="is-the-firewall-open-for-sql-server-does-the-instance-support-remote-connections"></a>¿Está abierto el firewall para SQL Server? ¿La instancia admite las conexiones remotas?

1. Para determinar si SQL Server admite las conexiones remotas, consulte [configurar conexiones a servidores remotos](../database-engine/configure-windows/view-or-configure-remote-server-connection-options-sql-server.md).

2. Determinar si se ha creado una regla de firewall para SQL Server. Por motivos de seguridad, en una instalación predeterminada, no sería posible para el cliente de R o Python remoto para conectarse a la instancia. Para obtener más información, consulte [solución de problemas de conexión a SQL Server](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md).

### <a name="can-you-run-r-script-outside-t-sql"></a>¿Puede ejecutar el script de R fuera de la instrucción T-SQL?

Puede intentar ejecutar el tiempo de ejecución de R que esté asociada con la instancia de SQL Server con otras herramientas de R. De este modo, puede determinar si están instaladas las bibliotecas necesarias.

Una instalación básica de R incluye varias herramientas que puede usar para ejecutar un script de R desde la línea de comandos, así como RGui para la ejecución interactiva de scripts.

Si el runtime de R está funcionando, pero el script devuelve errores, se recomienda que intente depurar el script en un entorno de desarrollo de R dedicado, como R Tools para Visual Studio.

También se recomienda que revise y ligeramente vuelva a escribir el script para corregir los problemas con los tipos de datos que pueden surgir al mover los datos entre R y el motor de base de datos. Para obtener más información, consulte [tipos de datos y las bibliotecas de R](r/r-libraries-and-data-types.md).

Además, puede usar el paquete de sqlrutils para incluir el script de R en un formato que sea más fácil utilizado como un procedimiento almacenado. Para obtener más información, vea:
* [Generar un procedimiento almacenado para el código de R mediante el paquete sqlrutils](r/generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md)
* [Crear un procedimiento almacenado mediante sqlrutils](r/how-to-create-a-stored-procedure-using-sqlrutils.md)

## <a name="see-also"></a>Vea también

[Solucionar problemas de aprendizaje automático en SQL Server](machine-learning-troubleshooting-faq.md)
