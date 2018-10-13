---
title: Proporcionar a los usuarios permiso para SQL Server Machine Learning Services | Microsoft Docs
description: Cómo proporcionar a los usuarios permiso para SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/05/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: ad5c3fa3bf94bb88041c9ec81773b2a26013e517
ms.sourcegitcommit: 485e4e05d88813d2a8bb8e7296dbd721d125f940
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/11/2018
ms.locfileid: "49100336"
---
# <a name="give-users-permission-to-sql-server-machine-learning-services"></a>Proporcionar a los usuarios permiso para SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo se describe cómo se puede conceder permiso para ejecutar scripts externos en SQL Server Machine Learning Services y conceder permisos de DDL (lenguaje) para las bases de datos de lectura, escritura o definición de datos de usuarios.

Se requiere un inicio de sesión de SQL Server o la cuenta de usuario de Windows para ejecutar scripts externos que usan datos de SQL Server o que se ejecutan con SQL Server como el contexto de cálculo.

La cuenta de inicio de sesión o usuario identifica la *entidad de seguridad*, que puedan necesitar varios niveles de acceso, según los requisitos de script externo:

+ Permiso para acceder a la base de datos donde están habilitados los scripts externos.
+ Permisos para leer datos de objetos protegidos, como tablas.
+ La capacidad de escribir nuevos datos en una tabla, como un modelo o los resultados de puntuación.
+ La capacidad para crear nuevos objetos, como tablas, procedimientos almacenados que use el script externo, o las funciones personalizadas que el uso de R o trabajo de Python.
+ Derecho a instalar nuevos paquetes en el equipo de SQL Server, o usar paquetes proporcionados a un grupo de usuarios.

Por lo tanto, cada persona que ejecuta un script externo mediante SQL Server como el contexto de ejecución debe asignarse a un usuario en la base de datos. Con la seguridad de SQL Server, es más fácil crear roles para administrar conjuntos de permisos y asignar a usuarios a esos roles, en lugar de establecer permisos de usuario de forma individual.

Incluso los usuarios que usan R o Python en una herramienta externa deben asignarse a una cuenta en la base de datos o el inicio de sesión si el usuario necesita para ejecutar un script externo en bases de datos, o datos y objetos de base de datos de access. Los mismos permisos son necesarios si la secuencia de comandos externa se envía desde un cliente de ciencia de datos remoto o al uso de un procedimiento almacenado de T-SQL.

Por ejemplo, suponga que ha creado un script externo que se ejecuta en el equipo local, y desea ejecutar ese código en SQL Server. Debe asegurarse de que se cumplan las condiciones siguientes:

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

<a name="permissions-external-script"></a> 

## <a name="permission-to-run-scripts"></a>Permiso para ejecutar scripts

Si instaló [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usted mismo y ejecuta scripts de R o Python en su propia instancia, normalmente ejecutar secuencias de comandos como administrador. Por lo tanto, tendrá permiso implícito en varias operaciones y todos los datos de la base de datos.

Sin embargo, la mayoría de los usuarios, no tiene estos permisos elevados. Por ejemplo, los usuarios de una organización que usa inicios de sesión SQL para tener acceso a la base de datos generalmente no tiene permisos elevados. Por lo tanto, para cada usuario que usa R o Python, debe conceder a los usuarios de Machine Learning Services el permiso para ejecutar scripts externos en cada base de datos donde se usa el idioma. A continuación, se indica cómo puede hacerlo.

```SQL
USE <database_name>
GO
GRANT EXECUTE ANY EXTERNAL SCRIPT  TO [UserName]
```

> [!NOTE]
> Permisos no son específicos del lenguaje de secuencia de comandos compatible. En otras palabras, no hay niveles de permisos independientes para el script de R en comparación con el script de Python. Si necesita mantener permisos independientes para estos idiomas, instalar R y Python en instancias independientes.

<a name="permissions-db"></a> 

## <a name="grant-databases-permissions"></a>Conceder permisos de las bases de datos

Mientras que un usuario ejecuta secuencias de comandos, el usuario deba leer datos de otras bases de datos. El usuario también podría necesitar crear nuevas tablas para almacenar resultados y escribir datos en tablas.

Para cada cuenta de usuario de Windows o inicio de sesión SQL que ejecuta scripts de R o Python, asegúrese de que tiene los permisos adecuados en la base de datos específica: `db_datareader` para leer datos, `db_datawriter` para guardar los objetos en la base de datos o `db_ddladmin` para crear objetos Por ejemplo, procedimientos almacenados o tablas que contiene había entrenado y datos serializados.

Por ejemplo, la siguiente [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción proporciona el inicio de sesión SQL *MySQLLogin* los derechos para ejecutar consultas de T-SQL en la *ML_Samples* base de datos. Para ejecutar esta instrucción, el inicio de sesión de SQL debe existir en el contexto de seguridad del servidor.

```SQL
USE ML_Samples
GO
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'
```

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de los permisos incluidos en cada rol, consulte [roles de nivel de base de datos](../../relational-databases/security/authentication-access/database-level-roles.md).