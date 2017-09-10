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
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8388d7c9d22a49a49a1a45a6fa6b479107f9ccae
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="security-overview-sql-server-r-services"></a>Información general sobre seguridad (SQL Server R Services)

En este tema se describe la arquitectura de seguridad general que se usa para conectar el motor de base de datos de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] y los componentes relacionados con el tiempo de ejecución de R. Se proporcionan ejemplos del proceso de seguridad para dos escenarios comunes al usar R en un entorno empresarial:

+ Ejecutar funciones de RevoScaleR en [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] desde un cliente de ciencia de datos
+ Ejecutar R directamente desde [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] mediante procedimientos almacenados

## <a name="security-overview"></a>Información general sobre seguridad

Un [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] se requiere inicio de sesión o cuenta de usuario de Windows para ejecutar scripts de R que usan datos de SQL Server o que se ejecutan con SQL Server como el contexto de proceso. Este requisito se aplica a los [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] y servicios de aprendizaje de máquina de SQL Server de 2017. 

Identifica la cuenta de inicio de sesión o usuario la *entidad de seguridad*, que puedan necesitar varios niveles de acceso, según los requisitos de script de R:
+ Permiso de acceso a la base de datos donde está habilitada la R
+ Permisos para leer datos de objetos protegidos, como las tablas
+ La capacidad para escribir nuevos datos a una tabla, por ejemplo, un modelo o resultados de puntuación
+ La capacidad para crear nuevos objetos, como tablas, procedimientos almacenados que utilice un script de R o personalizar las funciones que use R el trabajo
+ El derecho para instalar nuevos paquetes en el equipo de SQL Server o en paquetes de R de uso proporcionados a un grupo de usuarios. 

Por lo tanto, cada persona que ejecuta el código de R con [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] como la ejecución del contexto debe estar asignado a un inicio de sesión en la base de datos. Con la seguridad de SQL Server, es generalmente más fácil crear roles para administrar conjuntos de permisos y asignar a usuarios a esos roles, en lugar de establecer permisos de usuario de forma individual. 

Por ejemplo, suponga que ha creado algún código de R que se ejecuta en su equipo portátil, y desea ejecutar ese código [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. Puede hacerlo solo si se cumplen estas condiciones:

+ La base de datos permite las conexiones remotas.
+ Se ha agregado un inicio de sesión de SQL con el nombre y la contraseña usados en el código de R a [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] en el nivel de instancia. O bien, si usa la Autenticación integrada de Windows, el usuario de Windows especificado en la cadena de conexión debe agregarse como usuario de la instancia.
+ El inicio de sesión SQL o el usuario de Windows debe tener el permiso para ejecutar scripts externos. Por lo general, este permiso solo lo puede agregar un administrador de bases de datos.
+ El inicio de sesión de SQL o el usuario de Windows deben agregarse como usuario con los permisos adecuados en cada base de datos en la que el trabajo de R realice cualquiera de estas operaciones:
    + Recuperar datos
    + Escribir o actualizar datos 
    + Crear objetos como tablas o procedimientos almacenados

Después de que el inicio de sesión o la cuenta de usuario de Windows se ha aprovisionado y conceder los permisos necesarios, puede ejecutar código R en [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] mediante un objeto de origen de datos de R o mediante una llamada a un procedimiento almacenado. Cada vez que se inicia R desde [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], la seguridad del motor de base de datos obtiene el contexto de seguridad del usuario que inició el trabajo de R o se ejecutó el procedimiento almacenado y administra las asignaciones del usuario o inicio de sesión a los objetos protegibles. 

Por lo tanto, todos los trabajos de R que se inician desde un cliente remoto deben especificar la información de inicio de sesión o usuario como parte de la cadena de conexión.

## <a name="interaction-of-includessnoversionmdincludesssnoversion-mdmd-security-and-launchpad-security"></a>Interacción de la seguridad de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] y la seguridad de Launchpad

Cuando se ejecuta un script de R en el contexto del equipo con [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], el servicio [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] obtiene una cuenta de trabajo disponible (una cuenta de usuario local) de un grupo de cuentas de trabajo establecido para el proceso externo y usa esa cuenta de trabajo para realizar las tareas relacionadas. 

Por ejemplo, si inicia un trabajo de R con sus credenciales de dominio de Windows, la cuenta podría asignarse a la cuenta de trabajo de Launchpad *SQLRUser01*.

Después de la asignación a una cuenta de trabajo, [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] crea un token de usuario que se usa para iniciar procesos. 

Cuando se completen todas las operaciones de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], la cuenta de trabajo de usuario se marcará como libre y se devolverá al grupo.

Para obtener más información sobre [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)], vea [New Components in SQL Server to Support R Integration](../../advanced-analytics/r-services/new-components-in-sql-server-to-support-r.md) (Nuevos componentes de SQL Server para la integración de R).

> [!NOTE]
Para que Launchpad administre las cuentas de trabajo y ejecute trabajos de R, el grupo que contiene las cuentas de trabajo (SQLRUserGroup) debe tener el permiso "Permitir el inicio de sesión local". De lo contrario, R Services podría no funcionar. De forma predeterminada, este permiso se concede a todos los nuevos usuarios locales, pero en algunas organizaciones podrían aplicarse directivas de grupo más estrictas que impidan que las cuentas de trabajo se conecten a SQL Server para realizar trabajos de R.  

## <a name="security-of-worker-accounts"></a>Seguridad de las cuentas de trabajo

La asignación de un usuario externo de Windows o inicio de sesión SQL válido para una cuenta de trabajo es válida solo durante la duración de la duración de la consulta SQL que se ejecuta el script de R. 

Las consultas en paralelo desde el mismo inicio de sesión se asignan a la misma cuenta de trabajo de usuario.

[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] administra los directorios que se usan para los procesos mediante RLauncher, y directorios son de acceso restringido. La cuenta de trabajo no puede tener acceso a los archivos de las carpetas situadas por encima de la suya propia, pero puede leer, escribir o eliminar elementos secundarios situados bajo la carpeta de trabajo de la sesión que se ha creado para la consulta SQL con el script de R.

Para obtener más información sobre cómo cambiar el número de cuentas de trabajo, los nombres de las cuentas o las contraseñas, vea [Modify the User Account Pool for SQL Server R Services](../../advanced-analytics/r-services/modify-the-user-account-pool-for-sql-server-r-services.md) (Modificar el grupo de cuentas de usuario para SQL Server R Services).


## <a name="security-isolation-for-multiple-external-scripts"></a>Aislamiento de seguridad para varios scripts externos

El mecanismo de aislamiento se basa en las cuentas de usuario físico. Cuando se inician los procesos satélite para el tiempo de ejecución de un lenguaje específico, cada tarea satélite usa la cuenta de trabajo especificada por [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]. Si una tarea requiere varios satélites, como en el caso de las consultas en paralelo, se usa una cuenta de trabajo única para todas las tareas relacionadas.

Ninguna cuenta de trabajo puede ver o manipular los archivos usados por otras cuentas de trabajo.
 
Si es administrador del equipo, puede ver los directorios creados para cada proceso. Cada directorio se identifica mediante su GUID de sesión.

## <a name="see-also"></a>Vea también
[Información general sobre la arquitectura](../../advanced-analytics/r-services/architecture-overview-sql-server-r.md)

