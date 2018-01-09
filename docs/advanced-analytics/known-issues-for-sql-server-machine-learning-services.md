---
title: "Problemas conocidos de los servicios de aprendizaje de máquina | Documentos de Microsoft"
ms.date: 11/16/2017
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2b37a63a-5ff5-478e-bcc2-d13da3ac241c
caps.latest.revision: "53"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: b46930980f845294a1a9fefa056c2e71a9cecae0
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="known-issues-in-machine-learning-services"></a>Problemas conocidos en servicios de aprendizaje de máquina

Este artículo describen los problemas conocidos o limitaciones con componentes que se proporcionan como una opción en SQL Server 2016 y SQL Server 2017 de aprendizaje automático.

Esta información se aplica a todas las opciones siguientes, a menos que se indique lo contrario:

* SQL Server 2016

  - R Services (en bases de datos)
  - Microsoft R Server (independiente)

* SQL Server 2017

  - Servicios de R (en bases de datos) de aprendizaje automático
  - Servicios para Python (en bases de datos) de aprendizaje automático
  - Machine Learning Server (independiente)

## <a name="setup-and-configuration-issues"></a>Problemas de instalación y configuración

Para obtener una descripción de los procesos y preguntas comunes relacionadas con la instalación inicial y la configuración, consulte [preguntas más frecuentes de actualización e instalación](r/upgrade-and-installation-faq-sql-server-r-services.md). Contiene información acerca de las actualizaciones, en paralelo e instalación de nuevos componentes de R o Python.

### <a name="unable-to-install-sql-server-machine-learning-features-on-a-domain-controller"></a>No se puede instalar características de aprendizaje de máquina de SQL Server en un controlador de dominio

Si intenta instalar SQL Server 2016 R Services o servicios de aprendizaje de SQL Server de 2017 máquinas en un controlador de dominio, el programa de instalación produce un error, con estos errores:

>*"Se ha producido un error durante el proceso de instalación de la característica".*
> 
>*"No se encuentra el grupo con identidad..."*
> 
>*"Código de error de componente: 0 x 80131509"*

El error se produce porque, en un controlador de dominio, el servicio no puede crear el 20 cuentas locales deben ejecutar el aprendizaje automático. En general, no se recomienda instalar SQL Server en un controlador de dominio. Para obtener más información, consulte [boletín de soporte técnico 2032911](https://support.microsoft.com/en-us/help/2032911/you-may-encounter-problems-when-installing-sql-server-on-a-domain-cont).

### <a name="install-the-latest-service-release-to-ensure-compatibility-with-microsoft-r-client"></a>Instalar la versión más reciente del servicio para garantizar la compatibilidad con el cliente de Microsoft R

Si instala la versión más reciente del cliente de Microsoft R y utilizarlo para ejecutar R en SQL Server en un contexto de proceso remoto, podría obtener un error similar al siguiente:

>*Se ejecutan 9.x.x de versión del cliente de Microsoft R en el equipo, que es incompatible con Microsoft R Server versión 8.x.x. Download and install a compatible version.* (Está ejecutando la versión 9.0.0 del Cliente de Microsoft R en el equipo, que es incompatible con Microsoft R Server versión 8.0.3. Descargue e instale una versión compatible).

SQL Server 2016 requiere que las bibliotecas de R en el cliente coinciden exactamente con las bibliotecas de R en el servidor. La restricción se ha quitado para las versiones posteriores a R Server 9.0.1. Sin embargo, si se produce este error, compruebe la versión de las bibliotecas de R que se usa el cliente y el servidor y, si es necesario, actualice el cliente para que coincida con la versión del servidor.

La versión de R que se instala con SQL Server R Services se actualiza cada vez que se instala una versión de servicio de SQL Server. Para asegurarse de que siempre tiene las versiones más recientes de componentes de R, asegúrese de instalar todos los service packs.

Para garantizar la compatibilidad con el cliente de Microsoft R 9.0.0, instale las actualizaciones que se describen en este [artículo de soporte técnico](https://support.microsoft.com/kb/3210262).

Para evitar problemas con los paquetes de R, también puede actualizar la versión de las bibliotecas de R que se instalan en el servidor, cambiando a la directiva de ciclo de vida moderna que se describe en [la siguiente sección](#bkmk_sqlbindr). Al hacerlo, se actualiza la versión de R que se instala con SQL Server en la misma programación que se publiquen las actualizaciones de Microsoft R Server, lo que garantiza que tanto el servidor como el cliente siempre tienen las versiones más recientes de Microsoft R.

**Se aplica a:** SQL Server 2016 R Services, con R Server versión 9.0.0 o versiones anteriores

### <a name="unable-to-install-python-components-in-offline-installations-of-sql-server-2017-ctp-20-or-later"></a>No se puede instalar componentes de Python en instalaciones sin conexión de SQL Server de 2017 CTP 2.0 o posterior

Si instala una versión preliminar de 2017 de SQL Server en un equipo sin acceso a internet, se puede producir un error en el programa de instalación mostrar la página que solicita la ubicación de los componentes de Python descargados. En ese caso, puede instalar la característica Servicios de aprendizaje de máquina, pero no los componentes de Python.

Este problema se corrigió en la versión de lanzamiento. Si se produce este problema, como alternativa, puede habilitar temporalmente acceso a internet para la duración de la instalación. Esta limitación no se aplica a R.

**Se aplica a:** 2017 de SQL Server con Python ### <a name="bkmk_sqlbindr"> </a> de versión no compatible de advertencia cuando se conecta a una versión anterior de SQL Server R Services desde un cliente mediante el uso de[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]

Cuando se ejecuta código de R en un contexto de proceso de SQL Server 2016 y cualquiera de las dos instrucciones siguientes es verdadera, podría aparecer un error similar al siguiente:
* Instaló R Server (independiente) en un equipo cliente mediante el Asistente para instalación [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)].
* Ha instalado Microsoft R Server usando el [separar Windows installer](https://docs.microsoft.com/r-server/install/r-server-install-windows).

>*Está ejecutando la versión 9.0.0 R del cliente de Microsoft en el equipo, que es incompatible con la versión 8.0.3 de Microsoft R Server. Download and install a compatible version.* (Está ejecutando la versión 9.0.0 del Cliente de Microsoft R en el equipo, que es incompatible con Microsoft R Server versión 8.0.3. Descargue e instale una versión compatible).

Puede usar _enlace_ en Microsoft R Server 9.0 y versiones posteriores, para actualizar los componentes de R en instancias de SQL Server 2016. Para determinar si son compatibles con las actualizaciones para su versión de servicios de R, consulte [actualizar una instancia de servicios de R mediante SqlBindR.exe](/r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

**Se aplica a:** SQL Server 2016 R Services, con R Server versión 9.0.0 o versiones anteriores

### <a name="setup-for-sql-server-2016-service-releases-might-fail-to-install-newer-versions-of-r-components"></a>La instalación de las versiones de servicio de SQL Server 2016 podrían producir un error al instalar versiones más recientes de los componentes de R

Cuando se instala una actualización acumulativa o instala un service pack para SQL Server 2016 en un equipo que no está conectado a internet, el Asistente para la instalación podría producir mostrar el símbolo del sistema que le permite actualizar los componentes de R mediante el uso de archivos .cab descargados. Este error se produce normalmente cuando varios componentes se instalaron con el motor de base de datos.

Como alternativa, puede instalar la versión de servicio utilizando la línea de comandos y especificando la */MRCACHEDIRECTORY* argumento tal como se muestra en este ejemplo, que instala las actualizaciones de CU1:

`C:\<path to installation media>\SQLServer2016-KB3164674-x64.exe /Action=Patch /IACCEPTROPENLICENSETERMS /MRCACHEDIRECTORY=<path to CU1 CAB files>`

Para obtener los instaladores más recientes, consulte [instalar componentes de aprendizaje de máquina sin acceso a internet](r/installing-ml-components-without-internet-access.md).

**Se aplica a:** SQL Server 2016 R Services, con R Server versión 9.0.0 o versiones anteriores

### <a name="launchpad-services-fails-to-start-if-the-version-is-different-from-the-r-version"></a>No se puede iniciar si la versión es diferente de la versión de R services LaunchPad

Si instala SQL Server R Services por separado desde el motor de base de datos y las versiones de compilación son diferentes, puede ver el error siguiente en el registro de eventos del sistema:

>_El servicio Launchpad de SQL Server no pudo iniciarse debido al siguiente error: el servicio no respondió a la solicitud de inicio o control de manera oportuna._

Por ejemplo, este error podría producirse si instala el motor de base de datos mediante el uso de la versión de lanzamiento, aplicar una revisión para actualizar el motor de base de datos y, a continuación, agregar la característica Servicios de R mediante la versión de lanzamiento.

Para evitar este problema, asegúrese de que todos los componentes tengan el mismo número de versión. Si actualiza un componente, asegúrese de aplicar la misma actualización a los demás componentes instalados.

Para ver una lista de los números de versión de R que son necesarias para cada versión de SQL Server 2016, vea [componentes instalar R sin acceso a internet](r/installing-ml-components-without-internet-access.md).

### <a name="remote-compute-contexts-are-blocked-by-a-firewall-in-sql-server-instances-that-are-running-on-azure-virtual-machines"></a>Contextos de proceso remoto bloqueados por un firewall en instancias de SQL Server que se ejecutan en máquinas virtuales de Azure

Si ha instalado [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] en una máquina virtual de Windows Azure, no puede usar los contextos de proceso que requieren el uso del área de trabajo de la máquina virtual. El motivo es que, de forma predeterminada, el firewall en máquinas virtuales de Azure incluye una regla que bloquea la red acceso para las cuentas de usuario locales de R.

Como alternativa, en la máquina virtual de Azure, abra **Firewall de Windows con seguridad avanzada**, seleccione **reglas de salida**y deshabilite la regla siguiente: **bloquear el acceso de red para las cuentas de usuario local de R en Instancia de SQL Server MSSQLSERVER**. También puede dejar la regla habilitada, pero cambie la propiedad de seguridad a **permitir si es seguro**.

### <a name="implied-authentication-in-sqlexpress"></a>Autenticación implícita en SQLEXPRESS

Al ejecutar trabajos de R desde una estación de trabajo de ciencia de datos remoto mediante la autenticación integrada de Windows, SQL Server usa *autenticación implícita* para generar las llamadas ODBC locales que podrían ser requeridas por la secuencia de comandos. Pero esta característica no funcionaba en la compilación RTM de SQL Server Express Edition.

Para corregir el problema, se recomienda que actualice a una versión de servicio posterior.

Si no puede actualizar, use un inicio de sesión de SQL para ejecutar los trabajos de R remotos que requieran llamadas ODBC incrustadas.

**Se aplica a:** Express Edition de servicios de SQL Server 2016 R

### <a name="performance-limits-when-libraries-used-by-sql-server-are-called-from-other-tools"></a>Límites de rendimiento cuando se llaman a bibliotecas utilizadas por SQL Server desde otras herramientas

Es posible llamar al bibliotecas que se instalan para SQL Server desde una aplicación externa, como RGui de aprendizaje automático. Si lo hace, podría ser la manera más conveniente para realizar ciertas tareas, como instalar nuevos paquetes, o ejecutar pruebas ad hoc en los ejemplos de código muy breve. Sin embargo, fuera de SQL Server, rendimiento podría ser limitado. 

Por ejemplo, incluso si está utilizando SQL Server Enterprise Edition, R se ejecuta en modo de un único subproceso cuando se ejecuta el código de R con herramientas externas. Para obtener las ventajas de rendimiento en SQL Server, iniciar una conexión de SQL Server y usar [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) para llamar en tiempo de ejecución de script externo.

+ En general, evite llamar al bibliotecas que se utilizan con SQL Server desde herramientas externas de aprendizaje automático.
+ Si tiene que depurar R o código de Python, es normalmente más fácil hacerlo fuera de SQL Server. Para obtener las mismas bibliotecas que se encuentran en SQL Server, puede instalar el cliente de Microsoft R o [servidor de aprendizaje de máquina](r/create-a-standalone-r-server.md).

### <a name="external-script-execution-is-throttled-due-to-resource-governance-default-values"></a>Ejecución de scripts externos está limitada debido a los valores predeterminados de regulación de recursos

En Enterprise Edition, puede usar grupos de recursos para administrar procesos de script externos. En algunas versiones de lanzamiento temprano, la memoria máxima que se puede asignar a los procesos de R era un 20 por ciento. Por lo tanto, si el servidor tiene 32 GB de RAM, los archivos ejecutables de R (RTerm.exe y BxlServer.exe) pueden utilizar un máximo de 6,4 GB en una sola solicitud.

Si se producen las limitaciones de recursos, compruebe el valor predeterminado actual. Si el 20 por ciento no es suficiente, consulte la documentación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] sobre cómo cambiar este valor.

**Se aplica a:** R Services SQL Server 2016, Enterprise Edition

## <a name="r-issues"></a>Problemas de R

Esta sección contiene los problemas conocidos que son específicos para ejecutar código R en SQL Server, así como algunos problemas que están relacionados con las bibliotecas de R y herramientas publicados por Microsoft, incluidos los RevoScaleR.

Para otros problemas conocidos que podrían afectar a las soluciones de R, vaya a la [sitio Microsoft R Server](https://docs.microsoft.com/machine-learning-server/resources-known-issues).

### <a name="limitations-on-processor-affinity-for-r-jobs"></a>Limitaciones de la afinidad del procesador para trabajos de R

En la compilación de lanzamiento inicial de SQL Server 2016, se podía establecer la afinidad del procesador solo para la CPU en el primer grupo de k. Por ejemplo, si el servidor es una máquina de socket de 2 con dos grupos k, procesadores solo desde el primer grupo de k se usan para los procesos de R. La misma limitación se aplica al configurar el regulador de recursos para trabajos de script de R.

Este problema está corregido en SQL Server 2016 Service Pack 1. Se recomienda que actualice a la versión más reciente del servicio.

**Se aplica a:** versión RTM de SQL Server 2016 R Services

### <a name="changes-to-column-types-cannot-be-performed-when-reading-data-in-a-sql-server-compute-context"></a>No se pueden realizar cambios en los tipos de columna al leer datos en un contexto de proceso de SQL Server

Si el contexto de proceso está establecido en la instancia de SQL Server, no puede usar el argumento _colClasses_ (u otros argumentos similares) para cambiar el tipo de datos de las columnas en el código de R.

Por ejemplo, la instrucción siguiente producirá un error si la columna CRSDepTimeStr no es ya un entero:

```r
data <- RxSqlServerData(sqlQuery = "SELECT CRSDepTimeStr, ArrDelay  FROM AirlineDemoSmall",
                                connectionString = connectionString,
                                colClasses = c(CRSDepTimeStr = "integer"))
```

Como alternativa, puede volver a escribir la consulta SQL para utilizar CAST o convertir y presentar los datos en R utilizando el tipo de datos correcto. En general, rendimiento es mejor cuando se trabaja con datos mediante SQL en lugar de cambiar los datos en el código de R.

**Se aplica a:** R Services SQL Server 2016

### <a name="limits-on-size-of-serialized-models"></a>Límites de tamaño de los modelos serializados

Al guardar un modelo en una tabla de SQL Server, debe serializar el modelo y guardarla en un formato binario. En teoría, el tamaño máximo de un modelo que se pueden almacenar con este método es 2 GB, que es el tamaño máximo de columnas de varbinary de SQL Server.

Si necesita utilizar modelos más grandes, están disponibles las siguientes soluciones alternativas:

+ Tomar medidas para reducir el tamaño del modelo. Algunos paquetes de código abierto R incluir una gran cantidad de información en el objeto de modelo y gran parte de esta información se puede quitar para la implementación. 
+ Usar selección de características para quitar las columnas innecesarias.
+ Si usa un algoritmo de código abierto, considere la posibilidad de una implementación similar mediante el algoritmo correspondiente en MicrosoftML o RevoScaleR. Estos paquetes se han optimizado para escenarios de implementación.
+ Después de que el modelo se ha racionalizado y reduce el tamaño con los pasos anteriores, vea si la [memCompress](https://www.rdocumentation.org/packages/base/versions/3.4.1/topics/memCompress) función de R base puede utilizarse para reducir el tamaño del modelo antes de pasarlo a SQL Server. Esta opción es mejor cuando el modelo está cerca del límite de 2 GB.
+ Para los modelos más grandes, puede usar SQL Server [FileTable](..\relational-databases\blob\filetables-sql-server.md) característica para almacenar los modelos, en lugar de utilizar una columna varbinary.

    Para usar FileTables, debe agregar una excepción de firewall, porque los datos almacenados en FileTables está administrados por el controlador de sistema de archivos de Filestream en SQL Server y las reglas de firewall predeterminada bloquean el acceso de archivos de red. Para obtener más información, consulte [habilitar los requisitos previos para FileTable](../relational-databases/blob/enable-the-prerequisites-for-filetable.md). 

    Después de haber habilitado FileTable, para escribir el modelo, obtiene una ruta de acceso de SQL mediante la API de FileTable y, a continuación, escribir el modelo en esa ubicación desde el código. Cuando tiene que leer el modelo, obtiene la ruta de acceso de SQL y, a continuación, llamar a del modelo utilizando la ruta de acceso de la secuencia de comandos. Para obtener más información, consulte [obtener acceso a FileTables con API de archivo de entrada y salida](../relational-databases/blob/access-filetables-with-file-input-output-apis.md).

### <a name="avoid-clearing-workspaces-when-you-execute-r-code-in-a-includessnoversionincludesssnoversion-mdmd-compute-context"></a>Evitar borrar áreas de trabajo cuando se ejecuta código de R en un [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] contexto de proceso

Si utiliza el comando R para borrar el área de trabajo de los objetos mientras se ejecuta código R en un [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] cálculo, o si desactiva el área de trabajo como parte de un script de R llama mediante [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), es posible que obtenga este Error: 

>*objeto de área de trabajo no se encontró ' revoScriptConnection'*

`revoScriptConnection` es un objeto del área de trabajo de R que contiene información sobre una sesión de R a la que se llama desde [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Pero si su código de R incluye un comando para borrar el área de trabajo (como `rm(list=ls()))`, también se borrarán toda la información sobre la sesión y otros objetos del área de trabajo de R.

Como alternativa, evitar indiscriminado borrado de las variables y otros objetos mientras ejecuta R en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Aunque el área de trabajo de acción de borrar es común cuando se trabaja en la consola de R, puede tener consecuencias no deseadas.

* Para eliminar variables específicas, use el objeto R *quitar* función: `remove('name1', 'name2', ...)`.
* Si quiere eliminar varias variables, guarde los nombres de las variables temporales en una lista y realice periódicamente la recolección de elementos no utilizados.

### <a name="restrictions-on-data-that-can-be-provided-as-input-to-an-r-script"></a>Restricciones en los datos que se pueden proporcionar como entrada para un script de R

No puede usar un script de R en los siguientes tipos de resultados de consulta:

- Datos de una consulta de [!INCLUDE[tsql](../includes/tsql-md.md)] que haga referencia a columnas AlwaysEncrypted.
  
- Datos de una consulta de [!INCLUDE[tsql](../includes/tsql-md.md)] que haga referencia a columnas enmascaradas.
  
     Si necesita usar datos enmascaradas en un script de R, una posible solución alternativa es realizar una copia de los datos en una tabla temporal y usar esos datos en su lugar.

### <a name="use-of-strings-as-factors-can-lead-to-performance-degradation"></a>Uso de cadenas como factores pueden provocar una degradación del rendimiento

Uso de variables de tipo de cadena como factores pueden aumentar considerablemente la cantidad de memoria utilizada para las operaciones de R. Se trata de un problema conocido con R en general, y hay muchos artículos sobre el tema. Por ejemplo, vea [factores no son objetos de primera clase en R, mediante el montaje de Juan, en blogs de R)](https://www.r-bloggers.com/factors-are-not-first-class-citizens-in-r/) o [stringsAsFactors: una biografía no autorizada, por Roger Peng](https://simplystatistics.org/2015/07/24/stringsasfactors-an-unauthorized-biography/). 

Aunque el problema no es específico de SQL Server, puede afectar considerablemente al rendimiento del código de R que se ejecutan en SQl Server. Las cadenas se almacenan normalmente como varchar o nvarchar y, si una columna de datos de cadena tiene muchos valores únicos, el proceso de convertir internamente estos números enteros y de vuelta a cadenas de R incluso puede provocar errores de asignación de memoria.

Si no requiera un tipo de datos de cadena para otras operaciones, asignar los valores de cadena en un valor numérico (entero) tipo de datos como parte de la preparación de datos sería beneficioso desde la perspectiva del rendimiento y la escalabilidad.

Para obtener una descripción de este problema y otras sugerencias, vea [rendimiento para los servicios de R - optimización datos](r/r-and-data-optimization-r-services.md).

### <a name="arguments-varstokeep-and-varstodrop-are-not-supported-for-sql-server-data-sources"></a>Argumentos *varsToKeep* y *varsToDrop* no se admiten para los orígenes de datos de SQL Server

Cuando utilice la función rxDataStep para escribir los resultados en una tabla, con el *varsToKeep* y *varsToDrop* es una forma práctica de especificar las columnas para incluir o excluir como parte de la operación. Sin embargo, estos argumentos no se admiten para los orígenes de datos de SQL Server.

### <a name="limited-support-for-sql-data-types-in-spexecuteexternalscript"></a>Compatibilidad limitada para tipos de datos SQL en`sp_execute_external_script`

No todos los tipos de datos que se admiten en SQL pueden usarse en R. Como solución alternativa, considere la posibilidad de convertir el tipo de datos no admitido a un tipo de datos compatible antes de pasar los datos a sp_execute_external_script.

Para obtener más información, consulte [tipos de datos y las bibliotecas de R](r/r-libraries-and-data-types.md).

### <a name="possible-string-corruption"></a>Posibles daños en una cadena

Cualquier de ida y vuelta de datos de cadena de [!INCLUDE[tsql](../includes/tsql-md.md)] para R y, a continuación, [!INCLUDE[tsql](../includes/tsql-md.md)] puede producir daños. Esto es debido a las diferentes codificaciones que se usan en R y en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], así como las distintas intercalaciones y lenguajes que se admiten en R y [!INCLUDE[tsql](../includes/tsql-md.md)]. Cualquier cadena con una codificación que no sea ASCII puede controlarse potencialmente de manera incorrecta.

Cuando se envían datos de cadena a R, convertirlo en una representación ASCII, si es posible.

Esta limitación se aplica a los datos que se pasan entre SQL Server y Python así. Caracteres multibyte se deben pasar como UTF-8 y almacenan como datos Unicode.

### <a name="only-one-value-of-type-raw-can-be-returned-from-spexecuteexternalscript"></a>Solo un valor de tipo `raw` puede devolverse desde`sp_execute_external_script`

Cuando un tipo de datos binarios (I+d **sin formato** tipo de datos) se devuelve desde R, el valor se debe enviar en la trama de datos de salida.

Con datos de tipos distintos de **sin formato**, pueden devolver valores de parámetro junto con los resultados del procedimiento almacenado mediante la adición de la palabra clave OUTPUT. Para obtener más información, consulte [parámetros](https://docs.microsoft.com/sql/relational-databases/stored-procedures/parameters).

Si desea utilizar varios conjuntos de resultados que incluyen valores de tipo **sin formato**, una posible solución alternativa es realizar varias llamadas de procedimiento almacenado, o para enviar el resultado conjunto a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mediante ODBC.

### <a name="loss-of-precision"></a>Pérdida de precisión

Dado que [!INCLUDE[tsql](../includes/tsql-md.md)] y R admiten diversos tipos de datos, tipos de datos numéricos pueden perder precisión durante la conversión.

Para obtener más información acerca de la conversión implícita del tipo de datos, vea [tipos de datos y las bibliotecas de R](r/r-libraries-and-data-types.md).

### <a name="variable-scoping-error-when-you-use-the-transformfunc-parameter-the-sample-data-set-for-the-analysis-has-no-variables"></a>Error de ámbito cuando se usa el parámetro transformFunc de variable: *el conjunto de datos de ejemplo para el análisis no tiene variables*

Para transformar los datos mientras se realiza el modelado, puede pasar un *transformFunc* argumento en una función como `rxLinmod` o `rxLogit`. Sin embargo, llamadas a funciones anidadas pueden provocar errores de ámbito en el contexto de proceso de SQL Server, incluso si las llamadas funcionan correctamente en el contexto de proceso local.

Por ejemplo, supongamos que ha definido dos funciones, `f` y `g`, en su entorno global local, y `g` llamadas `f`. En las llamadas remotas o distribuidas en las que participa `g`, la llamada a `g` podría generar un error porque no se encuentra `f` , incluso si ha pasado `f` y `g` a la llamada remota.

Si se produce este problema, puede solucionarlo insertando la definición de `f` en la definición de `g`, en cualquier lugar antes de que `g` llame a `f`.

Por ejemplo:

```r
f <- function(x) { 2*x * 3 }
g <- function(y) {
              a <- 10 * y
               f(a)
}
```

Para evitar el error, vuelva a escribir la definición de los siguientes:

```r
g <- function(y){
              f <- function(x) { 2*x +3}
              a <- 10 * y
              f(a)
}
```

### <a name="data-import-and-manipulation-using-revoscaler"></a>Importación de datos y manipulación con RevoScaleR

Cuando **varchar** columnas se leen desde una base de datos se recortan los espacios en blanco. Para evitarlo, ponga las cadenas entre caracteres que no sean espacios en blanco.

Cuando las funciones como `rxDataStep` se utilizan para crear las tablas de base de datos que tienen **varchar** columnas, el ancho de columna se calcula en función de una muestra de los datos. Si el ancho varía, podría ser necesario rellenar todas las cadenas con una longitud común.

El uso de una transformación para cambiar el tipo de datos de una variable no se admite cuando se usan llamadas repetidas a `rxImport` o `rxTextToXdf` para importar y anexar filas combinando varios archivos de entrada en un solo archivo .xdf.

### <a name="limited-support-for-rxexec"></a>Compatibilidad limitada con rxexec

En SQL Server 2016, el `rxExec` función que se proporciona el RevoScaleR paquete se puede utilizar sólo en modo de subproceso único.

Paralelismo de `rxExec` en varios procesos se ha planeado para una versión futura.

### <a name="increase-the-maximum-parameter-size-to-support-rxgetvarinfo"></a>Aumentar el tamaño máximo de parámetro para admitir rxGetVarInfo

Si usa conjuntos de datos con un número muy elevado de variables (por ejemplo, más de 40 000), establezca el `max-ppsize` marca al iniciar R para usar funciones como `rxGetVarInfo`. La marca `max-ppsize` especifica el tamaño máximo de la pila de protección del puntero.

Si usa la consola de R (por ejemplo, en rgui.exe o rterm.exe), puede establecer el valor de max-ppsize en 500 000. Para ello, escriba lo siguiente:

```r
R --max-ppsize=500000
```

Si usas el [!INCLUDE[rsql_developr](../includes/rsql-developr-md.md)] entorno, puede establecer el `max-ppsize` marca mediante la realización de la siguiente llamada al ejecutable RevoIDE:

```
RevoIDE.exe /RCommandLine --max-ppsize=500000  
```

### <a name="issues-with-the-rxdtree-function"></a>Problemas con la función rxDTree

La función `rxDTree` no admite actualmente transformaciones en la fórmula. En particular, no se admite el uso de la sintaxis `F()` para crear factores sobre la marcha. Sin embargo, automáticamente se segmentan los datos numéricos.

Los factores ordenados se tratan igual que los factores de todas las funciones de análisis RevoScaleR, excepto `rxDTree`.

## <a name="python-code-execution-or-python-package-issues"></a>La ejecución de código Python o problemas de paquete de Python

Esta sección contiene los problemas conocidos que son específicos a la ejecución de Python a SQL Server, así como problemas relacionados con los paquetes de Python publicados por Microsoft, incluidos los [revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package) y [microsoftml](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package).

### <a name="call-to-pretrained-model-fails-if-path-to-model-is-too-long"></a>Se produce un error en la llamada al modelo previamente entrenado si la ruta de acceso al modelo es demasiado largo

Si instala los modelos previamente entrenados en una instalación predeterminada, según el nombre del equipo y el nombre de instancia, la ruta de acceso completa resultante en el archivo de modelo entrenado puede ser demasiado largo para Python leer. Esta limitación se corregirá en una versión de próximos servicios.

Hay varias soluciones posibles: 

+ Al instalar los modelos previamente entrenados, elija una ubicación personalizada.
+ Si es posible, instale la instancia de SQL Server en una ruta de acceso de instalación personalizada, como C:\SQL\MSSQL14. MSSQLSERVER.
+ Utilice la utilidad Windows [Fsutil](https://technet.microsoft.com/library/cc788097(v=ws.11).aspx) para crear un vínculo físico que el archivo de modelo se asigna a una ruta más corta. 

### <a name="failure-to-initialize-a-varbinary-variable-causes-an-error-in-bxlserver"></a>Error al inicializar una variable varbinary provoca un error en BxlServer

Si ejecuta el código Python en SQL Server mediante `sp_execute_external_script`y el código tiene las variables de tipo varbinary (max), varchar (max) u otros tipos similares de salida, la variable se debe inicializar o bien establecerse como parte de la secuencia de comandos. En caso contrario, el componente de intercambio de datos, BxlServer, genera un error y deja de funcionar.

Esta limitación se corregirá en una versión de próximos servicios. Como alternativa, asegúrese de que la variable se inicializa dentro del script de Python. Puede utilizarse cualquier valor válido, como en los ejemplos siguientes:

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

## <a name="revolution-r-enterprise-and-microsoft-r-open"></a>Revolution R Enterprise y Microsoft R Open

Esta sección enumeran los problemas específicos de las herramientas de rendimiento que proporcionan Revolution Analytics, el desarrollo y la conectividad de R. Estas herramientas se proporcionaron en versiones anteriores de una versión preliminar de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].

En general, recomendamos que desinstale las versiones anteriores y que instale la versión más reciente de SQL Server o Microsoft R Server.

### <a name="running-side-by-side-versions-of-revolution-r-enterprise"></a>Ejecutan versiones en paralelo de Revolution R Enterprise

Instalación en paralelo de Revolution R Enterprise con cualquier versión de [!INCLUDE[rsql_productname_md](../includes/rsql-productname-md.md)] no se admite.

Si tiene una licencia para usar una versión diferente de Revolution R Enterprise, debe colocarla en un equipo diferente de donde se encuentran la instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y las estaciones de trabajo que quiera usar para conectarse a la instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .

### <a name="the-use-of-an-r-productivity-environment-is-not-supported"></a>No se admite el uso de un entorno de productividad de R

Algunas versiones preliminares de [!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)] incluye un entorno de desarrollo de R para Windows creado mediante Revolution Analytics. Esta herramienta ya no está disponible y no se admite.

Para ofrecer compatibilidad con [!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)], se recomienda encarecidamente que instale Microsoft R Client o Microsoft R Server en lugar de las herramientas de Revolution Analytics. [R Tools para Visual Studio](https://www.visualstudio.com/vs/rtvs/) y [código de Visual Studio](https://code.visualstudio.com/) también es compatible con soluciones de Microsoft R.

### <a name="compatibility-issues-with-sqlite-odbc-driver-and-revoscaler"></a>Problemas de compatibilidad con el controlador ODBC de SQLite y RevoScaleR

Revisión 0.92 del controlador ODBC de SQLite es compatible con RevoScaleR. Las revisiones de 0.88 a 0.91 y 0.93 y versiones posteriores se sabe que son compatibles.


## <a name="see-also"></a>Vea también

[Novedades de SQL Server 2016](../sql-server/what-s-new-in-sql-server-2016.md)

[Solución de problemas de aprendizaje automático en SQL Server](machine-learning-troubleshooting-faq.md)
