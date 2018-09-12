---
title: Seguridad para SQL Server machine learning y R | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: c04670464d23f0951a957df945a2e81b817ae134
ms.sourcegitcommit: 2666ca7660705271ec5b59cc5e35f6b35eca0a96
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2018
ms.locfileid: "43889191"
---
# <a name="security-for-sql-server-machine-learning-and-r"></a>Seguridad para SQL Server machine learning y R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artículo describe la arquitectura general de seguridad que se utiliza para conectar el [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] motor y los componentes relacionados con el tiempo de ejecución de R de la base de datos. Se proporcionan ejemplos del proceso de seguridad para estos escenarios habituales para usar R en un entorno empresarial:

+ Ejecutar funciones de RevoScaleR en [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] desde un cliente de ciencia de datos
+ Ejecutar R directamente desde [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] mediante procedimientos almacenados

## <a name="security-overview"></a>Información general sobre seguridad

Un [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] inicio de sesión o cuenta de usuario de Windows se requiere para ejecutar scripts de R que usan datos de SQL Server o que se ejecutan con SQL Server como el contexto de cálculo. Este requisito se aplica a ambos [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] y SQL Server 2017 [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)].

La cuenta de inicio de sesión o usuario identifica la *entidad de seguridad*, que puedan necesitar varios niveles de acceso, según los requisitos de script de R:

+ Permiso para acceder a la base de datos donde está habilitado R
+ Permisos para leer datos de objetos protegidos, como tablas
+ La capacidad de escribir nuevos datos en una tabla, como un modelo o los resultados de puntuación
+ La capacidad para crear nuevos objetos, como tablas, procedimientos almacenados que use el script de R o personalizado, las funciones que el trabajo de uso de R
+ El derecho a instalar nuevos paquetes en el equipo de SQL Server, o paquetes de uso de R proporcionados a un grupo de usuarios. 

Por lo tanto, cada persona que ejecuta el código de R con [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] como la ejecución del contexto debe estar asignado a un inicio de sesión en la base de datos. Con la seguridad de SQL Server, es generalmente más fácil crear roles para administrar conjuntos de permisos y asignar a usuarios a esos roles, en lugar de establecer permisos de usuario de forma individual. 

Por ejemplo, suponga que ha creado algún código de R que se ejecuta en el equipo portátil, y que desea ejecutar ese código [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. Puede hacerlo solo si se cumplen estas condiciones:

+ La base de datos permite las conexiones remotas.
+ Se ha agregado un inicio de sesión de SQL con el nombre y la contraseña usados en el código de R a [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] en el nivel de instancia. O bien, si usa la Autenticación integrada de Windows, el usuario de Windows especificado en la cadena de conexión debe agregarse como usuario de la instancia.
+ El inicio de sesión SQL o el usuario de Windows debe tener el permiso para ejecutar scripts externos. Por lo general, este permiso solo lo puede agregar un administrador de bases de datos.
+ El inicio de sesión de SQL o el usuario de Windows deben agregarse como usuario con los permisos adecuados en cada base de datos en la que el trabajo de R realice cualquiera de estas operaciones:
    + Recuperar datos
    + Escribir o actualizar datos 
    + Crear objetos como tablas o procedimientos almacenados

El inicio de sesión o cuenta de usuario de Windows una vez aprovisionado y tengan los permisos necesarios, puede ejecutar código R en [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] mediante el uso de un objeto de origen de datos de R o mediante una llamada a un procedimiento almacenado. Cada vez que se inicie R desde [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], la seguridad del motor de base de datos obtiene el contexto de seguridad del usuario que inició el trabajo de R o se ejecutó el procedimiento almacenado y administra las asignaciones del usuario o inicio de sesión a objetos protegibles. 

Por lo tanto, todos los trabajos de R que se inician desde un cliente remoto deben especificar la información de inicio de sesión o usuario como parte de la cadena de conexión.

## <a name="interaction-of-includessnoversionmdincludesssnoversion-mdmd-security-and-launchpad-security"></a>Interacción de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] seguridad y la seguridad de Launchpad

Cuando se ejecuta un script de R en el contexto del equipo con [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], el servicio [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] obtiene una cuenta de trabajo disponible (una cuenta de usuario local) de un grupo de cuentas de trabajo establecido para el proceso externo y usa esa cuenta de trabajo para realizar las tareas relacionadas. 

Por ejemplo, si inicia un trabajo de R con sus credenciales de dominio de Windows, la cuenta podría asignarse a la cuenta de trabajo de Launchpad *SQLRUser01*.

Después de la asignación a una cuenta de trabajo, [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] crea un token de usuario que se usa para iniciar procesos. 

Cuando se completen todas las operaciones de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], la cuenta de trabajo de usuario se marcará como libre y se devolverá al grupo.

Para obtener más información sobre el servicio, consulte [Extensibility framework](../concepts/extensibility-framework.md). 

### <a name="implied-authentication"></a>Autenticación implícita

**Autenticación implícita** es el término que se usa para el proceso en la que SQL Server obtiene el usuario las credenciales y, a continuación, ejecuta todas las tareas de script externo en nombre de los usuarios, suponiendo que el usuario tiene los permisos correctos en la base de datos. Autenticación implícita es especialmente importante si el script de R que necesita realizar una llamada ODBC fuera de la base de datos de SQL Server. Por ejemplo, el código puede recuperar una lista más corta de factores desde una hoja de cálculo u otro origen.

Para que tales llamadas de bucle invertido se realice correctamente, el grupo que contiene las cuentas de trabajo, SQLRUserGroup, debe tener permisos de "Permitir iniciar sesión localmente". De forma predeterminada, este permiso se concede a todos los nuevos usuarios locales, pero en algunas organizaciones podrían aplicarse directivas de grupo más estrictas.

![Autenticación implícita para R](media/implied-auth-rsql.png)

## <a name="security-of-worker-accounts"></a>Seguridad de cuentas de trabajo

La asignación de un usuario externo de Windows o inicio de sesión SQL válido para una cuenta de trabajo es válida solo durante la vigencia de la duración de la consulta SQL que se ejecuta el script de R.

Las consultas en paralelo desde el mismo inicio de sesión se asignan a la misma cuenta de trabajo de usuario.

[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] administra los directorios que se usan para los procesos mediante RLauncher, y directorios son de acceso restringido. La cuenta de trabajo no puede tener acceso a los archivos de las carpetas situadas por encima de la suya propia, pero puede leer, escribir o eliminar elementos secundarios situados bajo la carpeta de trabajo de la sesión que se ha creado para la consulta SQL con el script de R.

Para obtener más información acerca de cómo cambiar el número de cuentas de trabajo, los nombres de cuentas o contraseñas de cuentas, vea [modificar el grupo de cuentas de usuario para el aprendizaje automático de SQL Server](../../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md).

## <a name="security-isolation-for-multiple-external-scripts"></a>Aislamiento de seguridad para varios scripts externos

El mecanismo de aislamiento se basa en las cuentas de usuario físico. Cuando se inician los procesos satélite para el tiempo de ejecución de un lenguaje específico, cada tarea satélite usa la cuenta de trabajo especificada por [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]. Si una tarea requiere varios satélites, como en el caso de las consultas en paralelo, se usa una cuenta de trabajo única para todas las tareas relacionadas.

Ninguna cuenta de trabajo puede ver o manipular los archivos usados por otras cuentas de trabajo.
 
Si es administrador del equipo, puede ver los directorios creados para cada proceso. Cada directorio se identifica mediante su GUID de sesión.

## <a name="see-also"></a>Vea también

[Introducción a la arquitectura para el aprendizaje automático de SQL Server](../../advanced-analytics/r/architecture-overview-sql-server-r.md)
