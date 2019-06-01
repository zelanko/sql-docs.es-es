---
title: 'Información general de seguridad para las extensiones de R y Python: SQL Server Machine Learning'
description: Información general sobre la seguridad para el marco de extensibilidad en SQL Server Machine Learning Services. Seguridad para inicio de sesión y cuentas de usuario, el servicio Launchpad de SQL Server, cuentas de trabajo, que se ejecutan varias secuencias de comandos y los permisos de archivo.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 1f19e3322b8aee78fdb5a76a29a719148cc6a0c7
ms.sourcegitcommit: 944af0f6b31bf07c861ddd4d7960eb7f018be06e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/31/2019
ms.locfileid: "66454541"
---
# <a name="security-overview-for-the-extensibility-framework-in-sql-server-machine-learning-services"></a>Información general de seguridad para el marco de extensibilidad en SQL Server Machine Learning Services

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo se describe la arquitectura general de seguridad que se utiliza para integrar el motor de base de datos de SQL Server y los componentes relacionados con el marco de extensibilidad. Examina los elementos protegibles, servicios, identidad de proceso y permisos. Para obtener más información sobre los conceptos clave y los componentes de extensibilidad en SQL Server, vea [arquitectura de extensibilidad en SQL Server Machine Learning Services](extensibility-framework.md)].

## <a name="securables-for-external-script"></a>Elementos protegibles de scripts externos

Un script externo escrito en R o Python se envía como un parámetro de entrada a un [procedimiento almacenado del sistema](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) creado para este propósito, o se encapsula en un procedimiento almacenado que defina. Como alternativa, podría tener modelos previamente entrenados y almacenados en un formato binario en una tabla de base de datos, que se puede llamar en un T-SQL [PREDICT](../../t-sql/queries/predict-transact-sql.md) función.

Como el script se proporciona a través de los objetos de esquema de base de datos existente, tablas y procedimientos almacenados, hay nuevas no [elementos protegibles](../../relational-databases/security/securables.md) para SQL Server Machine Learning Services.

Independientemente de cómo se usa la secuencia de comandos, o bien, están formados, se creará y probablemente se guardan los objetos de base de datos, pero no se introduce ningún nuevo tipo de objeto para almacenar la secuencia de comandos. Como resultado, la capacidad de consumir, crear y guardar la base de datos de objetos depende en gran medida de los permisos de base de datos ya definidos para los usuarios.

<a name="permissions"></a>

## <a name="permissions"></a>Permisos

Modelo de seguridad de datos de SQL Server de inicios de sesión de base de datos y funciones amplían al script de R y Python. Se requiere un inicio de sesión de SQL Server o la cuenta de usuario de Windows para ejecutar scripts externos que usan datos de SQL Server o que se ejecutan con SQL Server como el contexto de cálculo. Usuarios de base de datos que tienen permisos para ejecutar una consulta ad hoc pueden tener acceso a los mismos datos desde el script de R o Python.

La cuenta de inicio de sesión o usuario identifica la *entidad de seguridad*, que puedan necesitar varios niveles de acceso, según los requisitos de script externo:

+ Permiso para acceder a la base de datos donde están habilitados los scripts externos.
+ Permisos para leer datos de objetos protegidos, como tablas.
+ La capacidad de escribir nuevos datos en una tabla, como un modelo o los resultados de puntuación.
+ La capacidad para crear nuevos objetos, como tablas, procedimientos almacenados que use el script externo, o las funciones personalizadas que el uso de R o trabajo de Python.
+ Derecho a instalar nuevos paquetes en el equipo de SQL Server, o usar paquetes proporcionados a un grupo de usuarios.

Cada persona que ejecuta un script externo mediante SQL Server como el contexto de ejecución debe asignarse a un usuario en la base de datos. En lugar de individualmente conjunto base de datos permisos de usuario, puede crear roles para administrar conjuntos de permisos y asignar a usuarios a esos roles, en lugar de establecer permisos de usuario de forma individual.

Para obtener más información, consulte [conceder a los usuarios permiso para SQL Server Machine Learning Services](../../advanced-analytics/security/user-permission.md).

## <a name="permissions-when-using-an-external-client-tool"></a>Permisos cuando se usa una herramienta cliente externo

Los usuarios que usan R o Python en una herramienta cliente externo deben tener su inicio de sesión o cuenta asignada a un usuario en la base de datos si es necesario ejecutar un script externo en bases de datos, o datos y objetos de base de datos de access. Los mismos permisos son necesarios si se envía la secuencia de comandos externo desde un cliente de ciencia de datos remoto o ejecutan mediante un procedimiento almacenado de T-SQL.

Por ejemplo, suponga que ha creado un script externo que se ejecuta en el equipo local, y desea que se ejecute el script en SQL Server. Debe asegurarse de que se cumplan las condiciones siguientes:

+ La base de datos permite las conexiones remotas.
+ Se agregó el inicio de sesión SQL o la cuenta de Windows que usa para el acceso a la base de datos a SQL Server en el nivel de instancia.
+ El inicio de sesión SQL o el usuario de Windows debe tener el permiso para ejecutar scripts externos. Por lo general, este permiso solo lo puede agregar un administrador de bases de datos.
+ El inicio de sesión SQL o el usuario de la ventana debe agregarse como un usuario con los permisos adecuados en cada base de datos donde la secuencia de comandos externa lleva a cabo cualquiera de estas operaciones:
  + Recuperación de datos.
  + Escribir o actualizar datos.
  + Crear nuevos objetos, como tablas o procedimientos almacenados.

El inicio de sesión o cuenta de usuario de Windows una vez aprovisionado y tengan los permisos necesarios, puede ejecutar un script externo en SQL Server mediante el uso de un objeto de origen de datos en R o **revoscalepy** biblioteca de Python, o mediante una llamada a un procedimiento procedimiento que contiene el script externo.

Cada vez que se inicia un script externo desde SQL Server, la seguridad del motor de base de datos obtiene el contexto de seguridad del usuario que inició el trabajo y administra las asignaciones del usuario o inicio de sesión a objetos protegibles.

Por lo tanto, todos los scripts externos que se inician desde un cliente remoto deben especificar la información de inicio de sesión o usuario como parte de la cadena de conexión.

<a name="launchpad"></a>

## <a name="services-used-in-external-processing-launchpad"></a>Servicios que se usan en el procesamiento externo (Launchpad)

El marco de extensibilidad agrega un nuevo servicio de NT para el [lista de servicios](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md#Service_Details) en una instalación de SQL Server: [**SQL Server Launchpad (MSSSQLSERVER)** ](extensibility-framework.md#launchpad).

El motor de base de datos, usa el servicio Launchpad de SQL Server para crear instancias de una sesión de R o Python como un proceso independiente. El proceso se ejecuta bajo una cuenta con pocos privilegios; distinto de SQL Server, Launchpad propio y la identidad del usuario en la que se ejecutó la consulta de host o el procedimiento almacenada. Ejecutar script en un proceso independiente, bajo cuenta con pocos privilegios, es la base del modelo de seguridad y aislamiento para R y Python en SQL Server.

Además de iniciar los procesos externos, Launchpad también es responsable de seguimiento de la identidad del usuario que realiza la llamada y se asigna esa identidad para la cuenta de trabajo con pocos privilegios usada para iniciar el proceso. En algunos escenarios, donde un script o código devuelva la llamada a SQL Server para los datos y las operaciones, Launchpad es normalmente capaz de administrar la transferencia de identidad sin problemas. Script que contiene las instrucciones SELECT o llamar a funciones y otros objetos de programación normalmente se realizará correctamente si el usuario que realiza la llamada tiene permisos suficientes.

> [!NOTE]
> De forma predeterminada, [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] está configurado para ejecutarse bajo **NT Service\MSSQLLaunchpad**, que se aprovisiona con todos los permisos necesarios para ejecutar scripts externos. Para obtener más información sobre las opciones configurables, consulte [configuración del servicio Launchpad de SQL Server](../security/sql-server-launchpad-service-account.md).

<a name="sqlrusergroup"></a>

## <a name="identities-used-in-processing-sqlrusergroup"></a>Identidades que se usan en el procesamiento (SQLRUserGroup)

**SQLRUserGroup** (grupo de usuarios restringidos de SQL) se crea el programa de instalación de SQL Server y contiene un grupo de cuentas de usuario de Windows locales con pocos privilegios. Cuando se necesita un proceso externo, Launchpad toma una cuenta de trabajo disponible y lo usa para ejecutar un proceso. Más concretamente, Launchpad activa una cuenta de trabajo disponible, lo asigna a la identidad del usuario que realiza la llamada y ejecuta el script con la cuenta de trabajo.

+ **SQLRUserGroup** está vinculada a una instancia específica. Se necesita un grupo de cuentas de trabajo independiente para cada instancia de en qué equipo se ha habilitado el aprendizaje. Las cuentas no se pueden compartir entre instancias.

+ El tamaño del grupo de cuentas de usuario es estático y el valor predeterminado es 20, que es compatible con 20 sesiones simultáneas. El número de sesiones de tiempo de ejecución externos que se puede iniciar de forma simultánea está limitado por el tamaño de este grupo de cuentas de usuario. 

+ Los nombres de cuenta de trabajo en el grupo de tienen el formato Nombredeinstanciasql*nn*. Por ejemplo, en una instancia predeterminada, **SQLRUserGroup** contiene cuentas denominadas MSSQLSERVER01, MSSQLSERVER02 y así sucesivamente hasta MSSQLSERVER20.

Tareas en paralelo no consumen cuentas adicionales. Por ejemplo, si un usuario ejecuta una tarea de puntuación que se usa el procesamiento paralelo, se reutiliza la misma cuenta de trabajo para todos los subprocesos. Si piensa hacer un uso intensivo del aprendizaje automático, puede aumentar el número de cuentas utilizadas para ejecutar scripts externos. Para obtener más información, consulte [modificar el grupo de cuentas de usuario para el aprendizaje automático](../../advanced-analytics/administration/modify-user-account-pool.md).

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
### <a name="appcontainer-isolation-in-sql-server-2019"></a>Aislamiento de AppContainer en SQL Server 2019

En SQL Server 2019, el programa de instalación ya no crea cuentas de trabajo para **SQLRUserGroup**. En su lugar, se logra el aislamiento a través de [AppContainers](https://docs.microsoft.com/windows/desktop/secauthz/appcontainer-isolation). En tiempo de ejecución, cuando se detecta un script externo en un procedimiento almacenado o una consulta, SQL Server llama a Launchpad con una solicitud para un iniciador específica de la extensión. LaunchPad invoca el entorno adecuado en tiempo de ejecución en un proceso bajo su identidad y crea una instancia de un AppContainer que lo contiene. Este cambio es beneficiosa porque ya no es necesaria la administración local de cuenta y la contraseña. Además, en las instalaciones donde las cuentas de usuario local están prohibidas, eliminación de la dependencia de la cuenta de usuario local significa que ahora puede usar esta característica.

Como se implementa mediante SQL Server, AppContainers son un mecanismo interno. Aunque no verá las evidencias físicas de AppContainers en el Monitor de proceso, se puede encontrar en las reglas de firewall de salida creadas por el programa de instalación para evitar que los procesos de realizar llamadas de red. Para obtener más información, consulte [configuración de Firewall para SQL Server Machine Learning Services](../../advanced-analytics/security/firewall-configuration.md).

> [!Note]
> En SQL Server 2019, **SQLRUserGroup** solo tiene un miembro que ahora es la única cuenta de servicio Launchpad de SQL Server en lugar de varias cuentas de trabajo.
::: moniker-end

### <a name="permissions-granted-to-sqlrusergroup"></a>Permisos concedidos a SQLRUserGroup

De forma predeterminada, los miembros de **SQLRUserGroup** dispone de lectura y escritura en archivos de SQL Server **Binn**, **R_SERVICES**, y **PYTHON_SERVICES** directorios, con acceso a los archivos ejecutables, bibliotecas y los conjuntos de datos integrados en las distribuciones de R y Python que se instala con SQL Server. 

Para proteger los recursos confidenciales en SQL Server, puede definir opcionalmente una lista de control de acceso (ACL) que se deniega el acceso a **SQLRUserGroup**. A la inversa, también puede conceder permisos a los recursos de datos local que existen en el equipo host, además del propio SQL Server. 

Por diseño, **SQLRUserGroup** no tiene permisos para todos los datos o un inicio de sesión de base de datos. En determinadas circunstancias, es posible que desea crear un inicio de sesión para permitir conexiones de retroceso de bucle, especialmente cuando una identidad de Windows de confianza es el usuario que realiza la llamada. Esta funcionalidad se denomina [ *autenticación implícita*](#implied-authentication). Para obtener más información, consulte [agregar SQLRUserGroup como un usuario de base de datos](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md).

## <a name="identity-mapping"></a>Asignación de identidades

Cuando se inicia una sesión, Launchpad asigna la identidad del usuario que realiza la llamada a una cuenta de trabajo. La asignación de un usuario externo de Windows o inicio de sesión SQL válido para una cuenta de trabajo es válida únicamente para el procedimiento almacenado de la duración de la instrucción SQL que ejecuta el script externo. Las consultas en paralelo desde el mismo inicio de sesión se asignan a la misma cuenta de trabajo de usuario.

Durante la ejecución, Launchpad crea las carpetas temporales para almacenar datos de la sesión, eliminándolos cuando finaliza la sesión. Los directorios son de acceso restringido. Para R, RLauncher realiza esta tarea. Para Python, PythonLauncher realiza esta tarea. Cada cuenta de trabajo individuales está restringido a su propia carpeta y no puede tener acceso a archivos en carpetas por encima de su propio nivel. Sin embargo, la cuenta de trabajo puede leer, escribir o eliminar a elementos secundarios en la carpeta de trabajo de la sesión que se creó. Si es administrador del equipo, puede ver los directorios creados para cada proceso. Cada directorio se identifica mediante su GUID de sesión.

<a name="implied-authentication"></a>

## <a name="implied-authentication-loop-back-requests"></a>Autenticación implícita (bucle espera solicitudes)

*Autenticación implícita* describe el comportamiento de solicitud de conexión en la que los procesos externos que se ejecutan como cuentas de trabajo con privilegios bajos se presentan como una identidad de usuario de confianza a SQL Server en bucle espera las solicitudes de datos o las operaciones. Como concepto, autenticación implícita es única para la autenticación de Windows, en las cadenas de conexión de SQL Server especificando una conexión de confianza en las solicitudes que se originan desde procesos externos como script de R o Python. A veces también se conoce como un *realizamos otro bucle*.

Las conexiones de confianza son factibles desde un script de R y Python, pero solo con una configuración adicional. En la arquitectura de extensibilidad, los procesos de R y Python se ejecutan en cuentas de trabajo, hereda los permisos del elemento primario **SQLRUserGroup**. Cuando se especifica una cadena de conexión `Trusted_Connection=True`, la identidad de la cuenta de trabajo se presenta en la solicitud de conexión, que se conoce de forma predeterminada para SQL Server.

Para facilitar las conexiones de confianza correcta, se debe crear un inicio de sesión de base de datos para el **SQLRUserGroup**. Una vez hecho esto, cualquier conexión de cualquier miembro de confianza **SQLRUserGroup** tiene derechos de inicio de sesión para SQL Server. Para obtener instrucciones detalladas, consulte [agregar SQLRUserGroup para un inicio de sesión de base de datos](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md).

Las conexiones de confianza no son la formulación de una solicitud de conexión utilizada más comúnmente. Cuando el script de R o Python especifica una conexión, puede ser más habitual utilizar un inicio de sesión SQL, o un nombre de usuario completamente especificada y una contraseña si la conexión es a un origen de datos ODBC.

### <a name="how-implied-authentication-works-for-r-and-python-sessions"></a>Implícito en cómo funciona la autenticación para las sesiones de R y Python

El siguiente diagrama muestra la interacción de componentes de SQL Server con el tiempo de ejecución de R y cómo lo hace la autenticación implícita para R.

![Autenticación implícita para R](../security/media/implied-auth-rsql.png)

El diagrama siguiente muestra la interacción de componentes de SQL Server con el tiempo de ejecución de Python y cómo lo hace la autenticación implícita para Python.

![Autenticación implícita para Python](../security/media/implied-auth-python2.png)

## <a name="no-support-for-transparent-data-encryption-at-rest"></a>No se admite el cifrado transparente de datos en reposo

[Cifrado de datos transparente (TDE)](../../relational-databases/security/encryption/transparent-data-encryption.md) no es compatible con los datos enviados o recibidos desde el tiempo de ejecución de scripts externos. El motivo es que el proceso externo (R o Python) se ejecuta fuera del proceso de SQL Server. Por lo tanto, los datos utilizados por el tiempo de ejecución externo no está protegidos por las características de cifrado del motor de base de datos. Este comportamiento es similar a cualquier otro cliente que se ejecutan en el equipo de SQL Server que lee datos de la base de datos y realiza una copia.

Como consecuencia, TDE **no** aplicar a todos los datos que se utilice en scripts de R o Python, o a ningún dato guardado en disco, o en ningún resultado intermedio persistente. Sin embargo, otros tipos de cifrado, como el cifrado de BitLocker de Windows o de terceros que se aplicarán en el nivel de archivo o carpeta, todavía se aplican.

En el caso de [Always Encrypted](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md), tiempos de ejecución externos no tienen acceso a las claves de cifrado. Por lo tanto, no se puede enviar datos a las secuencias de comandos.

## <a name="next-steps"></a>Pasos siguientes

En este artículo, ha aprendido los componentes y modelo de interacción de la arquitectura de seguridad integradas en el [marco de extensibilidad](../../advanced-analytics/concepts/extensibility-framework.md). Puntos clave tratados en este artículo incluyen el propósito de las cuentas de Launchpad, SQLRUserGroup y de trabajo, el aislamiento de procesos de R y Python, y cómo se asignan las identidades de usuario a las cuentas de trabajo. 

Como paso siguiente, revise las instrucciones para [conceder permisos](../../advanced-analytics/security/user-permission.md). Para los servidores que usan la autenticación de Windows, también debe revisar [agregar SQLRUserGroup para un inicio de sesión de base de datos](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md) para obtener información sobre cuándo se requiere configuración adicional.