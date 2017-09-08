---
title: "Problemas conocidos de los servicios de aprendizaje de máquina | Documentos de Microsoft"
ms.custom:
- SQL2016_New_Updated
ms.date: 06/16/2017
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
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b7b9d53a87490e83f888b47b1cff87191b9693a8
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="known-issues-for-machine-learning-services"></a>Problemas conocidos de los servicios de aprendizaje de máquina

Este tema describe los problemas conocidos o limitaciones con componentes que se proporcionan como una opción en SQL Server 2016 y SQL Server 2017 de aprendizaje automático.

Se aplica a todos los elementos siguientes a menos que se indique específicamente:

+ SQL Server 2016

  - R Services (en bases de datos)
  - Microsoft R Server (independiente)

+ SQL Server 2017

  - Servicios de R (en bases de datos) de aprendizaje automático
  - Servicios para Python (en bases de datos) de aprendizaje automático
  - Machine Learning Server (independiente)

## <a name="setup-and-configuration-issues"></a>El programa de instalación y problemas de configuración

A continuación se enumeran una descripción de procesado y comunes preguntas relacionadas con la instalación y configuración iniciales: [actualización y preguntas más frecuentes de instalación](r/upgrade-and-installation-faq-sql-server-r-services.md).

También consulte este artículo para obtener información acerca de las actualizaciones, en paralelo e instalación de nuevos componentes de R o Python.

### <a name="unable-to-install-python-components-in-in-offline-installs-of-sql-server-2017"></a>No se puede instalar componentes de Python en instalaciones sin conexión de SQL Server 2017

Si instala SQL Server 2017 en un equipo sin acceso a Internet, el programa de instalación puede producir un error mostrar la página que solicita la ubicación de los componentes de Python descargados; por lo tanto, podrá instalar la característica Servicios de aprendizaje de máquina, pero no los componentes de Python.

Este problema se corregirá en una próxima versión. Como alternativa, puede habilitar temporalmente acceso a Internet para la duración del programa de instalación. Esta limitación no se aplica a R.

**Se aplica a:** SQL Server 2017 con Python

### <a name="install-latest-service-release-to-ensure-compatibility-with-microsoft-r-client"></a>Instalar la última versión de servicio para garantizar la compatibilidad con Cliente de Microsoft R

Si instala la versión más reciente del cliente de Microsoft R y utilizarlo para ejecutar R el contexto de proceso de SQL Server mediante un control remoto, puede aparecer un error similar al siguiente:

*Se ejecutan 9.x.x de versión del cliente de Microsoft R en el equipo, que es incompatible con el 8.x.x de versión de Microsoft R Server. Download and install a compatible version.* (Está ejecutando la versión 9.0.0 del Cliente de Microsoft R en el equipo, que es incompatible con Microsoft R Server versión 8.0.3. Descargue e instale una versión compatible).

SQL Server 2016 requiere que las bibliotecas de R en el cliente coinciden exactamente con las bibliotecas de R en el servidor. Que se ha quitado la restricción para libera posterior a R Server 9.0.1. Sin embargo, si se produce este error, compruebe la versión de las bibliotecas de R usado por el cliente y el servidor, NLA si es necesario, actualice el cliente para que coincida con la versión del servidor.

La versión de R que se instala con SQL Server R Services se actualiza cada vez que se instala una versión de servicio de SQL Server. Por lo tanto, para asegurarse de que siempre tiene las versiones más recientes de componentes de R, debe instalar todos los service packs.

Para que haya compatibilidad con Cliente de Microsoft R 9.0.0, debe instalar las actualizaciones que se describen en este [artículo de soporte técnico](https://support.microsoft.com/kb/3210262).

Para evitar problemas con los paquetes de R, también puede actualizar la versión de las bibliotecas de R que se instalan en el servidor, cambiando a la directiva de ciclo de vida modernos como se describe en [en esta sección](#bkmk_sqlbindr). Al hacerlo, se actualiza la versión de R instalada con SQL Server en la misma programación que se publiquen las actualizaciones de Microsoft R Server, asegurándose de que tanto el servidor como el cliente pueden tener siempre las versiones más recientes de Microsoft R.

**Se aplica a:** SQL Server 2016 R Services, con R Server versión 9.0.0 o versiones anteriores

### <a name="bkmk_sqlbindr"></a>Advertencia de versión no compatible al conectarse a una versión anterior de SQL Server R Services desde un cliente mediante[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]

Si ha instalado Microsoft R Server en un equipo cliente mediante el Asistente para la instalación de [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] o el nuevo instalador independiente de [Microsoft R Server](https://msdn.microsoft.com/microsoft-r/rserver-install-windows)y ejecuta código de R en un contexto de proceso que usa una versión anterior de SQL Server R Services, podría aparecer un error similar al siguiente:

*Está ejecutando la versión 9.0.0 R del cliente de Microsoft en el equipo, que es incompatible con la versión 8.0.3 de Microsoft R Server. Download and install a compatible version.* (Está ejecutando la versión 9.0.0 del Cliente de Microsoft R en el equipo, que es incompatible con Microsoft R Server versión 8.0.3. Descargue e instale una versión compatible).

La herramienta **SqlBindR.exe** se proporciona en la versión Microsoft R Server 9.0 para admitir la actualización de instancias de SQL Server a una versión 9.0 compatible. Se agregará compatibilidad con la actualización de instancias de R Services a 9.0 en SQL Server como parte de una próxima versión de servicio. Las versiones que son candidatos para la futura de actualización incluyen SQL Server 2016 RTM CU3 + y SP1 + y 1.1 de CTP de SQL Server de 2017.

**Se aplica a:** SQL Server 2016 R Services, con R Server versión 9.0.0 o versiones anteriores

### <a name="setup-for-sql-server-2016-service-releases-might-fail-to-install-newer-versions-of-r-components"></a>La instalación de las versiones de servicio de SQL Server 2016 podrían producir un error al instalar versiones más recientes de los componentes de R

Al instalar una actualización acumulativa o un Service Pack para SQL Server 2016 en un equipo que no está conectado a Internet, el Asistente para la instalación podría no mostrar el mensaje que le permite actualizar los componentes de R mediante los archivos CAB descargados. Esto suele ocurrir cuando se instalan varios componentes con el motor de base de datos.

Como alternativa, puede instalar la versión de servicio utilizando la línea de comandos y especificando la */MRCACHEDIRECTORY* argumento tal como se muestra en este ejemplo, que instala las actualizaciones de CU1:

`C:\<path to installation media>\SQLServer2016-KB3164674-x64.exe /Action=Patch /IACCEPTROPENLICENSETERMS /MRCACHEDIRECTORY=<path to CU1 CAB files>`

Para obtener los instaladores más recientes, consulte [instalar componentes de aprendizaje de máquina sin acceso a Internet](r/installing-ml-components-without-internet-access.md).

**Se aplica a:** SQL Server 2016 R Services, con R Server versión 9.0.0 o versiones anteriores

### <a name="launchpad-services-fails-to-start-if-version-is-different-than-r-version"></a>No se puede iniciar el servicio Launchpad si la versión es diferente a la versión de R

Si instala R Services por separado desde el motor de base de datos y las versiones de compilación son diferentes, verá este error en el registro de eventos del sistema: _servicio el Launchpad de SQL Server no pudo iniciarse debido al siguiente error: el servicio no se ejecutó responder a la solicitud de inicio o control de manera oportuna._

Por ejemplo, este error podría producirse si instala el motor de base de datos mediante la versión de lanzamiento, aplica una revisión para actualizar el motor de base de datos y, después, agrega R Services con la versión de lanzamiento.

Para evitar este problema, asegúrese de que todos los componentes tengan el mismo número de versión. Si actualiza un componente, asegúrese de aplicar la misma actualización a los demás componentes instalados.

Para ver una lista de los números de versión de R necesarios para cada versión de SQL Server 2016, consulte [Instalación de componentes de R sin acceso a Internet](r/installing-ml-components-without-internet-access.md).

### <a name="remote-compute-contexts-blocked-by-firewall-in-sql-server-instances-running-on-azure-virtual-machines"></a>Contextos de proceso remoto bloqueados por el firewall en instancias de SQL Server que se ejecutan en máquinas virtuales de Azure

Si ha instalado [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] en una máquina virtual de Microsoft Azure, es posible que no pueda usar contextos de proceso que requieran el uso del área de trabajo de la máquina virtual. El motivo es que, de forma predeterminada, el firewall de la máquina virtual de Azure incluye una regla que bloquea el acceso a la red para las cuentas de usuario locales de R.

Como solución alternativa, en la máquina virtual de Azure, abra **Firewall de Windows con seguridad avanzada**, seleccione **Reglas de salida**y deshabilite la regla "Bloquear el acceso a la red para las cuentas de usuario locales de R en la instancia de SQL Server MSSQLSERVER".

### <a name="implied-authentication-in-sqlexpress"></a>Autenticación implícita en SQLEXPRESS

Al ejecutar trabajos de R desde una estación de trabajo de ciencia de datos remota mediante la autenticación integrada de Windows, SQL Server usará la *autenticación implícita* para generar las llamadas ODBC locales que solicite el script. Pero esta característica no funcionaba en la compilación RTM de SQL Server Express Edition.

Para corregir el problema, se recomienda que actualice a una versión de servicio posterior.

Si no puede actualizar, use un inicio de sesión de SQL para ejecutar los trabajos de R remotos que requieran llamadas ODBC incrustadas.

**Se aplica a:** Express Edition de servicios de SQL Server 2016 R

### <a name="performance-limits-when-r-libraries-are-called-from-standalone-r-tools"></a>Limita el rendimiento cuando se llaman a bibliotecas de R desde herramientas independientes R

Es posible llamar a las herramientas de R y las bibliotecas que se instalan para SQL Server R Services desde una aplicación externa de R como RGui. Esto puede resultar útil cuando se va a instalar nuevos paquetes o ejecutar pruebas ad hoc en los ejemplos de código muy breve.

Sin embargo, tenga en cuenta que fuera de SQL Server, rendimiento será limitada. Por ejemplo, incluso si ha adquirido la edición Enterprise de SQL Server, R se ejecutará en modo de subproceso único cuando se ejecuta el código de R con herramientas externas. El rendimiento será superior si ejecuta el código de R e inicia una conexión de SQL Server y usando [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), que llamará a las bibliotecas de R para usted.

+ Evite llamar a las bibliotecas de R que SQL Server usa desde herramientas externas de R.
+ Si tiene que ejecutar mucho código R en el equipo de SQL Server sin usar SQL server, instale una instancia independiente de R como cliente de Microsoft R y, a continuación, asegúrese de que las herramientas de desarrollo de R señalen a la nueva biblioteca.

Para obtener más información, vea [Crear un R Server independiente](r/create-a-standalone-r-server.md).

### <a name="r-script-throttled-due-to-resource-governance-default-values"></a>Script de R limitado debido a los valores predeterminados de regulación de recursos

En Enterprise Edition, puede usar grupos de recursos para administrar procesos de script externos. En algunas versiones de lanzamiento temprano, la memoria máxima que se puede asignar a los procesos de R era 20%. Por lo tanto, si el servidor tenía 32 GB de RAM, los ejecutables de R (RTerm.exe y BxlServer.exe) podían usar un máximo de 6,4 GB en una única solicitud.

Si se encuentra ante limitaciones de recursos, compruebe el valor predeterminado actual y, si el 20 % no es suficiente, consulte cómo cambiar este valor en la documentación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .

**Se aplica a:** R Services SQL Server 2016, Enterprise Edition

## <a name="r-code-execution-and-package-or-function-issues"></a>La ejecución de código de R y los problemas de la función o paquete

Esta sección contiene los problemas conocidos que son específicos para ejecutar código R en SQL Server, así como algunos problemas relacionados con las bibliotecas de R y herramientas publicados por Microsoft, incluidos los RevoScaleR.

Para otros problemas conocidos que podrían afectar a las soluciones de R, vea el sitio de Microsoft R Server: [problemas conocidos relacionados con Microsoft R Server](https://msdn.microsoft.com/microsoft-r/rserver-known-issues)

### <a name="limitations-on-processor-affinity-for-r-jobs"></a>Limitaciones de la afinidad del procesador para trabajos de R

En la compilación de lanzamiento inicial de SQL Server 2016, se podía establecer la afinidad del procesador solo para la CPU en el primer grupo de k. Por ejemplo, si el servidor es una máquina de dos socket con dos grupos K, solo se usan los procesadores del primer grupo K para los procesos de R. La misma limitación se aplica al configurar el gobierno de recursos para trabajos del script de R.

Este problema está corregido en SQL Server 2016 Service Pack 1.

**Se aplica a:** versión RTM de SQL Server 2016 R Services

### <a name="changes-to-column-types-cannot-be-performed-when-reading-data-in-a-sql-server-compute-context"></a>No se pueden realizar cambios en los tipos de columna al leer datos en un contexto de proceso de SQL Server

Si el contexto de proceso está establecido en la instancia de SQL Server, no puede usar el argumento _colClasses_ (u otros argumentos similares) para cambiar el tipo de datos de las columnas en el código de R.

Por ejemplo, la instrucción siguiente producirá un error si la columna CRSDepTimeStr no es ya un entero:

~~~~
data <- RxSqlServerData(sqlQuery = "SELECT CRSDepTimeStr, ArrDelay  FROM AirlineDemoSmall",
                                connectionString = connectionString,
                                colClasses = c(CRSDepTimeStr = "integer"))
~~~~

Este problema se corregirá en una versión posterior.

Como solución alternativa, puede volver a escribir la consulta SQL para usar CAST o CONVERT y presentar los datos a R con el tipo de datos correcto. En general, es mejor para el rendimiento trabajar con los datos mediante SQL, en lugar de cambiar los datos en el código de R.

**Se aplica a:** R Services SQL Server 2016

### <a name="avoid-clearing-workspaces-when-executing-r-code-in-a-includessnoversionincludesssnoversion-mdmd-compute-context"></a>Evitar borrar áreas de trabajo al ejecutar código de R en un contexto de proceso de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]

Si usa el comando de R para borrar los objetos del área de trabajo mientras se ejecuta código de R en un contexto de proceso de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , o si borra el área de trabajo como parte de un script de R llamado mediante [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), podría recibir este error: *workspace object 'revoScriptConnection' not found*(No se encontró el objeto del área de trabajo 'revoScriptConnection').

`revoScriptConnection` es un objeto del área de trabajo de R que contiene información sobre una sesión de R a la que se llama desde [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Pero si su código de R incluye un comando para borrar el área de trabajo (como `rm(list=ls()))`, también se borrarán toda la información sobre la sesión y otros objetos del área de trabajo de R.

Como solución alternativa, evite borrar indiscriminadamente las variables y otros objetos mientras se ejecuta R en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Aunque es habitual borrar el área de trabajo cuando se trabaja en la consola de R, puede tener consecuencias no deseadas.

+ Para eliminar variables específicas, use la función de R *remove* : `remove('name1', 'name2', ...)`
+ Si quiere eliminar varias variables, guarde los nombres de las variables temporales en una lista y realice periódicamente la recolección de elementos no utilizados.

### <a name="restrictions-on-data-that-can-be-provided-as-input-to-an-r-script"></a>Restricciones en los datos que se pueden proporcionar como entrada para un script de R

No puede usar un script de R en los siguientes tipos de resultados de consulta:

- Datos de una consulta de [!INCLUDE[tsql](../includes/tsql-md.md)] que haga referencia a columnas AlwaysEncrypted.
  
- Datos de una consulta de [!INCLUDE[tsql](../includes/tsql-md.md)] que haga referencia a columnas enmascaradas.
  
     Si necesita usar datos enmascaradas en un script de R, una posible solución alternativa es realizar una copia de los datos en una tabla temporal y usar esos datos en su lugar.

### <a name="arguments-varstokeep-and-varstodrop-not-supported-for-sql-server-data-sources"></a>Argumentos *varsToKeep* y *varsToDrop* no se admite para orígenes de datos de SQL Server

Cuando utilice la función rxDataStep para escribir los resultados en una tabla, con el *varsToKeep* y *varsToDrop* es una forma práctica de especificar las columnas para incluir o excluir como parte de la operación. Actualmente, estos argumentos no se admiten para los orígenes de datos de SQL Server.

Esta limitación se quitará en una versión posterior.

### <a name="limited-support-for-sql-data-types-in-spexecuteexternalscript"></a>Compatibilidad limitada para tipos de datos SQL en`sp_execute_external_script`

No todos los tipos de datos que se admiten en SQL pueden usarse en R. Como solución alternativa, considere la posibilidad de convertir el tipo de datos no admitido a un tipo de datos compatible antes de pasar los datos a sp_execute_external_script.

Para obtener más información, consulte [tipos de datos y bibliotecas de R](r/r-libraries-and-data-types.md).

### <a name="possible-string-corruption"></a>Posibles daños en una cadena

Cualquier recorrido de ida y vuelta de datos de cadena de [!INCLUDE[tsql](../includes/tsql-md.md)] a R y después de vuelta a [!INCLUDE[tsql](../includes/tsql-md.md)] puede producir daños. Esto se debe a las diferentes codificaciones que se usan en R y en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], así como a las distintas intercalaciones e idiomas que se admiten en R y [!INCLUDE[tsql](../includes/tsql-md.md)]. Cualquier cadena con una codificación que no sea ASCII puede controlarse potencialmente de manera incorrecta.

Al enviar datos de cadena a R, si es posible conviértalos en una representación ASCII.

### <a name="only-one-value-of-type-raw-can-be-returned-from-spexecuteexternalscript"></a>Solo un valor de tipo `raw` puede devolverse desde`sp_execute_external_script`

Cuando se devuelve desde R un tipo de datos binarios (el tipo de datos **raw** de R), debe ser el valor en la trama de datos de salida.

En versiones posteriores se agregará compatibilidad con varias salidas **raw** .

Si quiere tener varios conjuntos de salida, una posible solución alternativa es realizar varias llamadas de procedimiento almacenado y enviar el conjunto de resultados a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mediante ODBC.

Tenga en cuenta que puede devolver valores de parámetro junto con los resultados del procedimiento almacenado. Para ello, simplemente agregue la palabra clave OUTPUT. Para obtener más información, consulte [Devolver datos mediante parámetros OUTPUT](https://technet.microsoft.com/library/ms187004.aspx).

### <a name="loss-of-precision"></a>Pérdida de precisión

[!INCLUDE[tsql](../includes/tsql-md.md)] y R admiten diferentes tipos de datos, por lo que los tipos de datos numéricos pueden perder precisión durante la conversión.

Para obtener más información acerca de la conversión implícita de tipos de datos, vea [Working with R Data Types](r/r-libraries-and-data-types.md).

### <a name="variable-scoping-error-the-sample-data-set-for-the-analysis-has-no-variables-when-using-the-transformfunc-parameter"></a>Error de ámbito de variable "El conjunto de datos de ejemplo para el análisis no tiene variables" al usar el parámetro transformFunc

Puede pasar un argumento *transfomFunc* en una función como `rxLinmod` o `rxLogit` to transfom the data while modelling. Sin embargo, las llamadas a funciones anidadas pueden provocar errores de ámbito en el contexto de proceso de SQL Server, incluso si las llamadas funcionan correctamente en el contexto de proceso local.

Por ejemplo, supongamos que ha definido dos funciones `f` y `g` en su entorno global local, y que `g` llama a `f`. En las llamadas remotas o distribuidas en las que participa `g`, la llamada a `g` podría generar un error porque no se encuentra `f` , incluso si ha pasado `f` y `g` a la llamada remota.

Si se produce este problema, puede solucionarlo insertando la definición de `f` en la definición de `g`, en cualquier lugar antes de que `g` llame a `f`.

Por ejemplo:

```  
f <- function(x) { 2*x + 3 }  
g <- function(y) {   
              a <- 10 * y  
               f(a)  
}  
  
```  


Para evitar el error, vuelva a escribir como se indica a continuación:

```  
g <- function(y){  
              f <- function(x) { 2*x +3}  
              a <- 10 * y  
              f(a)  
}  
  
```  

### <a name="data-import-and-manipulation-using-revoscaler"></a>Importación de datos y manipulación con RevoScaleR

Al leer columnas **varchar** de una base de datos, se eliminarán los espacios en blanco. Para evitarlo, ponga las cadenas entre caracteres que no sean espacios en blanco.

Cuando use funciones como `rxDataStep` para crear tablas de base de datos con columnas **varchar** , el ancho de columna se calcula en función de una muestra de los datos. Si el ancho varía, puede que sea necesario rellenar todas las cadenas con una longitud común.

El uso de una transformación para cambiar el tipo de datos de una variable no se admite cuando se usan llamadas repetidas a `rxImport` o `rxTextToXdf` para importar y anexar filas combinando varios archivos de entrada en un solo archivo .xdf.

### <a name="limited-support-for-rxexec"></a>Compatibilidad limitada con rxexec

En SQL Server 2016, el `rxExec` función proporcionada por el paquete RevoScaleR puede utilizarse únicamente en el modo de un único subproceso.

En una próxima versión se agregará paralelismo para `rxExec` entre varios procesos.

### <a name="increase-maximum-parameter-size-to-support-rxgetvarinfo"></a>Aumento del tamaño máximo de parámetro para admitir rxGetVarInfo

Si usa conjuntos de datos con números de variables muy grandes (por ejemplo, más de 40 000), debe establecer la marca `max-ppsize` al iniciar R para poder usar funciones como `rxGetVarInfo`.  La marca `max-ppsize` especifica el tamaño máximo de la pila de protección del puntero.

Si usa la consola de R (por ejemplo, en rgui.exe o rterm.exe), puede establecer el valor de max-ppsize en 500 000. Para ello, escriba lo siguiente:

```  
R --max-ppsize=500000  
```  
  
Si usa el entorno de [!INCLUDE[rsql_developr](../includes/rsql-developr-md.md)] , puede establecer la marca `max-ppsize` mediante esta llamada al ejecutable RevoIDE:

```  
RevoIDE.exe /RCommandLine --max-ppsize=500000  
```  

### <a name="issues-with-the-rxdtree-function"></a>Problemas con la función rxDTree

La función `rxDTree` no admite actualmente transformaciones en la fórmula. En particular, no se admite el uso de la sintaxis `F()` para crear factores sobre la marcha. Sin embargo, los datos numéricos se discretizan automáticamente.

Los factores ordenados se tratan igual que los factores de todas las funciones de análisis RevoScaleR, excepto `rxDTree`.

## <a name="revolution-r-enterprise-and-microsoft-r-open"></a>Revolution R Enterprise y Microsoft R Open

En esta sección se enumeran los problemas específicos de la conectividad, el desarrollo y las herramientas de rendimiento de R que proporciona Revolution Analytics. Estas herramientas se proporcionaron en versiones preliminares anteriores de  [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]. 

En general, recomendamos que desinstale las versiones anteriores y que instale la versión más reciente de SQL Server o Microsoft R Server.

### <a name="running-side-by-side-versions-of-revolution-r-enterprise"></a>Ejecución de versiones en paralelo de Revolution R Enterprise

No se admite la instalación en paralelo de Revolution R Enterprise con ninguna versión de [!INCLUDE[rsql_productname_md](../includes/rsql-productname-md.md)] .

Si tiene una licencia para usar una versión diferente de Revolution R Enterprise, debe colocarla en un equipo diferente de donde se encuentran la instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y las estaciones de trabajo que quiera usar para conectarse a la instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .

### <a name="use-of-r-productivity-environment-not-supported"></a>Uso de R Productivity Environment no compatible

Algunas versiones preliminares de [!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)] incluyen un entorno de desarrollo de R para Windows creado mediante Revolution Analytics. Esta herramienta ya no está disponible y no se admite.

Para ofrecer compatibilidad con [!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)], se recomienda encarecidamente que instale Microsoft R Client o Microsoft R Server en lugar de las herramientas de Revolution Analytics. [Herramientas de R para Visual Studio](https://www.visualstudio.com/vs/rtvs/) es otro cliente recomendado que admite soluciones de Microsoft R.

### <a name="compatibility-issues-with-sqlite-odbc-driver-and-revoscaler"></a>Problemas de compatibilidad con el controlador ODBC de SQLite y RevoScaleR

La revisión 0.92 del controlador ODBC de SQLite no es compatible con RevoScaleR, pero se sabe que las revisiones de 0.88 a 0.91 y 0.93 y posteriores son compatibles.

## <a name="see-also"></a>Vea también

[Novedades de SQL Server 2016](../sql-server/what-s-new-in-sql-server-2016.md)


