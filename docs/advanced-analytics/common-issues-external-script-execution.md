---
title: Problemas comunes con el servicio Launchpad y ejecución de scripts externos en SQL Server | Documentos de Microsoft
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/31/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 08ab6e2db6d6cde5e41f7ddb88c8afd1da241df7
ms.sourcegitcommit: 2d93cd115f52bf3eff3069f28ea866232b4f9f9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/01/2018
ms.locfileid: "34706843"
---
# <a name="common-issues-with-launchpad-service-and-external-script-execution-in-sql-server"></a>Problemas comunes con el servicio Launchpad y ejecución de scripts externos en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

 Servicio SQL Server de confianza Launchpad es compatible con la ejecución de scripts externos para R y Python. En SQL Server 2016 R Services SP1 proporciona el servicio. SQL Server 2017 incluye el ombre Launchpad como parte de la instalación inicial.

Varios problemas pueden evitar Launchpad desde el comienzo, incluidos los problemas de configuración o de cambios o falta de protocolos de red. Este artículo proporciona instrucciones para muchos problemas de la solución. Para cualquiera que falta, puede publicar preguntas para el [foro de servidor de aprendizaje de máquina](https://social.msdn.microsoft.com/Forums/home?category=MicrosoftR).

**Se aplica a:** servicios de aprendizaje de automático de SQL Server 2016 R Services, SQL Server de 2017

## <a name="determine-whether-launchpad-is-running"></a>Determinar si se está ejecutando Launchpad

1. Abra la **servicios** panel (Services.msc). O bien, desde la línea de comandos, escriba **SQLServerManager13.msc** o **SQLServerManager14.msc** para abrir [Administrador de configuración de SQL Server](https://docs.microsoft.com/sql/relational-databases/sql-server-configuration-manager).

2. Tome nota de la cuenta de servicio que se está ejecutando Launchpad. Cada instancia donde está habilitada la R o Python debe tener su propia instancia del servicio Launchpad. Por ejemplo, el servicio para una instancia con nombre podría ser algo parecido a _MSSQLLaunchpad$ InstanceName_.

3. Si el servicio está detenido, reinícielo. En el reinicio, si hay algún problema con la configuración, se publica un mensaje en el registro de eventos del sistema y se detiene el servicio de nuevo. Compruebe el registro de eventos del sistema para obtener más información acerca de por qué se detuvo el servicio.

4. Revise el contenido de RSetup.log y asegúrese de que no hay ningún error en el programa de instalación. Por ejemplo, el mensaje *salir con el código 0* indica un error del servicio al iniciar.

5. Para buscar otros errores, revise el contenido de rlauncher.log.

## <a name="check-the-launchpad-service-account"></a>Comprobación de la cuenta de servicio de Launchpad

La cuenta de servicio predeterminado podría ser "servicio NT\$SQL2016" o "servicio NT\$SQL2017". La parte final puede variar, según el nombre de instancia SQL.

El servicio Launchpad (Launchpad.exe) se ejecuta con una cuenta de servicio con privilegios bajos. Sin embargo, para iniciar R y Python y comunicarse con la instancia de base de datos, la cuenta de servicio Launchpad requiere los siguientes derechos de usuario:

- Iniciar sesión como servicio (SeServiceLogonRight)
- Reemplazar un token de nivel de proceso (SeAssignPrimaryTokenPrivilege)
- Omitir la comprobación transversal (SeChangeNotifyPrivilege)
- Ajustar las cuotas de memoria para un proceso (SeIncreaseQuotaSizePrivilege)

Para obtener información acerca de estos derechos de usuario, vea la sección "derechos y privilegios de Windows" en [Windows configurar cuentas de servicio y permisos](../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).

> [!TIP]
> Si está familiarizado con el uso de la herramienta de la plataforma de diagnóstico de soporte técnico (SDP) para diagnósticos de SQL Server, puede usar SDP para revisar el archivo de salida con el nombre MachineName_UserRights.txt.

## <a name="user-group-for-launchpad-cannot-log-on-locally"></a>Grupo de usuarios de Launchpad no puede iniciar sesión localmente

Durante la instalación de servicios de aprendizaje automático, SQL Server crea el grupo de usuarios de Windows **SQLRUserGroup** y, a continuación, se aprovisiona con todos los derechos necesarios para Launchpad para conectarse a SQL Server y ejecutar trabajos de script externo. Si este grupo de usuarios está habilitada, también se usa para ejecutar scripts de Python.

Sin embargo, en organizaciones donde se aplican las directivas de seguridad más restrictivas, podrían haberse eliminados manualmente los derechos necesarios para este grupo o pueden revocar automáticamente por la directiva. Si se han quitado los derechos, Launchpad ya no puede conectarse a SQL Server y SQL Server no se puede llamar al runtime externo.

Para corregir el problema, asegúrese de que el grupo **SQLRUserGroup** tiene el derecho de sistema **Permitir el inicio de sesión local**.

Para obtener más información, consulte [Windows configurar cuentas de servicio y permisos](https://msdn.microsoft.com/library/ms143504.aspx#Windows).

## <a name="permissions-to-run-external-scripts"></a>Permisos para ejecutar scripts externos

Aunque se Launchpad está configurado correctamente, devuelve un error si el usuario no tiene permiso para ejecutar scripts de R o Python.

Si ha instalado a SQL Server como un administrador de base de datos o es un propietario de base de datos, este permiso se concede automáticamente. Sin embargo, otros usuarios suelen tener más permisos limitados. Si intenta ejecutar un script de R, producirá un error de Launchpad.

Para corregir el problema, en SQL Server Management Studio, un administrador de seguridad puede modificar el inicio de sesión SQL o la cuenta de usuario de Windows mediante la ejecución de la secuencia de comandos siguiente:

```SQL
GRANT EXECUTE ANY EXTERNAL SCRIPT TO <username>
```

Para obtener más información, consulte [GRANT (Transact-SQL](../t-sql/statements/grant-transact-sql.md).

## <a name="common-launchpad-errors"></a>Errores comunes de Launchpad

Esta sección enumeran los mensajes de error más comunes que devuelve Launchpad.

## <a name="unable-to-launch-runtime-for-r-script"></a>"No se puede iniciar en tiempo de ejecución de script de R"

Si no se puede iniciar sesión en el grupo de Windows para los usuarios de R (que también se utilizan para Python) a la instancia que se ejecuta los servicios de R, pueden aparecer los errores siguientes:

- Errores generados al intentar ejecutar scripts R:

    * *No se puede iniciar el tiempo de ejecución para el script 'R'. Compruebe la configuración del tiempo de ejecución 'R'.*

    * *An external script error occurred. Unable to launch the runtime.* (Error en el script externo. No se puede iniciar el tiempo de ejecución).

- Los errores generados por el [!INCLUDE[rsql_launchpad](../includes/rsql-launchpad-md.md)] servicio:

    * *Failed to initialize the launcher RLauncher.dll*

    * *No launcher dlls were registered!*

    * *Registros de seguridad indican que la cuenta de servicio de NT no pudo iniciar sesión*

Para obtener información sobre cómo conceder los permisos necesarios de este grupo de usuarios, consulte [instalar SQL Server 2016 R Services](install/sql-r-services-windows-install.md).

> [!NOTE]
> Esta limitación no se aplica si usa inicios de sesión de SQL para ejecutar scripts de R desde una estación de trabajo remota.

## <a name="logon-failure-the-user-has-not-been-granted-the-requested-logon-type"></a>"Error de inicio de sesión: el usuario no tiene el tipo de inicio de sesión solicitado"

De forma predeterminada, [!INCLUDE[rsql_launchpad_md](../includes/rsql-launchpad-md.md)] utiliza la cuenta siguiente en el inicio: `NT Service\MSSQLLaunchpad`. La cuenta está configurada por [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] el programa de instalación tenga todos los permisos necesarios.

Si asigna una cuenta diferente a Launchpad o la derecha se quita una directiva en el equipo de SQL Server, la cuenta no tenga los permisos necesarios y puede que vea este error:

>*ERROR_LOGON_TYPE_NOT_GRANTED 1385 (0x569) Error de inicio de sesión: el usuario no tiene permisos para el tipo de inicio de sesión solicitado en el equipo.*

Para conceder los permisos necesarios a la nueva cuenta de servicio, use la aplicación de directiva de seguridad Local y actualizar los permisos en la cuenta para incluir los siguientes permisos:

+ Ajustar las cuotas de memoria de un proceso (SeIncreaseQuotaPrivilege)
+ Omitir la comprobación transversal (SeChangeNotifyPrivilege)
+ Iniciar sesión como servicio (SeServiceLogonRight)
+ Reemplazar un token de nivel de proceso (SeAssignPrimaryTokenPrivilege)

## <a name="unable-to-communicate-with-the-launchpad-service"></a>"No se puede comunicar con el servicio Launchpad"

Si ha instalado y, a continuación, habilita el aprendizaje automático, pero este error aparece cuando intenta ejecutar un script de R o Python, puede haberse detenido el servicio Launchpad para la instancia de ejecución.

1. Desde un símbolo del sistema de Windows, abra el Administrador de configuración de SQL Server. Para obtener más información, vea [SQL Server Configuration Manager](https://docs.microsoft.com/sql/relational-databases/sql-server-configuration-manager).

2. Haga clic en Launchpad de SQL Server para la instancia y, a continuación, seleccione **propiedades**.

3. Seleccione el **servicio** ficha y, a continuación, compruebe que el servicio se está ejecutando. Si no se está ejecutando, cambie la **iniciar modo** a **automática**y, a continuación, seleccione **aplicar**.

4. Reiniciar el servicio normalmente corrige el problema para que puedan ejecutarse los scripts de aprendizaje de máquina. Si el reinicio no soluciona el problema, tenga en cuenta la ruta de acceso y los argumentos en la **ruta de acceso binaria** propiedad y haga lo siguiente:

    A. Revise el archivo .config del iniciador y asegúrese de que el directorio de trabajo es válido.

    B. Asegúrese de que el grupo de Windows que se usa por Launchpad puede conectarse a la instancia de SQL Server, como se describe en el [sección anterior](#bkmk_LaunchpadTS).

    c. Si cambia cualquiera de las propiedades del servicio, reinicie el servicio Launchpad.

## <a name="fatal-error-creation-of-tmpfile-failed"></a>"Error de creación de un error irrecuperable de tmpFile"

En este escenario, se han instalado correctamente características de aprendizaje de máquina y Launchpad se ejecuta. Intenta ejecutar un código de R o Python sencillo, pero no se Launchpad con un error similar al siguiente: 

>*No se puede comunicar con el tiempo de ejecución de script de R. Compruebe los requisitos de tiempo de ejecución de R.*

Al mismo tiempo, el tiempo de ejecución de script externo escribe el mensaje siguiente como parte del mensaje STDERR: 

>*Error irrecuperable: creación de tmpfile error.*

Este error indica que la cuenta que está intentando usar Launchpad no tiene permiso para iniciar sesión en la base de datos. Esta situación puede ocurrir cuando se implementan directivas de seguridad estricta. Para determinar si este es el caso, revise los registros de SQL Server y compruebe para ver si la cuenta de MSSQLSERVER01 se denegó al inicio de sesión. Se proporciona la misma información en los registros que son específicos de R\_servicios o PYTHON\_servicios. Busque ExtLaunchError.log.

De forma predeterminada, 20 cuentas configuradas y asociadas con el proceso de Launchpad.exe, con los nombres MSSQLSERVER01 a través de MSSQLSERVER20. Si realiza un uso intensivo de R o Python, puede aumentar el número de cuentas.

Para resolver el problema, asegúrese de que el grupo tiene *permitir el registro local* permisos a la instancia local donde se han instalado y habilitado características de aprendizaje de la máquina. En algunos entornos, este nivel de permiso puede requerir una excepción de GPO desde el Administrador de red.

## <a name="not-enough-quota-to-process-this-command"></a>"No hay suficiente cuota para procesar este comando"

Este error puede deberse a una de las siguientes operaciones:

- LaunchPad puede tener usuarios externos insuficiente para ejecutar la consulta externa. Por ejemplo, si tiene más de 20 consultas externas al mismo tiempo, y solo hay 20 usuarios de forma predeterminada, una o más consultas podrían producir errores.

- Hay suficiente memoria disponible para procesar la tarea de R. Este error se produce con mayor frecuencia en un entorno de forma predeterminada, donde SQL Server puede usar hasta un 70 por ciento de los recursos del equipo. Para obtener información sobre cómo modificar la configuración del servidor para admitir el mayor uso de recursos mediante R, consulte [el código de R en marcha](r/operationalizing-your-r-code.md).

## <a name="cant-find-package"></a>"No se encuentra el paquete"

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

## <a name="launchpad-shuts-down-due-to-mismatched-dlls"></a>LaunchPad cierra a causa de los archivos DLL que no coinciden

Si instala el motor de base de datos con otras características, el servidor, de revisión y, a continuación, agregar más adelante la característica de aprendizaje automático mediante el medio original, puede instalarse una versión incorrecta de los componentes de aprendizaje automático. Cuando se Launchpad detecta un error de coincidencia de versión, se cierra y crea un archivo de volcado de memoria.

Para evitar este problema, asegúrese de instalar las nuevas características en el mismo nivel de revisión como instancia del servidor.

**El método incorrecto de actualización:**

1. Instalar a SQL Server 2016 sin servicios de R.
2. Actualizar SQL Server 2016 la actualización acumulativa 2.
3. Instalar R Services (In-Database) mediante el uso de los medios RTM.

**La manera correcta para actualizar:**

1. Instalar a SQL Server 2016 sin servicios de R.
2. Actualizar SQL Server 2016 en el nivel de revisión deseado. Por ejemplo, instale Service Pack 1 y, a continuación, la actualización acumulativa 2.
3. Para agregar la característica en el nivel de revisión correcto, vuelva a ejecutar el programa de instalación de SP1 y CU2 y, a continuación, elija R Services (In-Database). 

## <a name="launchpad-fails-to-start-if-8dot3-notation-is-required"></a>No se puede iniciar si se requiere la notación de tiene el formato 8.3 LaunchPad

> [!NOTE] 
> En sistemas más antiguos, Launchpad no se iniciará si hay un requisito de notación tiene el formato 8.3. Este requisito se ha quitado en versiones posteriores. Los clientes de servicios de SQL Server 2016 R deben instalar uno de los siguientes:
> * SP1 de SQL Server 2016 y CU1: [la actualización acumulativa 1 para SQL Server](https://support.microsoft.com/help/3208177/cumulative-update-1-for-sql-server-2016-sp1).
> * SQL Server 2016 RTM, la actualización acumulativa 3 y esto [revisión](https://support.microsoft.com/help/3210110/on-demand-hotfix-update-package-for-sql-server-2016-cu3), que está disponible a petición.

Por compatibilidad con R, SQL Server 2016 R Services (In-Database) requiere la unidad donde está instalada la característica para admitir la creación de nombres cortos de archivo mediante *tiene el formato 8.3 notación*. Un nombre de 8.3 archivo también se denomina un *nombre corto de archivo*, y se utiliza por compatibilidad con versiones anteriores de Microsoft Windows o como una alternativa a los nombres de archivo largos.

Si el volumen donde esté instalando R no admite nombres cortos de archivo, los procesos que se ejecuten código R en SQL Server no pueda encontrar el archivo ejecutable correcto y no se iniciará el Launchpad.

Como alternativa, puede habilitar la notación tiene el formato 8.3 en el volumen donde está instalado SQL Server y está instalado R Services. Después, debe proporcionar el nombre corto del directorio de trabajo en el archivo de configuración de R Services.

1. Para habilitar la notación tiene el formato 8.3, ejecute la utilidad fsutil con la *8dot3name* argumento tal como se describe aquí: [8dot3name fsutil](https://technet.microsoft.com/library/ff621566(v=ws.11).aspx).

2. Una vez habilitada la notación tiene el formato 8.3, abra el archivo RLauncher.config y tenga en cuenta la propiedad de `WORKING_DIRECTORY`. Para obtener información acerca de cómo encontrar este archivo, consulte [recopilación de datos para la solución de problemas de aprendizaje automático](data-collection-ml-troubleshooting-process.md).

3. Use la utilidad fsutil con la *archivo* argumento para especificar una ruta de acceso de archivo corto para la carpeta que se especifica en WORKING_DIRECTORY.

4. Edite el archivo de configuración para especificar el mismo directorio de trabajo que especificó en la propiedad WORKING_DIRECTORY. Como alternativa, puede especificar un directorio de trabajo diferente y elija una ruta de acceso existente que ya es compatible con la notación de tiene el formato 8.3.


## <a name="next-steps"></a>Pasos siguientes

[Problemas conocidos y solución de problemas de servicios de aprendizaje de máquina](machine-learning-troubleshooting-faq.md)

[Recopilación de datos para la solución de problemas de aprendizaje automático](data-collection-ml-troubleshooting-process.md)

[Preguntas más frecuentes sobre actualización e instalación](r/upgrade-and-installation-faq-sql-server-r-services.md)

[Solucionar problemas de conexiones de motor de base de datos](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)
