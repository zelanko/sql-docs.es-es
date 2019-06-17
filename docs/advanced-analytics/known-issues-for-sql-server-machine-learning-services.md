---
title: 'Problemas conocidos de lenguaje R y la integración de Python: SQL Server Machine Learning Services'
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 805dd613c49351c0106231b9147a4af54ac8cf0d
ms.sourcegitcommit: a91c3f4fe2587d474cd4d470bda93239ba2693bb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/14/2019
ms.locfileid: "67140729"
---
# <a name="known-issues-in-machine-learning-services"></a>Problemas conocidos de Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo se describe problemas conocidos o las limitaciones de los componentes de aprendizaje automático que se proporcionan como una opción en [SQL Server 2016 R Services](install/sql-r-services-windows-install.md) y [SQL Server 2017 Machine Learning Services con R y Python](install/sql-machine-learning-services-windows-install.md).

## <a name="setup-and-configuration-issues"></a>Problemas de instalación y configuración

Para obtener una descripción de los procesos y preguntas comunes relacionadas con la instalación y configuración iniciales, consulte [actualización e instalación de preguntas más frecuentes sobre](r/upgrade-and-installation-faq-sql-server-r-services.md). Contiene información sobre las actualizaciones, la instalación en paralelo y la instalación de nuevos componentes de R o Python.

### <a name="1-inconsistent-results-in-mkl-computations-due-to-missing-environment-variable"></a>1. Resultados incoherentes en los cálculos de MKL debido a que falta la variable de entorno

**Se aplica a:** Archivos binarios R_SERVER 9.0, 9.1, 9.2 o 9.3.

R_SERVER usa Intel Math Kernel Library (MKL). Para los cálculos que implican MKL, pueden producirse resultados incoherentes si su sistema no tiene una variable de entorno. 

Establezca la variable de entorno `'MKL_CBWR'=AUTO` para garantizar la reproducibilidad numérico condicional en R_SERVER. Para obtener más información, consulte [Introducción a la reproducibilidad numéricos condicional (CNR)](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr).

**Solución alternativa**

1. En el Panel de Control, haga clic en **sistema y seguridad** > **sistema** > **configuración avanzada del sistema**  >   **Las Variables de entorno**.

2. Crear una nueva variable de usuario o del sistema. 

  + Establezca el nombre de variable a 'MKL_CBWR'.
  + Establezca el "valor de la Variable' en 'Automático'.

3. Reinicie R_SERVER. En SQL Server, puede reiniciar el servicio Launchpad de SQL Server.

> [!NOTE]
> Si está ejecutando la versión preliminar de 2019 de SQL Server en Linux, editar o crear *. bash_profile* en su directorio principal de usuario, agregue la línea `export MKL_CBWR="AUTO"`. Ejecute este archivo escribiendo `source .bash_profile` en un símbolo del sistema de bash. Reiniciar R_SERVER escribiendo `Sys.getenv()` en el símbolo del sistema de R.

### <a name="2-r-script-runtime-error-sql-server-2017-cu5-cu7-regression"></a>2. Error de tiempo de ejecución del Script de R (SQL Server 2017 CU5 CU7 regresión)

Para SQL Server 2017, en las actualizaciones acumulativas 5 a 7, hay una regresión en la **rlauncher.config** donde la ruta de acceso del directorio temporal incluye un espacio de archivo. Esta regresión se ha corregido en CU8.

El error que verá al ejecutar el script de R incluye los siguientes mensajes:

> *No se puede comunicar con el tiempo de ejecución de script 'R'. Compruebe los requisitos de tiempo de ejecución 'R'.*
>
> Mensajes STDERR del script externo: 
>
> *Error irrecuperable: no se puede crear 'R_TempDir'*

**Solución alternativa**

Aplicar CU8 cuando esté disponible. Como alternativa, puede volver a crear **rlauncher.config** ejecutando **registerrext** con desinstalar o instalar en un símbolo del sistema con privilegios elevados. 

```cmd
<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExt.exe /uninstall /sqlbinnpath:<SQLInstanceBinnPath> /userpoolsize:0 /instance:<SQLInstanceName>

<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExt.exe /install /sqlbinnpath:<SQLInstanceBinnPath> /userpoolsize:0 /instance:<SQLInstanceName>
```

El ejemplo siguiente muestra los comandos con la instancia predeterminada "MSSQL14. Instala MSSQLSERVER"en" C:\Program Files\Microsoft SQL Server\":

```cmd
"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRext.exe" /uninstall /sqlbinnpath:"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\Binn" /userpoolsize:0 /instance:MSSQLSERVER

"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRext.exe" /install /sqlbinnpath:"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\Binn" /userpoolsize:0 /instance:MSSQLSERVER
```

### <a name="3-unable-to-install-sql-server-machine-learning-features-on-a-domain-controller"></a>3. No se puede instalar características de aprendizaje automático de SQL Server en un controlador de dominio

Si intenta instalar SQL Server 2016 R Services o SQL Server 2017 Machine Learning Services en un controlador de dominio, el programa de instalación produce un error, con estos errores:

> *Se produjo un error durante el proceso de instalación de la característica*
> 
> *No se puede encontrar el grupo con la identidad*
> 
> *Código de error de componente: 0x80131509*

El error se produce porque, en un controlador de dominio, el servicio no puede crear el 20 cuentas locales necesarias para ejecutar aprendizaje automático. En general, no se recomienda instalar SQL Server en un controlador de dominio. Para obtener más información, consulte [boletín de soporte técnico 2032911](https://support.microsoft.com/help/2032911/you-may-encounter-problems-when-installing-sql-server-on-a-domain-cont).

### <a name="4-install-the-latest-service-release-to-ensure-compatibility-with-microsoft-r-client"></a>4. Instalar la versión más reciente del servicio para garantizar la compatibilidad con Microsoft R Client

Si instala la versión más reciente de Microsoft R Client y usarlo para ejecutar R en SQL Server en un contexto de cálculo remoto, es posible que obtenga un error similar al siguiente:

> *Está ejecutando en el equipo, que es incompatible con Microsoft R Server versión 8.x.x 9.x.x de versión de Microsoft R Client. Download and install a compatible version.* (Está ejecutando la versión 9.0.0 del Cliente de Microsoft R en el equipo, que es incompatible con Microsoft R Server versión 8.0.3. Descargue e instale una versión compatible).

SQL Server 2016 requiere que las bibliotecas de R en el cliente coincidan con las bibliotecas de R en el servidor. La restricción se ha quitado para las versiones posteriores a R Server 9.0.1. Sin embargo, si se produce este error, compruebe la versión de las bibliotecas de R que se usa el cliente y el servidor y, si es necesario, actualice el cliente para que coincida con la versión del servidor.

La versión de R que se instala con SQL Server R Services se actualiza cada vez que se instala una versión de servicio de SQL Server. Para asegurarse de que siempre tiene las versiones más actualizadas de los componentes de R, asegúrese de instalar todos los service packs.

Para garantizar la compatibilidad con el cliente de Microsoft R 9.0.0, instalar las actualizaciones que se describen en este [artículo de soporte técnico](https://support.microsoft.com/kb/3210262).

Para evitar problemas con los paquetes de R, también puede actualizar la versión de las bibliotecas de R que están instalados en el servidor, cambiando su contrato de servicio para usar la directiva de soporte técnico de ciclo de vida moderno, como se describe en [la siguiente sección](#bkmk_sqlbindr). Al hacerlo, se actualiza la versión de R que se instala con SQL Server en la misma programación que se usan para las actualizaciones de machine Learning Server (anteriormente Microsoft R Server).

**Se aplica a:** SQL Server 2016 R Services, con R Server versión 9.0.0 o versiones anteriores

### <a name="5-r-components-missing-from-cu3-setup"></a>5. Componentes de R que faltan en el programa de instalación CU3

Un número limitado de máquinas virtuales de Azure aprovisionado sin los archivos de instalación de R deben estar incluidos con SQL Server. El problema se aplica a las máquinas virtuales aprovisionadas en el período de 2018-01-05-2018-01-23. Este problema también puede afectar a las instalaciones locales, si ha aplicado la actualización CU3 para SQL Server 2017 durante el período de 05-01-2018 en 2018-01-23.

Una versión de servicio ha sido proporcionada incluye la versión correcta de los archivos de instalación de R.

+ [Paquete de actualización acumulativa 3 para SQL Server 2017 KB4052987](https://www.microsoft.com/download/details.aspx?id=56128).

Para instalar los componentes y reparación de SQL Server 2017 CU3, debe desinstalar CU3 y vuelva a instalar la versión actualizada:

1. Descargue el archivo de instalación CU3 actualizado, que incluye a los instaladores de R.
2. Desinstalar CU3. En el Panel de Control, busque **desinstalar una actualización**y, a continuación, seleccione "Revisión 3015 para SQL Server 2017 (KB4052987) (64 bits)". Continúe con los pasos de desinstalación.
3. Vuelva a instalar la actualización CU3, haciendo doble clic en la actualización de KB4052987 que acaba de descargar: `SQLServer2017-KB4052987-x64.exe`. Siga las instrucciones de instalación.

### <a name="6-unable-to-install-python-components-in-offline-installations-of-sql-server-2017-ctp-20-or-later"></a>6. No se puede instalar componentes de Python en las instalaciones sin conexión de SQL Server 2017 CTP 2.0 o posterior

Si instala una versión de vista previa de SQL Server 2017 en un equipo sin acceso a internet, el programa de instalación podría no mostrar la página que solicita la ubicación de los componentes de Python descargados. En ese caso, puede instalar la característica de Machine Learning Services, pero no los componentes de Python.

Este problema se ha corregido en la versión de lanzamiento. Además, esta limitación no se aplica a los componentes de R.

**Se aplica a:** SQL Server 2017 con Python

### <a name="bkmk_sqlbindr"></a> Advertencia de versión incompatible al conectarse a una versión anterior de SQL Server R Services desde un cliente mediante el uso de [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]

Al ejecutar código R en el contexto de cálculo de un servidor SQL Server 2016, es posible que vea el siguiente error:

> *Está ejecutando la versión 9.0.0 del cliente de Microsoft R en el equipo, que no es compatible con Microsoft R Server versión 8.0.3. Download and install a compatible version.* (Está ejecutando la versión 9.0.0 del Cliente de Microsoft R en el equipo, que es incompatible con Microsoft R Server versión 8.0.3. Descargue e instale una versión compatible).

Este mensaje aparece si cualquiera de las dos instrucciones siguientes es true,

+ Instaló R Server (independiente) en un equipo cliente mediante el Asistente para instalación [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)].
+ Ha instalado Microsoft R Server mediante el uso de la [separar el instalador de Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows).

Para asegurarse de que el cliente y servidor usan la misma versión que es posible que deba usar _enlace_compatible para Microsoft R Server 9.0 y versiones posteriores actualizar los componentes de R en las instancias de SQL Server 2016. Para determinar si la compatibilidad con las actualizaciones está disponible para su versión de R Services, consulte [actualizar una instancia de R Services con SqlBindR.exe](install/upgrade-r-and-python.md).

**Se aplica a:** SQL Server 2016 R Services, con R Server versión 9.0.0 o versiones anteriores

### <a name="7-setup-for-sql-server-2016-service-releases-might-fail-to-install-newer-versions-of-r-components"></a>7. La instalación de las versiones de servicio de SQL Server 2016 podrían producir un error al instalar versiones más recientes de los componentes de R

Al instalar una actualización acumulativa o instalar un service pack para SQL Server 2016 en un equipo que no está conectado a internet, el Asistente para la instalación podría no mostrar el mensaje que le permite actualizar los componentes de R mediante el uso de los archivos CAB descargados. Este error suele producirse cuando varios componentes se instalaron con el motor de base de datos.

Como alternativa, puede instalar la versión del servicio mediante la línea de comandos y especificando el `MRCACHEDIRECTORY` argumento tal como se muestra en este ejemplo, que instala las actualizaciones de CU1:

`C:\<path to installation media>\SQLServer2016-KB3164674-x64.exe /Action=Patch /IACCEPTROPENLICENSETERMS /MRCACHEDIRECTORY=<path to CU1 CAB files>`

Para obtener los instaladores más recientes, consulte [instalar componentes de aprendizaje automático sin acceso a internet](install/sql-ml-component-install-without-internet-access.md).

**Se aplica a:** SQL Server 2016 R Services, con R Server versión 9.0.0 o versiones anteriores

### <a name="8-launchpad-services-fails-to-start-if-the-version-is-different-from-the-r-version"></a>8. No se puede iniciar si la versión es diferente de la versión de R services LaunchPad

Si instala SQL Server R Services por separado desde el motor de base de datos y las versiones de compilación son diferentes, es posible que vea el siguiente error en el registro de eventos del sistema:

> *El servicio Launchpad de SQL Server no pudo iniciarse debido al error siguiente: El servicio no respondió a la solicitud de inicio o control de manera oportuna.*

Por ejemplo, este error podría producirse si instala el motor de base de datos mediante el uso de la versión de lanzamiento, aplica una revisión para actualizar el motor de base de datos y, a continuación, agregar la característica R Services con la versión de lanzamiento.

Para evitar este problema, use una utilidad como el Administrador de archivos para comparar las versiones de Launchpad.exe con la versión de los archivos binarios SQL, como sqldk.dll. Todos los componentes deben tener el mismo número de versión. Si actualiza un componente, asegúrese de aplicar la misma actualización a los demás componentes instalados.

Busque Launchpad en el `Binn` carpeta para la instancia. Por ejemplo, podría ser la ruta de acceso en una instalación predeterminada de SQL Server 2016, `C:\Program Files\Microsoft SQL Server\MSSQL.13.InstanceNameMSSQL\Binn`. 

### <a name="9-remote-compute-contexts-are-blocked-by-a-firewall-in-sql-server-instances-that-are-running-on-azure-virtual-machines"></a>9. Contextos de cálculo remoto están bloqueados por un firewall en instancias de SQL Server que se ejecutan en máquinas virtuales de Azure

Si ha instalado [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] en una máquina virtual de Windows Azure, es posible que no pueda usar contextos de cálculo que requieren el uso del área de trabajo de la máquina virtual. El motivo es que, de forma predeterminada, el firewall en Azure virtual machines incluye una regla que bloquea el acceso para las cuentas de usuario locales de R la red.

Como alternativa, en la máquina virtual de Azure, abra **Firewall de Windows con seguridad avanzada**, seleccione **reglas de salida**y deshabilitar la regla siguiente: **Bloquear el acceso de red para las cuentas de usuario local de R en la instancia de SQL Server MSSQLSERVER**. También puede dejar activada la regla, pero cambie la propiedad de seguridad a **permitir si es seguro**.

### <a name="10-implied-authentication-in-sqlexpress"></a>10. Autenticación implícita en SQLEXPRESS

Al ejecutar trabajos de R desde una estación de trabajo de ciencia de datos remoto mediante la autenticación de Windows integrada, SQL Server usa *autenticación implícita* para generar las llamadas ODBC locales que podrían ser necesaria para la secuencia de comandos. Pero esta característica no funcionaba en la compilación RTM de SQL Server Express Edition.

Para corregir el problema, se recomienda que actualice a una versión de servicio posterior.

Si no es posible la actualización, como alternativa, utilice un inicio de sesión SQL para ejecutar trabajos de R remotos que requieran llamadas ODBC incrustadas.

**Se aplica a:** Edición Express de SQL Server 2016 R Services

### <a name="11-performance-limits-when-libraries-used-by-sql-server-are-called-from-other-tools"></a>11. Límites de rendimiento cuando se llama a bibliotecas que usa SQL Server desde otras herramientas

Es posible llamar a las bibliotecas que se instalan para SQL Server desde una aplicación externa, como RGui de aprendizaje automático. Si lo hace, podría ser la manera más conveniente para realizar ciertas tareas, como instalar nuevos paquetes o la ejecución de pruebas ad hoc en los ejemplos de código muy corto. Sin embargo, fuera de SQL Server, rendimiento podría ser limitado. 

Por ejemplo, incluso si se usa SQL Server Enterprise Edition, R se ejecuta en modo uniproceso al ejecutar el código de R con herramientas externas. Para obtener las ventajas de rendimiento en SQL Server, iniciar una conexión de SQL Server y usar [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) para llamar al tiempo de ejecución de scripts externos.

En general, evite llamar a las bibliotecas que utilizan SQL Server desde herramientas externas de aprendizaje automático. Si tiene que depurar R o código de Python, es normalmente más fácil hacerlo fuera de SQL Server. Para obtener las mismas bibliotecas que se encuentran en SQL Server, puede instalar Microsoft R Client [Machine Learning Server (independiente) de SQL Server 2017](install/sql-machine-learning-standalone-windows-install.md), o [SQL Server 2016 R Server (independiente)](install/sql-r-standalone-windows-install.md).

### <a name="12-sql-server-data-tools-does-not-support-permissions-required-by-external-scripts"></a>12. SQL Server Data Tools no es compatible con los permisos requeridos por los scripts externos

Al usar Visual Studio o SQL Server Data Tools para publicar un proyecto de base de datos, si cualquier entidad de seguridad tiene los permisos específicos para la ejecución de scripts externos, podría obtener un error como este:

> *Modelo TSQL: Error detectado al aplicar la base de datos de ingeniería inversa. El permiso no se reconoció y no se importó.*

Actualmente el modelo de DACPAC no es compatible con los permisos usados por R Services o servicios de Machine Learning, como GRANT ANY EXTERNAL SCRIPT o EXECUTE ANY EXTERNAL SCRIPT. Este problema se corregirá en una versión posterior.

Como alternativa, ejecute la concesión adicional instrucciones en un script posterior a la implementación.

### <a name="13-external-script-execution-is-throttled-due-to-resource-governance-default-values"></a>13. Ejecución de scripts externos está limitada debido a los valores predeterminados de regulación de recursos

En Enterprise Edition, puede usar grupos de recursos para administrar procesos de script externos. En algunas compilaciones de versión temprana, la memoria máxima que se pueden asignar a los procesos de R era un 20 por ciento. Por lo tanto, si el servidor tenía 32 GB de RAM, los archivos ejecutables de R (RTerm.exe y BxlServer.exe) podrían usar un máximo de 6,4 GB en una sola solicitud.

Si se producen las limitaciones de recursos, compruebe el valor predeterminado actual. Si el 20 por ciento no es suficiente, consulte la documentación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] sobre cómo cambiar este valor.

**Se aplica a:** SQL Server 2016 R Services, Enterprise Edition

## <a name="r-script-execution-issues"></a>Problemas de ejecución del script de R

Esta sección contiene problemas conocidos que son específicos para ejecutar R en SQL Server, así como algunos problemas relacionados con las bibliotecas de R y herramientas publicadas por Microsoft, incluyendo RevoScaleR.

Para otros problemas conocidos que podrían afectar a las soluciones de R, consulte el [Machine Learning Server](https://docs.microsoft.com/machine-learning-server/resources-known-issues) sitio.

### <a name="1-access-denied-warning-when-executing-r-scripts-on-sql-server-in-a-non-default-location"></a>1. Acceso denegado advertencia al ejecutar scripts de R en SQL Server en una ubicación no predeterminada

Si la instancia de SQL Server se ha instalado en una ubicación no predeterminada, como fuera de la `Program Files` carpeta, la advertencia ACCESS_DENIED se produce al intentar ejecutar scripts que instalan un paquete. Por ejemplo:

> *En `normalizePath(path.expand(path), winslash, mustWork)` : ruta de acceso [2] = "~ExternalLibraries/R/8/1": Se denegó el acceso*

La razón es que una función de R intenta leer la ruta de acceso y se produce un error si el grupo de usuarios integrados **SQLRUserGroup**, no tiene acceso de lectura. La advertencia que se genera no bloquea la ejecución del script de R actual, pero la advertencia puede repetirse varias veces siempre que el usuario ejecuta cualquier otro script de R.

Si ha instalado SQL Server en la ubicación predeterminada, este error no se produce, porque todos los usuarios de Windows tener permisos de lectura en el `Program Files` carpeta.

Este problema ia corregido en una próxima versión de servicio. Como alternativa, proporcione el grupo, **SQLRUserGroup**, con acceso de lectura para todas las carpetas primarias de `ExternalLibraries`.

### <a name="2-serialization-error-between-old-and-new-versions-of-revoscaler"></a>2. Error de serialización entre las versiones antiguas y nuevas de RevoScaleR

Al pasar un modelo con un formato serializado a una instancia remota de SQL Server, puede aparecer el error: 

> *Error en memDecompress (datos, tipo = descomprimir) -3 de error interno en memDecompress(2).*

Este error se produce si se guardó el modelo utilizando una versión reciente de la función de serialización, [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel), pero la instancia de SQL Server donde se deserializa el modelo tiene una versión anterior de las APIs de RevoScaleR, de SQL Server 2017 CU2 o una versión anterior.

Como alternativa, puede actualizar la instancia de SQL Server 2017 CU3 o posterior.

El error no aparece si la versión de API es el mismo, o si va a mover un modelo guardado con una función de serialización anterior a un servidor que usa una versión más reciente de la API de serialización.

En otras palabras, use la misma versión de RevoScaleR para las operaciones de serialización y deserialización.

### <a name="3-real-time-scoring-does-not-correctly-handle-the-learningrate-parameter-in-tree-and-forest-models"></a>3. Puntuación en tiempo real no controla correctamente el _learningRate_ parámetro en modelos de árbol y de bosque

Si crea un modelo con un árbol de decisión o un método de bosque de decisión y especifique la velocidad de aprendizaje, es posible que vea resultados incoherentes al usar `sp_rxpredict` o SQL `PREDICT` función, en comparación con uno `rxPredict`.

La causa es un error en la API que modela los procesos que se serializa y se limita a la `learningRate` parámetro: por ejemplo, en [rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees), o

Este problema se soluciona en una próxima versión de servicio.

### <a name="4-limitations-on-processor-affinity-for-r-jobs"></a>4. Limitaciones de la afinidad del procesador para trabajos de R

En la compilación de la versión inicial de SQL Server 2016, se pudo establecer la afinidad del procesador solo para la CPU en el primer grupo k. Por ejemplo, si el servidor es una máquina de 2-socket con dos grupos k, procesadores solo desde el primer grupo k se usan para los procesos de R. La misma limitación se aplica al configurar el regulador de recursos para trabajos de script de R.

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

Como alternativa, puede volver a escribir la consulta SQL para usar CAST o CONVERT y presentar los datos a R mediante el tipo de datos correcto. En general, rendimiento es mejor cuando se trabaja con datos mediante SQL en lugar de cambiar los datos en el código de R.

**Se aplica a:** SQL Server 2016 R Services

### <a name="6-limits-on-size-of-serialized-models"></a>6. Límites de tamaño de los modelos serializados

Al guardar un modelo en una tabla de SQL Server, debe serializar el modelo y guárdelo en un formato binario. En teoría, el tamaño máximo de un modelo que se puede almacenar con este método es 2 GB, que es el tamaño máximo de columnas de varbinary de SQL Server.

Si necesita usar modelos de mayor tamaño, están disponibles las siguientes soluciones alternativas:

+ Tomar medidas para reducir el tamaño del modelo. Algunos paquetes de código abierto R incluyen una gran cantidad de información en el objeto de modelo y gran parte de esta información se puede quitar para la implementación. 
+ Usar selección de características para quitar las columnas innecesarias.
+ Si usa un algoritmo de código abierto, considere la posibilidad de una implementación similar mediante el algoritmo correspondiente en MicrosoftML o RevoScaleR. Estos paquetes se han optimizado para escenarios de implementación.
+ Después de que el modelo ha sido racionalizado y reduce el tamaño con los pasos anteriores, vea si la [memCompress](https://www.rdocumentation.org/packages/base/versions/3.4.1/topics/memCompress) función en R base puede utilizarse para reducir el tamaño del modelo antes de pasarlo a SQL Server. Esta opción es mejor cuando el modelo está cerca del límite de 2 GB.
+ Para los modelos más grandes, puede usar SQL Server [FileTable](../relational-databases/blob/filetables-sql-server.md) para almacenar los modelos de características, en lugar de utilizar una columna varbinary.

    Para usar FileTables, debe agregar una excepción de firewall, porque el controlador del sistema de archivos de Filestream en SQL Server administra los datos almacenados en tablas Filetable y reglas de firewall predeterminada bloquean acceso a archivos de red. Para obtener más información, consulte [habilitar los requisitos previos para FileTable](../relational-databases/blob/enable-the-prerequisites-for-filetable.md).

    Después de haber habilitado la FileTable, para escribir el modelo, obtener una ruta de acceso de SQL mediante la API de FileTable y, a continuación, escribe el modelo en esa ubicación desde el código. Cuando deba leer el modelo, obtener la ruta de acceso de SQL y, a continuación, llamar al modelo mediante la ruta de acceso de la secuencia de comandos. Para obtener más información, consulte [obtener acceso a FileTables con API de archivo de entrada y salida](../relational-databases/blob/access-filetables-with-file-input-output-apis.md).

### <a name="7-avoid-clearing-workspaces-when-you-execute-r-code-in-a-includessnoversionincludesssnoversion-mdmd-compute-context"></a>7. Evitar borrar áreas de trabajo cuando se ejecuta código R en un [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] contexto de proceso

Si usa un comando de R para borrar el área de trabajo de objetos mientras se ejecuta código R en un [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] contexto, de proceso o si borra el área de trabajo como parte de un script de R llamado mediante el uso de [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), podría recibir este error : *revoScriptConnection del objeto de área de trabajo no encontrado*

`revoScriptConnection` es un objeto del área de trabajo de R que contiene información sobre una sesión de R a la que se llama desde [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Pero si su código de R incluye un comando para borrar el área de trabajo (como `rm(list=ls()))`, también se borrarán toda la información sobre la sesión y otros objetos del área de trabajo de R.

Como alternativa, evite borrar indiscriminadamente las variables y otros objetos mientras se ejecuta R [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Aunque es habitual borrar el área de trabajo cuando se trabaja en la consola de R, puede tener consecuencias no deseadas.

* Para eliminar variables específicas, use el R `remove` función: por ejemplo, `remove('name1', 'name2', ...)`
* Si quiere eliminar varias variables, guarde los nombres de las variables temporales en una lista y realice periódicamente la recolección de elementos no utilizados.

### <a name="8-restrictions-on-data-that-can-be-provided-as-input-to-an-r-script"></a>8. Restricciones en los datos que se pueden proporcionar como entrada para un script de R

No puede usar un script de R en los siguientes tipos de resultados de consulta:

- Datos de una consulta de [!INCLUDE[tsql](../includes/tsql-md.md)] que haga referencia a columnas AlwaysEncrypted.
  
- Datos de una consulta de [!INCLUDE[tsql](../includes/tsql-md.md)] que haga referencia a columnas enmascaradas.
  
     Si necesita usar datos enmascaradas en un script de R, una posible solución alternativa es realizar una copia de los datos en una tabla temporal y usar esos datos en su lugar.

### <a name="9-use-of-strings-as-factors-can-lead-to-performance-degradation"></a>9. Uso de cadenas como factores pueden provocar una degradación del rendimiento

Uso de variables de tipo de cadena como factores pueden aumentar considerablemente la cantidad de memoria usada para las operaciones de R. Se trata de un problema conocido con R en general, y hay muchos artículos sobre el tema. Por ejemplo, vea [factores no son ciudadanos de primera clase de R, por John montar en R bloggers)](https://www.r-bloggers.com/factors-are-not-first-class-citizens-in-r/) o [stringsAsFactors: Una biografía no autorizada, por Roger Peng](https://simplystatistics.org/2015/07/24/stringsasfactors-an-unauthorized-biography/). 

Aunque el problema no es específico de SQL Server, puede afectar considerablemente al rendimiento del código de R que se ejecutan en SQl Server. Las cadenas se almacenan normalmente como varchar o nvarchar y, si una columna de datos de cadena tiene muchos valores únicos, el proceso de convertir internamente estos números enteros y de vuelta a las cadenas de r incluso puede conducir a errores de asignación de memoria.

Si no absolutamente necesita un tipo de datos string para otras operaciones, asignar los valores de cadena a un valor numérico (entero) tipo de datos como parte de la preparación de datos sería beneficioso desde una perspectiva de rendimiento y escalabilidad.

Para obtener una explicación de este problema y otras sugerencias, consulte [rendimiento para R Services: optimización de datos](r/r-and-data-optimization-r-services.md).

### <a name="10-arguments-varstokeep-and-varstodrop-are-not-supported-for-sql-server-data-sources"></a>10. Argumentos *varsToKeep* y *varsToDrop* no se admiten para los orígenes de datos de SQL Server

Cuando usa la función rxDataStep para escribir los resultados en una tabla, utilizando el *varsToKeep* y *varsToDrop* es una forma práctica de especificar las columnas para incluir o excluir como parte de la operación. Sin embargo, estos argumentos no se admiten para los orígenes de datos de SQL Server.

### <a name="11-limited-support-for-sql-data-types-in-spexecuteexternalscript"></a>11. Compatibilidad limitada para tipos de datos SQL en el Service Pack\_ejecutar\_externo\_script

No todos los tipos de datos que se admiten en SQL pueden usarse en R. Como alternativa, considere la posibilidad de convertir el tipo de datos no admitido a un tipo de datos compatibles antes de pasar los datos a sp\_ejecutar\_externo\_secuencia de comandos.

Para obtener más información, consulte [tipos de datos y las bibliotecas de R](r/r-libraries-and-data-types.md).

### <a name="12-possible-string-corruption-using-unicode-strings-in-varchar-columns"></a>12. Daños en una cadena posible uso de cadenas de unicode en las columnas varchar

Transfiere datos de unicode en las columnas varchar de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a R o Python puede producir daños en una cadena. Esto es debido a la codificación para estos cadena unicode en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] intercalaciones pueden no coincidir con la codificación UTF-8 predeterminada utilizados en R o Python. 

Para enviar los datos de cadena que no sean ASCII de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a R y Python, utilice la codificación UTF-8 (disponible en [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]) o usar el tipo nvarchar para el mismo.

### <a name="13-only-one-value-of-type-raw-can-be-returned-from-spexecuteexternalscript"></a>13. Solo un valor de tipo `raw` pueden devolverse desde `sp_execute_external_script`

Cuando un tipo de datos binarios (el R **raw** tipo de datos) se devuelve desde R, se debe enviar el valor en la trama de datos de salida.

Con datos de tipos distintos de **raw**, puede devolver valores de parámetro junto con los resultados del procedimiento almacenado mediante la adición de la palabra clave OUTPUT. Para obtener más información, consulte [parámetros](https://docs.microsoft.com/sql/relational-databases/stored-procedures/parameters).

Si desea utilizar varios conjuntos de resultados que incluyen valores de tipo **raw**, una posible solución alternativa es hacer varias llamadas de procedimiento almacenado, o para enviar el resultado se establece volver [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mediante ODBC.

### <a name="14-loss-of-precision"></a>14. Pérdida de precisión

Dado que [!INCLUDE[tsql](../includes/tsql-md.md)] y R admiten diferentes tipos de datos, tipos de datos numéricos pueden perder precisión durante la conversión.

Para obtener más información acerca de la conversión implícita del tipo de datos, vea [tipos de datos y las bibliotecas de R](r/r-libraries-and-data-types.md).

### <a name="15-variable-scoping-error-when-you-use-the-transformfunc-parameter"></a>15. Variable de error de ámbito cuando se usa el parámetro transformFunc

Para transformar los datos mientras se realiza el modelado, puede pasar un *transformFunc* argumento en una función como `rxLinmod` o `rxLogit`. Sin embargo, las llamadas a funciones anidadas pueden provocar errores de ámbito en el contexto de cálculo de SQL Server, incluso si las llamadas funcionan correctamente en el contexto de proceso local.

> *El conjunto de datos de ejemplo para el análisis no tiene variables*

Por ejemplo, suponga que ha definido dos funciones `f` y `g`, en el entorno global local, y `g` llamadas `f`. En llamadas remotas o distribuidas que implican `g`, la llamada a `g` podría producir este error, porque `f` no se encuentra, incluso si ha pasado `f` y `g` a la llamada remota.

Si se produce este problema, puede solucionarlo insertando la definición de `f` en la definición de `g`, en cualquier lugar antes de que `g` llame a `f`.

Por ejemplo:

```R
f <- function(x) { 2*x * 3 }
g <- function(y) {
              a <- 10 * y
               f(a)
}
```

Para evitar el error, vuelva a escribir la definición como sigue:

```R
g <- function(y){
              f <- function(x) { 2*x +3}
              a <- 10 * y
              f(a)
}
```

### <a name="16-data-import-and-manipulation-using-revoscaler"></a>16. Importación de datos y manipulación con RevoScaleR

Cuando **varchar** columnas se leen desde una base de datos, se recorta el espacio en blanco. Para evitarlo, ponga las cadenas entre caracteres que no sean espacios en blanco.

Cuando las funciones como `rxDataStep` se utilizan para crear las tablas de base de datos que tienen **varchar** columnas, el ancho de columna se calcula en función de una muestra de los datos. Si el ancho varía, podría ser necesario rellenar todas las cadenas con una longitud común.

El uso de una transformación para cambiar el tipo de datos de una variable no se admite cuando se usan llamadas repetidas a `rxImport` o `rxTextToXdf` para importar y anexar filas combinando varios archivos de entrada en un solo archivo .xdf.

### <a name="17-limited-support-for-rxexec"></a>17. Compatibilidad limitada para rxExec

En SQL Server 2016, el `rxExec` función que se proporciona mediante el RevoScaleR paquete se puede usar solo en modo de subproceso único.

### <a name="18-increase-the-maximum-parameter-size-to-support-rxgetvarinfo"></a>18. Aumentar el tamaño máximo del parámetro para admitir rxGetVarInfo

Si usa conjuntos de datos con un número extremadamente grande de variables (por ejemplo, más de 40 000), establezca el `max-ppsize` marca al iniciar R para usar funciones como `rxGetVarInfo`. La marca `max-ppsize` especifica el tamaño máximo de la pila de protección del puntero.

Si usa la consola de R (por ejemplo, RGui.exe o RTerm.exe), puede establecer el valor de _max-ppsize_ a 500000 escribiendo:

```R
R --max-ppsize=500000
```

### <a name="19-issues-with-the-rxdtree-function"></a>19. Problemas con la función rxDTree

La función `rxDTree` no admite actualmente transformaciones en la fórmula. En particular, no se admite el uso de la sintaxis `F()` para crear factores sobre la marcha. Sin embargo, los datos numéricos se discretizan automáticamente.

Los factores ordenados se tratan igual que los factores de todas las funciones de análisis RevoScaleR, excepto `rxDTree`.

### <a name="20-datatable-as-an-outputdataset-in-r"></a>20. Data.Table como un OutputDataSet en R

Uso de `data.table` como un `OutputDataSet` en R no se admite en SQL Server 2017 acumulativa actualización 13 (CU13) y versiones anteriores. Es posible que aparezca el mensaje siguiente:

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

`data.table` como un `OutputDataSet` en R se admite en SQL Server 2017 acumulativa Update 14 (CU14) y versiones posteriores.

## <a name="python-script-execution-issues"></a>Problemas de ejecución de script de Python

Esta sección contiene problemas conocidos que son específicos de Python en ejecución en SQL Server, así como los problemas relativos a los paquetes de Python publicados por Microsoft, incluidos [revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package) y [microsoftml](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package).

### <a name="1-call-to-pretrained-model-fails-if-path-to-model-is-too-long"></a>1. Se produce un error en la llamada al modelo previamente entrenado si la ruta de acceso al modelo es demasiado largo

Si instaló los modelos previamente entrenados en una versión de SQL Server 2017, la ruta de acceso completa al archivo del modelo entrenado puede ser demasiado largo para Python leer. Esta limitación se ha corregido en una versión posterior del servicio.

Hay varias soluciones posibles: 

+ Cuando se instalación en los modelos previamente entrenados, elija una ubicación personalizada.
+ Si es posible, instale la instancia de SQL Server en una ruta de instalación personalizada con una ruta más corta, como C:\SQL\MSSQL14. MSSQLSERVER.
+ Use la utilidad Windows [Fsutil](https://technet.microsoft.com/library/cc788097(v=ws.11).aspx) para crear un vínculo físico que el archivo de modelo se asigna a una ruta más corta.
+ Actualice a la versión más reciente del servicio.

### <a name="2-error-when-saving-serialized-model-to-sql-server"></a>2. Error al guardar serializa el modelo a SQL Server

Al pasar un modelo a una instancia remota de SQL Server y si se intenta leer el modelo binario mediante el `rx_unserialize` funcionando en [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package), puede aparecer el error: 

> *NameError: rx_unserialize_model' nombre' no está definido*

Este error se produce si ha guardado el modelo utilizando una versión reciente de la función de serialización, pero la instancia de SQL Server donde se deserializa el modelo no reconoce la API de serialización.

Para resolver el problema, actualice la instancia de SQL Server 2017 CU3 o posterior.

### <a name="3-failure-to-initialize-a-varbinary-variable-causes-an-error-in-bxlserver"></a>3. Error al inicializar una variable varbinary produce un error en BxlServer

Si ejecuta el código de Python en SQL Server mediante `sp_execute_external_script`y el código tiene variables de tipo varbinary (max), varchar (max) o tipos similares de salida, la variable debe inicializado o se establece como parte de la secuencia de comandos. En caso contrario, el componente de intercambio de datos, BxlServer, genera un error y deja de funcionar.

Esta limitación se corregirá en una próxima versión de servicio. Como alternativa, asegúrese de que se inicialice la variable dentro del script de Python. Puede usar cualquier valor válido, como en los ejemplos siguientes:

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

### <a name="4-telemetry-warning-on-successful-execution-of-python-code"></a>4. Advertencia de telemetría en la ejecución correcta del código de Python

A partir de SQL Server 2017 CU2, puede aparecer el siguiente mensaje incluso si el código de Python en caso contrario, se ejecuta correctamente:

> *Mensajes STDERR del script externo:* 
>  *~PYTHON_SERVICES\lib\site-packages\revoscalepy\utils\RxTelemetryLogger*
> *SyntaxWarning: telemetry_state es usar antes de la declaración global*

Este problema se corrigió en SQL Server 2017 actualización acumulativa 3 (CU3). 

### <a name="5-numeric-decimal-and-money-data-types-not-supported"></a>5. No admitidos los tipos de datos numérico, decimal y money

A partir de SQL Server 2017 acumulativa Update 12 (CU12), los tipos de datos numérico, decimal y money en WITH RESULT SETS no se admiten cuando se usa Python con `sp_execute_external_script`. Es posible que aparezcan los mensajes siguientes:

> *[Código: 39004, estado de SQL: S1000] se ha producido un error de script "Python" durante la ejecución de 'sp_execute_external_script' con HRESULT 0 x 80004004.*

> *[Código: 39019, estado de SQL: S1000] se ha producido un error de script externo:*
> 
> *Error de SqlSatelliteCall: Tipo no compatible en el esquema de salida. Tipos admitidos: bit, smallint, int, datetime, smallmoney, real y float. Char, varchar se admite parcialmente.*

Esto se ha solucionado en SQL Server 2017 acumulativa Update 14 (CU14).

## <a name="revolution-r-enterprise-and-microsoft-r-open"></a>Revolution R Enterprise y Microsoft R Open

Esta sección enumeran los problemas específicos de conectividad de R, desarrollo y las herramientas de rendimiento que proporcionan Revolution Analytics. Estas herramientas se proporcionaron en versiones preliminares anteriores de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].

En general, se recomienda que desinstale estas versiones anteriores e instale la versión más reciente de SQL Server o Microsoft R Server.

### <a name="1-revolution-r-enterprise-is-not-supported"></a>1. No se admite Revolution R Enterprise

Instalación en paralelo de Revolution R Enterprise con cualquier versión de [!INCLUDE[rsql_productname_md](../includes/rsql-productname-md.md)] no se admite.

Si tiene una licencia existente de Revolution R Enterprise, debe colocarla en un equipo independiente desde el [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] instancia y cualquier estación de trabajo que desea usar para conectarse a la [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] instancia.

Algunas versiones preliminares de [!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)] incluye un entorno de desarrollo de R para Windows creado mediante Revolution Analytics. Esta herramienta ya no está disponible y no se admite.

Para ofrecer compatibilidad con [!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)], le recomendamos que instale Microsoft R Client en su lugar. [Herramientas de R para Visual Studio](https://www.visualstudio.com/vs/rtvs/) y [Visual Studio Code](https://code.visualstudio.com/) también es compatible con soluciones de Microsoft R.

### <a name="2-compatibility-issues-with-sqlite-odbc-driver-and-revoscaler"></a>2. Problemas de compatibilidad con el controlador ODBC de SQLite y RevoScaleR

Revisión 0.92 del controlador ODBC de SQLite es compatible con RevoScaleR. Las revisiones de 0.88 a 0.91 y 0.93 y posteriormente se sabe que son compatibles.

## <a name="see-also"></a>Vea también

[Novedades de SQL Server 2016](../sql-server/what-s-new-in-sql-server-2016.md)

[Solución de problemas de aprendizaje automático en SQL Server](machine-learning-troubleshooting-faq.md)
