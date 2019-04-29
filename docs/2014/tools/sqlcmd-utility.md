---
title: sqlcmd, utilidad | Microsoft Docs
ms.custom: ''
ms.date: 11/29/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- statements [SQL Server], command prompt
- QUIT command
- Transact-SQL statements, command prompt
- EXIT command
- sqlcmd commands
- ED command
- sqlcmd utility
- command prompt utilities [SQL Server], sqlcmd
- '!! command'
- stored procedures [SQL Server], command prompt
- system stored procedures [SQL Server], command prompt
- sqlcmd utility, about sqlcmd utility
- scripts [SQL Server], command prompt
- RESET command
- GO command
ms.assetid: e1728707-5215-4c04-8320-e36f161b834a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d128085012c0ef3a9bc58b147f982a26d2c094b8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63035394"
---
# <a name="sqlcmd-utility"></a>sqlcmd Utility
  El `sqlcmd` utilidad le permite introducir [!INCLUDE[tsql](../includes/tsql-md.md)] instrucciones, procedimientos del sistema y archivos de script en el símbolo del sistema, en **Editor de consultas** en modo SQLCMD, en un archivo de script de Windows o en un paso de trabajo del sistema operativo (Cmd.exe) de un [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Trabajo del agente. Esta utilidad usa ODBC para ejecutar lotes de [!INCLUDE[tsql](../includes/tsql-md.md)].  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] usa el [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]SqlClient para la ejecución en normal y el modo SQLCMD en **Editor de consultas**. Cuando `sqlcmd` se ejecuta desde la línea de comandos, `sqlcmd` usa el controlador ODBC. Dado que se pueden aplicar diferentes opciones predeterminadas, podría obtener un comportamiento diferente al ejecutar la misma consulta en el modo SQLCMD de [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] y en la utilidad `sqlcmd`.  
  
 Actualmente, `sqlcmd` no requiere un espacio entre la opción de línea de comandos y el valor. Sin embargo, en versiones futuras, se puede requerir un espacio entre la opción de línea de comandos y el valor.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
   sqlcmd  
   -a  
   packet_size  
   -A (dedicated administrator connection)  
-b (terminate batch job if there is an error)  
-cbatch_terminator-C (trust the server certificate)  
-ddb_name-e (echo input)  
-E (use trusted connection)  
-fcodepage | i:codepage[,o:codepage] | o:codepage[,i:codepage]  
-hrows_per_header-Hworkstation_name-iinput_file-I (enable quoted identifiers)  
-k[1 | 2] (remove or replace control characters)  
-Kapplication_intent-llogin_timeout-L[c] (list servers, optional clean output)  
-merror_level-Mmultisubnet_failover-N (encrypt connection)  
-ooutput_file-p[1] (print statistics, optional colon format)  
-Ppassword-q "cmdline query"-Q "cmdline query" (and exit)  
-r[0 | 1] (msgs to stderr)  
-R (use client regional settings)  
-scol_separator-S [protocol:]server[\instance_name][,port]  
-tquery_timeout-u (unicode output file)  
-Ulogin_id-vvar = "value"-Verror_severity_level-wcolumn_width-W (remove trailing spaces)  
-x (disable variable substitution)  
-X[1] (disable commands, startup script, environment variables and optional exit)  
-yvariable_length_type_display_width-Yfixed_length_type_display_width-znew_password -Znew_password (and exit)  
  
-? (usage)  
```  
  
## <a name="command-line-options"></a>Opciones de línea de comandos  
 **Opciones relacionadas con el inicio de sesión**  
  **-A**  
 Inicia sesión en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] con una Conexión de administrador dedicada (DAC). Este tipo de conexión se utiliza para solucionar problemas de un servidor. Solo funcionará con equipos servidores que admitan DAC. Si DAC no está disponible, `sqlcmd` genera un mensaje de error y, después, se cierra. Para obtener más información sobre DAC, vea [Conexión de diagnóstico para administradores de bases de datos](../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md).  
  
 **-C**  
 Este modificador lo usa el cliente para configurarlo de forma que confíe implícitamente en el certificado de servidor sin validación. Esta opción es equivalente a la opción de ADO.NET `TRUSTSERVERCERTIFICATE = true`.  
  
 **-d** _db_name_  
 Problemas de un `USE` *db_name* instrucción cuando se inicia `sqlcmd`. Esta opción establece la variable de scripting de `sqlcmd` SQLCMDDBNAME. Especifica la base de datos inicial. El valor predeterminado es la propiedad de base de datos predeterminada del inicio de sesión. Si la base de datos no existe, se genera un mensaje de error y `sqlcmd` se cierra.  
  
 **-l** _login_timeout_  
 Especifica el número de segundos que tienen que transcurrir antes de que un inicio de sesión de `sqlcmd` en el proveedor ODBC agote el tiempo de espera cuando se intente conectar a un servidor. Esta opción establece la variable de scripting de `sqlcmd` SQLCMDLOGINTIMEOUT. El tiempo de espera predeterminado para el inicio de sesión de `sqlcmd` es de ocho segundos. El período de tiempo de espera de inicio de sesión debe ser un número comprendido entre 0 y 65534. Si el valor proporcionado no es numérico o no está dentro de este intervalo, `sqlcmd` genera un mensaje de error. El valor 0 especifica que el tiempo de espera es infinito.  
  
 **-E**  
 Usa una conexión de confianza en lugar de usar un nombre de usuario y una contraseña para iniciar sesión en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. De manera predeterminada, si no se especifica -E, `sqlcmd` usa la opción de conexión de confianza.  
  
 La opción **-E** omite la posible configuración de la variable de entorno de nombre de usuario y contraseña, como SQLCMDPASSWORD. Si se usa la opción **-E** junto con la opción **-U** o la opción **-P**, se genera un mensaje de error.  
  
 **-H** _workstation_name_  
 Un nombre de estación de trabajo. Esta opción establece la variable de scripting de `sqlcmd` SQLCMDWORKSTATION. El nombre de la estación de trabajo se muestra en la columna **hostname** de la vista de catálogo **sys.processes** y se puede devolver mediante el procedimiento almacenado **sp_who**. Si no se especifica esta opción, el nombre actual del equipo es el valor predeterminado. Este nombre se puede usar para identificar diferentes sesiones de `sqlcmd`.  
  
 **-K** _application_intent_  
 Declara el tipo de carga de trabajo de la aplicación al conectarse a un servidor. El único valor actualmente admitido es **de solo lectura**. Si no se especifica **-K**, la utilidad sqlcmd no admitirá la conectividad con una réplica secundaria en el grupo de disponibilidad AlwaysOn. Para más información, consulte [Secundarias activas: réplicas secundarias legibles](../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md).  
  
 `-M` *multisubnet_failover*  
 Especifique siempre `-M` al conectarse a un agente de escucha de un grupo de disponibilidad de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o a una instancia de clúster de conmutación por error de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. `-M` proporciona una detección más rápida del servidor activo (actualmente) y una conexión al mismo. Si no se especifica `-M`, `-M` está desactivado. Para obtener más información acerca de [!INCLUDE[ssHADR](../includes/sshadr-md.md)], consulte [los agentes de escucha del grupo de disponibilidad, conectividad de cliente y conmutación por error de aplicación &#40;SQL Server&#41;](../database-engine/listeners-client-connectivity-application-failover.md), [creación y configuración de grupos de disponibilidad &#40;SQL Server&#41;](../database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server.md), [agrupación en clústeres de conmutación por error y grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md), y [secundarias activas: Las réplicas secundarias legibles](../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md) .  
  
 **-N**  
 Este modificador lo usa el cliente para solicitar una conexión cifrada.  
  
 **-P** _password_  
 Es una contraseña especificada por el usuario. En las contraseñas se distingue entre mayúsculas y minúsculas. Si se usa la opción - U y **-P** no se usa la opción y no se ha establecido la variable de entorno SQLCMDPASSWORD, `sqlcmd` pide al usuario una contraseña. Si el **-P** opción se utiliza al final de la línea de comandos sin especificar ninguna contraseña `sqlcmd` utiliza la contraseña predeterminada (NULL).  
  
> [!IMPORTANT]  
>  No utilice una contraseña en blanco. Utilice una contraseña segura. Para obtener más información, consulte [Strong Passwords](../relational-databases/security/strong-passwords.md).  
  
 El mensaje de contraseña se muestra en la consola de la siguiente manera: `Password:`  
  
 La entrada del usuario queda oculta. Esto significa que no se muestra nada y que el cursor permanece en su posición.  
  
 La variable de entorno SQLCMDPASSWORD permite establecer una contraseña predeterminada para la sesión actual. Por lo tanto, las contraseñas no tienen que estar codificadas de forma rígida en los archivos por lotes.  
  
 En el siguiente ejemplo primero se establece la variable SQLCMDPASSWORD en el símbolo del sistema y, después, se obtiene acceso a la utilidad `sqlcmd`. En el símbolo del sistema, escriba:  
  
 `SET SQLCMDPASSWORD= p@a$$w0rd`  
  
> [!IMPORTANT]  
>  La contraseña será visible para cualquiera que pueda ver el monitor del equipo.  
  
 En el siguiente símbolo del sistema, escriba:  
  
 `sqlcmd`  
  
 Si la combinación de nombre de usuario y contraseña no es correcta, se genera un mensaje de error.  
  
> [!NOTE]  
>  La variable de entorno OSQLPASSWORD se ha conservado por motivos de compatibilidad. La variable de entorno SQLCMDPASSWORD tiene prioridad sobre la variable de entorno OSQLPASSWORD; Esto significa que `sqlcmd` y **osql** se puede usar una junto a la otra sin interferencias y que los scripts anteriores seguirán funcionando.  
  
 Si se usa la opción **-P** junto con la opción **-E** , se genera un mensaje de error.  
  
 Si la opción **-P** va seguida de más de un argumento, se genera un mensaje de error y el programa se cierra.  
  
 **-S** [*protocolo*:]*servidor*[**\\**_nombre_de_instancia_][**,**_puerto_]  
 Especifica la instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a la que hay que conectarse. Establece la variable de scripting de `sqlcmd` SQLCMDSERVER.  
  
 Especifique *nombre_de_servidor* para conectar con la instancia predeterminada de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en ese equipo servidor. Especifique *nombre_de_servidor* [ **\\**_nombre_de_instancia_ ] para conectar con una instancia con nombre de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en ese equipo servidor. Si no se especifica ningún equipo, `sqlcmd` se conecta a la instancia predeterminada de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en el equipo local. Esta opción es necesaria si se ejecuta `sqlcmd` desde un equipo remoto conectado a la red.  
  
 *protocolo* puede ser `tcp` (TCP/IP), `lpc` (memoria compartida), o `np` (canalizaciones con nombre).  
  
 Si no especifica un *nombre_servidor* [ **\\** _instance_name_ ] al iniciar `sqlcmd`, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] busca y usa el Variable de entorno SQLCMDSERVER.  
  
> [!NOTE]  
>  La variable de entorno OSQLSERVER se ha conservado por motivos de compatibilidad. La variable de entorno SQLCMDSERVER tiene prioridad sobre la variable de entorno OSQLSERVER; Esto significa que `sqlcmd` y **osql** se puede usar una junto a la otra sin interferencias y que los scripts anteriores seguirán funcionando.  
  
 **-U** _login_id_  
 Es el identificador de inicio de sesión del usuario.  
  
> [!NOTE]  
>  La variable de entorno OSQLUSER está disponible por motivos de compatibilidad con versiones anteriores. La variable de entorno SQLCMDUSER tiene prioridad sobre OSQLUSER. Esto significa que `sqlcmd` y **osql** puede usarse junto a la otra sin interferencias. También significa que los scripts de **osql** existentes seguirán funcionando.  
  
 Si no la **- U** opción ni la **-P** se especifica la opción, `sqlcmd` intenta conectarse mediante el uso de [!INCLUDE[msCoName](../includes/msconame-md.md)] modo de autenticación de Windows. La autenticación se basa en la cuenta de Windows del usuario que está ejecutando `sqlcmd`.  
  
 Si se usa la opción **-U** junto con la opción **-E** (descrita más adelante en este tema), se genera un mensaje de error. Si la opción **-U** va seguida de más de un argumento, se genera un mensaje de error y el programa se cierra.  
  
 **-z** _nueva_contraseña_  
 Cambiar contraseña:  
  
 `sqlcmd -U someuser -P s0mep@ssword -z a_new_p@a$$w0rd`  
  
 **-Z** _nueva_contraseña_  
 Cambiar contraseña y salir:  
  
 `sqlcmd -U someuser -P s0mep@ssword -Z a_new_p@a$$w0rd`  
  
 **Opciones de entrada o salida**  
  **-f** _página_de_códigos_ | **i:**_página_de_códigos_[**,o:**_página_de_códigos_] | **o:**_página_de_códigos_[**,i:**_página_de_códigos_]  
 Especifica las páginas de códigos de entrada y de salida. El número de página de códigos es un valor numérico que especifica una página de códigos instalada en Windows.  
  
 Reglas de conversión de páginas de códigos:  
  
-   Si no se especifica ninguna página de códigos, `sqlcmd` usará la página de códigos actual para los archivos de entrada y salida, a menos que el archivo de entrada sea un archivo Unicode, en cuyo caso no es necesaria la conversión.  
  
-   `sqlcmd` reconoce automáticamente los archivos de entrada Unicode "big endian" y "little endian". Si se ha especificado la opción **-u** , la salida siempre será Unicode "little endian".  
  
-   Si no se especifica ningún archivo de salida, la página de códigos de salida será la página de códigos de la consola. Esto permite que la salida se muestre correctamente en la consola.  
  
-   Si hay varios archivos de entrada, se considera que pertenecen a la misma página de códigos. Los archivos de entrada Unicode y no Unicode pueden ser mixtos.  
  
 Escriba `chcp` en el símbolo del sistema para comprobar la página de códigos de Cmd.exe.  
  
 **-i** _archivo_de_entrada_[**,**_archivo_de_entrada2_...]  
 Identifica el archivo que contiene un lote de instrucciones SQL o procedimientos almacenados. Se pueden especificar varios archivos que se leerán y se procesarán en orden. No use ningún espacio entre los nombres de archivo. `sqlcmd` comprobará primero si todos los archivos especificados existen. Si uno o más archivos no existen, `sqlcmd` se cerrará. Las opciones -i y -Q/-q se excluyen mutuamente.  
  
 Ejemplos de rutas de acceso:  
  
 **-i** C:\\< nombre de archivo\>  
  
 **-i** \\ \\< servidor\>\\< recursoCompartido$ >\\< nombre de archivo\>  
  
 **-i** "C:\Una carpeta\\<nombreDeArchivo\>"  
  
 Las rutas de acceso a archivos que contengan espacios deben escribirse entre comillas.  
  
 Esta opción se puede usar más de una vez: **-i**_archivo_de_entrada_ **-I**_I archivo_de_entrada._  
  
 **-o** _output_file_  
 Identifica el archivo que recibe la salida de `sqlcmd`.  
  
 Si se especifica **-u** , *archivo_de_salida* se almacena en formato Unicode. Si el nombre de archivo no es válido, se genera un mensaje de error y `sqlcmd` se cierra. `sqlcmd` no admite la escritura simultánea de varios procesos de `sqlcmd` en el mismo archivo. El archivo de salida estará dañado o será incorrecto. Vea el modificador **-f** para obtener más información sobre los formatos de archivo. Este archivo se creará si no existe. Se sobrescribirá cualquier archivo con el mismo nombre que pertenezca a una sesión de `sqlcmd` anterior. El archivo que se especifica aquí no es el archivo **stdout** . Si se especifica un archivo **stdout** , este archivo no se usará.  
  
 Ejemplos de rutas de acceso:  
  
 **-o** C:\\< nombreDeArchivo>  
  
 **-o** \\ \\< servidor\>\\< recursoCompartido$ >\\< nombre de archivo\>  
  
 **-o "** C:\Una carpeta\\<nombreDeArchivo\>"  
  
 Las rutas de acceso a archivos que contengan espacios deben escribirse entre comillas.  
  
 **-r**[**0** | **1**]  
 Redirige la salida del mensaje de error a la pantalla (**stderr**). Si no especifica ningún parámetro o si especifica **0**, solo se redirigirán los mensajes de error con un nivel de gravedad 11 o superior. Si especifica **1**, toda salida de mensaje, incluida PRINT, se redirigirá. No surte efecto si se usa -o. De forma predeterminada, los mensajes se envían a **stdout**.  
  
 **-R**  
 Hace que `sqlcmd` localizar numérico, moneda, fecha y las columnas de tiempo para recuperarse [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] según la configuración regional del cliente. De forma predeterminada, estas columnas se muestran con la configuración regional del servidor.  
  
 **-u**  
 Especifica que *archivo_de_salida* se almacena en formato Unicode, independientemente del formato de *archivo_de_entrada*.  
  
 **Opciones de ejecución de consultas**  
  **-e**  
 Escribe scripts de entrada en el dispositivo de salida estándar (**stdout**).  
  
 **-I**  
 Activa (establece en ON) la opción de conexión SET QUOTED_IDENTIFIER. De forma predeterminada, la opción está establecida en OFF. Para obtener más información, vea [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-quoted-identifier-transact-sql).  
  
 **-q"** _consulta cmdline_ **"**  
 Ejecuta una consulta cuando se inicia `sqlcmd`, pero no cierra `sqlcmd` cuando finaliza la consulta. Se pueden ejecutar varias consultas delimitadas por punto y coma. Utilice las comillas alrededor de la consulta, como se muestra en el siguiente ejemplo.  
  
 En el símbolo del sistema, escriba:  
  
 `sqlcmd -d AdventureWorks2012 -q "SELECT FirstName, LastName FROM Person.Person WHERE LastName LIKE 'Whi%';"`  
  
 `sqlcmd -d AdventureWorks2012 -q "SELECT TOP 5 FirstName FROM Person.Person;SELECT TOP 5 LastName FROM Person.Person;"`  
  
> [!IMPORTANT]  
>  No use el terminador GO en la consulta.  
  
 Si se especifica `-b` junto con esta opción, `sqlcmd` se cierra en caso de error. `-b` se describe más adelante en este tema.  
  
 **-Q"** _consulta cmdline_ **"**  
 Ejecuta una consulta cuando se inicia `sqlcmd` e inmediatamente después cierra `sqlcmd`. Se pueden ejecutar varias consultas delimitadas por punto y coma.  
  
 Utilice las comillas alrededor de la consulta, como se muestra en el siguiente ejemplo.  
  
 En el símbolo del sistema, escriba:  
  
 `sqlcmd -d AdventureWorks2012 -Q "SELECT FirstName, LastName FROM Person.Person WHERE LastName LIKE 'Whi%';"`  
  
 `sqlcmd -d AdventureWorks2012 -Q "SELECT TOP 5 FirstName FROM Person.Person;SELECT TOP 5 LastName FROM Person.Person;"`  
  
> [!IMPORTANT]  
>  No use el terminador GO en la consulta.  
  
 Si se especifica `-b` junto con esta opción, `sqlcmd` se cierra en caso de error. `-b` se describe más adelante en este tema.  
  
 **-t** _tiempo_de_espera_de_consulta_  
 Especifica el número de segundos que tienen que transcurrir antes de que un comando (o la instrucción de SQL) exceda el tiempo de espera. Esta opción establece la `sqlcmd` SQLCMDSTATTIMEOUT variable de scripting. Si no se especifica ningún valor para *tiempo_de_espera* , el comando no tiene tiempo de espera. *tiempo_de_espera**consulta* debe ser un número comprendido entre 1 y 65534. Si el valor proporcionado no es numérico o no está dentro de este intervalo, `sqlcmd` genera un mensaje de error.  
  
> [!NOTE]  
>  El tiempo de espera real puede variar unos segundos con respecto al valor de *tiempo_de_espera* especificado.  
  
 **-vvar =** _value_[ **var =** _value_...]  
 Crea un `sqlcmd`variable de scripting que puede usarse en un `sqlcmd` secuencia de comandos. Si el valor contiene espacios en blanco, especifíquelo entre comillas. Puede especificar varios  **_var_**=**"*`values`*"** valores. Si hay errores en alguno de los valores especificados, `sqlcmd` genera un mensaje de error y después se cierra.  
  
 `sqlcmd -v MyVar1=something MyVar2="some thing"`  
  
 `sqlcmd -v MyVar1=something -v MyVar2="some thing"`  
  
 **-x**  
 Hace que `sqlcmd` omita las variables de scripting. Es útil cuando un script contiene muchas instrucciones INSERT que pueden contener cadenas con el mismo formato que las variables normales, por ejemplo, $(*nombre_de_variable*).  
  
 **Opciones de formato**  
  **-h** _headers_  
 Especifica el número de filas que se van a imprimir entre los encabezados de las columnas. La opción predeterminada es imprimir los encabezados una vez para cada conjunto de resultados de la consulta. Esta opción establece la variable de scripting de `sqlcmd` SQLCMDHEADERS. Use **-1** para especificar que no se deben imprimir los encabezados. Cualquier valor no válido hará que `sqlcmd` genere un mensaje de error y se cierre.  
  
 **-k** [**1** | **2**]  
 Quita todos los caracteres de control, como tabulaciones y nuevos caracteres de línea de la salida. De este modo se conserva el formato de las columnas cuando se devuelven datos. Si se especifica 1, los caracteres de control se reemplazan con un solo espacio. Si se especifica 2, los caracteres de control consecutivos se reemplazan por un solo espacio. **-k** equivale a **-k1**.  
  
 **-s** _col_separator_  
 Especifica el carácter separador de columnas. El valor predeterminado es un espacio en blanco. Esta opción establece la variable de scripting de `sqlcmd` SQLCMDCOLSEP. Para usar caracteres que tienen un significado especial para el sistema operativo, como la y comercial (&) o el punto y coma (;), incluya el carácter entre comillas ("). El separador de columnas puede ser cualquier carácter de 8 bits.  
  
 **-w** _column_width_  
 Especifica el ancho de pantalla para la salida. Esta opción establece la variable de scripting de `sqlcmd` SQLCMDCOLWIDTH. El ancho de columna debe ser un número mayor que 8 y menor que 65536. Si el ancho de columna especificado no está en ese intervalo, `sqlcmd` generará un mensaje de error. El ancho predeterminado es 80 caracteres. Cuando la línea de salida supera el ancho de columna especificado, se ajusta a la siguiente línea.  
  
 **-W**  
 Esta opción quita los espacios finales de una columna. Use esta opción junto con la opción **-s** cuando prepare datos que se vayan a exportar a otra aplicación. No se puede usar con las opciones **-y** ni **-Y** .  
  
 **-y** _anchura_de_visualización_de_tipo_de_longitud_variable_  
 Establece la variable de scripting de `sqlcmd` SQLCMDMAXVARTYPEWIDTH. El valor predeterminado es 256. Limita el número de caracteres que se devuelve para tipos de datos de longitud variable y gran tamaño:  
  
-   `varchar(max)`  
  
-   `nvarchar(max)`  
  
-   `varbinary(max)`  
  
-   `xml`  
  
-   `UDT (user-defined data types)`  
  
-   `text`  
  
-   `ntext`  
  
-   `image`  
  
> [!NOTE]  
>  Los UDT pueden ser de longitud fija, en función de la implementación. Si esta longitud de un UDT de longitud fija es más corta que *anchura_de_visualización*, el valor del UDT devuelto no se ve afectado. No obstante, si la longitud es mayor que *anchura_de_visualización*, la salida queda truncada.  
  
 
> [!IMPORTANT]  
>  Use la opción **-y 0** con mucha precaución, ya que puede causar graves problemas de rendimiento en el servidor y en la red, según el tamaño de los datos devueltos.  
  
 **-Y** _anchura_de_visualización_de_tipo_de_longitud_fija_  
 Establece la variable de scripting de `sqlcmd` SQLCMDMAXFIXEDTYPEWIDTH. El valor predeterminado es 0 (ilimitado). Limita el número de caracteres que se devuelve para los siguientes tipos de datos:  
  
-   `char(` *n* `)`, donde 1 < = n < = 8000  
  
-   `nchar(n` *n* `)`, donde 1 < = n < = 4000  
  
-   `varchar(n` *n* `)`, donde 1 < = n < = 8000  
  
-   `nvarchar(n` *n* `)`, donde 1 < = n < = 4000  
  
-   `varbinary(n` *n* `)`, donde 1 < = n < = 4000  
  
-   `variant`  
  
 **Opciones de informes de errores**  
  `-b`  
 Especifica que `sqlcmd` se cierre y devuelva un valor de DOS ERRORLEVEL cuando se produce un error. El valor que se devuelve a la variable DOS ERRORLEVEL es **1** cuando el mensaje de error de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tiene un nivel de gravedad superior a 10; de lo contrario, el valor devuelto es **0**. Si se ha establecido la opción `-V` además de `-b`, `sqlcmd` no notificará un error si el nivel de gravedad es inferior a los valores establecidos mediante `-V`. Los archivos por lotes del símbolo del sistema pueden probar el valor de ERRORLEVEL y controlar el error apropiadamente. `sqlcmd` no notifica los mensajes de error con un nivel de gravedad de 10 (mensajes informativos).  
  
 Si el script de `sqlcmd` contiene un comentario incorrecto, un error de sintaxis o carece de una variable de scripting, el valor de ERRORLEVEL devuelto es 1.  
  
 **-m** _error_level_  
 Controla qué mensajes de error se envían a **stdout**. Se envían los mensajes que tienen un nivel de gravedad mayor o igual que este nivel. Cuando este valor se establece en **-1**, se envían todos los mensajes, incluidos los informativos. No se permiten espacios entre **-m** y **-1**. Por ejemplo, **-m-1** es válido, pero **-m-1** no.  
  
 Esta opción también establece la variable de scripting de `sqlcmd` SQLCMDERRORLEVEL. El valor predeterminado de esta variable es 0.  
  
 `-V` *error_severity_level*  
 Controla el nivel de gravedad que se usa para establecer la variable ERRORLEVEL. Los mensajes de error que tienen niveles de gravedad mayores o iguales que este valor establecen ERRORLEVEL. Los valores menores que 0 se notifican como 0. Los archivos CMD y por lotes se pueden usar para probar el valor de la variable ERRORLEVEL.  
  
 **Otras opciones**  
  **-a** _packet_size_  
 Solicita un paquete de un tamaño diferente. Esta opción establece la variable de scripting de `sqlcmd` SQLCMDPACKETSIZE. *tamaño_paquete* debe ser un valor entre 512 y 32767. El valor predeterminado es 4096. Un tamaño de paquete mayor puede mejorar el rendimiento de la ejecución de scripts que comprenden gran cantidad de instrucciones de SQL entre los comandos GO. Puede solicitar un tamaño de paquete mayor. No obstante, si se deniega la solicitud, `sqlcmd` usa el valor predeterminado de servidor para el tamaño de paquete.  
  
 **-c** _terminador_de_lote_  
 Especifica el terminador del lote. De forma predeterminada, los comandos se terminan y se envían a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] escribiendo la palabra "GO" en una línea aparte. Cuando restablezca el terminador del lote, no use palabras claves de [!INCLUDE[tsql](../includes/tsql-md.md)] ni caracteres especiales que tengan un significado especial para el sistema operativo, incluso aunque vayan precedidos de una barra diagonal invertida.  
  
 **-L**[**c**]  
 Enumera los equipos servidores configurados localmente y los nombres de los equipos servidores que difunden en la red. Este parámetro no se puede usar en combinación con otros parámetros. El número máximo de equipos de servidor que se puede enumerar es 3000. Si la lista de servidor se trunca debido al tamaño del búfer, aparece un mensaje de advertencia.  
  
> [!NOTE]  
>  Debido a la naturaleza de las difusiones en las redes, `sqlcmd` podría no recibir una respuesta de todos los servidores a tiempo. Por lo tanto, la lista de servidores devuelta puede variar en cada invocación de esta opción.  
  
 Si se especifica el parámetro opcional **c** , la salida aparece sin lo servidores: la línea de encabezado y cada línea de servidor se muestra sin espacios iniciales. Esto se denomina salida limpia. La salida limpia mejora el rendimiento del procesamiento de los lenguajes de scripting.  
  
 **-p**[**1**]  
 Imprime estadísticas de rendimiento para cada conjunto de resultados. A continuación se muestra un ejemplo del formato para las estadísticas de rendimiento:  
  
 `Network packet size (bytes): n`  
  
 `x xact[s]:`  
  
 `Clock Time (ms.): total       t1  avg       t2 (t3 xacts per sec.)`  
  
 Donde:  
  
 `x` = número de transacciones que procesa [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 `t1` indica el tiempo total de todas las transacciones.  
  
 `t2` = tiempo medio de una única transacción.  
  
 `t3` = número medio de transacciones por segundo.  
  
 Todos los tiempos se indican en milisegundos.  
  
 Si se especifica el parámetro opcional **1** , el formato de salida de las estadísticas es el separado por dos puntos, que se puede importar fácilmente en una hoja de cálculo o se puede procesar en un script.  
  
 Si el parámetro opcional tiene cualquier valor distinto de **1**, se genera un error y `sqlcmd` se cierra.  
  
 `-X`[**1**]  
 Deshabilita los comandos que pueden poner en peligro la seguridad del sistema cuando se ejecuta `sqlcmd` desde un archivo por lotes. Los comandos deshabilitados se siguen reconociendo; `sqlcmd` emite un mensaje de advertencia y sigue ejecutándose. Si el parámetro opcional **1** se especifica, `sqlcmd` genera un mensaje de error y, a continuación, se cierra. Los siguientes comandos se deshabilitan cuando se usa la opción `-X`:  
  
-   **ED**  
  
-   **!!** _command_  
  
 Si se especifica la opción `-X`, eso evita que se pasen variables de entorno a `sqlcmd`. También impide que el script de inicio especificada mediante la variable de scripting SQLCMDINI se ejecute. Para obtener más información acerca de `sqlcmd` las variables de scripting, consulte [usar sqlcmd con Variables de Scripting](../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md).  
  
 **-?**  
 Muestra el resumen de la sintaxis de las opciones de `sqlcmd`.  
  
## <a name="remarks"></a>Comentarios  
 Las opciones no tienen que utilizarse forzosamente en el orden mostrado en la sección de sintaxis.  
  
 Cuando se devuelven varios resultados, `sqlcmd` imprime una línea en blanco entre cada conjunto de resultados de un lote. Además, el "\<x > filas afectadas" no aparece el mensaje cuando no se aplica a la instrucción ejecutada.  
  
 Para usar `sqlcmd` de forma interactiva, escriba `sqlcmd` en el símbolo del sistema con una o varias de las opciones descritas anteriormente en este tema. Para más información, vea [Usar la utilidad sqlcmd](../relational-databases/scripting/sqlcmd-use-the-utility.md).  
  
> [!NOTE]  
>  Las opciones **-L**, **-Q**, **-Z** o **-i** provocar `sqlcmd` se cierre después de la ejecución.  
  
 La longitud total de la línea de comandos de `sqlcmd` en el entorno de comandos (Cmd.exe), incluidos todos los argumentos y las variables expandidas, es la que determine el sistema operativo para Cmd.exe.  
  
## <a name="variable-precedence-low-to-high"></a>Precedencia de variables (menor a mayor)  
  
1.  Variables de entorno de nivel de sistema.  
  
2.  Variables de entorno de nivel de usuario.  
  
3.  Shell de comandos (**establecer** X = Y) establecido en el símbolo del sistema antes de ejecutar `sqlcmd`.  
  
4.  **sqlcmd-v** X=Y  
  
5.  **:Setvar** X Y  
  
> [!NOTE]  
>  Para ver las variables de entorno, en el **Panel de control**, abra **Sistema**y haga clic en la pestaña **Opciones avanzadas** .  
  
## <a name="sqlcmd-scripting-variables"></a>Variables de scripting sqlcmd  
  
|Variable|Modificador relacionado|L/E|Default|  
|--------------|--------------------|----------|-------------|  
|SQLCMDUSER|-U|R|""|  
|SQLCMDPASSWORD|-P|--|""|  
|SQLCMDSERVER|-S|R|"DefaultLocalInstance"|  
|SQLCMDWORKSTATION|-H|R|"ComputerName"|  
|SQLCMDDBNAME|-d|R|""|  
|SQLCMDLOGINTIMEOUT|-l|L/E|"8" (segundos)|  
|SQLCMDSTATTIMEOUT|-T|L/E|"0" = esperar indefinidamente|  
|SQLCMDHEADERS|-H|L/E|"0"|  
|SQLCMDCOLSEP|-S|L/E|"|  
|SQLCMDCOLWIDTH|-w|L/E|"0"|  
|SQLCMDPACKETSIZE|-A|R|"4096"|  
|SQLCMDERRORLEVEL|-M|L/E|0|  
|SQLCMDMAXVARTYPEWIDTH|-y|L/E|"256"|  
|SQLCMDMAXFIXEDTYPEWIDTH|-y|L/E|"0" = ilimitado|  
|SQLCMDEDITOR||L/E|"edit.com"|  
|SQLCMDINI||R|""|  
  
 SQLCMDUSER, SQLCMDPASSWORD y SQLCMDSERVER se establecen cuando se usa **:Connect**  
  
 .  
  
 L indica que el valor solo puede establecerse una vez durante la inicialización del programa.  
  
 L/E indica que el valor puede modificarse mediante el comando **setvar** y que los comandos siguientes se verán influidos por el nuevo valor.  
  
## <a name="sqlcmd-commands"></a>Comandos de sqlcmd  
 Además de las instrucciones [!INCLUDE[tsql](../includes/tsql-md.md)] de `sqlcmd`, también están disponibles los siguientes comandos:  
  
|||  
|-|-|  
|**GO** [*count*]|**:List**|  
|[**:**] **RESET**|**:Error**|  
|[**:**] **ED**|**:Out**|  
|[**:**] **!!**|**:Perftrace**|  
|[**:**] **QUIT**|**:Connect**|  
|[**:**] **EXIT**|**:On Error**|  
|**:r**|**:Help**|  
|**:ServerList**|**:XML** [**ON** &#124; **OFF**]|  
|**:Setvar**|**:Listvar**|  
  
 Tenga en cuenta lo siguiente cuando use comandos de `sqlcmd`:  
  
-   Todos los comandos de `sqlcmd`, excepto GO, deben ir precedidos de dos puntos (:).  
  
    > [!IMPORTANT]  
    >  Para mantener la compatibilidad con los scripts de **osql** existentes, algunos de los comandos se reconocerán sin los dos puntos. Esto se indica por [**:**].  
  
-   Los comandos de `sqlcmd` se reconocen solo si aparecen al principio de una línea.  
  
-   Los comandos de `sqlcmd` no distinguen entre mayúsculas y minúsculas.  
  
-   Cada comando debe estar en una línea separada. Un comando no puede ir seguido de una instrucción de [!INCLUDE[tsql](../includes/tsql-md.md)] o de otro comando.  
  
-   Los comandos se ejecutan inmediatamente. No se colocan en el búfer de ejecución, como es el caso de las instrucciones [!INCLUDE[tsql](../includes/tsql-md.md)] .  
  
 **Editar comandos**  
  [**:**] **ED**  
 Inicia el editor de texto. Este editor se puede utilizar para editar el lote actual de [!INCLUDE[tsql](../includes/tsql-md.md)] o el último lote ejecutado. Para editar el último lote ejecutado, el comando **ED** debe escribirse inmediatamente después de que se complete la ejecución del último lote.  
  
 El editor de texto se define mediante la variable de entorno SQLCMDEDITOR. El editor predeterminado es "Edit". Para cambiar el editor, establezca la variable de entorno SQLCMDEDITOR. Por ejemplo, para establecer el editor en el Bloc de notas de [!INCLUDE[msCoName](../includes/msconame-md.md)] , en el símbolo del sistema, escriba:  
  
 `SET SQLCMDEDITOR=notepad`  
  
 [**:**] **RESET**  
 Borra la caché de instrucciones.  
  
 **:List**  
 Imprime el contenido de la memoria caché de instrucciones.  
  
 **Variables**  
  **: Setvar** \< **var**> [ **"*`value`*"** ]  
 Define las variables de scripting de `sqlcmd`. Las variables de scripting tienen el siguiente formato: `$(VARNAME)`.  
  
 Los nombres de variables no distinguen entre mayúsculas y minúsculas.  
  
 Las variables de scripting pueden establecerse de los siguientes modos:  
  
-   Implícitamente mediante una opción de línea de comandos. Por ejemplo, el **-l** opción establece la SQLCMDLOGINTIMEOUT `sqlcmd` variable.  
  
-   Explícitamente mediante el comando **:Setvar** .  
  
-   Al definir una variable de entorno antes de ejecutar `sqlcmd`.  
  
> [!NOTE]  
>  La opción `-X` impide que las variables de entorno se pasen a `sqlcmd`.  
  
 Si una variable definida mediante **:Setvar** y una variable de entorno tienen el mismo nombre, la variable definida mediante **:Setvar** tiene prioridad.  
  
 Los nombres de variables no deben contener caracteres de espacio en blanco.  
  
 Los nombres de variable no pueden tener el mismo formato que una expresión variable como $(var).  
  
 Si el valor de la cadena de la variable de script contiene espacios en blanco, incluya el valor entre comillas. Si un valor para la variable del script no se especifica, la variable de script se elimina.  
  
 **:Listvar**  
 Muestra una lista de variables de scripting que están establecidas actualmente.  
  
> [!NOTE]  
>  Solo se establecen mediante variables de scripting `sqlcmd`y los que se establecen mediante el **: Setvar** se mostrará el comando.  
  
 **Comandos de salida**  
  **:Error**   
 **_\<_** _filename_  **_>|_ STDERR|STDOUT**  
 Redirige toda la salida de error al archivo especificado por *nombre_de_archivo*, a **stderr** o a **stdout**. El comando **Error** puede aparecer varias veces en un script. De forma predeterminada, la salida de error se envía a **stderr**.  
  
 *Nombre de archivo*  
 Crea y abre un archivo que recibirá la salida. Si el archivo ya existe, se truncará en cero bytes. Si el archivo no está disponible a causa de los permisos u otros motivos, la salida no se cambiará y se enviará al último destino especificado o al predeterminado.  
  
 **STDERR**  
 Cambia la salida del error al flujo **stderr** . Si se ha redirigido, el destino al cual se redirige el flujo recibirá la salida del error.  
  
 **STDOUT**  
 Cambia la salida del error al flujo **stdout** . Si se ha redirigido, el destino al cual se redirige el flujo recibirá la salida del error.  
  
 **:Out \<** _nombre_de_archivo_ **>**| **STDERR**| **STDOUT**  
 Crea y redirige todos los resultados de consulta al archivo especificado por *file name*, a **stderr** o a **stdout**. De forma predeterminada, la salida se envía a **stdout**. Si el archivo ya existe, se truncará en cero bytes. El comando **Out** puede aparecer varias veces en un script.  
  
 **:Perftrace \<** _nombre_de_archivo_ **>**| **STDERR**| **STDOUT**  
 Crea y redirige toda la información de seguimiento de rendimiento al archivo especificado por *nombre_de_archivo*, a **stderr** o a **stdout**. De forma predeterminada, la salida de seguimiento de rendimiento se envía a **stdout**. Si el archivo ya existe, se truncará en cero bytes. El comando **Perftrace** puede aparecer varias veces en un script.  
  
 **Comandos de control de ejecución**  
  **: En caso de Error**[ `exit`  |  `ignore`]  
 Establece la acción que se llevará a cabo cuando se produzca un error durante la ejecución del script o del lote.  
  
 Cuando se usa la opción `exit`, `sqlcmd` se cierra con el valor de error correspondiente.  
  
 Cuando se usa la opción `ignore`, `sqlcmd` pasa por alto el error y continúa con la ejecución del lote o del script. De forma predeterminada, se imprimirá un mensaje de error.  
  
 [**:**] **QUIT**  
 Hace que `sqlcmd` se cierre.  
  
 [**:**] **EXIT**[ **(*`statement`*)** ]  
 Permite usar el resultado de una instrucción SELECT como valor devuelto de `sqlcmd`. Si es numérica, la primera columna de la última fila del resultado se convierte en un entero de 4 bytes (long). MS-DOS pasa el byte bajo al proceso primario o al nivel de errores del sistema operativo. Windows 200x pasa el entero de 4 bytes completo. La sintaxis es la siguiente:  
  
 `:EXIT(query)`  
  
 Por ejemplo:  
  
 `:EXIT(SELECT @@ROWCOUNT)`  
  
 También puede incluir el parámetro **EXIT** como parte de un archivo por lotes. Por ejemplo, en el símbolo del sistema, escriba:  
  
 `sqlcmd -Q "EXIT(SELECT COUNT(*) FROM '%1')"`  
  
 El `sqlcmd` utilidad envía todo entre los paréntesis **()** al servidor. Si un procedimiento almacenado del sistema selecciona un conjunto y devuelve un valor, solo se devuelve la selección. La instrucción EXIT **()** sin nada entre los paréntesis ejecuta todo lo que precede a estos en el lote y, después, se cierra sin ningún valor devuelto.  
  
 Cuando se especifica una consulta incorrecta, `sqlcmd` se cierra sin devolver ningún valor.  
  
 Aquí se muestra una lista de formatos de EXIT:  
  
-   :EXIT  
  
 No ejecuta el lote y, después, sale de forma inmediata y no devuelve ningún valor.  
  
-   :EXIT( )  
  
 Ejecuta el lote y, a continuación, sale sin devolver ningún valor.  
  
-   :EXIT(query)  
  
 Ejecuta el lote que incluye la consulta y, a continuación, se cierra tras devolver el resultado de la consulta.  
  
 Si se usa RAISERROR en un script de `sqlcmd` y se genera el estado 127, `sqlcmd` se cerrará y devolverá un identificador de mensaje al cliente. Por ejemplo:  
  
 `RAISERROR(50001, 10, 127)`  
  
 Este error hará que el script de `sqlcmd` finalice y devuelva el identificador de mensaje 50001 al cliente.  
  
 Los valores devueltos -1 a -99 están reservados para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]; `sqlcmd` define los siguientes valores devueltos adicionales:  
  
|Valores devueltos|Descripción|  
|-------------------|-----------------|  
|-100|Error encontrado antes de seleccionar el valor devuelto.|  
|-101|No se encontró ninguna fila al seleccionar el valor devuelto.|  
|-102|Error de conversión al seleccionar el valor devuelto.|  
  
 **GO** [*count*]  
 GO marca tanto el final de un lote como la ejecución de cualquier instrucción de [!INCLUDE[tsql](../includes/tsql-md.md)] almacenada en caché. Cuando especifique un valor para *count*, las instrucciones almacenadas en caché se ejecutarán tantas veces como indique *count* , como un solo lote.  
  
 **Otros comandos**  
  **:r \<** _nombre_de_archivo_ **>**  
 Analiza adicional [!INCLUDE[tsql](../includes/tsql-md.md)] instrucciones y `sqlcmd` comandos desde el archivo especificado por **< *`filename`* >** en la caché de instrucciones.  
  
 Si el archivo contiene instrucciones [!INCLUDE[tsql](../includes/tsql-md.md)] que no van seguidas de **GO**, debe escribir **GO** en la línea que sigue a **:r**.  
  
> [!NOTE]  
>  **\<** _nombre de archivo_ **>** es de lectura en relación con el directorio de inicio en el que `sqlcmd` se ejecutó.  
  
 El archivo se leerá y se ejecutará después de que se encuentre un terminador de lote. Puede emitir varios comandos **:r** . El archivo puede incluir cualquier comando de `sqlcmd`. Eso incluye el terminador de lote **GO**.  
  
> [!NOTE]  
>  El recuento de líneas que se muestra en el modo interactivo aumentará en uno por cada comando **:r** que se encuentre. El comando **:r** aparecerá en la salida del comando de lista.  
  
 **:Serverlist**  
 Enumera los servidores configurados localmente y los nombres de los servidores que difunden en la red.  
  
 **:Connect** _server_name_[**\\**_instance_name_] [-l *timeout*] [-U *user_name* [-P *password*]]  
 Conecta con una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. También cierra la conexión actual.  
  
 Opciones de tiempo de espera:  
  
|||  
|-|-|  
|0|espera indefinidamente|  
|n>0|espera durante n segundos|  
  
 La variable de scripting SQLCMDSERVER reflejará la conexión activa actual.  
  
 Si no se especifica *timeout* , el valor de la variable SQLCMDLOGINTIMEOUT es el predeterminado.  
  
 Si solo se especifica *nombre_del_usuario* (como opción o como variable de entorno), se solicitará al usuario que especifique una contraseña. Esto no es así si se han establecido las variables de entorno SQLCMDUSER o SQLCMDPASSWORD. Si no se proporcionan opciones ni variables de entorno, se iniciará sesión en modo Autenticación de Windows. Por ejemplo, para conectar con una instancia, `instance1`, de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], `myserver`, mediante seguridad integrada, se necesitaría lo siguiente:  
  
 `:connect myserver\instance1`  
  
 Para conectar con la instancia predeterminada de `myserver` con variables de script, utilizaría lo siguiente:  
  
 `:setvar myusername test`  
  
 `:setvar myservername myserver`  
  
 `:connect $(myservername) $(myusername)`  
  
 [**:**] **!!**\< *command*>  
 Ejecuta comandos del sistema operativo. Para ejecutar un comando del sistema operativo, inicie una línea con dos signos de exclamación (**!!**) seguidos por el comando del sistema operativo. Por ejemplo:  
  
 `:!! Dir`  
  
> [!NOTE]  
>  El comando se ejecuta en el equipo en el que se ejecuta `sqlcmd`.  
  
 **:XML** [**ON** | **OFF**]  
 Para obtener más información, vea "Formato de salida XML", más adelante en este tema  
  
 **:Help**  
 Muestra los comandos de `sqlcmd` junto con una breve descripción de cada comando.  
  
### <a name="sqlcmd-file-names"></a>Nombres de archivo de sqlcmd  
 `sqlcmd` se pueden especificar archivos de entrada con el **-i** opción o el **: r** comando. Los archivos de salida se pueden especificar con la opción **-o** o con los comandos **:Error**, **:Out** y **:Perftrace** . A continuación se incluyen algunas directrices para trabajar con estos archivos:  
  
-   **: Error**, **: Out** y **: Perftrace** debe usar independiente **< *`filename`* >**. Si el mismo **< *`filename`* >** es usa, pueden mezclar las entradas de los comandos.  
  
-   Si `sqlcmd` llama a un archivo de entrada ubicado en un servidor remoto desde un equipo local y el archivo contiene una ruta de acceso de archivo del tipo :out c:\archivoDeSalida.txt. el archivo de salida se creará en el equipo local y no en el servidor remoto.  
  
-   Las rutas de acceso de archivo válidas se incluyen: C:\\**<*`filename`*>**, \\ \\< servidor\>\\< recursoCompartido$ >\\ **< *`filename`* >** y "carpeta C:\Some\\  **< *`file name`*>**". Si hay algún espacio en blanco en la ruta de acceso, use comillas.  
  
-   Cada nueva sesión de `sqlcmd` sobrescribirá los archivos existentes que tengan el mismo nombre.  
  
### <a name="informational-messages"></a>Mensajes informativos  
 `sqlcmd` imprime los mensajes informativos enviados por el servidor. En el siguiente ejemplo, tras ejecutar las instrucciones de [!INCLUDE[tsql](../includes/tsql-md.md)] , se imprime un mensaje informativo.  
  
 En el símbolo del sistema, escriba lo siguiente:  
  
 `sqlcmd`  
  
 `At the sqlcmd prompt type:`  
  
 `USE AdventureWorks2012;`  
  
 `GO`  
  
 Al presionar ENTRAR, se imprime el siguiente mensaje informativo: "Contexto de base de datos cambiado a 'AdventureWorks2012'".  
  
### <a name="output-format-from-transact-sql-queries"></a>Formato de salida de consultas de Transact-SQL  
 `sqlcmd` primero imprime un encabezado de columna que contiene los nombres de columna especificados en la lista de selección. Los nombres de columna se separan mediante el carácter SQLCMDCOLSEP. De forma predeterminada, es un espacio en blanco. Si el nombre de la columna es más corto que el ancho de la columna, la salida se rellena con espacios hasta la siguiente columna.  
  
 Esta línea irá seguida de una línea separadora, que es una serie de caracteres de guión. La siguiente salida muestra un ejemplo.  
  
 Inicie `sqlcmd`. En el símbolo del sistema de `sqlcmd`, escriba lo siguiente:  
  
 `USE AdventureWorks2012;`  
  
 `SELECT TOP (2) BusinessEntityID, FirstName, LastName`  
  
 `FROM Person.Person;`  
  
 `GO`  
  
 Cuando presione ENTRAR, se devolverá el siguiente conjunto de resultados.  
  
 `BusinessEntityID FirstName    LastName`  
  
 `---------------- ------------ ----------`  
  
 `285              Syed         Abbas`  
  
 `293              Catherine    Abel`  
  
 `(2 row(s) affected)`  
  
 Aunque la columna `BusinessEntityID` tiene solo 4 caracteres de ancho, se ha expandido para acomodar el nombre de columna más largo. De forma predeterminada, la salida finaliza a los 80 caracteres. Esto se puede cambiar mediante la opción **-w** o estableciendo la variable de scripting SQLCMDCOLWIDTH.  
  
### <a name="xml-output-format"></a>Formato de salida XML  
 La salida XML de una cláusula FOR XML se ofrece sin formato en un flujo continuo.  
  
 Cuando espere una salida XML, use el siguiente comando: `:XML ON`.  
  
> [!NOTE]  
>  `sqlcmd` devuelve mensajes de error en el formato habitual. Tenga en cuenta que los mensajes de error también salen en el flujo de texto XML en formato XML. Con `:XML ON`, `sqlcmd` no muestra mensajes informativos.  
  
 Para desactivar el modo XML, use el siguiente comando: `:XML OFF`.  
  
 El comando GO no debe aparecer antes de que se emita el comando XML OFF, ya que el comando XML OFF vuelve a cambiar `sqlcmd` a la salida orientada a filas.  
  
 Los datos XML (de flujo) y los datos del conjunto de filas no se pueden mezclar. Si el comando XML ON no se ha emitido antes de ejecutar una instrucción [!INCLUDE[tsql](../includes/tsql-md.md)] que genera flujos XML, la salida será confusa. Si se ha emitido el comando XML ON, no se pueden ejecutar instrucciones [!INCLUDE[tsql](../includes/tsql-md.md)] que den como resultado conjuntos de filas normales.  
  
> [!NOTE]  
>  El comando **:XML** no admite la instrucción SET STATISTICS XML.  
  
## <a name="sqlcmd-best-practices"></a>Prácticas recomendadas para sqlcmd  
 Use las siguientes prácticas para maximizar la seguridad y la eficacia.  
  
-   Use seguridad integrada.  
  
-   Use `-X` en los entornos automatizados.  
  
-   Proteja los archivos de entrada y salida mediante los permisos del sistema de archivos NTFS adecuados.  
  
-   Para aumentar el rendimiento, haga tanto como pueda en una sola sesión de `sqlcmd` en vez de emplear varias.  
  
-   Establezca valores de tiempo de espera para la ejecución de lotes y consultas superiores a los que prevea para la ejecución de cada lote o consulta.  
  
## <a name="see-also"></a>Vea también  
 [Iniciar la utilidad sqlcmd](../relational-databases/scripting/sqlcmd-start-the-utility.md)   
 [Ejecutar archivos de scripts Transact-SQL mediante sqlcmd](../relational-databases/scripting/sqlcmd-run-transact-sql-script-files.md)   
 [Usar la utilidad sqlcmd](../relational-databases/scripting/sqlcmd-use-the-utility.md)   
 [Usar sqlcmd con variables de script](../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md)   
 [Conectarse al motor de base de datos con sqlcmd](../relational-databases/scripting/sqlcmd-connect-to-the-database-engine.md)   
 [Modificar scripts SQLCMD con el Editor de consultas](../relational-databases/scripting/edit-sqlcmd-scripts-with-query-editor.md)   
 [Administrar pasos de trabajo](../ssms/agent/manage-job-steps.md)   
 [Crear un paso de trabajo CmdExec](../ssms/agent/create-a-cmdexec-job-step.md)  
  
  
