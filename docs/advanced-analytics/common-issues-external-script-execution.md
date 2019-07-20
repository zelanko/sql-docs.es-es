---
title: Problemas comunes con el servicio Launchpad y la ejecución de scripts externos
ms.prod: sql
ms.technology: ''
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 3786ab3ee17bbbc0b54e439e3466236af098ffd3
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345170"
---
# <a name="common-issues-with-launchpad-service-and-external-script-execution-in-sql-server"></a>Problemas comunes con el servicio Launchpad y la ejecución de scripts externos en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

 SQL Server servicio Launchpad de confianza admite la ejecución de scripts externos para R y Python. En SQL Server servicios de R 2016, SP1 proporciona el servicio. SQL Server 2017 incluye el servicio Launchpad como parte de la instalación inicial.

Varios problemas pueden impedir que Launchpad se inicie, incluidos los problemas de configuración o los cambios, o los protocolos de red que faltan. En este artículo se proporcionan instrucciones para la solución de problemas. En caso de que no se haya perdido, puede publicar preguntas en el [Foro de machine learning Server](https://social.msdn.microsoft.com/Forums/en-US/home?category=MicrosoftR).

## <a name="determine-whether-launchpad-is-running"></a>Determinar si se está ejecutando Launchpad

1. Abra el panel **servicios** (Services. msc). O bien, desde la línea de comandos, escriba **SQLServerManager13. msc** o **SQLServerManager14. msc** para abrir [Administrador de configuración de SQL Server](https://docs.microsoft.com/sql/relational-databases/sql-server-configuration-manager).

2. Tome nota de la cuenta de servicio en la que se ejecuta Launchpad. Cada instancia de en la que R o Python está habilitada debe tener su propia instancia del servicio Launchpad. Por ejemplo, el servicio de una instancia con nombre podría ser similar a _MSSQLLaunchpad $ InstanceName_.

3. Si el servicio está detenido, reinícielo. Al reiniciar, si hay algún problema con la configuración, se publica un mensaje en el registro de eventos del sistema y el servicio se vuelve a detener. Compruebe el registro de eventos del sistema para obtener detalles sobre por qué se detuvo el servicio.

4. Revise el contenido de RSetup. log y asegúrese de que no haya ningún error en la instalación. Por ejemplo, el mensaje que *sale del código 0* indica un error del servicio que se va a iniciar.

5. Para buscar otros errores, revise el contenido de rlauncher. log.

## <a name="check-the-launchpad-service-account"></a>Comprobar la cuenta de servicio de Launchpad

La cuenta de servicio predeterminada podría ser "NT\$Service SQL2016" o "NT\$Service SQL2017". La última parte puede variar en función del nombre de la instancia de SQL.

El servicio Launchpad (Launchpad. exe) se ejecuta mediante una cuenta de servicio con pocos privilegios. Sin embargo, para iniciar R y Python y comunicarse con la instancia de base de datos, la cuenta de servicio de Launchpad requiere los siguientes derechos de usuario:

- Iniciar sesión como servicio (SeServiceLogonRight)
- Reemplazar un token de nivel de proceso (SeAssignPrimaryTokenPrivilege)
- Omitir la comprobación transversal (SeChangeNotifyPrivilege)
- Ajustar las cuotas de memoria de un proceso (SeIncreaseQuotaSizePrivilege)

Para obtener información acerca de estos derechos de usuario, consulte la sección "privilegios y derechos de Windows" en [configurar los permisos y las cuentas de servicio de Windows](../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).

> [!TIP]
> Si está familiarizado con el uso de la herramienta de la plataforma de diagnóstico de soporte técnico (SDP) para SQL Server diagnósticos, puede usar SDP para revisar el archivo de salida con el nombre MachineName_UserRights. txt.

## <a name="user-group-for-launchpad-cannot-log-on-locally"></a>El grupo de usuarios para Launchpad no puede iniciar sesión localmente

Durante la instalación de Machine Learning Services, SQL Server crea el grupo de usuarios de Windows **SQLRUserGroup** y, a continuación, lo aprovisiona con todos los derechos necesarios para que Launchpad se conecte a SQL Server y ejecute trabajos de scripts externos. Si este grupo de usuarios está habilitado, también se usa para ejecutar scripts de Python.

Sin embargo, en las organizaciones en las que se aplican directivas de seguridad más restrictivas, es posible que se hayan quitado manualmente los derechos necesarios para este grupo o que la Directiva los revoque automáticamente. Si se han quitado los derechos, Launchpad ya no podrá conectarse a SQL Server y SQL Server no podrá llamar al tiempo de ejecución externo.

Para corregir el problema, asegúrese de que el grupo **SQLRUserGroup** tiene el derecho de sistema **Permitir el inicio de sesión local**.

Para obtener más información, consulte [Configurar los permisos y las cuentas de servicio de Windows](../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).

## <a name="permissions-to-run-external-scripts"></a>Permisos para ejecutar scripts externos

Aunque Launchpad esté configurado correctamente, devuelve un error si el usuario no tiene permiso para ejecutar scripts de R o Python.

Si ha instalado SQL Server como administrador de bases de datos o si es propietario de la base de datos, se le concederá automáticamente este permiso. Sin embargo, otros usuarios suelen tener permisos más limitados. Si intentan ejecutar un script de R, recibirán un error de Launchpad.

Para corregir el problema, en SQL Server Management Studio, un administrador de seguridad puede modificar el inicio de sesión de SQL o la cuenta de usuario de Windows mediante la ejecución del siguiente script:

```sql
GRANT EXECUTE ANY EXTERNAL SCRIPT TO <username>
```

Para obtener más información, vea [Grant (Transact-SQL](../t-sql/statements/grant-transact-sql.md)).

## <a name="common-launchpad-errors"></a>Errores comunes de Launchpad

En esta sección se enumeran los mensajes de error más comunes que Launchpad devuelve.

## <a name="unable-to-launch-runtime-for-r-script"></a>"No se puede iniciar el tiempo de ejecución para script R"

Si el grupo de Windows para los usuarios de R (también usados para Python) no puede iniciar sesión en la instancia que está ejecutando R Services, podrían aparecer los siguientes errores:

- Errores generados al intentar ejecutar scripts de R:

    * *No se puede iniciar el tiempo de ejecución para el script 'R'. Compruebe la configuración del tiempo de ejecución 'R'.*

    * *An external script error occurred. Unable to launch the runtime.* (Error en el script externo. No se puede iniciar el tiempo de ejecución).

- Errores generados por [!INCLUDE[rsql_launchpad](../includes/rsql-launchpad-md.md)] el servicio:

    * *Failed to initialize the launcher RLauncher.dll*

    * *No launcher dlls were registered!*

    * *Los registros de seguridad indican que el servicio NT de la cuenta no pudo iniciar sesión*

Para obtener información acerca de cómo conceder a este grupo de usuarios los permisos necesarios, consulte [instalación de SQL Server 2016 R Services](install/sql-r-services-windows-install.md).

> [!NOTE]
> Esta limitación no se aplica si usa inicios de sesión de SQL para ejecutar scripts de R desde una estación de trabajo remota.

## <a name="logon-failure-the-user-has-not-been-granted-the-requested-logon-type"></a>"Error de inicio de sesión: no se ha concedido al usuario el tipo de inicio de sesión solicitado"

De forma predeterminada [!INCLUDE[rsql_launchpad_md](../includes/rsql-launchpad-md.md)] , usa la siguiente cuenta en el `NT Service\MSSQLLaunchpad`Inicio:. El [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] programa de instalación configura la cuenta para que tenga todos los permisos necesarios.

Si asigna una cuenta diferente a Launchpad, o una directiva en la máquina SQL Server quita el derecho, es posible que la cuenta no tenga los permisos necesarios y que vea este error:

>*ERROR_LOGON_TYPE_NOT_GRANTED 1385 (0x569) Error de inicio de sesión: el usuario no tiene permisos para el tipo de inicio de sesión solicitado en el equipo.*

Para conceder los permisos necesarios a la nueva cuenta de servicio, use la aplicación de directiva de seguridad local y actualice los permisos en la cuenta para incluir los permisos siguientes:

+ Ajustar las cuotas de memoria de un proceso (SeIncreaseQuotaPrivilege)
+ Omitir la comprobación transversal (SeChangeNotifyPrivilege)
+ Iniciar sesión como servicio (SeServiceLogonRight)
+ Reemplazar un token de nivel de proceso (SeAssignPrimaryTokenPrivilege)

## <a name="unable-to-communicate-with-the-launchpad-service"></a>"No se puede comunicar con el servicio Launchpad"

Si ha instalado y habilitado el aprendizaje automático, pero obtiene este error al intentar ejecutar un script de R o Python, es posible que el servicio Launchpad de la instancia haya dejado de ejecutarse.

1. Desde un símbolo del sistema de Windows, abra el Administrador de configuración de SQL Server. Para obtener más información, vea [SQL Server Configuration Manager](https://docs.microsoft.com/sql/relational-databases/sql-server-configuration-manager).

2. Haga clic con el botón secundario en SQL Server Launchpad para la instancia y seleccione **propiedades**.

3. Seleccione la pestaña **servicio** y compruebe que el servicio se está ejecutando. Si no se está ejecutando, cambie el **modo de inicio** a **automático**y, a continuación, seleccione **aplicar**.

4. El reinicio del servicio normalmente corrige el problema para que puedan ejecutarse los scripts de aprendizaje automático. Si el reinicio no soluciona el problema, anote la ruta de acceso y los argumentos de la propiedad **ruta de acceso binaria** y haga lo siguiente:

    a. Revise el archivo. config del iniciador y asegúrese de que el directorio de trabajo es válido.

    b. Asegúrese de que el grupo de Windows que usa Launchpad puede conectarse a la instancia de SQL Server.

    c. Si cambia cualquiera de las propiedades del servicio, reinicie el servicio Launchpad.

## <a name="fatal-error-creation-of-tmpfile-failed"></a>"Error irrecuperable al crear tmpFile

En este escenario, ha instalado correctamente las características de aprendizaje automático y Launchpad se está ejecutando. Intenta ejecutar algunos códigos sencillos de R o Python, pero Launchpad produce un error similar al siguiente: 

>*No se puede comunicar con el Runtime para el script de R. Compruebe los requisitos del tiempo de ejecución de R.*

Al mismo tiempo, el tiempo de ejecución de script externo escribe el mensaje siguiente como parte del mensaje STDERR: 

>*Error irrecuperable: error al crear tmpfile.*

Este error indica que la cuenta que Launchpad está intentando usar no tiene permiso para iniciar sesión en la base de datos. Esta situación puede producirse cuando se implementan estrictas directivas de seguridad. Para determinar si este es el caso, revise los registros de SQL Server y compruebe si la cuenta MSSQLSERVER01 se denegó en el inicio de sesión. En los registros que son específicos de R\_Services o de los servicios de Python\_, se proporciona la misma información. Busque ExtLaunchError. log.

De forma predeterminada, se configuran 20 cuentas y se asocian al proceso Launchpad. exe, con los nombres MSSQLSERVER01 a MSSQLSERVER20. Si hace un uso intensivo de R o Python, puede aumentar el número de cuentas.

Para resolver el problema, asegúrese de que el grupo tenga los permisos *permitir el inicio de sesión local* en la instancia local, donde se han instalado y habilitado las características de aprendizaje automático. En algunos entornos, este nivel de permiso puede requerir una excepción de GPO del administrador de red.

## <a name="not-enough-quota-to-process-this-command"></a>"No hay cuota suficiente para procesar este comando"

Este error puede significar una de varias cosas:

- Launchpad podría no tener suficientes usuarios externos para ejecutar la consulta externa. Por ejemplo, si está ejecutando más de 20 consultas externas simultáneamente y solo hay 20 usuarios predeterminados, puede producirse un error en una o más consultas.

- No hay suficiente memoria disponible para procesar la tarea de R. Este error se produce con mayor frecuencia en un entorno predeterminado, donde SQL Server podría estar usando hasta el 70 por ciento de los recursos del equipo. Para obtener información sobre cómo modificar la configuración del servidor para admitir un mayor uso de los recursos de R, consulte puesta en [operación del código de r](r/operationalizing-your-r-code.md).

## <a name="cant-find-package"></a>"No se encuentra el paquete"

Si ejecuta código R en SQL Server y obtiene este mensaje, pero no obtuvo el mensaje cuando ejecutó el mismo código fuera de SQL Server, significa que el paquete no se instaló en la ubicación de biblioteca predeterminada que usa SQL Server.

Este error puede producirse de muchas maneras:

- Ha instalado un nuevo paquete en el servidor, pero se ha denegado el acceso, por lo que R ha instalado el paquete en una biblioteca de usuario.

- Instaló R Services y, a continuación, instaló otra herramienta de R o un conjunto de bibliotecas, como Microsoft R Server (independiente), Microsoft R Client, RStudio, etc.

Para determinar la ubicación de la biblioteca de paquetes de R utilizada por la instancia, abra SQL Server Management Studio (o cualquier otra herramienta de consulta de base de datos), conéctese a la instancia de y, a continuación, ejecute el siguiente procedimiento almacenado:

```sql
EXEC sp_execute_external_script @language = N'R',  
@script = N' print(normalizePath(R.home())); print(.libPaths());'; 
```

#### <a name="sample-results"></a>Ejemplo de resultados

*Mensaje(s) STDOUT del script externo:*

*[1] "C:\\archivos\\de programa\\Microsoft SQL Server MSSQL13. SQL2016\\R_SERVICES*

*[1] "C:/archivos de programa/Microsoft SQL Server/MSSQL13. SQL2016/R_SERVICES/Library "*

Para resolver el problema, debe volver a instalar el paquete en la biblioteca de instancias de SQL Server.

>[!NOTE]
>Si ha actualizado una instancia de SQL Server 2016 para usar la versión más reciente de Microsoft R, la ubicación predeterminada de la biblioteca es diferente. Para obtener más información, consulte [uso de SqlBindR para actualizar una instancia de R Services](install/upgrade-r-and-python.md).

## <a name="launchpad-shuts-down-due-to-mismatched-dlls"></a>Launchpad se cierra debido a archivos dll no coincidentes

Si instala el motor de base de datos con otras características, aplique una revisión al servidor y, después, agregue la característica Machine Learning con el medio original, se puede instalar la versión incorrecta de los componentes Machine Learning. Cuando Launchpad detecta una discrepancia de versiones, se apaga y crea un archivo de volcado de memoria.

Para evitar este problema, asegúrese de instalar todas las características nuevas en el mismo nivel de revisión que la instancia del servidor.

**La manera equivocada de actualizar:**

1. Instale SQL Server 2016 sin R Services.
2. Actualización SQL Server 2016 acumulativa 2.
3. Instale R Services (en base de datos) mediante el uso de los medios de RTM.

**La manera correcta de actualizar:**

1. Instale SQL Server 2016 sin R Services.
2. Actualice SQL Server 2016 al nivel de revisión deseado. Por ejemplo, instale el Service Pack 1 y, a continuación, la actualización acumulativa 2.
3. Para agregar la característica en el nivel de revisión correcto, vuelva a ejecutar el programa de instalación de SP1 y CU2 y, a continuación, elija R Services (en base de datos). 

## <a name="launchpad-fails-to-start-if-8dot3-notation-is-required"></a>Launchpad no se inicia si se requiere una notación 8.3

> [!NOTE] 
> En sistemas más antiguos, Launchpad puede no iniciarse si hay un requisito de notación 8.3. Este requisito se ha quitado en versiones posteriores. Los clientes de SQL Server 2016 R Services deben instalar una de las siguientes opciones:
> * SQL Server 2016 SP1 y CU1: [Actualización acumulativa 1 para SQL Server](https://support.microsoft.com/help/3208177/cumulative-update-1-for-sql-server-2016-sp1).
> * SQL Server 2016 RTM, actualización acumulativa 3 y esta [revisión](https://support.microsoft.com/help/3210110/on-demand-hotfix-update-package-for-sql-server-2016-cu3), que está disponible a petición.

Por compatibilidad con R, SQL Server 2016 R Services (en base de datos) requerían la unidad en la que se instaló la característica para admitir la creación de nombres de archivo cortos mediante la *notación 8.3*. Un nombre de archivo 8,3 también se denomina *nombre de archivo corto*y se usa por compatibilidad con versiones anteriores de Microsoft Windows o como alternativa a los nombres de archivo largos.

Si el volumen en el que está instalando R no admite nombres de archivo cortos, es posible que los procesos que inician R desde SQL Server no puedan encontrar el archivo ejecutable correcto y que Launchpad no se inicie.

Como solución alternativa, puede habilitar la notación 8.3 en el volumen en el que está instalado SQL Server y en el que está instalado R Services. Después, debe proporcionar el nombre corto del directorio de trabajo en el archivo de configuración de R Services.

1. Para habilitar la notación 8.3, ejecute la utilidad fsutil con el argumento *8dot3name* como se describe aquí: [fsutil 8dot3name](https://technet.microsoft.com/library/ff621566(v=ws.11).aspx).

2. Una vez habilitada la notación 8.3, abra el archivo RLauncher. config y anote la propiedad `WORKING_DIRECTORY`de. Para obtener información sobre cómo encontrar este archivo, consulte [recopilación de datos para la solución de problemas de machine learning](data-collection-ml-troubleshooting-process.md).

3. Use la utilidad fsutil con el argumento *File* para especificar una ruta de acceso de archivo corta para la carpeta especificada en WORKING_DIRECTORY.

4. Edite el archivo de configuración para especificar el mismo directorio de trabajo que especificó en la propiedad WORKING_DIRECTORY. También puede especificar un directorio de trabajo diferente y elegir una ruta de acceso existente que ya sea compatible con la notación 8.3.


## <a name="next-steps"></a>Pasos siguientes

[Solución de problemas y problemas conocidos de Machine Learning Services](machine-learning-troubleshooting-faq.md)

[Recopilación de datos para la solución de problemas de machine learning](data-collection-ml-troubleshooting-process.md)

[Preguntas más frecuentes sobre actualización e instalación](r/upgrade-and-installation-faq-sql-server-r-services.md)

[Solucionar problemas de conexiones del motor de base de datos](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)
