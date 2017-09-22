---
title: "Problemas comunes con la ejecución de scripts externos en SQL Server | Documentos de Microsoft"
ms.custom:
- SQL2016_New_Updated
ms.date: 08/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: 1
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: a6aeda8e785fcaabef253a8256b5f6f7a842a324
ms.openlocfilehash: be817ff6961e68227cdae8aff14049b55652099c
ms.contentlocale: es-es
ms.lasthandoff: 09/21/2017

---
# <a name="common-issues-with-external-script-execution-in-sql-server"></a>Problemas comunes con la ejecución de scripts externos en SQL Server

Este artículo contiene una lista de problemas conocidos y los problemas comunes al ejecutar código R o Python en SQL Server.

Antes de empezar, se recomienda que recopilar cierta información sobre el sistema. Para obtener información sobre cómo hacerlo, consulte [recopilación de datos para la solución de problemas de](data-collection-ml-troubleshooting-process.md).

Además, revise una lista de los problemas comunes que son específicas de la instalación inicial o la configuración: [el programa de instalación y preguntas más frecuentes sobre actualización](r/upgrade-and-installation-faq-sql-server-r-services.md).

**Se aplica a:** servicios de aprendizaje de automático de SQL Server 2016 R Services, SQL Server de 2017

## <a name="launchpad-issues"></a>Problemas de LaunchPad

El servicio de SQL Server de confianza Launchpad administra la ejecución de scripts externos y comunicación con R, Python u otros tiempos de ejecución externos. Varios problemas pueden evitar Launchpad desde el comienzo, incluidos los problemas de configuración o de cambios o falta de protocolos de red.

Como parte del proceso de solución de problemas, comience por responder a las siguientes preguntas:

- ¿Se Launchpad siempre no se ejecuta o se detuvo trabajar?
- ¿Qué cuenta de servicio Launchpad se ejecuta en?
- ¿Qué derechos de usuario tiene la cuenta de servicio Launchpad?

### <a name="determine-whether-launchpad-is-running"></a>Determinar si se está ejecutando Launchpad

1. Abra la **servicios** panel (Services.msc). O bien, desde la línea de comandos, escriba **SQLServerManager13.msc** o **SQLServerManager14.msc** para abrir [Administrador de configuración de SQL Server](https://docs.microsoft.com/sql/relational-databases/sql-server-configuration-manager).

2. Tome nota de la cuenta de servicio que se está ejecutando Launchpad. Cada instancia donde está habilitada la R o Python debe tener su propia instancia del servicio Launchpad. Por ejemplo, el servicio para una instancia con nombre podría ser algo parecido a _MSSQLLaunchpad$ InstanceName_.

3. Si el servicio está detenido, reinícielo. En el reinicio, si hay algún problema con la configuración, se publica un mensaje en el registro de eventos del sistema y se detiene el servicio de nuevo. Compruebe el registro de eventos del sistema para obtener más información acerca de por qué se detuvo el servicio.

4. Revise el contenido de RSetup.log y asegúrese de que no hay ningún error en el programa de instalación. Por ejemplo, el mensaje *salir con el código 0* indica un error del servicio al iniciar.

5. Para buscar otros errores, revise el contenido de rlauncher.log.

### <a name="check-the-launchpad-service-account"></a>Comprobación de la cuenta de servicio de Launchpad

La cuenta de servicio predeterminado podría ser "servicio NT\$SQL2016" o "servicio NT\$SQL2017". La parte final puede variar, según el nombre de instancia SQL.

El servicio Launchpad (Launchpad.exe) se ejecuta con una cuenta de servicio con privilegios bajos. Sin embargo, para iniciar R y Python y comunicarse con la instancia de base de datos, la cuenta de servicio Launchpad requiere los siguientes derechos de usuario:

- Iniciar sesión como servicio (SeServiceLogonRight)
- Reemplazar un token de nivel de proceso (SeAssignPrimaryTokenPrivilege)
- Omitir la comprobación transversal (SeChangeNotifyPrivilege)
- Ajustar las cuotas de memoria para un proceso (SeIncreaseQuotaSizePrivilege)

Para obtener información acerca de estos derechos de usuario, vea la sección "derechos y privilegios de Windows" en [Windows configurar cuentas de servicio y permisos](/sql-docs/docs/database-engine/configure-windows/configure-windows-service-accounts-and-permissions).

> [!TIP]
> Si está familiarizado con el uso de la herramienta de la plataforma de diagnóstico de soporte técnico (SDP) para diagnósticos de SQL Server, puede usar SDP para revisar el archivo de salida con el nombre MachineName_UserRights.txt.

### <a name="review-launchpad-requirements"></a>Revisar los requisitos de Launchpad

Cualquiera de varios problemas puede impedir que Launchpad se inicie. Puede iniciar y detener el servicio Launchpad o bloqueo, o el servicio se detiene debido a un tiempo de espera de conexión. En estos casos, el sistema normalmente ha cambiado o configura de modo que no se puede ejecutar Launchpad.

#### <a name="determine-whether-8dot3-notation-is-enabled"></a>Determinar si se habilita la notación de tiene el formato 8.3

Por compatibilidad con R, SQL Server 2016 R Services (In-Database) requiere la unidad donde está instalada la característica para admitir la creación de nombres cortos de archivo mediante *tiene el formato 8.3 notación*. Un nombre de 8.3 archivo también se denomina un *nombre corto de archivo*, y se utiliza por compatibilidad con versiones anteriores de Microsoft Windows o como una alternativa a los nombres de archivo largos.

Si el volumen donde esté instalando R no admite nombres cortos de archivo, los procesos que se ejecuten código R en SQL Server no pueda encontrar el archivo ejecutable correcto y no se iniciará el Launchpad.

Como alternativa, puede habilitar la notación tiene el formato 8.3 en el volumen donde está instalado SQL Server y está instalado R Services. Después, debe proporcionar el nombre corto del directorio de trabajo en el archivo de configuración de R Services.

1. Para habilitar la notación tiene el formato 8.3, ejecute la utilidad fsutil con la *8dot3name* argumento tal como se describe aquí: [8dot3name fsutil](https://technet.microsoft.com/library/ff621566(v=ws.11).aspx).

2. Una vez habilitada la notación tiene el formato 8.3, abra el archivo RLauncher.config y tenga en cuenta la propiedad de `WORKING_DIRECTORY`. Para obtener información acerca de cómo encontrar este archivo, consulte [recopilación de datos para la solución de problemas de aprendizaje automático](data-collection-ml-troubleshooting-process.md).

3. Use la utilidad fsutil con la *archivo* argumento para especificar una ruta de acceso de archivo corto para la carpeta que se especifica en WORKING_DIRECTORY.

4. Edite el archivo de configuración para especificar el mismo directorio de trabajo que especificó en la propiedad WORKING_DIRECTORY. Como alternativa, puede especificar un directorio de trabajo diferente y elija una ruta de acceso existente que ya es compatible con la notación de tiene el formato 8.3.

> [!NOTE] 
> Esta restricción se ha quitado en las versiones posteriores. Si experimenta este problema, instale una de las siguientes acciones:
> * SP1 de SQL Server 2016 y CU1: [la actualización acumulativa 1 para SQL Server](https://support.microsoft.com/help/3208177/cumulative-update-1-for-sql-server-2016-sp1).
> * SQL Server 2016 RTM, Service Pack 3 y esto [revisión](https://support.microsoft.com/help/3210110/on-demand-hotfix-update-package-for-sql-server-2016-cu3), que está disponible a petición.

#### <a name="the-user-group-for-launchpad-cannot-log-on-locally"></a>El grupo de usuarios para Launchpad no puede iniciar sesión localmente

Durante la instalación de servicios de aprendizaje automático, SQL Server crea el grupo de usuarios de Windows **SQLRUserGroup** y, a continuación, se aprovisiona con todos los derechos necesarios para Launchpad para conectarse a SQL Server y ejecutar trabajos de script externo. Si este grupo de usuarios está habilitada, también se usa para ejecutar scripts de Python.

Sin embargo, en organizaciones donde se aplican las directivas de seguridad más restrictivas, podrían haberse eliminados manualmente los derechos necesarios para este grupo o pueden revocar automáticamente por la directiva. Si se han quitado los derechos, Launchpad ya no puede conectarse a SQL Server y SQL Server no se puede llamar al runtime externo.

Para corregir el problema, asegúrese de que el grupo **SQLRUserGroup** tiene el derecho de sistema **Permitir el inicio de sesión local**.

Para obtener más información, vea [Configurar los permisos y las cuentas de servicio de Windows](https://msdn.microsoft.com/library/ms143504.aspx#Windows).

#### <a name="improper-setup-leading-to-mismatched-dlls"></a>Programa de instalación incorrecto dan lugar a archivos DLL que no coinciden

Si instala el motor de base de datos con otras características, el servidor, de revisión y, a continuación, agregar más adelante la característica de aprendizaje automático mediante el medio original, puede instalarse una versión incorrecta de los componentes de aprendizaje automático. Cuando se Launchpad detecta un error de coincidencia de versión, se cierra y crea un archivo de volcado de memoria.

Para evitar este problema, asegúrese de instalar las nuevas características en el mismo nivel de revisión como instancia del servidor.

**La dirección incorrecta para actualizar**:

1. Instalar a SQL Server 2016 sin servicios de R.
2. Actualizar SQL Server 2016 la actualización acumulativa 2.
3. Instalar R Services (In-Database) mediante el uso de los medios RTM.

**La manera correcta para actualizar**:

1. Instalar a SQL Server 2016 sin servicios de R.
2. Actualizar SQL Server 2016 en el nivel de revisión deseado. Por ejemplo, instale Service Pack 1 y, a continuación, la actualización acumulativa 2.
3. Para agregar la característica en el nivel de revisión correcto, vuelva a ejecutar el programa de instalación de SP1 y CU2 y, a continuación, elija R Services (In-Database). 

#### <a name="check-to-see-whether-a-user-has-rights-to-run-external-scripts"></a>Compruebe si un usuario tiene derechos para ejecutar scripts externos

Aunque se Launchpad está configurado correctamente, devuelve un error si el usuario no tiene permiso para ejecutar scripts de R o Python.

Si ha instalado a SQL Server como un administrador de base de datos o es un propietario de base de datos, este permiso se concede automáticamente. Sin embargo, otros usuarios suelen tener más permisos limitados. Si intenta ejecutar un script de R, producirá un error de Launchpad.

Para corregir el problema, en SQL Server Management Studio, un administrador de seguridad puede modificar el inicio de sesión SQL o la cuenta de usuario de Windows mediante la ejecución de la secuencia de comandos siguiente:

```SQL
GRANT EXECUTE ANY EXTERNAL SCRIPT
```

### <a name="common-launchpad-errors"></a>Errores comunes de Launchpad

Esta sección enumeran los mensajes de error más comunes que devuelve Launchpad.

#### <a name="error-unable-to-launch-runtime-for-r-script"></a>Error: *no se puede iniciar en tiempo de ejecución de script de R*

Si no se puede iniciar sesión en el grupo de Windows para los usuarios de R (que también se utilizan para Python) a la instancia que se ejecuta los servicios de R, pueden aparecer los errores siguientes:

- Errores generados al intentar ejecutar scripts R:

    * *No se puede iniciar el tiempo de ejecución para el script 'R'. Compruebe la configuración del tiempo de ejecución 'R'.*

    * *An external script error occurred. Unable to launch the runtime.* (Error en el script externo. No se puede iniciar el tiempo de ejecución).

- Los errores generados por el [!INCLUDE[rsql_launchpad](../includes/rsql-launchpad-md.md)] servicio:

    * *Failed to initialize the launcher RLauncher.dll*

    * *No launcher dlls were registered!*

    * *Registros de seguridad indican que la cuenta de servicio de NT no pudo iniciar sesión*

Para obtener información sobre cómo conceder los permisos necesarios de este grupo de usuarios, consulte [configurar SQL Server R Services](r/set-up-sql-server-r-services-in-database.md).

> [!NOTE]
> Esta limitación no se aplica si usa inicios de sesión de SQL para ejecutar scripts de R desde una estación de trabajo remota.

#### <a name="error-logon-failure-the-user-has-not-been-granted-the-requested-logon-type"></a>Error: *error de inicio de sesión: el usuario no tiene el tipo de inicio de sesión solicitado*

De forma predeterminada, [!INCLUDE[rsql_launchpad_md](../includes/rsql-launchpad-md.md)] utiliza la cuenta siguiente en el inicio: `NT Service\MSSQLLaunchpad`. La cuenta está configurada por [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] el programa de instalación tenga todos los permisos necesarios.

Si asigna una cuenta diferente a Launchpad o la derecha se quita una directiva en el equipo de SQL Server, la cuenta no tenga los permisos necesarios y puede que vea este error:

>*ERROR_LOGON_TYPE_NOT_GRANTED 1385 (0x569) Error de inicio de sesión: el usuario no tiene permisos para el tipo de inicio de sesión solicitado en el equipo.*

Para conceder los permisos necesarios a la nueva cuenta de servicio, use la aplicación de directiva de seguridad Local y actualizar los permisos en la cuenta para incluir los siguientes permisos:

+ Ajustar las cuotas de memoria de un proceso (SeIncreaseQuotaPrivilege)
+ Omitir la comprobación transversal (SeChangeNotifyPrivilege)
+ Iniciar sesión como servicio (SeServiceLogonRight)
+ Reemplazar un token de nivel de proceso (SeAssignPrimaryTokenPrivilege)

#### <a name="error-unable-to-communicate-with-the-launchpad-service"></a>Error: *no se puede comunicar con el servicio Launchpad*

Si ha instalado y, a continuación, habilita el aprendizaje automático, pero este error aparece cuando intenta ejecutar un script de R o Python, puede haberse detenido el servicio Launchpad para la instancia de ejecución.

1. Desde un símbolo del sistema de Windows, abra el Administrador de configuración de SQL Server. Para obtener más información, vea [SQL Server Configuration Manager](https://docs.microsoft.com/sql/relational-databases/sql-server-configuration-manager).

2. Haga clic en Launchpad de SQL Server para la instancia y, a continuación, seleccione **propiedades**.

3. Seleccione el **servicio** ficha y, a continuación, compruebe que el servicio se está ejecutando. Si no se está ejecutando, cambie la **iniciar modo** a **automática**y, a continuación, seleccione **aplicar**.

4. Reiniciar el servicio normalmente corrige el problema para que puedan ejecutarse los scripts de aprendizaje de máquina. Si el reinicio no soluciona el problema, tenga en cuenta la ruta de acceso y los argumentos en la **ruta de acceso binaria** propiedad y haga lo siguiente:

    a. Revise el archivo .config del iniciador y asegúrese de que el directorio de trabajo es válido.

    b. Asegúrese de que el grupo de Windows que se usa por Launchpad puede conectarse a la instancia de SQL Server, como se describe en el [sección anterior](#bkmk_LaunchpadTS).

    c. Si cambia cualquiera de las propiedades del servicio, reinicie el servicio Launchpad.

#### <a name="error-fatal-error-creation-of-tmpfile-failed"></a>Error: *no se pudo crear error irrecuperable tmpFile*

En este escenario, se han instalado correctamente características de aprendizaje de máquina y Launchpad se ejecuta. Intenta ejecutar un código de R o Python sencillo, pero no se Launchpad con un error similar al siguiente: 

>*No se puede comunicar con el tiempo de ejecución de script de R. Compruebe los requisitos de tiempo de ejecución de R.*

Al mismo tiempo, el tiempo de ejecución de script externo escribe el mensaje siguiente como parte del mensaje STDERR: 

>*Error irrecuperable: creación de tmpfile error.*

Este error indica que la cuenta que está intentando usar Launchpad no tiene permiso para iniciar sesión en la base de datos. Esta situación puede ocurrir cuando se implementan directivas de seguridad estricta. Para determinar si este es el caso, revise los registros de SQL Server y compruebe para ver si la cuenta de MSSQLSERVER01 se denegó al inicio de sesión. Se proporciona la misma información en los registros que son específicos de R\_servicios o PYTHON\_servicios. Busque ExtLaunchError.log.

De forma predeterminada, 20 cuentas configuradas y asociadas con el proceso de Launchpad.exe, con los nombres MSSQLSERVER01 a través de MSSQLSERVER20. Si realiza un uso intensivo de R o Python, puede aumentar el número de cuentas.

Para resolver el problema, asegúrese de que el grupo tiene *permitir el registro local* permisos a la instancia local donde se han instalado y habilitado características de aprendizaje de la máquina. En algunos entornos, este nivel de permiso puede requerir una excepción de GPO desde el Administrador de red.

## <a name="r-script-issues"></a>Problemas de script de R

Esta sección contiene algunos problemas comunes que son específicas para la ejecución de script de R y errores de script de R. La lista no es exhaustiva, porque hay muchos paquetes de R y errores pueden diferir entre las versiones del mismo paquete de R. Se recomienda registrar errores de script de R en el [foro de Microsoft R Server](https://social.msdn.microsoft.com/Forums/home?forum=MicrosoftR), que es compatible con todos ellos relacionados con productos: R Services (In-Database), servicios de aprendizaje de máquina con Python, Microsoft R Client y Microsoft R Server.

### <a name="multiple-r-instances-on-the-same-computer"></a>Varias instancias de R en el mismo equipo

Es fácil para instalar varias distribuciones de R en el mismo equipo, o para instalar varias copias del mismo paquete de R en distintas versiones. Por ejemplo, si instala el servidor de aprendizaje de máquina (independiente) y servicios de aprendizaje de máquina (In-Database), los instaladores crear versiones independientes de las bibliotecas de R. 

La duplicación puede resultar confusa cuando intenta ejecutar un script desde una línea de comandos y no está seguro de qué bibliotecas que está usando. También puede ser confuso si instala un paquete en la biblioteca incorrecta y no se puede encontrar el paquete cuando intente ejecutarlo desde SQL Server.

+ Evite el uso directo de las bibliotecas de R y herramientas que se instalan para el uso de la instancia de SQL Server, excepto en casos limitados, como solución de problemas o instalación de nuevos paquetes. 
+ Si tiene que utilizar una herramienta de línea de comandos de R, puede instalar [Microsoft R cliente](https://docs.microsoft.com/r-server/r-client/what-is-microsoft-r-client).
+ SQL Server proporciona administración de bases de datos de paquetes de R. Se trata de la manera más fácil de crear las bibliotecas de paquete de R que pueden compartirse entre usuarios. Para obtener más información, consulte [instalar y administrar paquetes de R](r/installing-and-managing-r-packages.md).

### <a name="avoid-clearing-the-workspace-while-youre-running-r-in-a-sql-compute-context"></a>Evitar borrar el área de trabajo mientras se ejecuta R en un contexto de proceso SQL

Aunque el área de trabajo de acción de borrar es común cuando se trabaja en la consola de R, puede tener consecuencias no deseadas en una instancia de SQL contexto de proceso.

`revoScriptConnection`es un objeto en el área de trabajo de R que contiene información sobre una sesión de R que se llama desde SQL Server. Sin embargo, si el código de R incluye un comando para borrar el área de trabajo (como `rm(list=ls())`), se desactiva toda la información acerca de la sesión y otros objetos en el área de trabajo de R.

Como alternativa, evite indiscriminado borrado de las variables y otros objetos mientras se ejecuta R en SQL Server. Puede eliminar variables específicas mediante la **quitar** función:

```R
remove('name1', 'name2', ...)
```

Si hay varias variables para eliminar, se recomienda que guarde los nombres de variables temporales a una lista y, a continuación, realizar las colecciones de elementos no utilizados periódicamente en la lista.

### <a name="implied-authentication-for-remote-execution-via-odbc"></a>Autenticación implícita para la ejecución remota a través de ODBC

Si se conecta a la [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] comandos del equipo para ejecutar R mediante el uso de la **RevoScaleR** funciones, puede obtener un error cuando se usa llamadas ODBC que escriben datos en el servidor. Este error se produce cuando se utiliza la autenticación de Windows.

La razón es que las cuentas de trabajo que se crean para R Services no tiene permiso para conectarse al servidor. Por lo tanto, no se puede ejecutar llamadas ODBC en su nombre. El problema no se produce con los inicios de sesión SQL porque, con los inicios de sesión SQL, las credenciales se pasan explícitamente desde el cliente de R a la instancia de SQL Server y, a continuación, en ODBC. Sin embargo, también es menos seguro que usar la autenticación de Windows utilizando los inicios de sesión SQL.

Para habilitar las credenciales de Windows que se pasan de forma segura desde un script que ha iniciado de forma remota, SQL Server debe emular las credenciales. Este proceso se denomina _autenticación implícita_. Para solucionar este problema, las cuentas de trabajo que ejecutan scripts de R o Python en el equipo de SQL Server deben tener los permisos correctos.

1. Abra [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] en la instancia donde desea ejecutar código R como administrador.

2. Ejecute el script siguiente. Asegúrese de editar el nombre del grupo de usuario, si cambia el valor predeterminado y los nombres de equipo y la instancia.

    ```SQL
    USE [master]
    GO
    
    CREATE LOGIN [computername\\SQLRUserGroup] FROM WINDOWS WITH
    DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[language]
    GO
    ```

### <a name="the-r-script-works-outside-of-t-sql-but-not-in-a-stored-procedure"></a>El script de R funciona fuera de T-SQL, pero no en un procedimiento almacenado

Antes de ajustar el código de R en un procedimiento almacenado, es una buena idea para ejecutar el código de R en un IDE externo o en una de las herramientas de R como RTerm o RGui. Mediante estos métodos, puede probar y depurar el código mediante el uso de los mensajes de error detallados que se devuelven mediante R.

Sin embargo, a veces código que funciona perfectamente en un IDE o utilidad externos podría no ejecutarse en un procedimiento almacenado o en un servidor SQL Server el contexto de proceso. Si esto ocurre, hay una variedad de problemas para buscar antes de que se puede suponer que el paquete no funciona en SQL Server.

1. Compruebe si se está ejecutando Launchpad.

2. Revise los mensajes para ver si los datos de entrada o datos de salida contienen columnas con tipos de datos incompatibles o no es compatible. Por ejemplo, las consultas en una base de datos SQL a menudo devuelven GUID o ROWGUID, ambos de los cuales no son compatibles. Para obtener más información, consulte [tipos de datos y las bibliotecas de R](r/r-libraries-and-data-types.md).

3. Revise las páginas de ayuda para las funciones de R individuales determinar si se admiten todos los parámetros para el contexto de proceso de SQL Server. Para obtener ayuda de ScaleR, use los comandos de ayuda en línea R o vea [referencia de paquete](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler).

### <a name="you-get-different-results-from-the-same-script-when-running-in-sql-compared-to-other-environments"></a>Obtener resultados diferentes de la misma secuencia de comandos cuando se ejecuta en SQL en comparación con otros entornos

Scripts de R pueden devolver valores diferentes en un contexto de SQL Server, por varias razones:

- Conversión de tipos implícita se realiza automáticamente en algunos tipos de datos cuando los datos se pasan entre SQL Server y R. Para obtener más información, consulte [tipos de datos y las bibliotecas de R](r/r-libraries-and-data-types.md).

- Determinar si el valor de bits es un factor. Por ejemplo, a menudo hay diferencias en los resultados de las operaciones matemáticas para las bibliotecas de punto flotante de 32 bits y 64 bits.

- Determinar si los valores NaN se hayan producido en cualquier operación. Esto puede invalidar los resultados.

- Pequeñas diferencias pueden ampliarse al tomar una recíproco de un número casi cero.

- Errores de redondeo acumulados pueden producir, por ejemplo, los valores que son inferiores a cero en lugar de cero.

### <a name="error-not-enough-quota-to-process-this-command"></a>Error: *no hay cuota suficiente para procesar este comando*

Este error puede deberse a una de las siguientes operaciones:

- LaunchPad puede tener usuarios externos insuficiente para ejecutar la consulta externa. Por ejemplo, si tiene más de 20 consultas externas al mismo tiempo, y solo hay 20 usuarios de forma predeterminada, una o más consultas podrían producir errores.

- Hay suficiente memoria disponible para procesar la tarea de R. Este error se produce con mayor frecuencia en un entorno de forma predeterminada, donde SQL Server puede usar hasta un 70 por ciento de los recursos del equipo. Para obtener información sobre cómo modificar la configuración del servidor para admitir el mayor uso de recursos mediante R, consulte [el código de R en marcha](r/operationalizing-your-r-code.md).

### <a name="error-cant-find-package"></a>Error: *no se encuentra el paquete*

Si ejecuta código de R en SQL Server y recibe este mensaje, pero no obtuvo el mensaje al ejecutar el mismo código fuera de SQL Server, significa que el paquete no se instaló en la ubicación de biblioteca predeterminado utilizada por SQL Server.

Este error puede producirse de muchas formas:

- Instala un nuevo paquete en el servidor, pero se denegó el acceso, por lo que R instala el paquete a una biblioteca de usuario.

- Instala R Services y, a continuación, instaló otra herramienta de R o conjunto de bibliotecas, incluidos Microsoft R Server (independiente), Microsoft R Client, RStudio y así sucesivamente.

Para determinar la ubicación de la biblioteca de paquete de R que se usa por la instancia, abra SQL Server Management Studio (o cualquier otra herramienta de consulta de base de datos), conéctese a la instancia y, a continuación, ejecute el siguiente procedimiento almacenado:

```SQL
EXEC sp_execute_external_script @language = N'R',  
@script = N' print(normalizePath(R.home())); print(.libPaths());'; 
```

#### <a name="sample-results"></a>Ejemplo de resultados

*Mensaje(s) STDOUT del script externo:*

*[1] "C:\\archivos de programa\\de Microsoft SQL Server\\MSSQL13. SQL2016\\R_SERVICES "*

*[1] "C:/programa archivos/Microsoft SQL Server/MSSQL13. SQL2016/R_SERVICES/biblioteca"*

Para resolver el problema, debe volver a instalar el paquete a la biblioteca de la instancia de SQL Server.

>[!NOTE]
>Si ha actualizado una instancia de SQL Server 2016 para usar la versión más reciente de Microsoft R, la ubicación predeterminada de la biblioteca es diferente. Para obtener más información, consulte [SqlBindR de uso para actualizar una instancia de servicios de R](r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

## <a name="next-steps"></a>Pasos siguientes

[Solución de problemas y problemas conocidos de aprendizaje automático](machine-learning-troubleshooting-faq.md)

[Recopilación de datos para la solución de problemas de aprendizaje automático](data-collection-ml-troubleshooting-process.md)

[Preguntas más frecuentes sobre actualización e instalación](r/upgrade-and-installation-faq-sql-server-r-services.md)

[Solucionar problemas de conexiones de motor de base de datos](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)

