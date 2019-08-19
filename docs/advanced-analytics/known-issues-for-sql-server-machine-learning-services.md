---
title: Problemas conocidos del lenguaje R y la integración de Python
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 93b2871fa60d6a7c7a41fae202e960440b53c11e
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715191"
---
# <a name="known-issues-in-machine-learning-services"></a>Problemas conocidos de Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En este artículo se describen los problemas conocidos o las limitaciones de los componentes de aprendizaje automático que se proporcionan como una opción en [SQL Server 2016 R Services](r/sql-server-r-services.md) y [SQL Server Machine Learning Services con R y Python](what-is-sql-server-machine-learning.md).

## <a name="setup-and-configuration-issues"></a>Problemas de instalación y configuración

Para obtener una descripción de los procesos y preguntas comunes relacionadas con la configuración inicial y la configuración, consulte [preguntas más frecuentes sobre actualización e instalación](r/upgrade-and-installation-faq-sql-server-r-services.md). Contiene información acerca de las actualizaciones, la instalación en paralelo y la instalación de nuevos componentes de R o Python.

### <a name="1-inconsistent-results-in-mkl-computations-due-to-missing-environment-variable"></a>1. Resultados incoherentes en los cálculos de MKL debido a la falta de variable de entorno

**Se aplica a:** R_SERVER binarios 9,0, 9,1, 9,2 o 9,3.

R_SERVER usa la biblioteca Intel Math Kernel Library (MKL). En el caso de los cálculos que implican a MKL, pueden producirse resultados incoherentes si el sistema no tiene una variable de entorno. 

Establezca la variable `'MKL_CBWR'=AUTO` de entorno para garantizar la reproducibilidad numérica condicional en R_SERVER. Para obtener más información, consulte [Introducción a la reproducibilidad numérica condicional (CNR)](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr).

**Solución alternativa**

1. En el panel de control, haga clic en sistema **y seguridad** >  > **configuración** > avanzada del sistema**variables de entorno**.

2. Cree una nueva variable de usuario o del sistema. 

  + Establezca el nombre de la variable en ' MKL_CBWR '.
  + Establezca el valor de ' variable ' en ' AUTO '.

3. Reinicie R_SERVER. En SQL Server, puede reiniciar el servicio SQL Server Launchpad.

> [!NOTE]
> Si está ejecutando la versión preliminar de SQL Server 2019 en Linux, edite o cree *. bash_profile* en el directorio principal de usuario, `export MKL_CBWR="AUTO"`agregando la línea. Ejecute este archivo escribiendo `source .bash_profile` en un símbolo del sistema de Bash. Reinicie R_SERVER escribiendo `Sys.getenv()` en el símbolo del sistema de R.

### <a name="2-r-script-runtime-error-sql-server-2017-cu5-cu7-regression"></a>2. Error de tiempo de ejecución del script de R (SQL Server 2017 CU5-CU7 regresión)

Por SQL Server 2017, en las actualizaciones acumulativas 5 a 7, hay una regresión en el archivo **rlauncher. config** donde la ruta de acceso del archivo de directorio temporal incluye un espacio. Esta regresión se corrigió en CU8.

El error que verá al ejecutar el script de R incluye los siguientes mensajes:

> *No se puede comunicar con el tiempo de ejecución para el script ' R '. Compruebe los requisitos del tiempo de ejecución de "R".*
>
> Mensajes STDERR del script externo: 
>
> *Error irrecuperable: no se puede crear ' R_TempDir '*

**Solución alternativa**

Aplique CU8 cuando esté disponible. Como alternativa, puede volver a crear **rlauncher. config** ejecutando **registerrext** con Uninstall/install en un símbolo del sistema con privilegios elevados. 

```cmd
<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExt.exe /uninstall /sqlbinnpath:<SQLInstanceBinnPath> /userpoolsize:0 /instance:<SQLInstanceName>

<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExt.exe /install /sqlbinnpath:<SQLInstanceBinnPath> /userpoolsize:0 /instance:<SQLInstanceName>
```

En el ejemplo siguiente se muestran los comandos con la instancia predeterminada "MSSQL14. MSSQLSERVER "instalado en" C:\Archivos de Programa\microsoft\"SQL Server:

```cmd
"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRext.exe" /uninstall /sqlbinnpath:"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\Binn" /userpoolsize:0 /instance:MSSQLSERVER

"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRext.exe" /install /sqlbinnpath:"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\Binn" /userpoolsize:0 /instance:MSSQLSERVER
```

### <a name="3-unable-to-install-sql-server-machine-learning-features-on-a-domain-controller"></a>3. No se puede instalar SQL Server características de machine learning en un controlador de dominio

Si intenta instalar 2016 SQL Server R Services o SQL Server Machine Learning Services en un controlador de dominio, se producirá un error en la instalación, con estos errores:

> *Se produjo un error durante el proceso de instalación de la característica*
> 
> *No se encuentra el grupo con la identidad*
> 
> *Código de error de componente: 0x80131509*

El error se produce porque, en un controlador de dominio, el servicio no puede crear las 20 cuentas locales necesarias para ejecutar el aprendizaje automático. En general, no se recomienda instalar SQL Server en un controlador de dominio. Para obtener más información, consulte el [boletín de soporte 2032911](https://support.microsoft.com/help/2032911/you-may-encounter-problems-when-installing-sql-server-on-a-domain-cont).

### <a name="4-install-the-latest-service-release-to-ensure-compatibility-with-microsoft-r-client"></a>4. Instale la versión de servicio más reciente para garantizar la compatibilidad con Microsoft R Client

Si instala la versión más reciente de Microsoft R Client y la usa para ejecutar R en SQL Server en un contexto de cálculo remoto, podría obtener un error similar al siguiente:

> *Está ejecutando la versión 9. x. x de Microsoft R Client en el equipo, que es incompatible con Microsoft R Server versión 8. x.x. Download and install a compatible version.* (Está ejecutando la versión 9.0.0 del Cliente de Microsoft R en el equipo, que es incompatible con Microsoft R Server versión 8.0.3. Descargue e instale una versión compatible).

SQL Server 2016 requiere que las bibliotecas de R en el cliente coincidan exactamente con las bibliotecas de R en el servidor. La restricción se ha quitado para versiones posteriores a R Server 9.0.1. Sin embargo, si se produce este error, Compruebe la versión de las bibliotecas de R que usa el cliente y el servidor y, si es necesario, actualice el cliente para que coincida con la versión del servidor.

La versión de R que se instala con SQL Server R Services se actualiza cada vez que se instala una versión del servicio SQL Server. Para asegurarse de que siempre dispone de las versiones más actualizadas de los componentes de R, asegúrese de instalar todos los Service Pack.

Para garantizar la compatibilidad con Microsoft R Client 9.0.0, instale las actualizaciones que se describen en este [artículo de soporte técnico](https://support.microsoft.com/kb/3210262).

Para evitar problemas con los paquetes de R, también puede actualizar la versión de las bibliotecas de R que están instaladas en el servidor, cambiando el contrato de servicio para usar la Directiva de soporte del ciclo de vida moderno, tal como se describe en [la sección siguiente](#bkmk_sqlbindr). Al hacerlo, la versión de R que se instala con SQL Server se actualiza en la misma programación que se usa para las actualizaciones de machine learning Server (anteriormente Microsoft R Server).

**Se aplica a:** SQL Server 2016 R Services, con R Server versión 9.0.0 o anterior

### <a name="5-r-components-missing-from-cu3-setup"></a>5. Faltan componentes de R en la configuración de CU3

Un número limitado de máquinas virtuales de Azure se aprovisionó sin los archivos de instalación de R que deben incluirse con SQL Server. El problema se aplica a las máquinas virtuales aprovisionadas en el período de 2018-01-05 a 2018-01-23. Este problema también puede afectar a las instalaciones locales si aplicó la actualización de CU3 para SQL Server 2017 durante el período de 2018-01-05 a 2018-01-23.

Se ha proporcionado una versión de servicio que incluye la versión correcta de los archivos de instalación de R.

+ [Paquete de actualización acumulativa 3 para SQL Server 2017 KB4052987](https://www.microsoft.com/download/details.aspx?id=56128).

Para instalar los componentes y reparar SQL Server 2017 CU3, debe desinstalar CU3 y volver a instalar la versión actualizada:

1. Descargue el archivo de instalación de CU3 actualizado, que incluye los instaladores de R.
2. Desinstale CU3. En el panel de control, busque **desinstalar una actualización**y, a continuación, seleccione "revisión 3015 para SQL Server 2017 (KB4052987) (64-bit)". Continúe con los pasos de desinstalación.
3. Vuelva a instalar la actualización de CU3; para ello, haga doble clic en la actualización de KB4052987 que `SQLServer2017-KB4052987-x64.exe`acaba de descargar:. Siga las instrucciones de instalación.

### <a name="6-unable-to-install-python-components-in-offline-installations-of-sql-server-2017-ctp-20-or-later"></a>6. No se pueden instalar los componentes de Python en instalaciones sin conexión de SQL Server 2017 CTP 2,0 o posterior.

Si instala una versión preliminar de SQL Server 2017 en un equipo sin acceso a Internet, es posible que el instalador no muestre la página que solicita la ubicación de los componentes de Python descargados. En tal caso, puede instalar la característica Machine Learning Services, pero no los componentes de Python.

Este problema se ha corregido en la versión de lanzamiento. Además, esta limitación no se aplica a los componentes de R.

**Se aplica a:** SQL Server 2017 con Python

### <a name="bkmk_sqlbindr"></a>ADVERTENCIA de una versión incompatible cuando se conecta a una versión anterior de SQL Server R Services desde un cliente mediante[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]

Al ejecutar el código de R en un contexto de proceso de SQL Server 2016, es posible que vea el siguiente error:

> *Está ejecutando la versión 9.0.0 de Microsoft R Client en el equipo, que es incompatible con la versión de Microsoft R Server 8.0.3. Download and install a compatible version.* (Está ejecutando la versión 9.0.0 del Cliente de Microsoft R en el equipo, que es incompatible con Microsoft R Server versión 8.0.3. Descargue e instale una versión compatible).

Este mensaje se muestra si alguna de las dos instrucciones siguientes es true,

+ Ha instalado R Server (independiente) en un equipo cliente mediante el Asistente para la instalación [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]de.
+ Ha instalado Microsoft R Server con el [instalador de Windows independiente](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows).

Para asegurarse de que el servidor y el cliente usan la misma versión, es posible que deba usar el _enlace_, compatible con Microsoft R Server 9,0 y versiones posteriores, para actualizar los componentes de R en SQL Server instancias de 2016. Para determinar si la compatibilidad con las actualizaciones está disponible para su versión de R Services, vea [actualizar una instancia de r Services con SqlBindR. exe](install/upgrade-r-and-python.md).

**Se aplica a:** SQL Server 2016 R Services, con R Server versión 9.0.0 o anterior

### <a name="7-setup-for-sql-server-2016-service-releases-might-fail-to-install-newer-versions-of-r-components"></a>7. La instalación de las versiones de servicio de SQL Server 2016 podrían producir un error al instalar versiones más recientes de los componentes de R

Al instalar una actualización acumulativa o instalar un Service Pack para SQL Server 2016 en un equipo que no está conectado a Internet, es posible que el Asistente para la instalación no muestre el mensaje que le permite actualizar los componentes de R mediante el uso de archivos CAB descargados. Este error suele producirse cuando se instalan varios componentes junto con el motor de base de datos.

Como alternativa, puede instalar la versión del servicio mediante la línea de comandos y especificar el `MRCACHEDIRECTORY` argumento como se muestra en este ejemplo, que instala las actualizaciones de Cu1:

`C:\<path to installation media>\SQLServer2016-KB3164674-x64.exe /Action=Patch /IACCEPTROPENLICENSETERMS /MRCACHEDIRECTORY=<path to CU1 CAB files>`

Para obtener los instaladores más recientes, consulte [instalación de componentes de machine learning sin acceso a Internet](install/sql-ml-component-install-without-internet-access.md).

**Se aplica a:** SQL Server 2016 R Services, con R Server versión 9.0.0 o anterior

### <a name="8-launchpad-services-fails-to-start-if-the-version-is-different-from-the-r-version"></a>8. Los servicios de Launchpad no se inician si la versión es diferente de la versión de R

Si instala SQL Server R Services independientemente del motor de base de datos y las versiones de compilación son diferentes, es posible que vea el siguiente error en el registro de eventos del sistema:

> *No se pudo iniciar el servicio SQL Server Launchpad debido al siguiente error: El servicio no respondió a tiempo a la solicitud de inicio o de control.*

Por ejemplo, este error puede producirse si se instala el motor de base de datos mediante la versión de lanzamiento, se aplica una revisión para actualizar el motor de base de datos y, a continuación, se agrega la característica R Services mediante la versión de lanzamiento.

Para evitar este problema, use una utilidad como el administrador de archivos para comparar las versiones de Launchpad. exe con la versión de los archivos binarios de SQL, como sqldk. dll. Todos los componentes deben tener el mismo número de versión. Si actualiza un componente, asegúrese de aplicar la misma actualización a los demás componentes instalados.

Busque Launchpad en la `Binn` carpeta de la instancia. Por ejemplo, en una instalación predeterminada de SQL Server 2016, la ruta de acceso `C:\Program Files\Microsoft SQL Server\MSSQL.13.InstanceNameMSSQL\Binn`podría ser. 

### <a name="9-remote-compute-contexts-are-blocked-by-a-firewall-in-sql-server-instances-that-are-running-on-azure-virtual-machines"></a>9. Los contextos de cálculo remotos están bloqueados por un firewall en SQL Server instancias que se ejecutan en máquinas virtuales de Azure

Si ha instalado [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] en una máquina virtual de Windows Azure, es posible que no pueda usar contextos de proceso que requieran el uso del área de trabajo de la máquina virtual. La razón es que, de forma predeterminada, el Firewall de Azure virtual machines incluye una regla que bloquea el acceso a la red para las cuentas de usuario locales de R.

Como solución alternativa, en la máquina virtual de Azure, Abra **firewall de Windows con seguridad avanzada**, seleccione **reglas de salida**y deshabilite la regla siguiente: **Bloquear el acceso a la red para las cuentas de usuario locales de R en la instancia de SQL Server MSSQLSERVER**. También puede dejar la regla habilitada, pero cambiar la propiedad de seguridad a **permitir si es seguro**.

### <a name="10-implied-authentication-in-sqlexpress"></a>10. Autenticación implícita en SQLEXPRESS

Al ejecutar trabajos de R desde una estación de trabajo de ciencia de datos remota mediante la autenticación integrada de Windows, SQL Server usa la *autenticación implícita* para generar cualquier llamada ODBC local que pueda necesitar el script. Pero esta característica no funcionaba en la compilación RTM de SQL Server Express Edition.

Para corregir el problema, se recomienda que actualice a una versión de servicio posterior.

Si la actualización no es factible, como solución alternativa, use un inicio de sesión de SQL para ejecutar trabajos de R remotos que puedan requerir llamadas ODBC incrustadas.

**Se aplica a:** SQL Server 2016 R Services Express Edition

### <a name="11-performance-limits-when-libraries-used-by-sql-server-are-called-from-other-tools"></a>11. Límites de rendimiento cuando se llama a las bibliotecas utilizadas por SQL Server desde otras herramientas

Es posible llamar a las bibliotecas de machine learning que se instalan para SQL Server desde una aplicación externa, como RGui. Esto puede ser la manera más cómoda de realizar ciertas tareas, como instalar nuevos paquetes o ejecutar pruebas ad hoc en ejemplos de código muy cortos. Sin embargo, fuera de SQL Server, el rendimiento podría ser limitado. 

Por ejemplo, incluso si usa la edición Enterprise de SQL Server, R se ejecuta en modo de un solo subproceso al ejecutar el código de R mediante herramientas externas. Para obtener las ventajas del rendimiento en SQL Server, inicie una conexión SQL Server y use [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) para llamar al tiempo de ejecución del script externo.

En general, evite llamar a las bibliotecas de machine learning que se usan en SQL Server desde herramientas externas. Si necesita depurar código de R o Python, suele ser más fácil hacerlo fuera de SQL Server. Para obtener las mismas bibliotecas que están en SQL Server, puede instalar Microsoft R Client, [SQL Server 2017 machine learning Server (independiente)](install/sql-machine-learning-standalone-windows-install.md)o [SQL Server 2016 R Server (independiente)](install/sql-r-standalone-windows-install.md).

### <a name="12-sql-server-data-tools-does-not-support-permissions-required-by-external-scripts"></a>12. SQL Server Data Tools no admite los permisos requeridos por los scripts externos

Cuando se usa Visual Studio o SQL Server Data Tools para publicar un proyecto de base de datos, si alguna entidad de seguridad tiene permisos específicos para la ejecución de scripts externos, podría recibir un error similar al siguiente:

> *Modelo TSQL: Se detectó un error al aplicar ingeniería inversa a la base de datos. No se reconoció el permiso y no se importó.*

Actualmente, el modelo DACPAC no admite los permisos usados por R Services o Machine Learning Services, como CONCEDEr cualquier SCRIPT externo o ejecutar cualquier SCRIPT externo. Este problema se corregirá en una versión posterior.

Como alternativa, ejecute las instrucciones GRANT adicionales en un script posterior a la implementación.

### <a name="13-external-script-execution-is-throttled-due-to-resource-governance-default-values"></a>13. La ejecución de scripts externos está limitada debido a los valores predeterminados de gobierno de recursos

En Enterprise Edition, puede usar grupos de recursos para administrar procesos de script externos. En algunas compilaciones de versión tempranas, la memoria máxima que se podría asignar a los procesos de R fue del 20 por ciento. Por lo tanto, si el servidor tenía 32 GB de RAM, los ejecutables de R (RTerm. exe y BxlServer. exe) podrían usar un máximo de 6,4 GB en una sola solicitud.

Si encuentra limitaciones de recursos, compruebe el valor predeterminado actual. Si el 20% no es suficiente, consulte la documentación [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] sobre cómo cambiar este valor.

**Se aplica a:** SQL Server 2016 R Services, Enterprise Edition

## <a name="r-script-execution-issues"></a>Problemas de ejecución de scripts de R

Esta sección contiene problemas conocidos que son específicos de la ejecución de R en SQL Server, así como algunos problemas relacionados con las bibliotecas y herramientas de R publicadas por Microsoft, incluido RevoScaleR.

Para conocer otros problemas conocidos que pueden afectar a las soluciones de R, consulte el sitio de [machine learning Server](https://docs.microsoft.com/machine-learning-server/resources-known-issues) .

### <a name="1-access-denied-warning-when-executing-r-scripts-on-sql-server-in-a-non-default-location"></a>1. ADVERTENCIA de acceso denegado al ejecutar scripts de R en SQL Server en una ubicación no predeterminada

Si la instancia de SQL Server se ha instalado en una ubicación no predeterminada, como fuera de la `Program Files` carpeta, se genera la advertencia ACCESS_DENIED al intentar ejecutar scripts que instalan un paquete. Por ejemplo:

> *En `normalizePath(path.expand(path), winslash, mustWork)` : ruta de acceso [2] = "~ ExternalLibraries/R/8/1": Acceso denegado*

La razón es que una función de R intenta leer la ruta de acceso y produce un error si el grupo de usuarios integrado **SQLRUserGroup**no tiene acceso de lectura. La advertencia que se genera no bloquea la ejecución del script de R actual, pero la advertencia puede repetirse repetidamente siempre que el usuario ejecute cualquier otro script de R.

Si ha instalado SQL Server en la ubicación predeterminada, este error no se produce porque todos los usuarios de Windows tienen permisos de lectura en `Program Files` la carpeta.

Este problema IA se dirigió en una próxima versión de servicio. Como alternativa, proporcione el grupo, **SQLRUserGroup**, con acceso de lectura para todas las carpetas primarias `ExternalLibraries`de.

### <a name="2-serialization-error-between-old-and-new-versions-of-revoscaler"></a>2. Error de serialización entre versiones anteriores y nuevas de RevoScaleR

Al pasar un modelo con un formato serializado a una instancia de SQL Server remota, puede obtener el error: 

> *Error en memDecompress (Data, Type = descomprimite) error interno-3 en memDecompress (2).*

Este error se produce si guardó el modelo con una versión reciente de la función de serialización, [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel), pero la instancia de SQL Server donde se deserializa el modelo tiene una versión anterior de las API de RevoScaleR, de SQL Server 2017 Cu2 o anterior.

Como solución alternativa, puede actualizar la instancia de SQL Server 2017 a CU3 o posterior.

El error no aparece si la versión de la API es la misma, o si va a mover un modelo guardado con una función de serialización anterior a un servidor que usa una versión más reciente de la API de serialización.

En otras palabras, use la misma versión de RevoScaleR para las operaciones de serialización y deserialización.

### <a name="3-real-time-scoring-does-not-correctly-handle-the-_learningrate_-parameter-in-tree-and-forest-models"></a>3. La puntuación en tiempo real no controla correctamente el parámetro _learningRate_ en los modelos de árbol y bosque

Si crea un modelo mediante un método de árbol de decisión o de bosque de decisión y especifica la velocidad de aprendizaje, podría ver resultados incoherentes al `PREDICT` usar `sp_rxpredict` o la función de SQL `rxPredict`, en comparación con el uso de.

La causa es un error en la API que procesa modelos serializados y se limita al `learningRate` parámetro: por ejemplo, en [rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees), o bien

Este problema se trata en una próxima versión del servicio.

### <a name="4-limitations-on-processor-affinity-for-r-jobs"></a>4. Limitaciones de la afinidad del procesador para trabajos de R

En la versión de lanzamiento inicial de SQL Server 2016, puede establecer la afinidad del procesador solo para las CPU del primer grupo k. Por ejemplo, si el servidor es un equipo de dos sockets con dos grupos k, solo se usarán los procesadores del primer grupo k para los procesos de R. La misma limitación se aplica al configurar el gobierno de recursos para los trabajos de scripts de R.

Este problema está corregido en SQL Server 2016 Service Pack 1. Se recomienda que actualice a la versión más reciente del servicio.

**Se aplica a:** Versión RTM de SQL Server 2016 R Services

### <a name="5-changes-to-column-types-cannot-be-performed-when-reading-data-in-a-sql-server-compute-context"></a>5. No se pueden realizar cambios en los tipos de columna al leer datos en un contexto de proceso de SQL Server

Si el contexto de proceso está establecido en la instancia de SQL Server, no puede usar el argumento _colClasses_ (u otros argumentos similares) para cambiar el tipo de datos de las columnas en el código de R.

Por ejemplo, la instrucción siguiente producirá un error si la columna CRSDepTimeStr no es ya un entero:

```R
data <- RxSqlServerData(
  sqlQuery = "SELECT CRSDepTimeStr, ArrDelay  FROM AirlineDemoSmall", 
  connectionString = connectionString, 
  colClasses = c(CRSDepTimeStr = "integer"))
```

Como solución alternativa, puede volver a escribir la consulta SQL para utilizar CAST o CONVERT y presentar los datos a R usando el tipo de datos correcto. En general, el rendimiento es mejor cuando se trabaja con datos mediante SQL en lugar de mediante el cambio de datos en el código de R.

**Se aplica a:** SQL Server 2016 R Services

### <a name="6-limits-on-size-of-serialized-models"></a>6. Límites en el tamaño de los modelos serializados

Al guardar un modelo en una tabla de SQL Server, debe serializar el modelo y guardarlo en un formato binario. Teóricamente, el tamaño máximo de un modelo que se puede almacenar con este método es 2 GB, que es el tamaño máximo de las columnas varbinary en SQL Server.

Si necesita usar modelos de mayor tamaño, hay disponibles las siguientes soluciones alternativas:

+ Siga los pasos para reducir el tamaño del modelo. Algunos paquetes de R de código abierto incluyen una gran cantidad de información en el objeto de modelo y gran parte de esta información se puede quitar para su implementación. 
+ Use la selección de características para quitar columnas innecesarias.
+ Si usa un algoritmo de código abierto, considere una implementación similar con el algoritmo correspondiente en MicrosoftML o RevoScaleR. Estos paquetes se han optimizado para escenarios de implementación.
+ Después de racionalizar el modelo y reducir el tamaño con los pasos anteriores, vea si se puede usar la función [memCompress](https://www.rdocumentation.org/packages/base/versions/3.4.1/topics/memCompress) en base R para reducir el tamaño del modelo antes de pasarlo a SQL Server. Esta opción es mejor cuando el modelo está cerca del límite de 2 GB.
+ En el caso de los modelos de mayor tamaño , puede usar la característica SQL Server [FileTable](../relational-databases/blob/filetables-sql-server.md) para almacenar los modelos, en lugar de usar una columna varbinary.

    Para usar FileTables, debe agregar una excepción de firewall, porque los datos almacenados en FileTables se administran mediante el controlador de sistema de archivos de FileStream en SQL Server y las reglas de Firewall predeterminadas bloquean el acceso a archivos de red. Para obtener más información, vea [habilitar los requisitos previos de filetable](../relational-databases/blob/enable-the-prerequisites-for-filetable.md).

    Después de haber habilitado FileTable, para escribir el modelo, obtendrá una ruta de acceso de SQL mediante la API de FileTable y, a continuación, escribirá el modelo en esa ubicación desde el código. Cuando necesite leer el modelo, obtenga la ruta de acceso de SQL y, a continuación, llame al modelo mediante la ruta de acceso del script. Para obtener más información, consulte [acceso a FileTables con API de entrada-salida de archivo](../relational-databases/blob/access-filetables-with-file-input-output-apis.md).

### <a name="7-avoid-clearing-workspaces-when-you-execute-r-code-in-a-includessnoversionincludesssnoversion-mdmd-compute-context"></a>7. Evitar borrar áreas de trabajo cuando se ejecuta código R en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] un contexto de proceso

Si usa un comando de r para borrar el área de trabajo de objetos mientras se ejecuta código [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] R en un contexto de cálculo, o si borra el área de trabajo como parte de un script de r llamado mediante [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), podría obtener este error: *área de trabajo no se encontró el objeto revoScriptConnection*

`revoScriptConnection` es un objeto del área de trabajo de R que contiene información sobre una sesión de R a la que se llama desde [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Pero si su código de R incluye un comando para borrar el área de trabajo (como `rm(list=ls()))`, también se borrarán toda la información sobre la sesión y otros objetos del área de trabajo de R.

Como alternativa, evite el borrado indiscriminado de variables y otros objetos mientras ejecuta R en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Aunque es común borrar el área de trabajo cuando se trabaja en la consola de R, puede tener consecuencias imprevistas.

* Para eliminar variables específicas, use la función `remove` de R: por ejemplo,`remove('name1', 'name2', ...)`
* Si quiere eliminar varias variables, guarde los nombres de las variables temporales en una lista y realice periódicamente la recolección de elementos no utilizados.

### <a name="8-restrictions-on-data-that-can-be-provided-as-input-to-an-r-script"></a>8. Restricciones en los datos que se pueden proporcionar como entrada para un script de R

No puede usar un script de R en los siguientes tipos de resultados de consulta:

- Datos de una consulta de [!INCLUDE[tsql](../includes/tsql-md.md)] que haga referencia a columnas AlwaysEncrypted.
  
- Datos de una consulta de [!INCLUDE[tsql](../includes/tsql-md.md)] que haga referencia a columnas enmascaradas.
  
     Si necesita usar datos enmascaradas en un script de R, una posible solución alternativa es realizar una copia de los datos en una tabla temporal y usar esos datos en su lugar.

### <a name="9-use-of-strings-as-factors-can-lead-to-performance-degradation"></a>9. El uso de cadenas como factores puede provocar una degradación del rendimiento

El uso de variables de tipo cadena como factores puede aumentar considerablemente la cantidad de memoria que se usa para las operaciones de R. Se trata de un problema conocido con R en general y hay muchos artículos sobre el tema. Por ejemplo, vea [factores que no son ciudadanos de primera clase en r, por John Mount, en r-bloggers)](https://www.r-bloggers.com/factors-are-not-first-class-citizens-in-r/) o [stringsAsFactors: Una biografía no autorizada, de Roger Peng](https://simplystatistics.org/2015/07/24/stringsasfactors-an-unauthorized-biography/). 

Aunque el problema no es específico de SQL Server, puede afectar en gran medida al rendimiento de la ejecución de código de R en SQl Server. Normalmente, las cadenas se almacenan como varchar o nvarchar y, si una columna de datos de cadena tiene muchos valores únicos, el proceso de convertirlos internamente en enteros y volver a cadenas por R puede incluso provocar errores de asignación de memoria.

Si no necesita absolutamente un tipo de datos de cadena para otras operaciones, la asignación de los valores de cadena a un tipo de datos numérico (entero) como parte de la preparación de datos resultaría beneficioso en la perspectiva del rendimiento y la escala.

Para obtener una explicación de este problema y otras sugerencias, vea [rendimiento de R Services-optimización de datos](r/r-and-data-optimization-r-services.md).

### <a name="10-arguments-varstokeep-and-varstodrop-are-not-supported-for-sql-server-data-sources"></a>10. Los argumentos *varsToKeep* y *varsToDrop* no se admiten para los orígenes de datos de SQL Server

Cuando se usa la función rxDataStep para escribir los resultados en una tabla, el uso de *varsToKeep* y *varsToDrop* es una forma cómoda de especificar las columnas que se van a incluir o excluir como parte de la operación. Sin embargo, estos argumentos no se admiten para los orígenes de datos de SQL Server.

### <a name="11-limited-support-for-sql-data-types-in-sp_execute_external_script"></a>11. Compatibilidad limitada para tipos de datos de SQL\_en\_Sp\_ejecutar script externo

No todos los tipos de datos que se admiten en SQL pueden usarse en R. Como solución alternativa, considere la posibilidad de convertir el tipo de datos no admitido a un tipo de datos admitido\_antes\_de\_pasar los datos al script de ejecución del SP.

Para obtener más información, consulte [bibliotecas y tipos de datos de R](r/r-libraries-and-data-types.md).

### <a name="12-possible-string-corruption-using-unicode-strings-in-varchar-columns"></a>12. Posibles daños en las cadenas mediante cadenas Unicode en columnas VARCHAR

El paso de datos Unicode en columnas [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] VARCHAR de a R/Python puede producir daños en las cadenas. Esto se debe a que la codificación de estas cadenas Unicode en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] las intercalaciones puede no coincidir con la codificación UTF-8 predeterminada utilizada en R/Python. 

Para enviar datos de cadena no ASCII de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a R/Python, use la codificación UTF-8 (disponible en [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]) o use el tipo nvarchar para el mismo.

### <a name="13-only-one-value-of-type-raw-can-be-returned-from-sp_execute_external_script"></a>13. Solo se puede devolver un `raw` valor de tipo desde`sp_execute_external_script`

Cuando se devuelve un tipo de datos binario (el tipo de datos **raw** de r) desde R, el valor se debe enviar en la trama de datos de salida.

Con tipos de datos distintos de **raw**, puede devolver valores de parámetros junto con los resultados del procedimiento almacenado agregando la palabra clave output. Para obtener más información, vea [parámetros](https://docs.microsoft.com/sql/relational-databases/stored-procedures/parameters).

Si desea utilizar varios conjuntos de resultados que incluyan valores de tipo **raw**, una posible solución alternativa es realizar varias llamadas al procedimiento almacenado o devolver los conjuntos de resultados a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mediante ODBC.

### <a name="14-loss-of-precision"></a>14. Pérdida de precisión

Dado [!INCLUDE[tsql](../includes/tsql-md.md)] que y R admiten varios tipos de datos, los tipos de datos numéricos pueden sufrir una pérdida de precisión durante la conversión.

Para obtener más información sobre la conversión implícita de tipos de datos, vea [bibliotecas y tipos de datos de R](r/r-libraries-and-data-types.md).

### <a name="15-variable-scoping-error-when-you-use-the-transformfunc-parameter"></a>15. Error de ámbito de variable al usar el parámetro transformFunc

Para transformar los datos mientras se está modelando, puede pasar un argumento *transformFunc* en una función como `rxLinmod` o `rxLogit`. Sin embargo, las llamadas a funciones anidadas pueden provocar errores de ámbito en el contexto de proceso de SQL Server, incluso si las llamadas funcionan correctamente en el contexto de proceso local.

> *El conjunto de datos de ejemplo para el análisis no tiene variables*

Por ejemplo, supongamos que ha definido dos funciones `f` , `g`y, en el entorno global local y `g` llama `f`a. En las llamadas remotas o distribuidas `g`que implican `g` , la llamada a podría producir este `f` error, porque no se `f` encuentra, incluso si ha pasado `g` y a la llamada remota.

Si se produce este problema, puede solucionarlo insertando la definición de `f` en la definición de `g`, en cualquier lugar antes de que `g` llame a `f`.

Por ejemplo:

```R
f <- function(x) { 2*x * 3 }
g <- function(y) {
              a <- 10 * y
               f(a)
}
```

Para evitar el error, vuelva a escribir la definición de la siguiente manera:

```R
g <- function(y){
              f <- function(x) { 2*x +3}
              a <- 10 * y
              f(a)
}
```

### <a name="16-data-import-and-manipulation-using-revoscaler"></a>16. Importación de datos y manipulación con RevoScaleR

Cuando se leen columnas **VARCHAR** de una base de datos, se recortan los espacios en blanco. Para evitarlo, ponga las cadenas entre caracteres que no sean espacios en blanco.

Cuando `rxDataStep` se usan funciones como para crear tablas de base de datos que tienen columnas **VARCHAR** , el ancho de columna se calcula en función de una muestra de los datos. Si el ancho puede variar, podría ser necesario rellenar todas las cadenas con una longitud común.

El uso de una transformación para cambiar el tipo de datos de una variable no se admite cuando se usan llamadas repetidas a `rxImport` o `rxTextToXdf` para importar y anexar filas combinando varios archivos de entrada en un solo archivo .xdf.

### <a name="17-limited-support-for-rxexec"></a>17. Compatibilidad limitada para rxExec

En SQL Server 2016, la `rxExec` función proporcionada por el paquete RevoScaleR solo se puede usar en modo de un solo subproceso.

### <a name="18-increase-the-maximum-parameter-size-to-support-rxgetvarinfo"></a>18. Aumentar el tamaño máximo del parámetro para admitir rxGetVarInfo

Si usa conjuntos de datos con un número muy elevado de variables (por ejemplo, más de 40.000), `max-ppsize` establezca la marca al iniciar R para usar funciones `rxGetVarInfo`como. La marca `max-ppsize` especifica el tamaño máximo de la pila de protección del puntero.

Si usa la consola de R (por ejemplo, RGui. exe o RTerm. exe), puede establecer el valor de _Max-ppsize_ en 500000 escribiendo:

```R
R --max-ppsize=500000
```

### <a name="19-issues-with-the-rxdtree-function"></a>19. Problemas con la función rxDTree

La función `rxDTree` no admite actualmente transformaciones en la fórmula. En particular, no se admite el uso de la sintaxis `F()` para crear factores sobre la marcha. Sin embargo, los datos numéricos se discretizann automáticamente.

Los factores ordenados se tratan igual que los factores de todas las funciones de análisis RevoScaleR, excepto `rxDTree`.

### <a name="20-datatable-as-an-outputdataset-in-r"></a>20. Data. Table como OutputDataSet en R

No `data.table` se admite `OutputDataSet` el uso de como en R en la actualización acumulativa 13 (CU13) de SQL Server 2017 y versiones anteriores. Puede aparecer el mensaje siguiente:

```
Msg 39004, Level 16, State 20, Line 2
A 'R' script error occurred during execution of 
'sp_execute_external_script' with HRESULT 0x80004004.
Msg 39019, Level 16, State 2, Line 2
An external script error occurred: 
Error in alloc.col(newx) : 
  Internal error: length of names (0) is not length of dt (11)
Calls: data.frame ... as.data.frame -> as.data.frame.data.table -> copy -> alloc.col

Error in execution.  Check the output for more information.
Error in eval(expr, envir, enclos) : 
  Error in execution.  Check the output for more information.
Calls: source -> withVisible -> eval -> eval -> .Call
Execution halted
```

`data.table``OutputDataSet` como en R es compatible con la actualización acumulativa 14 de SQL Server 2017 (CU14) y versiones posteriores.

## <a name="python-script-execution-issues"></a>Problemas de ejecución del script de Python

Esta sección contiene problemas conocidos que son específicos de la ejecución de Python en SQL Server, así como de los problemas relacionados con los paquetes de Python publicados por Microsoft, incluidos [revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package) y [microsoftml](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package).

### <a name="1-call-to-pretrained-model-fails-if-path-to-model-is-too-long"></a>1. Se produce un error en la llamada a un modelo preentrenado si la ruta de acceso al modelo es demasiado larga

Si instaló los modelos previamente entrenados en una versión temprana de SQL Server 2017, la ruta de acceso completa al archivo de modelo entrenado podría ser demasiado larga para que Python lo lea. Esta limitación se corrige en una versión posterior del servicio.

Hay varias soluciones posibles: 

+ Al instalar los modelos previamente entrenados, elija una ubicación personalizada.
+ Si es posible, instale la instancia de SQL Server en una ruta de instalación personalizada con una ruta de acceso más corta, como C:\SQL\MSSQL14. MSSQLSERVER.
+ Use la utilidad de Windows [fsutil](https://technet.microsoft.com/library/cc788097(v=ws.11).aspx) para crear un vínculo físico que asigne el archivo de modelo a una ruta de acceso más corta.
+ Actualice a la versión más reciente del servicio.

### <a name="2-error-when-saving-serialized-model-to-sql-server"></a>2. Error al guardar el modelo serializado en SQL Server

Al pasar un modelo a una instancia de SQL Server remota e intentar leer el modelo binario con la `rx_unserialize` función en [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package), puede obtener el error: 

> *NameError: el nombre ' rx_unserialize_model ' no está definido*

Este error se produce si se ha guardado el modelo con una versión reciente de la función de serialización, pero la instancia de SQL Server donde se deserializa el modelo no reconoce la API de serialización.

Para resolver el problema, actualice la instancia de SQL Server 2017 a CU3 o posterior.

### <a name="3-failure-to-initialize-a-varbinary-variable-causes-an-error-in-bxlserver"></a>3. Si no se inicializa una variable varbinary, se produce un error en BxlServer

Si ejecuta código de Python en SQL Server con `sp_execute_external_script`y el código tiene variables de salida de tipo varbinary (Max), VARCHAR (Max) o tipos similares, la variable se debe inicializar o establecer como parte del script. De lo contrario, el componente de intercambio de datos, BxlServer, genera un error y deja de funcionar.

Esta limitación se solucionará en una próxima versión de servicio. Como alternativa, asegúrese de que la variable se inicializa dentro del script de Python. Se puede usar cualquier valor válido, como en los ejemplos siguientes:

```sql
declare @b varbinary(max);
exec sp_execute_external_script
  @language = N'Python'
  , @script = N'b = 0x0'
  , @params = N'@b varbinary(max) OUTPUT'
  , @b = @b OUTPUT;
go
```

```sql
declare @b varchar(30);
exec sp_execute_external_script
  @language = N'Python'
  , @script = N' b = ""  '
  , @params = N'@b varchar(30) OUTPUT'
  , @b = @b OUTPUT;
go
```

### <a name="4-telemetry-warning-on-successful-execution-of-python-code"></a>4. ADVERTENCIA de telemetría sobre la ejecución correcta del código de Python

A partir de SQL Server 2017 CU2, puede aparecer el mensaje siguiente aunque el código de Python se ejecute correctamente:

> *Mensajes stderr del script externo:* 
>  *~ PYTHON_SERVICES\lib\site-packages\revoscalepy\utils\RxTelemetryLogger*
> *SyntaxWarning: telemetry_state se usa antes de la declaración global*

Este problema se ha corregido en la actualización acumulativa 3 (CU3) de SQL Server 2017. 

### <a name="5-numeric-decimal-and-money-data-types-not-supported"></a>5. Tipos de datos numéricos, decimales y Monetarios no admitidos

A partir de SQL Server 2017, los tipos de datos de actualización acumulativa 12 (CU12), Numeric, decimal y Money de con conjuntos de resultados no se `sp_execute_external_script`admiten cuando se usa Python con. Pueden aparecer los siguientes mensajes:

> *Codifica 39004, estado de SQL: S1000] se produjo un error de script ' Python ' durante la ejecución of'sp_execute_external_script ' con HRESULT 0x80004004.*

> *Codifica 39019, estado de SQL: S1000] se produjo un error de script externo:*
> 
> *Error de SqlSatelliteCall: Tipo no compatible en el esquema de salida. Tipos admitidos: bit, smallint, int, DateTime, smallmoney, real y Float. Char, VARCHAR se admiten parcialmente.*

Esto se ha corregido en SQL Server 2017 Cumulative Update 14 (CU14).

## <a name="revolution-r-enterprise-and-microsoft-r-open"></a>Revolution R Enterprise y Microsoft R Open

En esta sección se enumeran los problemas específicos de las herramientas de conectividad, desarrollo y rendimiento de R proporcionadas por el análisis de revolución. Estas herramientas se proporcionaron en versiones preliminares anteriores de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].

En general, se recomienda desinstalar estas versiones anteriores e instalar la versión más reciente de SQL Server o Microsoft R Server.

### <a name="1-revolution-r-enterprise-is-not-supported"></a>1. No se admite la revolución R Enterprise

No se admite la instalación de revolución R en paralelo con [!INCLUDE[rsql_productname_md](../includes/rsql-productname-md.md)] cualquier versión de.

Si tiene una licencia existente de revolución R Enterprise, debe colocarla en un equipo independiente de la [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] instancia de y cualquier estación de trabajo que quiera usar para conectarse a la [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] instancia.

Algunas versiones preliminares de [!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)] incluían un entorno de desarrollo de R para Windows creado por el análisis de revolución. Esta herramienta ya no se proporciona y no se admite.

Por compatibilidad con [!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)], se recomienda instalar Microsoft R Client en su lugar. [Herramientas de R para Visual Studio](https://www.visualstudio.com/vs/rtvs/) y [Visual Studio Code](https://code.visualstudio.com/) también admiten soluciones de Microsoft R.

### <a name="2-compatibility-issues-with-sqlite-odbc-driver-and-revoscaler"></a>2. Problemas de compatibilidad con el controlador ODBC de SQLite y RevoScaleR

La revisión 0,92 del controlador ODBC de SQLite no es compatible con RevoScaleR. Se sabe que las revisiones 0.88-0.91 y 0,93 y versiones posteriores son compatibles.

## <a name="see-also"></a>Vea también

[Novedades de SQL Server 2016](../sql-server/what-s-new-in-sql-server-2016.md)

[Solución de problemas de machine learning en SQL Server](machine-learning-troubleshooting-faq.md)
