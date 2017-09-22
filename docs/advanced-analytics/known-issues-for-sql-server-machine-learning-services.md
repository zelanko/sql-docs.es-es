---
title: "Problemas conocidos de los servicios de aprendizaje de máquina | Documentos de Microsoft"
ms.custom:
- SQL2016_New_Updated
ms.date: 09/19/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2b37a63a-5ff5-478e-bcc2-d13da3ac241c
caps.latest.revision: 53
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: a6aeda8e785fcaabef253a8256b5f6f7a842a324
ms.openlocfilehash: 2d21756a05e9e51379faa194ec331517e510988d
ms.contentlocale: es-es
ms.lasthandoff: 09/21/2017

---
# <a name="known-issues-in-machine-learning-services"></a>Problemas conocidos en servicios de aprendizaje de máquina

Este artículo describen los problemas conocidos o limitaciones con componentes que se proporcionan como una opción en SQL Server 2016 y SQL Server 2017 de aprendizaje automático.

Esta información se aplica a todas las opciones siguientes, a menos que se indique específicamente:

* SQL Server 2016

  - R Services (en bases de datos)
  - Microsoft R Server (independiente)

* SQL Server 2017

  - Servicios de R (en bases de datos) de aprendizaje automático
  - Servicios para Python (en bases de datos) de aprendizaje automático
  - Machine Learning Server (independiente)

## <a name="setup-and-configuration-issues"></a>Problemas de instalación y configuración

Para obtener una descripción de los procesos y preguntas comunes relacionadas con la instalación inicial y la configuración, consulte [preguntas más frecuentes de actualización e instalación](r/upgrade-and-installation-faq-sql-server-r-services.md). Contiene información acerca de las actualizaciones, en paralelo e instalación de nuevos componentes de R o Python.

### <a name="unable-to-install-python-components-in-offline-installations-of-sql-server-2017-ctp-20-or-later"></a>No se puede instalar componentes de Python en instalaciones sin conexión de SQL Server de 2017 CTP 2.0 o posterior

Si instala una versión preliminar de 2017 de SQL Server en un equipo sin acceso a internet, se puede producir un error en el programa de instalación mostrar la página que solicita la ubicación de los componentes de Python descargados. En ese caso, puede instalar la característica Servicios de aprendizaje de máquina, pero no los componentes de Python.

Este problema se corrigió en la versión de lanzamiento. Si se produce este problema, como alternativa, puede habilitar temporalmente acceso a internet para la duración de la instalación. Esta limitación no se aplica a R.

**Se aplica a:** SQL Server 2017 con Python

### <a name="install-the-latest-service-release-to-ensure-compatibility-with-microsoft-r-client"></a>Instalar la versión más reciente del servicio para garantizar la compatibilidad con el cliente de Microsoft R

Si instala la versión más reciente del cliente de Microsoft R y utilizarlo para ejecutar R en SQL Server en un contexto de proceso remoto, podría obtener un error similar al siguiente:

>*Se ejecutan 9.x.x de versión del cliente de Microsoft R en el equipo, que es incompatible con Microsoft R Server versión 8.x.x. Download and install a compatible version.* (Está ejecutando la versión 9.0.0 del Cliente de Microsoft R en el equipo, que es incompatible con Microsoft R Server versión 8.0.3. Descargue e instale una versión compatible).

SQL Server 2016 requiere que las bibliotecas de R en el cliente coinciden exactamente con las bibliotecas de R en el servidor. La restricción se ha quitado para las versiones posteriores a R Server 9.0.1. Sin embargo, si se produce este error, compruebe la versión de las bibliotecas de R que se usa el cliente y el servidor y, si es necesario, actualice el cliente para que coincida con la versión del servidor.

La versión de R que se instala con SQL Server R Services se actualiza cada vez que se instala una versión de servicio de SQL Server. Para asegurarse de que siempre tiene las versiones más recientes de componentes de R, asegúrese de instalar todos los service packs.

Para garantizar la compatibilidad con el cliente de Microsoft R 9.0.0, instale las actualizaciones que se describen en este [artículo de soporte técnico](https://support.microsoft.com/kb/3210262).

Para evitar problemas con los paquetes de R, también puede actualizar la versión de las bibliotecas de R que se instalan en el servidor, cambiando a la directiva de ciclo de vida moderna que se describe en [la siguiente sección](#bkmk_sqlbindr). Al hacerlo, se actualiza la versión de R que se instala con SQL Server en la misma programación que se publiquen las actualizaciones de Microsoft R Server, lo que garantiza que tanto el servidor como el cliente siempre tienen las versiones más recientes de Microsoft R.

**Se aplica a:** SQL Server 2016 R Services, con R Server versión 9.0.0 o versiones anteriores

### <a name="bkmk_sqlbindr"></a>Cuando se conecta a una versión anterior de SQL Server R Services desde un cliente mediante el uso de advertencia de versión no compatible[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]

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

### <a name="performance-limits-when-r-libraries-are-called-from-other-r-tools"></a>Límites de rendimiento cuando se llaman a bibliotecas de R desde otras herramientas de R

Es posible llamar a las herramientas de R y las bibliotecas que se instalan para SQL Server desde una aplicación externa de R como RGui. Esta llamada puede resultar útil cuando se instalación nuevos paquetes, o cuando se ejecutan pruebas ad hoc en los ejemplos de código muy breve.

Sin embargo, tenga en cuenta que fuera de SQL Server, el rendimiento podría ser limitado. Por ejemplo, incluso si ha adquirido la edición Enterprise de SQL Server, R se ejecuta en modo de subproceso único cuando se ejecuta el código de R con herramientas externas. Rendimiento debería ser mejor si ejecuta el código de R e inicia una conexión de SQL Server y usando [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), que llama automáticamente a las bibliotecas de R.

* Evite llamar a las bibliotecas de R que se utilizan con SQL Server desde herramientas de R externas.
* Si tiene que ejecutar mucho código R en el equipo de SQL Server sin usar SQL Server, instale una instancia independiente de R, como el cliente de Microsoft R y, a continuación, asegúrese de que las herramientas de desarrollo de R señalen a la nueva biblioteca.

Para obtener más información, vea [Crear un R Server independiente](r/create-a-standalone-r-server.md).

### <a name="the-r-script-is-throttled-due-to-resource-governance-default-values"></a>El script de R está limitado debido a los valores predeterminados de regulación de recursos

En Enterprise Edition, puede usar grupos de recursos para administrar procesos de script externos. En algunas versiones de lanzamiento temprano, la memoria máxima que se puede asignar a los procesos de R era un 20 por ciento. Por lo tanto, si el servidor tiene 32 GB de RAM, los archivos ejecutables de R (RTerm.exe y BxlServer.exe) pueden utilizar un máximo de 6,4 GB en una sola solicitud.

Si se producen las limitaciones de recursos, compruebe el valor predeterminado actual. Si el 20 por ciento no es suficiente, consulte la documentación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] sobre cómo cambiar este valor.

**Se aplica a:** R Services SQL Server 2016, Enterprise Edition

## <a name="r-code-execution-and-package-or-function-issues"></a>Problemas de paquete o una función y la ejecución de código de R

Esta sección contiene los problemas conocidos que son específicos para ejecutar código R en SQL Server, así como algunos problemas que están relacionados con las bibliotecas de R y herramientas publicados por Microsoft, incluidos los RevoScaleR.

Para otros problemas conocidos que podrían afectar a las soluciones de R, vaya a la [sitio Microsoft R Server](https://msdn.microsoft.com/microsoft-r/rserver-known-issues).

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

Con datos de tipos distintos de **sin formato**, pueden devolver valores de parámetro junto con los resultados del procedimiento almacenado agregando la palabra clave OUTPUT. Para obtener más información, consulte [devolver datos mediante parámetros OUTPUT](https://technet.microsoft.com/library/ms187004.aspx).

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

## <a name="python-code-execution-or-python-package-issues"></a>La ejecución de código Python o problemas de paquete de Python

Esta sección contiene los problemas conocidos que son específicos a la ejecución de Python a SQL Server, así como problemas relacionados con los paquetes de Python publicados por Microsoft, incluidos los [revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package) y [microsoftml](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package).


## <a name="see-also"></a>Vea también

[Novedades de SQL Server 2016](../sql-server/what-s-new-in-sql-server-2016.md)

[Solución de problemas de aprendizaje automático en SQL Server](machine-learning-troubleshooting-faq.md)

