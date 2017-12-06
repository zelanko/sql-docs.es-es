---
title: "Seguridad de aprendizaje automático de SQL Server y R | Documentos de Microsoft"
ms.custom: 
ms.date: 11/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8fc84754-7fbf-4c1b-9150-7d88680b3e68
caps.latest.revision: "9"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 23c84c803d0d0c871d01d2f9e3a28f5d72fa2b0e
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/01/2017
---
# <a name="security-for-sql-server-machine-learning-and-r"></a>Seguridad de aprendizaje automático de SQL Server y R

Este artículo describe la arquitectura global de seguridad que se utiliza para conectar el [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] motor y componentes relacionados con el runtime de R de la base de datos. Se proporcionan ejemplos del proceso de seguridad para estos escenarios comunes para poder usar R en un entorno empresarial:

+ Ejecutar funciones de RevoScaleR en [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] desde un cliente de ciencia de datos
+ Ejecutar R directamente desde [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] mediante procedimientos almacenados

## <a name="security-overview"></a>Información general sobre seguridad

Un [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] se requiere inicio de sesión o cuenta de usuario de Windows para ejecutar scripts de R que usan datos de SQL Server o que se ejecutan con SQL Server como el contexto de proceso. Este requisito se aplica a ambos [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] y SQL Server 2017 [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)].

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

## <a name="interaction-of-includessnoversionmdincludesssnoversion-mdmd-security-and-launchpad-security"></a>Interacción de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] seguridad y la seguridad de Launchpad

Cuando se ejecuta un script de R en el contexto del equipo con [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], el servicio [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] obtiene una cuenta de trabajo disponible (una cuenta de usuario local) de un grupo de cuentas de trabajo establecido para el proceso externo y usa esa cuenta de trabajo para realizar las tareas relacionadas. 

Por ejemplo, si inicia un trabajo de R con sus credenciales de dominio de Windows, la cuenta podría asignarse a la cuenta de trabajo de Launchpad *SQLRUser01*.

Después de la asignación a una cuenta de trabajo, [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] crea un token de usuario que se usa para iniciar procesos. 

Cuando se completen todas las operaciones de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], la cuenta de trabajo de usuario se marcará como libre y se devolverá al grupo.

Para obtener más información acerca de [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)], consulte [componentes de SQL Server para admitir la integración de R](../../advanced-analytics/r/new-components-in-sql-server-to-support-r.md).

### <a name="implied-authentication"></a>Autenticación implícita

**Autenticación implícita** es el término que se usa para el proceso en el que SQL Server obtiene el usuario las credenciales y, a continuación, ejecuta todas las tareas de script externo en nombre de los usuarios, suponiendo que el usuario tiene los permisos correctos en la base de datos. Autenticación implícita es especialmente importante si el script de R es necesario realizar una llamada ODBC fuera de la base de datos de SQL Server. Por ejemplo, el código puede recuperar una lista más corta de factores desde una hoja de cálculo u otro origen.

Para que tales llamadas de bucle invertido, lleve a cabo correctamente, el grupo que contiene las cuentas de trabajo, SQLRUserGroup, debe tener permisos de "Allow Log on locally". De forma predeterminada, este derecho se concede a todos los nuevos usuarios locales, pero en algunas organizaciones puede que sea necesario más estrictas directivas de grupo.

![Autenticación implícita para R](media/implied-auth-rsql.png)

## <a name="security-of-worker-accounts"></a>Seguridad de las cuentas de trabajo

La asignación de un usuario externo de Windows o inicio de sesión SQL válido para una cuenta de trabajo es válida solo durante la duración de la duración de la consulta SQL que se ejecuta el script de R.

Las consultas en paralelo desde el mismo inicio de sesión se asignan a la misma cuenta de trabajo de usuario.

[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] administra los directorios que se usan para los procesos mediante RLauncher, y directorios son de acceso restringido. La cuenta de trabajo no puede tener acceso a los archivos de las carpetas situadas por encima de la suya propia, pero puede leer, escribir o eliminar elementos secundarios situados bajo la carpeta de trabajo de la sesión que se ha creado para la consulta SQL con el script de R.

Para obtener más información acerca de cómo cambiar el número de cuentas de trabajo, los nombres de cuenta o las contraseñas de cuentas, vea [modificar el grupo de cuentas de usuario para el aprendizaje automático de SQL Server](../../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md).

## <a name="security-isolation-for-multiple-external-scripts"></a>Aislamiento de seguridad para varios scripts externos

El mecanismo de aislamiento se basa en las cuentas de usuario físico. Cuando se inician los procesos satélite para el tiempo de ejecución de un lenguaje específico, cada tarea satélite usa la cuenta de trabajo especificada por [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]. Si una tarea requiere varios satélites, como en el caso de las consultas en paralelo, se usa una cuenta de trabajo única para todas las tareas relacionadas.

Ninguna cuenta de trabajo puede ver o manipular los archivos usados por otras cuentas de trabajo.
 
Si es administrador del equipo, puede ver los directorios creados para cada proceso. Cada directorio se identifica mediante su GUID de sesión.

## <a name="see-also"></a>Vea también

[Introducción a la arquitectura para el aprendizaje automático de SQL Server](../../advanced-analytics/r/architecture-overview-sql-server-r.md)
