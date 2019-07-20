---
title: Conceder permisos de base de datos para la ejecución de scripts de R y Python
description: Cómo conceder permisos de usuario de base de datos para la ejecución de scripts de R y Python en SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: a6b2fb46cb2ee361d858fa460119e6960d78fda7
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345096"
---
# <a name="give-users-permission-to-sql-server-machine-learning-services"></a>Conceder permiso a los usuarios para SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo se describe cómo puede conceder a los usuarios permiso para ejecutar scripts externos en SQL Server Machine Learning Services y proporcionar permisos de lectura, escritura o lenguaje de definición de datos (DDL) a las bases de datos.

Para obtener más información, vea la sección permisos en [información general sobre seguridad para el marco de extensibilidad](../../advanced-analytics/concepts/security.md#permissions).

<a name="permissions-external-script"></a>

## <a name="permission-to-run-scripts"></a>Permiso para ejecutar scripts

Si ha instalado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usted mismo y está ejecutando scripts de R o Python en su propia instancia, normalmente ejecutará los scripts como administrador. Por lo tanto, tiene permisos implícitos en varias operaciones y en todos los datos de la base de datos.

Sin embargo, la mayoría de los usuarios no tienen permisos elevados. Por ejemplo, los usuarios de una organización que usan inicios de sesión de SQL para tener acceso a la base de datos no suelen tener permisos elevados. Por lo tanto, para cada usuario que usa R o Python, debe conceder a los usuarios de Machine Learning Services el permiso para ejecutar scripts externos en cada base de datos en la que se usa el idioma. A continuación, se indica cómo puede hacerlo.

```sql
USE <database_name>
GO
GRANT EXECUTE ANY EXTERNAL SCRIPT TO [UserName]
```

> [!NOTE]
> Los permisos no son específicos del lenguaje de script admitido. En otras palabras, no hay niveles de permisos independientes para el script de R frente al script de Python. Si necesita mantener permisos independientes para estos idiomas, instale R y Python en instancias independientes.

<a name="permissions-db"></a> 

## <a name="grant-databases-permissions"></a>Permisos de base de datos Grant

Mientras un usuario ejecuta scripts, es posible que el usuario tenga que leer datos de otras bases de datos. El usuario también podría necesitar crear nuevas tablas para almacenar los resultados y escribir datos en las tablas.

Para cada cuenta de usuario de Windows o inicio de sesión de SQL que ejecute scripts de R o Python, asegúrese de que tiene los permisos `db_datareader` adecuados en la base `db_datawriter` de datos específica: para leer datos, `db_ddladmin` para guardar objetos en la base de datos o para crear objetos. como procedimientos almacenados o tablas que contienen datos entrenados y serializados.

Por ejemplo, la siguiente [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción proporciona al inicio de sesión de SQL *MySQLLogin* los derechos para ejecutar consultas de T-SQL en la base de datos *ML_Samples* . Para ejecutar esta instrucción, el inicio de sesión de SQL debe existir en el contexto de seguridad del servidor.

```sql
USE ML_Samples
GO
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'
```

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre los permisos incluidos en cada rol, vea [roles de nivel de base de datos](../../relational-databases/security/authentication-access/database-level-roles.md).