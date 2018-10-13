---
title: Seguridad para el aprendizaje automático de SQL Server | Microsoft Docs
description: Información general sobre la seguridad para el marco de extensibilidad en SQL Server Machine Learning Services. Seguridad para inicio de sesión y cuentas de usuario, el servicio Launchpad de SQL Server, cuentas de trabajo, que se ejecutan varias secuencias de comandos y los permisos de archivo.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/10/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: bee8e2162c56ac1b26273873943d848c2167dbda
ms.sourcegitcommit: 485e4e05d88813d2a8bb8e7296dbd721d125f940
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/11/2018
ms.locfileid: "49100406"
---
# <a name="security-overview-for-the-extensibility-framework-in-sql-server-machine-learning-services"></a>Información general de seguridad para el marco de extensibilidad en SQL Server Machine Learning Services

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo se describe la arquitectura general de seguridad que se usa para conectar el motor de base de datos de SQL Server y los componentes relacionados con el marco de extensibilidad. Describe las interacciones y componentes. 

<a name="launchpad"></a>

## <a name="sql-server-launchpad-service"></a>Servicio Launchpad de SQL Server

Para crear instancias de procesos externos, el motor de base de datos proporciona el servicio Launchpad de SQL Server para crear una sesión de R o Python. Otro [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] se crea la instancia del motor de base de datos a la que ha agregado integración de aprendizaje (R o Python) en SQL Server machine, un servicio por cada instancia de servicio.

De forma predeterminada, [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] está configurado para ejecutarse bajo **NT Service\MSSQLLaunchpad**, que se aprovisiona con todos los permisos necesarios para ejecutar scripts externos. Eliminación de los permisos de esta cuenta puede dar lugar a [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] no se pudo iniciar o para tener acceso a la instancia de SQL Server donde se deberían ejecutar scripts externos. Suele utilizarse como servicio LaunchPad-es, pero para obtener más información sobre las opciones configurables, consulte [configuración del servicio Launchpad de SQL Server](../security/sql-server-launchpad-service-account.md).

<a name="sqlrusergroup"></a>

## <a name="sqlrusergroup-and-worker-accounts"></a>Cuentas SQLRUserGroup y de trabajo

Ejecutan scripts externos en los procesos externos, bajo la identidad de cuentas de trabajo local con privilegios mínimos, sujeto a la lista de control de acceso (ACL) del elemento primario **SQLRUserGroup** (grupo de usuarios restringidos de SQL). 

**SQLRUserGroup** creado por el programa de instalación de SQL Server y contiene el grupo de cuentas de usuario de Windows locales. Cuando se necesita un proceso externo, Launchpad toma una cuenta de trabajo disponible y lo usa para ejecutar un proceso. Más concretamente, Launchpad activa una cuenta de trabajo disponible, lo asigna a la identidad del usuario que realiza la llamada y ejecuta el script con la cuenta de trabajo. 

+ **SQLRUserGroup** está vinculada a una instancia específica. Se necesita un grupo de cuentas de trabajo independiente para cada instancia de en qué equipo se ha habilitado el aprendizaje. Las cuentas no se pueden compartir entre instancias.

+ El tamaño del grupo de cuentas de usuario es estático y el valor predeterminado es 20, que es compatible con 20 sesiones simultáneas. El número de sesiones de tiempo de ejecución externos que se puede iniciar de forma simultánea está limitado por el tamaño de este grupo de cuentas de usuario. 

+ Los nombres de cuenta de trabajo en el grupo de tienen el formato Nombredeinstanciasql*nn*. Por ejemplo, en una instancia predeterminada, **SQLRUserGroup** contiene cuentas denominadas MSSQLSERVER01, MSSQLSERVER02 y así sucesivamente hasta MSSQLSERVER20.

Tareas en paralelo no consumen cuentas adicionales. Por ejemplo, si un usuario ejecuta una tarea de puntuación que se usa el procesamiento paralelo, se reutiliza la misma cuenta de trabajo para todos los subprocesos. Si piensa hacer un uso intensivo del aprendizaje automático, puede aumentar el número de cuentas utilizadas para ejecutar scripts externos. Para obtener más información, consulte [modificar el grupo de cuentas de usuario para el aprendizaje automático](../../advanced-analytics/administration/modify-user-account-pool.md).

### <a name="permissions-granted-to-sqlrusergroup"></a>Permisos concedidos a SQLRUserGroup

De forma predeterminada, los miembros de **SQLRUserGroup** dispone de lectura y escritura en archivos de SQL Server **Binn**, **R_SERVICES**, y **PYTHON_SERVICES** directorios, con acceso a los archivos ejecutables, bibliotecas y los conjuntos de datos integrados en las distribuciones de R y Python que se instala con SQL Server. 

Para proteger los recursos confidenciales en SQL Server, puede definir opcionalmente una lista de control de acceso (ACL) que se deniega el acceso a **SQLRUserGroup**. A la inversa, también puede conceder permisos a los recursos de datos local que existen en el equipo host, además del propio SQL Server. 

Por diseño, **SQLRUserGroup** no tiene permisos para todos los datos o un inicio de sesión de base de datos. En determinadas circunstancias, es posible que desea crear un inicio de sesión para permitir conexiones de retroceso de bucle, especialmente cuando una identidad de Windows de confianza es el usuario que realiza la llamada. Esta funcionalidad se denomina [ *autenticación implícita*](#implied-authentication). Para obtener más información, consulte [agregar SQLRUserGroup como un usuario de base de datos](../../advanced-analytics/security/add-sqlrusergroup-to-database.md).

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
### <a name="appcontainer-isolation-in-sql-server-2019"></a>Aislamiento de AppContainer en SQL Server 2019

En SQL Server 2019, el programa de instalación ya no crea cuentas de trabajo para **SQLRUserGroup**. En su lugar, se logra el aislamiento a través de [AppContainers](https://docs.microsoft.com/windows/desktop/secauthz/appcontainer-isolation). En tiempo de ejecución, cuando se detecta código o script incrustado en un procedimiento almacenado o una consulta, SQL Server llama a Launchpad con una solicitud para un iniciador específica de la extensión. LaunchPad invoca el entorno adecuado en tiempo de ejecución en un proceso bajo su identidad y crea una instancia de un AppContainer que lo contiene. Este cambio es beneficiosa porque ya no es necesaria la administración local de cuenta y la contraseña. Además, en las instalaciones donde las cuentas de usuario local están prohibidas, eliminación de la dependencia de la cuenta de usuario local significa que ahora puede usar esta característica.

Como se implementa mediante SQL Server, AppContainers son un mecanismo interno. Aunque no verá las evidencias físicas de AppContainers en el Monitor de proceso, se puede encontrar en las reglas de firewall de salida creadas por el programa de instalación para evitar que los procesos de realizar llamadas de red.

> [!Note]
> En SQL Server 2019, **SQLRUserGroup** solo tiene un miembro que ahora es la única cuenta de servicio Launchpad de SQL Server en lugar de varias cuentas de trabajo.
::: moniker-end

## <a name="user-security"></a>Seguridad del usuario

Modelo de seguridad de datos de SQL Server de inicios de sesión de base de datos y funciones amplían al script de R y Python. Los inicios de sesión de base de datos pueden basarse en las identidades de Windows o un usuario de base de datos de SQL Server. 

Como un usuario de base de datos, si tiene permisos para ejecutar una consulta determinada, cualquier script de R o Python que se ejecuta en SQL Server también tiene permiso para recuperar los mismos datos. La capacidad de consumir, crear y guardar la base de datos de objetos depende de los permisos de base de datos. Para obtener más información, consulte [conceder a los usuarios permiso para SQL Server Machine Learning Services](../../advanced-analytics/security/user-permission.md).

### <a name="mapping-user-identities-to-worker-accounts"></a>Asignación de identidades de usuario a cuentas de trabajo

Cuando se inicia una sesión, Launchpad asigna la identidad del usuario que realiza la llamada a una cuenta de trabajo. La asignación de un usuario externo de Windows o inicio de sesión SQL válido para una cuenta de trabajo es válida únicamente para el procedimiento almacenado de la duración de la instrucción SQL que ejecuta el script externo. Las consultas en paralelo desde el mismo inicio de sesión se asignan a la misma cuenta de trabajo de usuario.

Durante la ejecución, Launchpad crea las carpetas temporales para almacenar datos de la sesión, eliminándolos cuando finaliza la sesión. Los directorios son de acceso restringido. Para R, RLauncher realiza esta tarea. Para Python, PythonLauncher realiza esta tarea. Cada cuenta de trabajo individuales está restringido a su propia carpeta y no puede tener acceso a archivos en carpetas por encima de su propio nivel. Sin embargo, la cuenta de trabajo puede leer, escribir o eliminar a elementos secundarios en la carpeta de trabajo de la sesión que se creó. Si es administrador del equipo, puede ver los directorios creados para cada proceso. Cada directorio se identifica mediante su GUID de sesión.

<a name="implied-authentication"></a>

### <a name="implied-authentication"></a>Autenticación implícita

*Autenticación implícita* describe el comportamiento de solicitud de conexión en la que los procesos externos que se ejecutan como cuentas de trabajo con privilegios bajos se presentan como una identidad de usuario de confianza a SQL Server en bucle espera las solicitudes de datos o las operaciones. Como concepto, autenticación implícita es única para la autenticación de Windows, en las cadenas de conexión de SQL Server especificando una conexión de confianza en las solicitudes que se originan desde procesos externos como script de R o Python. A veces también se conoce como un *realizamos otro bucle*.

Las conexiones de confianza son factibles desde un script de R y Python, pero solo con una configuración adicional. En la arquitectura de extensibilidad, los procesos de R y Python se ejecutan en cuentas de trabajo, hereda los permisos del elemento primario **SQLRUserGroup**. Cuando se especifica una cadena de conexión "Trusted_Connection = True", la identidad de la cuenta de trabajo se presenta en la solicitud de conexión, que se conoce de forma predeterminada para SQL Server. 

Para facilitar las conexiones de confianza correcta, se debe crear un inicio de sesión de base de datos para el **SQLRUserGroup**. Una vez hecho esto, cualquier conexión de cualquier miembro de confianza **SQLRUserGroup** tiene derechos de inicio de sesión para SQL Server. Para obtener instrucciones detalladas, consulte [agregar SQLRUserGroup para un inicio de sesión de base de datos](../../advanced-analytics/security/add-sqlrusergroup-to-database.md).

Las conexiones de confianza no son la formulación de una solicitud de conexión utilizada más comúnmente. Cuando el script de R o Python especifica una conexión, puede ser más habitual utilizar un inicio de sesión SQL, o un nombre de usuario completamente especificada y una contraseña si la conexión es a un origen de datos ODBC.

#### <a name="how-implied-authentication-works-for-r-and-python-sessions"></a>Implícito en cómo funciona la autenticación para las sesiones de R y Python

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

Como paso siguiente, revise las instrucciones para [conceder permisos](../../advanced-analytics/security/user-permission.md). Para los servidores que usan la autenticación de Windows, también debe revisar [agregar SQLRUserGroup para un inicio de sesión de base de datos](../../advanced-analytics/security/add-sqlrusergroup-to-database.md) para obtener información sobre cuándo se requiere configuración adicional.