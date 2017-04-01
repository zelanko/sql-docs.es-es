---
title: "Informaci&#243;n general sobre seguridad (SQL Server R Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/10/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8fc84754-7fbf-4c1b-9150-7d88680b3e68
caps.latest.revision: 9
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 7
---
# Informaci&#243;n general sobre seguridad (SQL Server R Services)

Este tema describe la arquitectura de seguridad general que se utiliza para conectar el [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] motor y componentes relacionados con el tiempo de ejecución de R de la base de datos. Se proporcionan ejemplos del proceso de seguridad en dos escenarios comunes para el uso de R en un entorno empresarial:

+ Ejecutar funciones de RevoScaleR en [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] desde un cliente de ciencia de datos
+ Ejecutar R directamente desde [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] mediante procedimientos almacenados

## Información general sobre seguridad

Un [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Inicio de sesión o cuenta de usuario de Windows se requiere para ejecutar todos los trabajos de R que utilizan [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)]. La cuenta de inicio de sesión o usuario identifica la *entidad de seguridad*, que debe tener permiso de acceso a la base de datos donde se ejecuta R, así como permisos para leer datos de objetos protegidos, como tablas, o para escribir nuevos datos o agregar nuevos objetos si es necesario por el trabajo de R.

Por lo tanto, es un requisito estricto que cada persona que ejecuta el código R en [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] debe estar asignado a un inicio de sesión en la base de datos, independientemente de si ese código se envía desde un cliente de ciencia de datos remoto mediante las funciones de RevoScaleR o iniciado mediante un procedimiento almacenado de T-SQL. 

Por ejemplo, suponga que ha creado algún código de R que se ejecuta en el equipo portátil y desea ejecutar ese código [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. Debe asegurarse de que se cumplen las condiciones siguientes:

+ La base de datos permite conexiones remotas.
+ Se ha agregado un inicio de sesión SQL con el nombre y la contraseña que utilizó en el código R a la [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] en el nivel de instancia. O bien, si utiliza la autenticación integrada de Windows, el usuario de Windows especificado en la cadena de conexión debe agregarse como un usuario de la instancia.
+ El inicio de sesión SQL o el usuario de Windows debe tener el permiso para ejecutar scripts externos. Por lo general, este permiso sólo puede agregarse por un administrador de base de datos.
+ El inicio de sesión SQL o el usuario de la ventana debe agregarse como un usuario con los permisos adecuados en cada base de datos donde el trabajo de R realiza cualquiera de estas operaciones:
    + Recuperar datos
    + Escribir o actualizar datos 
    + Creación de nuevos objetos, como tablas o procedimientos almacenados

El inicio de sesión o la cuenta de usuario de Windows una vez aprovisionada y los permisos necesarios, puede ejecutar código R en [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] mediante un objeto de origen de datos de R o llamar a procedimientos almacenados. Cada vez que se inicia R desde [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], la seguridad del motor de base de datos obtiene el contexto de seguridad del usuario que inició el trabajo de R y administra las asignaciones del usuario o inicio de sesión a objetos asegurables. 

Por lo tanto, todos los trabajos de R que se inician desde un cliente remoto deben especificar la información de inicio de sesión o usuario como parte de la cadena de conexión.


## Interacción de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] seguridad y LaunchPad

Cuando se ejecuta un script de R en el contexto de la [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] equipo, el [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] servicio obtiene una cuenta de trabajo disponibles (una cuenta de usuario local) de un grupo de cuentas de trabajo establecido para el proceso externo y utiliza esa cuenta de trabajo para realizar las tareas relacionadas. 

Por ejemplo, si inicia un trabajo de R en sus credenciales de dominio de Windows, la cuenta podría asignarse a la cuenta de trabajo Launchpad *SQLRUser01*.

Después de la asignación a una cuenta de trabajo, [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] crea un token de usuario que se usa para iniciar procesos. 

Cuando todos los [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] operaciones se hayan completado, la cuenta de trabajo de usuario se marca como libres y devuelve al grupo.

Para obtener más información sobre [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)], consulte [nuevos componentes de SQL Server para la integración R](../../advanced-analytics/r-services/new-components-in-sql-server-to-support-r-services.md).

## Seguridad de las cuentas de trabajo
Esta asignación de un usuario externo de Windows o inicio de sesión SQL válido para una cuenta de trabajo es válida sólo para la duración de la duración de la consulta SQL que se ejecuta el script de R. 

Las consultas en paralelo desde el mismo inicio de sesión se asignan a la misma cuenta de trabajo.

Los directorios que se usa para los procesos administrados por el [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] mediante RLauncher, y directorios son de acceso restringido. La cuenta de trabajo no puede tener acceso a los archivos de carpetas por encima de su propio, pero puede leer, escribir o eliminar a elementos secundarios bajo la carpeta de trabajo de la sesión que creó para la consulta SQL con el script de R.

Para obtener más información acerca de cómo cambiar el número de cuentas de trabajo, los nombres de cuentas o contraseñas de cuentas, consulte [modificar el grupo de la cuenta de usuario de servicios de SQL Server R](../../advanced-analytics/r-services/modify-the-user-account-pool-for-sql-server-r-services.md).


## Aislamiento de seguridad para varios Scripts externos

El mecanismo de aislamiento se basa en las cuentas de usuario físico. Cuando se inician los procesos de satélite en tiempo de ejecución de un idioma específico, cada tarea de satélite usa la cuenta de trabajo especificada por el [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]. Si una tarea requiere varios satélites, por ejemplo, en el caso de las consultas en paralelo, se usa una cuenta de trabajo único para todas las tareas relacionadas.

Ninguna cuenta de trabajo puede ver o manipular los archivos utilizados por otras cuentas de trabajo.
 
Si es administrador en el equipo, puede ver los directorios creados para cada proceso. Cada directorio se identifica mediante su GUID de sesión.

## Vea también
[Información general sobre la arquitectura](../../advanced-analytics/r-services/architecture-overview-sql-server-r-services.md)