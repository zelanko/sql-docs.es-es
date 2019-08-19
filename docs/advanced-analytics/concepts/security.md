---
title: Información general de seguridad para las extensiones de R y Python
description: Información general sobre seguridad para el marco de extensibilidad en SQL Server Machine Learning Services. Seguridad para inicios de sesión y cuentas de usuario, SQL Server Launchpad servicio, cuentas de trabajo, ejecutar varios scripts y permisos de archivo.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f5b0af74633fb13b9cfd0b187bc2b180d7fd87b4
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715850"
---
# <a name="security-overview-for-the-extensibility-framework-in-sql-server-machine-learning-services"></a>Información general sobre seguridad para el marco de extensibilidad en SQL Server Machine Learning Services

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En este artículo se describe la arquitectura de seguridad general que se usa para integrar el motor de base de datos de SQL Server y los componentes relacionados con el marco de extensibilidad. Examina los elementos protegibles, los servicios, la identidad del proceso y los permisos. Para obtener más información sobre los conceptos clave y los componentes de extensibilidad en SQL Server, consulte la [arquitectura de extensibilidad en SQL Server Machine Learning Services](extensibility-framework.md)].

## <a name="securables-for-external-script"></a>Elementos protegibles para script externo

Un script externo escrito en R o Python se envía como parámetro de entrada a un [procedimiento almacenado del sistema](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) creado para este propósito, o se ajusta en un procedimiento almacenado que defina. Como alternativa, es posible que tenga modelos previamente entrenados y almacenados en un formato binario en una tabla de base de datos, a los que se puede llamar en una función de [predicción](../../t-sql/queries/predict-transact-sql.md) T-SQL.

Dado que el script se proporciona a través de objetos de esquema de base de datos existentes, procedimientos almacenados y tablas, no hay elementos [protegibles](../../relational-databases/security/securables.md) nuevos para SQL Server Machine Learning Services.

Independientemente de la forma en que use el script o, lo que contengan, los objetos de base de datos se crearán y, probablemente, se guardarán, pero no se introducirá ningún nuevo tipo de objeto para almacenar el script. Como resultado, la capacidad de consumir, crear y guardar objetos de base de datos depende en gran medida de los permisos de base de datos ya definidos para los usuarios.

<a name="permissions"></a>

## <a name="permissions"></a>Permisos

El modelo de seguridad de datos de SQL Server de los inicios de sesión y roles de base de datos se extiende al script de R y Python. Se requiere un inicio de sesión de SQL Server o una cuenta de usuario de Windows para ejecutar scripts externos que utilizan datos de SQL Server o que se ejecutan con SQL Server como el contexto de cálculo. Los usuarios de bases de datos que tienen permisos para ejecutar una consulta ad hoc pueden acceder a los mismos datos desde el script de R o Python.

El inicio de sesión o la cuenta de usuario identifica la *entidad de seguridad*, que podría necesitar varios niveles de acceso, en función de los requisitos de los scripts externos:

+ Permiso para obtener acceso a la base de datos donde se habilitan los scripts externos.
+ Permisos para leer datos de objetos protegidos como tablas.
+ La capacidad de escribir nuevos datos en una tabla, como un modelo, o la puntuación de los resultados.
+ La capacidad de crear nuevos objetos, como tablas, procedimientos almacenados que usan el script externo, o funciones personalizadas que utilizan el trabajo de R o Python.
+ Derecho a instalar nuevos paquetes en el SQL Server equipo o usar paquetes proporcionados a un grupo de usuarios.

Cada persona que ejecuta un script externo mediante SQL Server como contexto de ejecución debe estar asignada a un usuario de la base de datos. En lugar de establecer individualmente los permisos de usuario de base de datos, puede crear roles para administrar conjuntos de permisos y asignar usuarios a esos roles, en lugar de establecer individualmente los permisos de usuario.

Para obtener más información, vea [conceder permiso a los usuarios para SQL Server Machine Learning Services](../../advanced-analytics/security/user-permission.md).

## <a name="permissions-when-using-an-external-client-tool"></a>Permisos cuando se usa una herramienta de cliente externa

Los usuarios que usan R o Python en una herramienta de cliente externa deben tener su cuenta de inicio de sesión o cuenta asignada a un usuario en la base de datos si necesitan ejecutar un script externo en la base de datos, o tener acceso a objetos y datos de base de datos. Los mismos permisos son necesarios si el script externo se envía desde un cliente de ciencia de datos remoto o se ejecuta mediante un procedimiento almacenado de T-SQL.

Por ejemplo, suponga que ha creado un script externo que se ejecuta en el equipo local y desea ejecutar ese script en SQL Server. Debe asegurarse de que se cumplan las condiciones siguientes:

+ La base de datos permite las conexiones remotas.
+ El inicio de sesión de SQL o la cuenta de Windows que usó para el acceso a la base de datos se ha agregado al SQL Server en el nivel de instancia.
+ El inicio de sesión de SQL o el usuario de Windows deben tener el permiso para ejecutar scripts externos. Por lo general, este permiso solo lo puede agregar un administrador de bases de datos.
+ El inicio de sesión de SQL o el usuario de la ventana debe agregarse como un usuario con los permisos adecuados en cada base de datos donde el script externo realice cualquiera de estas operaciones:
  + Recuperando datos.
  + Escribir o actualizar datos.
  + Crear nuevos objetos, como tablas o procedimientos almacenados.

Una vez que se ha aprovisionado el inicio de sesión o la cuenta de usuario de Windows y dado los permisos necesarios, puede ejecutar un script externo en SQL Server mediante un objeto de origen de datos en R o la biblioteca **revoscalepy** en Python, o bien mediante una llamada a un procedimiento almacenado que contiene el script externo.

Siempre que se inicia un script externo desde SQL Server, la seguridad del motor de base de datos obtiene el contexto de seguridad del usuario que inició el trabajo y administra las asignaciones del usuario o el inicio de sesión en los objetos protegibles.

Por lo tanto, todos los scripts externos que se inician desde un cliente remoto deben especificar la información de inicio de sesión o de usuario como parte de la cadena de conexión.

<a name="launchpad"></a>

## <a name="services-used-in-external-processing-launchpad"></a>Servicios usados en el procesamiento externo (LaunchPad)

El marco de extensibilidad agrega un nuevo servicio NT a la [lista de servicios](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md#Service_Details) de una SQL Server instalación: [**SQL Server Launchpad (MSSSQLSERVER)** ](extensibility-framework.md#launchpad).

El motor de base de datos utiliza el servicio SQL Server Launchpad para crear instancias de una sesión de R o Python como un proceso independiente. El proceso se ejecuta con una cuenta con pocos privilegios. DISTINCT from SQL Server, Launchpad y la identidad del usuario en la que se ejecutó el procedimiento almacenado o la consulta de host. La ejecución de un script en un proceso independiente, en una cuenta con pocos privilegios, es la base del modelo de aislamiento y seguridad para R y Python en SQL Server.

Además de iniciar procesos externos, Launchpad también es responsable de realizar el seguimiento de la identidad del usuario que realiza la llamada y de asignar esa identidad a la cuenta de trabajador con pocos privilegios que se usa para iniciar el proceso. En algunos escenarios, donde el script o el código vuelven a SQL Server para los datos y las operaciones, Launchpad suele ser capaz de administrar la transferencia de identidad sin problemas. El script que contiene instrucciones SELECT o funciones de llamada y otros objetos de programación normalmente se realizará correctamente si el usuario que realiza la llamada tiene permisos suficientes.

> [!NOTE]
> De forma predeterminada [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] , está configurado para ejecutarse en **NT Service\MSSQLLaunchpad**, que se aprovisiona con todos los permisos necesarios para ejecutar scripts externos. Para obtener más información sobre las opciones configurables, vea [SQL Server Launchpad configuración del servicio](../security/sql-server-launchpad-service-account.md).

<a name="sqlrusergroup"></a>

## <a name="identities-used-in-processing-sqlrusergroup"></a>Identidades usadas en el procesamiento (SQLRUserGroup)

**SQLRUserGroup** (Grupo de usuarios restringidos de SQL) se crea al SQL Server el programa de instalación de y contiene un grupo de cuentas de usuario de Windows locales con pocos privilegios. Cuando se necesita un proceso externo, Launchpad toma una cuenta de trabajo disponible y la usa para ejecutar un proceso. Más concretamente, Launchpad activa una cuenta de trabajo disponible, la asigna a la identidad del usuario que realiza la llamada y ejecuta el script en la cuenta de trabajo.

+ **SQLRUserGroup** está vinculado a una instancia específica de. Se necesita un grupo de cuentas de trabajo independiente para cada instancia en la que se haya habilitado el aprendizaje automático. Las cuentas no se pueden compartir entre instancias.

+ El tamaño del grupo de cuentas de usuario es estático y el valor predeterminado es 20, que admite 20 sesiones simultáneas. El número de sesiones de tiempo de ejecución externas que se pueden iniciar simultáneamente está limitado por el tamaño de este grupo de cuentas de usuario. 

+ Los nombres de las cuentas de trabajo del grupo tienen el formato SQLInstanceName*nn*. Por ejemplo, en una instancia predeterminada, **SQLRUserGroup** contiene cuentas denominadas MSSQLSERVER01, MSSQLSERVER02 y así sucesivamente hasta MSSQLSERVER20.

Las tareas en paralelo no consumen cuentas adicionales. Por ejemplo, si un usuario ejecuta una tarea de puntuación que utiliza el procesamiento en paralelo, se reutiliza la misma cuenta de trabajo para todos los subprocesos. Si piensa hacer un uso intensivo del aprendizaje automático, puede aumentar el número de cuentas que se usan para ejecutar scripts externos. Para obtener más información, consulte [modificación del grupo de cuentas de usuario para machine learning](../../advanced-analytics/administration/modify-user-account-pool.md).

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
### <a name="appcontainer-isolation-in-sql-server-2019"></a>Aislamiento de AppContainer en SQL Server 2019

En SQL Server 2019, el programa de instalación ya no crea cuentas de trabajo para **SQLRUserGroup**. En su lugar, el aislamiento se logra a través de [AppContainers](https://docs.microsoft.com/windows/desktop/secauthz/appcontainer-isolation). En tiempo de ejecución, cuando se detecta un script externo en un procedimiento almacenado o una consulta, SQL Server llama a Launchpad con una solicitud para un iniciador específico de la extensión. Launchpad invoca el entorno en tiempo de ejecución adecuado en un proceso bajo su identidad y crea una instancia de un AppContainer para que lo contenga. Este cambio es beneficioso porque ya no se requiere la administración de cuentas y contraseñas locales. Además, en las instalaciones en las que están prohibidas las cuentas de usuario locales, la eliminación de la dependencia de la cuenta de usuario local significa que ahora puede usar esta característica.

Tal y como lo implementa SQL Server, AppContainers son un mecanismo interno. Aunque no verá evidencia física de AppContainers en el monitor de procesos, puede encontrarlos en reglas de Firewall de salida creadas por el programa de instalación para evitar que los procesos realicen llamadas de red. Para obtener más información, vea [configuración del firewall para SQL Server Machine Learning Services](../../advanced-analytics/security/firewall-configuration.md).

> [!Note]
> En SQL Server 2019, **SQLRUserGroup** solo tiene un miembro que ahora es la cuenta de servicio de SQL Server Launchpad única en lugar de varias cuentas de trabajo.
::: moniker-end

### <a name="permissions-granted-to-sqlrusergroup"></a>Permisos concedidos a SQLRUserGroup

De forma predeterminada, los miembros de **SQLRUserGroup** tienen permisos de lectura y ejecución en los archivos de los directorios de SQL Server **Binn**, **R_SERVICES**y **PYTHON_SERVICES** , con acceso a los ejecutables, las bibliotecas y los conjuntos de archivos integrados en R y las distribuciones de Python instaladas con SQL Server. 

Para proteger los recursos confidenciales en SQL Server, puede definir opcionalmente una lista de control de acceso (ACL) que deniegue el acceso a **SQLRUserGroup**. Por el contrario, también puede conceder permisos a los recursos de datos locales que existen en el equipo host, además de SQL Server mismo. 

Por diseño, **SQLRUserGroup** no tiene un inicio de sesión de base de datos ni permisos para ningún dato. En determinadas circunstancias, puede que desee crear un inicio de sesión para permitir las conexiones de bucle invertido, especialmente cuando una identidad de Windows de confianza es el usuario que realiza la llamada. Esta funcionalidad se denomina [*autenticación implícita*](#implied-authentication). Para obtener más información, vea [Agregar SQLRUserGroup como un usuario de base de datos](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md).

## <a name="identity-mapping"></a>Asignación de identidad

Cuando se inicia una sesión, Launchpad asigna la identidad del usuario que realiza la llamada a una cuenta de trabajo. La asignación de un usuario externo de Windows o un inicio de sesión de SQL válido a una cuenta de trabajo solo es válida para la duración del procedimiento almacenado de SQL que ejecuta el script externo. Las consultas en paralelo desde el mismo inicio de sesión se asignan a la misma cuenta de trabajo de usuario.

Durante la ejecución, Launchpad crea carpetas temporales para almacenar los datos de la sesión y se eliminan cuando finaliza la sesión. Los directorios tienen acceso restringido. Para R, RLauncher realiza esta tarea. En el caso de Python, PythonLauncher realiza esta tarea. Cada cuenta de trabajo individual está restringida a su propia carpeta y no puede tener acceso a los archivos de las carpetas situadas por encima de su propio nivel. Sin embargo, la cuenta de trabajo puede leer, escribir o eliminar elementos secundarios en la carpeta de trabajo de la sesión que se creó. Si es administrador del equipo, puede ver los directorios creados para cada proceso. Cada directorio se identifica mediante su GUID de sesión.

<a name="implied-authentication"></a>

## <a name="implied-authentication-loop-back-requests"></a>Autenticación implícita (solicitudes de bucle invertido)

La *autenticación implícita* describe el comportamiento de la solicitud de conexión en el que los procesos externos que se ejecutan como cuentas de trabajador con pocos privilegios se presentan como una identidad de usuario de confianza para SQL Server en las solicitudes de bucle invertido para los datos o las operaciones. Como concepto, la autenticación implícita es exclusiva de la autenticación de Windows, en SQL Server cadenas de conexión que especifican una conexión de confianza, en las solicitudes que se originan en procesos externos como el script de R o Python. A veces también se denomina *bucle*.

Las conexiones de confianza son factibles desde el script de R y Python, pero solo con una configuración adicional. En la arquitectura de extensibilidad, los procesos de R y Python se ejecutan en cuentas de trabajo, heredando los permisos del **SQLRUserGroup**primario. Cuando una cadena de conexión `Trusted_Connection=True`especifica, la identidad de la cuenta de trabajo se presenta en la solicitud de conexión, que se desconoce de forma predeterminada para SQL Server.

Para que las conexiones de confianza se realicen correctamente, debe crear un inicio de sesión de base de datos para **SQLRUserGroup**. Después de hacerlo, cualquier conexión de confianza de cualquier miembro de **SQLRUserGroup** tiene derechos de inicio de sesión en SQL Server. Para obtener instrucciones paso a paso, vea [Agregar SQLRUserGroup a un inicio de sesión de base de datos](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md).

Las conexiones de confianza no son la formulación más usada de una solicitud de conexión. Cuando el script de R o Python especifica una conexión, puede ser más común usar un inicio de sesión de SQL, o un nombre de usuario y una contraseña completos, si la conexión es a un origen de datos ODBC.

### <a name="how-implied-authentication-works-for-r-and-python-sessions"></a>Cómo funciona la autenticación implícita para sesiones de R y Python

En el diagrama siguiente se muestra la interacción de los componentes de SQL Server con el tiempo de ejecución de R y cómo realiza la autenticación implícita para R.

![Autenticación implícita para R](../security/media/implied-auth-rsql.png)

En el diagrama siguiente se muestra la interacción de los componentes de SQL Server con el tiempo de ejecución de Python y cómo realiza la autenticación implícita para Python.

![Autenticación implícita para Python](../security/media/implied-auth-python2.png)

## <a name="no-support-for-transparent-data-encryption-at-rest"></a>No se admiten Cifrado de datos transparente en reposo

[Cifrado de datos transparente (TDE)](../../relational-databases/security/encryption/transparent-data-encryption.md) no se admite para los datos enviados o recibidos desde el tiempo de ejecución del script externo. La razón es que el proceso externo (R o Python) se ejecuta fuera del proceso de SQL Server. Por lo tanto, los datos utilizados por el tiempo de ejecución externo no están protegidos por las características de cifrado del motor de base de datos. Este comportamiento no es diferente de cualquier otro cliente que se ejecute en el SQL Server equipo que lee los datos de la base de datos y realiza una copia.

Como consecuencia, TDE **no se** aplica a los datos que se usan en los scripts de R o Python, ni a los datos guardados en el disco, ni a los resultados intermedios persistentes. Sin embargo, todavía se aplican otros tipos de cifrado, como el cifrado de BitLocker de Windows o el cifrado de terceros en el nivel de archivo o carpeta.

En el caso de [Always Encrypted](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md), los tiempos de ejecución externos no tienen acceso a las claves de cifrado. Por lo tanto, no se pueden enviar datos a los scripts.

## <a name="next-steps"></a>Pasos siguientes

En este artículo, ha aprendido los componentes y el modelo de interacción de la arquitectura de seguridad integrada en el [marco](../../advanced-analytics/concepts/extensibility-framework.md)de extensibilidad. Los puntos clave que se describen en este artículo incluyen el propósito de las cuentas de Launchpad, SQLRUserGroup y Worker, el aislamiento de procesos de R y Python, y cómo se asignan las identidades de usuario a las cuentas de trabajo. 

Como paso siguiente, revise las instrucciones para [conceder permisos](../../advanced-analytics/security/user-permission.md). En el caso de los servidores que usan la autenticación de Windows, también debe revisar [Agregar SQLRUserGroup a un inicio de sesión de base de datos](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md) para obtener información cuando se requiere configuración adicional.