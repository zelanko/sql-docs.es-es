---
title: Solución de problemas con el servicio Launchpad
description: En este artículo se proporcionan instrucciones para solucionar problemas que impiden que se inicie el servicio SQL Server Trusted Launchpad, incluidos los cambios o problemas de configuración, o la falta de protocolos de red.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 07/30/2019
ms.topic: troubleshooting
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15'
ms.openlocfilehash: b57fdb3abd3482d6a395e1e6690f2e628a2a3e9e
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97470686"
---
# <a name="troubleshoot-issues-with-launchpad-service-and-external-script-execution-in-sql-server"></a>Solución de problemas con el servicio Launchpad y la ejecución de scripts externos en SQL Server
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

En este artículo se proporcionan instrucciones para solucionar problemas relacionados con el servicio SQL Server Trusted Launchpad. El servicio Launchpad admite la ejecución de scripts externos para R y Python. Hay varios problemas que pueden impedir que Launchpad se inicie, incluidos los cambios o problemas de configuración, o la falta de protocolos de red.  

## <a name="determine-whether-launchpad-is-running"></a>Determinación de si Launchpad se está ejecutando

1. Abra el panel **Servicios** (Services.msc). O bien, desde la línea de comandos, escriba **SQLServerManager13.msc** o **SQLServerManager14.msc** para abrir el [Administrador de configuración de SQL Server](../../relational-databases/sql-server-configuration-manager.md).

2. Tome nota de la cuenta de servicio en la que se ejecuta Launchpad. Cada instancia en la que R o Python estén habilitados debe tener su propia instancia del servicio Launchpad. Por ejemplo, el servicio de una instancia con nombre podría ser similar a _MSSQLLaunchpad$NombreInstancia_.

3. Si el servicio está detenido, reinícielo. Al reiniciarlo, si hay algún problema con la configuración, se publica un mensaje en el registro de eventos del sistema y el servicio se vuelve a detener. Compruebe el registro de eventos del sistema para obtener detalles sobre por qué se ha detenido el servicio.

4. Revise el contenido de RSetup.log y asegúrese de que no haya ningún error en la configuración. Por ejemplo, el mensaje *Saliendo con el código 0* indica un error en el inicio del servicio.

5. Para buscar otros errores, revise el contenido de rlauncher.log.

## <a name="check-the-launchpad-service-account"></a>Comprobación de la cuenta del servicio Launchpad

La cuenta de servicio predeterminada podría ser "NT Service\$SQL2016" o "NT Service\$SQL2017". La última parte puede variar en función del nombre de la instancia de SQL.

El servicio Launchpad (Launchpad.exe) se ejecuta mediante una cuenta de servicio con pocos privilegios. En cambio, para iniciar R y Python y comunicarse con la instancia de base de datos, la cuenta del servicio Launchpad requiere los siguientes derechos de usuario:

- Iniciar sesión como servicio (SeServiceLogonRight)
- Reemplazar un token de nivel de proceso (SeAssignPrimaryTokenPrivilege)
- Omitir la comprobación transversal (SeChangeNotifyPrivilege)
- Ajuste de las cuotas de la memoria para un proceso (SeIncreaseQuotaSizePrivilege)

Para más información sobre estos derechos de usuario, vea la sección "Derechos y privilegios de Windows" en [Configurar los permisos y las cuentas de servicio de Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).

> [!TIP]
> Si está familiarizado con el uso de la herramienta Support Diagnostics Platform (SDP) para llevar a cabo diagnósticos de SQL Server, puede usar SDP para revisar el archivo de salida denominado MachineName_UserRights.txt.

## <a name="user-group-for-launchpad-cannot-log-on-locally"></a>El grupo de usuarios de Launchpad no puede iniciar sesión localmente

Durante la configuración de Machine Learning Services, SQL Server crea el grupo de usuarios de Windows **SQLRUserGroup** y después lo aprovisiona con todos los derechos necesarios para que Launchpad se conecte a SQL Server y ejecute trabajos de scripts externos. Si este grupo de usuarios está habilitado, también se usa para ejecutar scripts de Python.

Pero en las organizaciones en las que se aplican directivas de seguridad más restrictivas, es posible que se hayan quitado manualmente los derechos necesarios para este grupo o que la directiva los revoque automáticamente. Si se han quitado los derechos, Launchpad ya no podrá conectarse a SQL Server y SQL Server no podrá llamar al entorno de ejecución externo.

Para corregir el problema, asegúrese de que el grupo **SQLRUserGroup** tiene el derecho de sistema **Permitir el inicio de sesión local**.

Para obtener más información, consulte [Configurar los permisos y las cuentas de servicio de Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).

## <a name="permissions-to-run-external-scripts"></a>Permisos para ejecutar scripts externos

Incluso si Launchpad está configurado correctamente, devuelve un error si el usuario no tiene permiso para ejecutar scripts de R o Python.

Si ha instalado SQL Server como administrador de base de datos o si la base de datos le pertenece, se le concederá automáticamente este permiso. En cambio, otros usuarios suelen tener permisos más limitados. Si intentan ejecutar un script de R, recibirán un error de Launchpad.

Para corregir el problema, en SQL Server Management Studio, un administrador de seguridad puede modificar el inicio de sesión de SQL o la cuenta de usuario de Windows al ejecutar el siguiente script:

```sql
GRANT EXECUTE ANY EXTERNAL SCRIPT TO <username>
```

Para más información, vea [GRANT (Transact-SQL)](../../t-sql/statements/grant-transact-sql.md).

## <a name="common-launchpad-errors"></a>Errores comunes de Launchpad

En esta sección se enumeran los mensajes de error más comunes que devuelve Launchpad.

::: moniker range=">=sql-server-2016"
## <a name="unable-to-launch-runtime-for-r-script"></a>"No se puede iniciar el tiempo de ejecución para el script de R"

Si el grupo de Windows de usuarios de R (también usado para Python) no puede iniciar sesión en la instancia que ejecuta R Services, podrían aparecer los siguientes errores:

- Errores generados al intentar ejecutar scripts de R:

    * *No se puede iniciar el tiempo de ejecución para el script 'R'. Compruebe la configuración del tiempo de ejecución 'R'.*

    * *An external script error occurred. Unable to launch the runtime.* (Error en el script externo. No se puede iniciar el tiempo de ejecución).

- Errores generados por el servicio [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]:

    * *Failed to initialize the launcher RLauncher.dll*

    * *No launcher dlls were registered!*

    * *Security logs indicate that the account NT SERVICE was unable to log on* (Los registros de seguridad indican que la cuenta NT SERVICE no pudo iniciar sesión)

Para más información sobre cómo asignar los permisos necesarios a este grupo de usuarios, vea [Instalación de SQL Server R Services](../install/sql-r-services-windows-install.md).

> [!NOTE]
> Esta limitación no se aplica si usa inicios de sesión de SQL para ejecutar scripts de R desde una estación de trabajo remota.
::: moniker-end

## <a name="logon-failure-the-user-has-not-been-granted-the-requested-logon-type"></a>"Error de inicio de sesión: el usuario no tiene permisos para el tipo de inicio de sesión solicitado"

De forma predeterminada, [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] usa la siguiente cuenta durante el inicio: `NT Service\MSSQLLaunchpad`. El programa de configuración de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] ha configurado la cuenta para que tenga todos los permisos necesarios.

Si asigna otra cuenta a Launchpad o si una directiva quita el derecho en el equipo de SQL Server, es posible que la cuenta no tenga los permisos necesarios y que vea este error:

>*ERROR_LOGON_TYPE_NOT_GRANTED 1385 (0x569) Error de inicio de sesión: el usuario no tiene permisos para el tipo de inicio de sesión solicitado en el equipo.*

Para conceder los permisos necesarios a la nueva cuenta de servicio, use la aplicación de directiva de seguridad local y actualice los permisos de la cuenta para que incluya los siguientes:

+ Ajustar las cuotas de memoria de un proceso (SeIncreaseQuotaPrivilege)
+ Omitir la comprobación transversal (SeChangeNotifyPrivilege)
+ Iniciar sesión como servicio (SeServiceLogonRight)
+ Reemplazar un token de nivel de proceso (SeAssignPrimaryTokenPrivilege)

## <a name="unable-to-communicate-with-the-launchpad-service"></a>"Unable to communicate with the Launchpad service" (No se puede establecer la comunicación con el servicio Launchpad)

Si ha instalado y habilitado el aprendizaje automático, pero recibe este error al intentar ejecutar un script de R o Python, es posible que el servicio Launchpad de la instancia haya dejado de ejecutarse.

1. Desde un símbolo del sistema de Windows, abra el Administrador de configuración de SQL Server. Para obtener más información, vea [SQL Server Configuration Manager](../../relational-databases/sql-server-configuration-manager.md).

2. Haga clic con el botón derecho en la instancia de SQL Server Launchpad y, después, seleccione **Propiedades**.

3. Seleccione la pestaña **Servicio** y compruebe que se está ejecutando. Si no es así, cambie **Modo de inicio** a **Automático** y luego seleccione **Aplicar**.

4. Al reiniciar el servicio se suele corregir el problema para que se puedan ejecutar los scripts de aprendizaje automático. Si el reinicio no soluciona el problema, anote la ruta de acceso y los argumentos de la propiedad **Ruta de acceso binaria** y haga lo siguiente:

    a. Revise el archivo .config del iniciador y asegúrese de que el directorio de trabajo es válido.

    b. Asegúrese de que el grupo de Windows que usa Launchpad puede conectarse a la instancia de SQL Server.

    c. Si cambia alguna de las propiedades del servicio, reinicie el servicio Launchpad.

## <a name="fatal-error-creation-of-tmpfile-failed"></a>"Fatal error creation of tmpFile failed" (Error irrecuperable: no se pudo crear tmpFile)

En este escenario, ha instalado correctamente las características de aprendizaje automático y Launchpad se está ejecutando. Intenta ejecutar algunos códigos sencillos de R o Python, pero Launchpad produce un error similar al siguiente: 

>*No se puede comunicar con el tiempo de ejecución para el script "R". Compruebe los requisitos del tiempo de ejecución "R".*

A la vez, el tiempo de ejecución del script externo escribe el siguiente mensaje como parte del mensaje de STDERR: 

>*Fatal error: creation of tmpfile failed.* (Error irrecuperable: no se pudo crear tmpfile).

Este error indica que la cuenta que Launchpad intenta usar no tiene permiso para iniciar sesión en la base de datos. Esta situación puede producirse si se implementan directivas de seguridad estrictas. Para determinar si este es el caso, revise los registros de SQL Server y compruebe si se ha denegado la cuenta MSSQLSERVER01 durante el inicio de sesión. En los registros que son específicos de R\_SERVICES o PYTHON\_SERVICES se proporciona la misma información. Busque ExtLaunchError.log.

De forma predeterminada, se configuran 20 cuentas que se asocian al proceso Launchpad.exe, con los nombres MSSQLSERVER01 a MSSQLSERVER20. Si usa mucho R o Python, puede aumentar el número de cuentas.

Para resolver el problema, asegúrese de que el grupo tiene el permiso *Permitir el inicio de sesión local* en la instancia local en la que se han instalado y habilitado las características de aprendizaje automático. En algunos entornos, este nivel de permiso puede necesitar una excepción de GPO del administrador de red.

## <a name="not-enough-quota-to-process-this-command"></a>"Not enough quota to process this command" (Cuota insuficiente para procesar este comando)

Este error puede tener varios significados:

- Launchpad podría no tener suficientes usuarios externos para ejecutar la consulta externa. Por ejemplo, si está ejecutando más de 20 consultas externas simultáneamente y solo hay 20 usuarios predeterminados, puede producirse un error en una o varias consultas.

- No hay memoria suficiente disponible para procesar la tarea de R. Este error se produce con mayor frecuencia en un entorno predeterminado, donde SQL Server podría estar usando hasta el 70 % de los recursos del equipo. Para más información sobre cómo modificar la configuración del servidor para que R use más recursos, vea [Operacionalización del código de R](../r/operationalizing-your-r-code.md).

## <a name="cant-find-package"></a>"Can't find package" (No se encuentra el paquete)

Si ejecuta código de R en SQL Server y recibe este mensaje, pero no ha recibido el mensaje al ejecutar el mismo código fuera de SQL Server, esto indica que el paquete no se ha instalado en la ubicación de la biblioteca predeterminada que usa SQL Server.

Este error puede producirse de varias maneras:

- Ha instalado un nuevo paquete en el servidor, pero se ha denegado el acceso, por lo que R ha instalado el paquete en una biblioteca de usuario.

- Ha instalado R Services y después ha instalado otra herramienta de R u otro conjunto de bibliotecas, como Microsoft R Server (independiente), Microsoft R Client, RStudio, etc.

Para determinar la ubicación de la biblioteca de paquetes de R que usa la instancia, abra SQL Server Management Studio (o cualquier otra herramienta de consulta de base de datos), conéctese a la instancia y luego ejecute el siguiente procedimiento almacenado:

```sql
EXEC sp_execute_external_script @language = N'R',  
@script = N' print(normalizePath(R.home())); print(.libPaths());'; 
```

#### <a name="sample-results"></a>Ejemplo de resultados

*Mensaje(s) STDOUT del script externo:*

*[1] "C:\\Archivos de programa\\Microsoft SQL Server\\MSSQL13.SQL2016\\R_SERVICES"*

*[1] "C:/Archivos de programa/Microsoft SQL Server/MSSQL13.SQL2016/R_SERVICES/library"*

Para resolver el problema, debe reinstalar el paquete en la biblioteca de instancias de SQL Server.

::: moniker range=">=sql-server-2016"
>[!NOTE]
>Si ha actualizado una instancia de SQL Server 2016 para usar la versión más reciente de Microsoft R, la ubicación predeterminada de la biblioteca es diferente. Para más información, vea [Uso de SqlBindR para actualizar una instancia de R Services](../install/upgrade-r-and-python.md).
::: moniker-end

::: moniker range=">=sql-server-2016"
## <a name="launchpad-shuts-down-due-to-mismatched-dlls"></a>Launchpad se cierra debido a archivos DLL que no coinciden

Si instala el motor de base de datos con otras características, aplica un parche al servidor y, después, agrega la característica Machine Learning mediante el soporte original, puede que se instale la versión incorrecta de los componentes de Machine Learning. Si Launchpad detecta un error de coincidencia de versiones, se cierra y crea un archivo de volcado de memoria.

Para evitar este problema, asegúrese de instalar todas las características nuevas en el mismo nivel de parche que la instancia del servidor.

**Forma incorrecta de actualizar:**

1. Instale SQL Server 2016 sin R Services.
2. Instale la actualización acumulativa 2 de SQL Server 2016.
3. Instale R Services (en base de datos) mediante el soporte de RTM.

**Forma correcta de actualizar:**

1. Instale SQL Server 2016 sin R Services.
2. Actualice SQL Server 2016 al nivel de parche que quiera. Por ejemplo, instale el Service Pack 1 y, luego, la actualización acumulativa 2.
3. Para agregar la característica en el nivel de parche correcto, vuelva a ejecutar el programa de instalación de SP1 y CU2 y, después, elija R Services (en base de datos). 

## <a name="launchpad-fails-to-start-if-8dot3-notation-is-required"></a>Launchpad no se inicia si se necesita una notación 8.3

> [!NOTE] 
> En sistemas más antiguos, puede que Launchpad no se inicie si se necesita una notación 8.3. Este requisito se ha quitado en versiones posteriores. Los clientes de SQL Server 2016 R Services deben instalar una de las siguientes opciones:
> * SQL Server 2016 SP1 y CU1: [actualización acumulativa 1 de SQL Server](https://support.microsoft.com/help/3208177/cumulative-update-1-for-sql-server-2016-sp1).
> * SQL Server 2016 RTM, actualización acumulativa 3 y esta [revisión](https://support.microsoft.com/help/3210110/on-demand-hotfix-update-package-for-sql-server-2016-cu3), que está disponible a petición.

Para mantener la compatibilidad con R, SQL Server 2016 R Services (en base de datos) requería la unidad en la que se ha instalado la característica para permitir crear nombres de archivo cortos mediante la *notación 8.3*. Un nombre de archivo 8.3 también se denomina *nombre de archivo corto* y se usa para que sea compatible con versiones anteriores de Microsoft Windows o como una alternativa a los nombres de archivo largos.

Si el volumen donde está instalando R no admite los nombres de archivo cortos, los procesos que inicien R desde SQL Server podrían no encontrar el ejecutable correcto y Launchpad no se iniciará.

Como solución alternativa, puede habilitar la notación 8.3 en el volumen donde estén instalados SQL Server y R Services. Después, debe proporcionar el nombre corto del directorio de trabajo en el archivo de configuración de R Services.

1. Para habilitar la notación 8.3, ejecute la utilidad fsutil con el argumento *8dot3name*, como se muestra aquí: [fsutil 8dot3name](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/ff621566(v=ws.11)).

2. Una vez que se haya habilitado la notación 8.3, abra el archivo RLauncher.config y apunte la propiedad de `WORKING_DIRECTORY`. Para más información sobre cómo encontrar este archivo, vea [Solución de problemas de recopilación de datos para Machine Learning](data-collection-ml-troubleshooting-process.md).

3. Use la utilidad fsutil con el argumento *file* para especificar una ruta de acceso del archivo corta para la carpeta especificada en WORKING_DIRECTORY.

4. Edite el archivo de configuración para especificar el mismo directorio de trabajo que ha indicado en la propiedad WORKING_DIRECTORY. También puede especificar otro directorio de trabajo y elegir una ruta de acceso existente que sea compatible con la notación 8.3.
::: moniker-end

## <a name="next-steps"></a>Pasos siguientes

[Solución de problemas y problemas conocidos de Machine Learning Services](machine-learning-troubleshooting-overview.md)

[Recopilación de datos para la solución de problemas de aprendizaje automático](data-collection-ml-troubleshooting-process.md)

[Instalación de SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md)

[Solución de problemas de conexiones de motor de base de datos](../../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)