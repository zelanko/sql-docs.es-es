---
title: "Problemas conocidos de SQL Server R Services | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/10/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2b37a63a-5ff5-478e-bcc2-d13da3ac241c
caps.latest.revision: 52
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 49
---
# Problemas conocidos de SQL Server R Services
  En este tema se describen las limitaciones y los problemas de [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] y sus componentes relacionados en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)].  
  
> [!NOTE]
> Los problemas adicionales relacionados con la instalación y la configuración iniciales se muestran aquí: [Preguntas más frecuentes sobre actualización e instalación](../../advanced-analytics/r-services/upgrade-and-installation-faq-sql-server-r-services.md).  
  
## <a name="r-services-in-database"></a>R Services (en bases de datos)  
 En esta sección se enumeran los problemas específicos de la característica del motor de base de datos que admite la integración de R.  

### <a name="install-latest-service-release-to-ensure-compatibility-with-microsoft-r-client"></a>Instalar la última versión de servicio para garantizar la compatibilidad con Cliente de Microsoft R

Si instala la versión más reciente del Cliente de Microsoft R y lo usa para ejecutar R en SQL Server mediante un contexto de proceso remoto, podría aparecer el error siguiente:

*You are running version 9.0.0 of Microsoft R client on your computer, which is incompatible with the Microsoft R server version 8.0.3. Download and install a compatible version.* (Está ejecutando la versión 9.0.0 del Cliente de Microsoft R en el equipo, que es incompatible con Microsoft R Server versión 8.0.3. Descargue e instale una versión compatible).

Normalmente, la versión de R que se instala con SQL Server R Services se actualiza cuando se publican versiones de servicio. Para garantizar que siempre tenga las versiones más actualizadas de los componentes de R, instale todos los Service Pack. Para que haya compatibilidad con Cliente de Microsoft R 9.0.0, debe instalar las actualizaciones que se describen en este [artículo de soporte técnico](https://support.microsoft.com/kb/3210262). 
  
### <a name="new-license-agreement-for-r-components-required-for-unattended-installs"></a>Nuevo contrato de licencia para los componentes de R necesarios para las instalaciones desatendidas  
 Si usa la línea de comandos para instalar una instancia de SQL Server que tiene instalado [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], debe editar la línea de comandos para usar el nuevo parámetro de contrato de licencia */IACCEPTROPENLICENSEAGREEMENT*. Puede producirse un error en la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si no se usa el argumento correcto.  
  
### <a name="warning-of-incompatible-version-when-connecting-to-older-version-of-sql-server--r-services-from-a-client-using-includesssqlv14mdtokensqlv14sssqlv14mdmd"></a>Advertencia de versión incompatible al conectarse a una versión anterior de SQL Server R Services desde un cliente mediante [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 

Si ha instalado Microsoft R Server en un equipo cliente mediante el Asistente para la instalación de [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] o el nuevo instalador independiente de [Microsoft R Server](https://msdn.microsoft.com/microsoft-r/rserver-install-windows) y ejecuta código de R en un contexto de proceso que usa una versión anterior de SQL Server R Services, podría aparecer un error similar al siguiente:

*You are running version 9.0.0 of Microsoft R Client on your computer, which is incompatible with the Microsoft R Server version 8.0.3. Download and install a compatible version.* (Está ejecutando la versión 9.0.0 del Cliente de Microsoft R en el equipo, que es incompatible con Microsoft R Server versión 8.0.3. Descargue e instale una versión compatible).

La herramienta **SqlBindR.exe** se proporciona en la versión Microsoft R Server 9.0 para admitir la actualización de instancias de SQL Server a una versión 9.0 compatible. Se agregará compatibilidad con la actualización de instancias de R Services a 9.0 en SQL Server como parte de una próxima versión de servicio. Entre las versiones candidatas a una futura actualización se incluyen SQL Server 2016 RTM CU3+ y SP1+, así como SQL Server vNext CTP 1.1. 

### <a name="setup-for-sql-server-2016-service-releases-might-fail-to-install-newer-versions-of-r-components"></a>La instalación de las versiones de servicio de SQL Server 2016 podrían producir un error al instalar versiones más recientes de los componentes de R

Al instalar una actualización acumulativa o un Service Pack para SQL Server 2016 en un equipo que no está conectado a Internet, el Asistente para la instalación podría no mostrar el mensaje que le permite actualizar los componentes de R mediante los archivos CAB descargados. Esto suele ocurrir cuando se instalan varios componentes con el motor de base de datos.
 
Como solución alternativa, puede instalar la versión de servicio mediante la línea de comandos. Para ello, especifique el argumento /MRCACHEDIRECTORY tal como se muestra en este ejemplo para CU1: 

`C:\<path to installation media>\SQLServer2016-KB3164674-x64.exe /Action=Patch /IACCEPTROPENLICENSETERMS /MRCACHEDIRECTORY=<path to CU1 CAB files>`

Para obtener los archivos CAB más recientes, consulte [Instalación de componentes de R sin acceso a Internet](../../advanced-analytics/r-services/installing-r-components-without-internet-access.md).

### <a name="windows-group-created-for-launchpad-must-have-an-account-in-the-sql-server-instance"></a>El grupo de Windows que se creó para Launchpad debe tener una cuenta en la instancia de SQL Server
 Al instalar SQL Server R Services, se crea un grupo de usuarios de Windows con el nombre predeterminado **SQLRUsers**, que Trusted Launchpad usa para ejecutar trabajos de R. Si necesita ejecutar trabajos de R desde un cliente remoto mediante la autenticación integrada de Windows, debe conceder a este grupo de usuarios de Windows permiso para iniciar sesión en la instancia de SQL Server donde está habilitado R.

En un entorno en el que el grupo **SQLRUsers** no tiene este permiso, pueden aparecer los errores siguientes:  
  
-   Al intentar ejecutar scripts de R:  
  
     *No se puede iniciar el tiempo de ejecución para el script 'R'. Compruebe la configuración del tiempo de ejecución 'R'.*  
  
     *An external script error occurred. Unable to launch the runtime.* (Error en el script externo. No se puede iniciar el tiempo de ejecución).  
  
-   Errores generados por el servicio de [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] :  
  
     *Failed to initialize the launcher RLauncher.dll* (No se pudo inicializar el iniciador RLauncher.dll)  
  
     *No launcher dlls were registered!* (No se registraron .dll de iniciador)  
  
-   Los registros de seguridad indican que la cuenta NT SERVICE\MSSQLLAUNCHPAD no pudo iniciar sesión.  
 
> [!NOTE]
> Si ejecuta trabajos de R en SQL Server Management Studio mediante la memoria compartida, podría no encontrarse ante esta limitación hasta que el trabajo de R use una llamada ODBC incrustada. 
> 
> Esta solución alternativa no es necesaria si usa inicios de sesión de SQL desde la estación de trabajo remota.

### <a name="launchpad-services-fails-to-start-if-version-is-different-than-r-version"></a>No se puede iniciar el servicio Launchpad si la versión es diferente a la versión de R
Si instala R Services por separado desde el motor de base de datos y las versiones son diferentes, podría ver este error en el registro de eventos del sistema: _The SQL Server Launchpad service failed to start due to the following error: The service did not respond to the start or control request in a timely fashion._ (El servicio Launchpad de SQL Server no pudo iniciarse debido al siguiente error: El servicio no respondió a tiempo a la solicitud de inicio o de control).

Por ejemplo, este error podría producirse si instala el motor de base de datos mediante la versión de lanzamiento, aplica una revisión para actualizar el motor de base de datos y, después, agrega R Services con la versión de lanzamiento.

Para evitar este problema, asegúrese de que todos los componentes tengan el mismo número de versión. Si actualiza un componente, asegúrese de aplicar la misma actualización a los demás componentes instalados.

Para ver una lista de los números de versión de R necesarios para cada versión de SQL Server 2016, consulte [Instalación de componentes de R sin acceso a Internet](../../advanced-analytics/r-services/installing-r-components-without-internet-access.md).


### <a name="service-account-for-launchpad-requires-permission-replace-process-level-token"></a>La cuenta de servicio de Launchpad requiere el permiso Reemplazar token de nivel de proceso
 Al instalar SQL Server R Services, Trusted Launchpad se inicia con la cuenta NT Service\MSSQLLaunchpad, que se aprovisiona de forma predeterminada con los permisos necesarios. Pero si usa una cuenta diferente o cambia los privilegios asociados a esta cuenta, Launchpad podría no iniciarse.
 
 Para asegurarse de que la cuenta del servicio Launchpad pueda iniciar sesión, conceda a la cuenta el privilegio `Replace Process Level Token`. Para obtener más información, consulte [Replace a process level token](https://technet.microsoft.com/itpro/windows/keep-secure/replace-a-process-level-token) (Reemplazar un token de nivel de proceso).

### <a name="remote-compute-contexts-blocked-by-firewall-in-sql-server-instances-running-on-azure-virtual-machines"></a>Contextos de proceso remoto bloqueados por el firewall en instancias de SQL Server que se ejecutan en máquinas virtuales de Azure  
 Si ha instalado [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] en una máquina virtual de Microsoft Azure, es posible que no pueda usar contextos de proceso que requieran el uso del área de trabajo de la máquina virtual. El motivo es que, de forma predeterminada, el firewall de la máquina virtual de Azure incluye una regla que bloquea el acceso a la red para las cuentas de usuario locales de R.  
  
 Como solución alternativa, en la máquina virtual de Azure, abra **Firewall de Windows con seguridad avanzada**, seleccione **Reglas de salida**y deshabilite la regla "Bloquear el acceso a la red para las cuentas de usuario locales de R en la instancia de SQL Server MSSQLSERVER".  
  
### <a name="implied-authentication-in-sqlexpress"></a>Autenticación implícita en SQLEXPRESS
Al ejecutar trabajos de R desde una estación de trabajo de ciencia de datos remota mediante la autenticación integrada de Windows, SQL Server usará la *autenticación implícita* para generar las llamadas ODBC locales que solicite el script. Pero esta característica no funcionaba en la compilación RTM de SQL Server Express Edition. 

Para corregir el problema, se recomienda que actualice a una versión de servicio posterior.

Si no puede actualizar, use un inicio de sesión de SQL para ejecutar los trabajos de R remotos que requieran llamadas ODBC incrustadas. 

### <a name="limitations-on-processor-affinity-for-r-jobs"></a>Limitaciones de la afinidad del procesador para trabajos de R 
 
En la compilación RTM de SQL Server 2016, se podía establecer la afinidad del procesador únicamente para las CPU del primer grupo K. Por ejemplo, si el servidor es una máquina de dos socket con dos grupos K, solo se usan los procesadores del primer grupo K para los procesos de R. La misma limitación se aplica al configurar el gobierno de recursos para trabajos del script de R.

Este problema está corregido en SQL Server 2016 Service Pack 1.

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
  
### <a name="resource-governance-default-values"></a>Valores predeterminados del gobierno de recursos  
En Enterprise Edition, puede usar grupos de recursos para administrar procesos de script externos. En algunas compilaciones, la memoria máxima que se puede asignar a los procesos de R era del 20 %. Por lo tanto, si el servidor tenía 32 GB de RAM, los ejecutables de R (RTerm.exe y BxlServer.exe) podían usar un máximo de 6,4 GB en una única solicitud. 

Si se encuentra ante limitaciones de recursos, compruebe el valor predeterminado actual y, si el 20 % no es suficiente, consulte cómo cambiar este valor en la documentación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  

### <a name="avoid-clearing-workspaces-when-executing-r-code-in-a-includessnoversiontokenssnoversionmdmd-compute-context"></a>Evitar borrar áreas de trabajo al ejecutar código de R en un contexto de proceso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Si usa el comando de R para borrar los objetos del área de trabajo mientras se ejecuta código de R en un contexto de proceso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o si borra el área de trabajo como parte de un script de R llamado mediante [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), podría recibir este error: *workspace object 'revoScriptConnection' not found* (No se encontró el objeto del área de trabajo 'revoScriptConnection').

`revoScriptConnection` es un objeto del área de trabajo de R que contiene información sobre una sesión de R a la que se llama desde [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Pero si su código de R incluye un comando para borrar el área de trabajo (como `rm(list=ls()))`, también se borrarán toda la información sobre la sesión y otros objetos del área de trabajo de R.

Como solución alternativa, evite borrar indiscriminadamente las variables y otros objetos mientras se ejecuta R en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Aunque es habitual borrar el área de trabajo cuando se trabaja en la consola de R, puede tener consecuencias no deseadas. 

+ Para eliminar variables específicas, use la función de R *remove*: `remove('name1', 'name2', ...)` 
+ Si quiere eliminar varias variables, guarde los nombres de las variables temporales en una lista y realice periódicamente la recolección de elementos no utilizados. 
   
### <a name="restrictions-on-data-that-can-be-provided-as-input-to-an-r-script"></a>Restricciones en los datos que se pueden proporcionar como entrada para un script de R  
 No puede usar un script de R en los siguientes tipos de resultados de consulta:  
  
-   Datos de una consulta de [!INCLUDE[tsql](../../includes/tsql-md.md)] que haga referencia a columnas AlwaysEncrypted.  
  
-   Datos de una consulta de [!INCLUDE[tsql](../../includes/tsql-md.md)] que haga referencia a columnas enmascaradas.  
  
     Si necesita usar datos enmascaradas en un script de R, una posible solución alternativa es realizar una copia de los datos en una tabla temporal y usar esos datos en su lugar.  
   
  
## <a name="microsoft-r-server-standalone"></a>Microsoft R Server (independiente)  
 En esta sección se enumeran los problemas específicos de la versión independiente de Microsoft R Server. 
  
### <a name="multiple-r-libraries-and-executables-are-installed-if-you-install-both-standalone-and-in-database"></a>Se instalan varias bibliotecas y ejecutables de R cuando se instalan la versión independiente y la versión en bases de datos  
 El programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] incluye la opción de instalar Microsoft R Server (independiente). La opción de Microsoft R Server (independiente) se puede usar en Enterprise Edition para instalar un servidor de Windows independiente que admita R pero que no requiera interactividad con SQL Server.    

> [!TIP] Esta opción independiente **no** es necesaria para usar R con [!INCLUDE[tsql](../../includes/tsql-md.md)].
> 
> Si necesita configurar un equipo cliente de ciencia de datos que pueda conectarse a [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] o a Microsoft R Server (independiente), se recomienda el [Cliente de Microsoft R](http://go.microsoft.com/fwlink/?LinkId=799768).  

Si instala R Services (en bases de datos) y Microsoft R Server (independiente) en el mismo equipo, tenga en cuenta que se creará una instancia independiente de R para cada instancia de SQL Server que tenga R habilitado, así como una instancia independiente de R para Microsoft R Server (independiente).  Por ejemplo, si ha instalado la instancia predeterminada, una instancia con nombre y R Server (independiente), podría tener tres instancias de R en el mismo equipo:  
  
-   **Independiente:** C:\Archivos de programa\Microsoft SQL Server\130\R_SERVER  
  
-   **Instancia predeterminada:** C:\Archivos de programa\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES  
  
-   **Instancia con nombre:** C:\Archivos de programa\Microsoft SQL Server\MSSQL13.<instance_name>\R_SERVICES  
  
> [!NOTE] 
> 
> Use las bibliotecas y las herramientas de R que estén asociadas a una instancia de base de datos solo desde el contexto de [!INCLUDE[tsql](../../includes/tsql-md.md)]. Si necesita ejecutar R con otras herramientas de R, asegúrese de hacer referencia a las bibliotecas de R que usa R Server (independiente), que se instalan de forma predeterminada en C:\Archivos de programa\Microsoft SQL Server\130\R_SERVER.  

### <a name="performance-limits-when-r-services-libraries-are-called-from-standalone-r-tools"></a>Límites de rendimiento cuando se llama a bibliotecas de R Services desde herramientas de R independiente

Las bibliotecas de R que usa SQL Server R Services se instalan de forma predeterminada en C:\Archivos de programa\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES. Es *posible* llamar a las herramientas y bibliotecas de R que están instaladas para SQL Server R Services desde una aplicación externa de R, como RGui. 

Pero si lo hace, el rendimiento se verá limitado. Por ejemplo, incluso si ha comprado la edición Enterprise de SQL Server, R se ejecutará en modo de subproceso único si ejecuta el código de R con herramientas externas. El rendimiento será mejor si para ejecutar el código de R inicia una conexión de SQL Server y usa [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), que llama automáticamente a las bibliotecas de R Services.

+ Evite llamar a las bibliotecas de R que SQL Server usa desde herramientas externas de R. 
+ Si necesita ejecutar R en el equipo con SQL Server mediante herramientas externas, debe instalar una instancia independiente de R y, después, asegurarse de que las herramientas de R apunten a la biblioteca nueva. 
+ Si usa Enterprise Edition, se recomienda que instale Microsoft R Server (independiente) en el equipo con SQL Server. Después, desde la herramienta externa que se usa para ejecutar código de R, haga referencia a las bibliotecas de R Server, que están instaladas de forma predeterminada en C:\Archivos de programa\Microsoft SQL Server\<número de versión>\R_SERVER. 

Para obtener más información, vea [Crear un R Server independiente](../../advanced-analytics/r-services/create-a-standalone-r-server.md).  
  
  
## <a name="general-r-issues"></a>Problemas generales de R  

 En esta sección se enumeran los problemas específicos de la conectividad de R y las herramientas de rendimiento.  
  
### <a name="limited-support-for-sql-data-types-in-spexecuteexternalscript"></a>Compatibilidad limitada con los tipos de datos en sp_execute_external_script  

 No todos los tipos de datos que se admiten en SQL pueden usarse en R. Como solución alternativa, considere la posibilidad de convertir el tipo de datos no admitido a un tipo de datos compatible antes de pasar los datos a sp_execute_external_script.  
  
 Para obtener más información, consulte [Working with R Data Types (Trabajar con tipos de datos de R)](../../advanced-analytics/r-services/working-with-r-data-types.md).  
  
### <a name="possible-string-corruption"></a>Posibles daños en una cadena  

 Cualquier recorrido de ida y vuelta de datos de cadena de [!INCLUDE[tsql](../../includes/tsql-md.md)] a R y después de vuelta a [!INCLUDE[tsql](../../includes/tsql-md.md)] puede producir daños. Esto se debe a las diferentes codificaciones que se usan en R y en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], así como a las distintas intercalaciones e idiomas que se admiten en R y [!INCLUDE[tsql](../../includes/tsql-md.md)]. Cualquier cadena con una codificación que no sea ASCII puede controlarse potencialmente de manera incorrecta.  
  
 Al enviar datos de cadena a R, si es posible conviértalos en una representación ASCII.  
  
### <a name="only-one-raw-value-can-be-returned-from-spexecuteexternalscript"></a>Solo se puede devolver un valor sin formato desde sp_execute_external_script  

 Cuando se devuelve desde R un tipo de datos binarios (el tipo de datos **raw** de R), debe ser el valor en la trama de datos de salida.  
  
 En versiones posteriores se agregará compatibilidad con varias salidas **raw** .  
  
 Si quiere tener varios conjuntos de salida, una posible solución alternativa es realizar varias llamadas de procedimiento almacenado y enviar el conjunto de resultados a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante ODBC.  
  
 Tenga en cuenta que puede devolver valores de parámetro junto con los resultados del procedimiento almacenado. Para ello, simplemente agregue la palabra clave OUTPUT. Para obtener más información, consulte [Devolver datos mediante parámetros OUTPUT](https://technet.microsoft.com/library/ms187004.aspx).
  
### <a name="loss-of-precision"></a>Pérdida de precisión  

 [!INCLUDE[tsql](../../includes/tsql-md.md)] y R admiten diferentes tipos de datos, por lo que los tipos de datos numéricos pueden perder precisión durante la conversión.  
  
 Para obtener más información acerca de la conversión implícita de tipos de datos, vea [Working with R Data Types](../../advanced-analytics/r-services/working-with-r-data-types.md).  
  
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
  
 Para evitar el error, vuelva a escribirlo de la manera siguiente:  
  
```  
g <- function(y){  
              f <- function(x) { 2*x +3}  
              a <- 10 * y  
              f(a)  
}  
  
```  

  
## <a name="revolution-r-enterprise-and-microsoft-r-open"></a>Revolution R Enterprise y Microsoft R Open 
 
 En esta sección se enumeran los problemas específicos de la conectividad, el desarrollo y las herramientas de rendimiento de R que proporciona Revolution Analytics. Estas herramientas se proporcionaron en versiones preliminares anteriores de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. 

En general, se recomienda que desinstale estas versiones anteriores y que instale la versión más reciente de SQL Server R Services, Microsoft R Server o Cliente de Microsoft R.
  
### <a name="running-side-by-side-versions-of-revolution-r-enterprise"></a>Ejecución de versiones en paralelo de Revolution R Enterprise  

 No se admite la instalación en paralelo de Revolution R Enterprise con ninguna versión de [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)].  
  
 Si tiene una licencia para usar una versión diferente de Revolution R Enterprise, debe colocarla en un equipo diferente de donde se encuentran la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y las estaciones de trabajo que quiera usar para conectarse a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
### <a name="limited-support-for-revoscaler-rxexec"></a>Compatibilidad limitada con RevoScaleR rxExec  

 A partir de RC0, la función `rxExec` proporcionada por [!INCLUDE[rsql_rre-short](../../includes/rsql-rre-short-md.md)] solo se puede usar en modo de subproceso único.  
  
 En una próxima versión se agregará paralelismo para `rxExec` entre varios procesos.  
  
### <a name="data-import-and-manipulation-using-revoscaler"></a>Importación de datos y manipulación con RevoScaleR  

 Al leer columnas **varchar** de una base de datos, se eliminarán los espacios en blanco. Para evitarlo, ponga las cadenas entre caracteres que no sean espacios en blanco.  
  
 Cuando use funciones como `rxDataStep` para crear tablas de base de datos con columnas **varchar** , el ancho de columna se calcula en función de una muestra de los datos. Si el ancho varía, puede que sea necesario rellenar todas las cadenas con una longitud común.  
  
 El uso de una transformación para cambiar el tipo de datos de una variable no se admite cuando se usan llamadas repetidas a `rxImport` o `rxTextToXdf` para importar y anexar filas combinando varios archivos de entrada en un solo archivo .xdf.  
  
### <a name="increase-maximum-parameter-size-to-support-rxgetvarinfo"></a>Aumento del tamaño máximo de parámetro para admitir rxGetVarInfo  

 Si usa conjuntos de datos con números de variables muy grandes (por ejemplo, más de 40 000), debe establecer la marca `max-ppsize` al iniciar R para poder usar funciones como `rxGetVarInfo`.  La marca `max-ppsize` especifica el tamaño máximo de la pila de protección del puntero.  
  
 Si usa la consola de R (por ejemplo, en rgui.exe o rterm.exe), puede establecer el valor de max-ppsize en 500 000. Para ello, escriba lo siguiente:  
  
```  
R --max-ppsize=500000  
```  
  
 Si usa el entorno de [!INCLUDE[rsql_developr](../../includes/rsql-developr-md.md)] , puede establecer la marca `max-ppsize` mediante esta llamada al ejecutable RevoIDE:  
  
```  
RevoIDE.exe /RCommandLine --max-ppsize=500000  
```  
  
### <a name="issues-with-rxdtree-function"></a>Problemas con la función rxDTree  

 La función `rxDTree` no admite actualmente transformaciones en la fórmula. En particular, no se admite el uso de la sintaxis `F()` para crear factores sobre la marcha. Sin embargo, los datos numéricos se discretizan automáticamente.  
  
 Los factores ordenados se tratan igual que los factores de todas las funciones de análisis RevoScaleR, excepto `rxDTree`.  
  
### <a name="using-the-r-productivity-environment"></a>Uso de R Productivity Environment  

Algunas versiones preliminares de [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] incluyen un entorno de desarrollo de R para Windows creado mediante Revolution Analytics. 

Pero a efectos de compatibilidad con [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], se recomienda encarecidamente que instale el Cliente de Microsoft R o Microsoft R Server en lugar de las herramientas de Revolution Analytics. [Herramientas de R para Visual Studio](https://www.visualstudio.com/vs/rtvs/) es otro cliente recomendado que admite soluciones de Microsoft R.
  
### <a name="compatibility-issues-with-sqlite-odbc-driver-and-revoscaler"></a>Problemas de compatibilidad con el controlador ODBC de SQLite y RevoScaleR  
 La revisión 0.92 del controlador ODBC de SQLite no es compatible con RevoScaleR, pero se sabe que las revisiones de 0.88 a 0.91 y 0.93 y posteriores son compatibles.  
  
## <a name="see-also"></a>Vea también  
[Novedades de SQL Server 2016](../../sql-server/what-s-new-in-sql-server-2016.md)
  