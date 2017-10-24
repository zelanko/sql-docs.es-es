---
title: "Información general sobre seguridad (SQL Server R Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/10/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8fc84754-7fbf-4c1b-9150-7d88680b3e68
caps.latest.revision: 9
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6ddfc3ccb67d017dc618cfbb7e7680c0164f3a21
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="security-overview"></a>Información general sobre seguridad

En este tema se describe la arquitectura de seguridad que se utiliza para conectar el [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] componentes de Python y motor de base de datos. Se proporcionan ejemplos del proceso de seguridad para dos escenarios comunes: ejecución de Python en SQL Server mediante un procedimiento almacenado y ejecutan Python con el servidor SQL Server como el contexto de proceso remoto.

## <a name="security-overview"></a>Información general sobre seguridad

Un [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] se requiere inicio de sesión o cuenta de usuario de Windows para ejecutar script de Python en SQL Server. Identifica la cuenta de inicio de sesión o usuario la *entidad de seguridad*, que debe tener permiso para tener acceso a la base de datos donde se recuperan los datos. Dependiendo de si el script de Python crea nuevos objetos o escribe nuevos datos, el usuario que tenga permisos para crear tablas, escribir datos, o crear funciones personalizadas o procedimientos almacenados.

Por lo tanto, es un requisito estricto que cada persona que ejecuta el código Python en [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] debe estar asignado a un inicio de sesión o la cuenta en la base de datos. Esta restricción se aplica independientemente de si se envía la secuencia de comandos desde un cliente de ciencia de datos remoto o se hayan iniciado mediante un procedimiento almacenado de T-SQL.

Por ejemplo, suponga que crea un script de Python que se ejecuta en su equipo portátil, y desea ejecutar ese código [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. Debe asegurarse de que se cumplan las condiciones siguientes:

+ La base de datos permite las conexiones remotas.
+ El inicio de sesión SQL o la cuenta de Windows que usa para el acceso de base de datos se ha agregado a la [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] en el nivel de instancia.
+ El inicio de sesión de SQL o el usuario de Windows deben tener permiso para ejecutar scripts externos. Por lo general, este permiso solo lo puede agregar un administrador de bases de datos.
+ El inicio de sesión SQL o el usuario de la ventana debe agregarse como un usuario con los permisos adecuados, en cada base de datos donde el script de Python para realizar cualquiera de estas operaciones:
    + Recuperar datos
    + Escribir o actualizar datos
    + Crear objetos como tablas o procedimientos almacenados

Después de que el inicio de sesión o la cuenta de usuario de Windows se ha aprovisionado y conceder los permisos necesarios, puede ejecutar código de Python en [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] mediante el uso de los objetos de origen de datos proporcionados por el **revoscalepy** biblioteca, o mediante una llamada a un procedimiento procedimiento que contiene el script de Python.

Cada vez que se inicia un script de Python desde [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], la seguridad del motor de base de datos obtiene el contexto de seguridad del usuario que inició el trabajo y administra las asignaciones del usuario o inicio de sesión a los objetos protegibles.

Por lo tanto, todos los scripts de Python que se inician desde un cliente remoto deben especificar la información de inicio de sesión o usuario como parte de la cadena de conexión.


## <a name="interaction-of-includessnoversionmdincludesssnoversion-mdmd-security-and-launchpad-security"></a>Interacción de la seguridad de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] y la seguridad de Launchpad

Cuando se ejecuta un script de Python en el contexto de la [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] equipo, el [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] servicio obtiene una cuenta de trabajo disponible (una cuenta de usuario local) desde un grupo de cuentas de trabajo establecido para los procesos externos y usa la cuenta de ese trabajo a realizar las tareas relacionadas.

Por ejemplo, suponga que se inicia un script de Python con sus credenciales de dominio de Windows. SQL Server obtendrá las credenciales y asignarla a una cuenta de trabajo Launchpad disponibles, como *SQLRUser01*.

> [!NOTE]
> El nombre del grupo de cuentas de trabajo es el mismo independientemente de si usas R o Python. Sin embargo, se crea un grupo independiente para cada instancia en el que habilite los idiomas externos.

Después de la asignación a una cuenta de trabajo, [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] crea un token de usuario que se usa para iniciar procesos. 

Cuando se completen todas las operaciones de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], la cuenta de trabajo de usuario se marcará como libre y se devolverá al grupo.

Para obtener más información acerca de [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)], consulte [nuevos componentes de SQL Server a la integración de compatibilidad con Python](../../advanced-analytics/python/new-components-in-sql-server-to-support-python-integration.md).

> [!NOTE]
> Para Launchpad administrar las cuentas de trabajo y ejecutar trabajos de Python, el grupo que contiene las cuentas de trabajo, *SQLRUserGroup*, debe tener permisos de "Permitir el registro local"; en caso contrario, no se puede iniciar el tiempo de ejecución de Python. De forma predeterminada, este derecho se concede a todos los nuevos usuarios locales, pero en algunas organizaciones puede que sea necesario más estrictas directivas de grupo, lo que evita las cuentas de trabajo de conectarse a SQL Server a los trabajos de Python.

## <a name="security-of-worker-accounts"></a>Seguridad de las cuentas de trabajo

La asignación de un usuario externo de Windows o inicio de sesión SQL válido para una cuenta de trabajo es válida únicamente para el procedimiento almacenado de la duración de la instrucción SQL que ejecuta el script de Python.

Las consultas en paralelo desde el mismo inicio de sesión se asignan a la misma cuenta de trabajo de usuario.

Los directorios que se usa para los procesos administrados por el [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)], y directorios son el acceso restringido. Para Python, PythonLauncher realiza esta tarea. Cada cuenta de trabajo individuales está restringido a su propia carpeta y no puede tener acceso a archivos en carpetas por encima de su propio nivel. Sin embargo, la cuenta del trabajador puede leer, escribir o eliminar a elementos secundarios en la carpeta de trabajo de la sesión que se creó.

Para obtener más información sobre cómo cambiar el número de cuentas de trabajo, los nombres de las cuentas o las contraseñas, vea [Modify the User Account Pool for SQL Server R Services](../../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md) (Modificar el grupo de cuentas de usuario para SQL Server R Services).


## <a name="security-isolation-for-multiple-external-scripts"></a>Aislamiento de seguridad para varios scripts externos

El mecanismo de aislamiento se basa en las cuentas de usuario físico. Cuando se inician los procesos satélite para el tiempo de ejecución de un lenguaje específico, cada tarea satélite usa la cuenta de trabajo especificada por [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]. Si una tarea requiere varios satélites, como en el caso de las consultas en paralelo, se usa una cuenta de trabajo única para todas las tareas relacionadas.

Ninguna cuenta de trabajo puede ver o manipular los archivos usados por otras cuentas de trabajo.

Si es administrador del equipo, puede ver los directorios creados para cada proceso. Cada directorio se identifica mediante su GUID de sesión.

## <a name="see-also"></a>Vea también

[Información general sobre la arquitectura](../../advanced-analytics/python/architecture-overview-sql-server-python.md)

