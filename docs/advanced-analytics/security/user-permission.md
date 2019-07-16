---
title: Conceder permisos de base de datos para la ejecución del script R y Python - SQL Server Machine Learning Services
description: Cómo conceder permisos de usuario de base de datos para la ejecución de scripts de R y Python en SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: e24095b7ec5aafd3439a3d344123c0a7f9dae86d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962323"
---
# <a name="give-users-permission-to-sql-server-machine-learning-services"></a>Proporcionar a los usuarios permiso para SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo se describe cómo se puede conceder permiso para ejecutar scripts externos en SQL Server Machine Learning Services y conceder permisos de DDL (lenguaje) para las bases de datos de lectura, escritura o definición de datos de usuarios.

Para obtener más información, consulte la sección permisos de [información general de seguridad para el marco de extensibilidad](../../advanced-analytics/concepts/security.md#permissions).

<a name="permissions-external-script"></a>

## <a name="permission-to-run-scripts"></a>Permiso para ejecutar scripts

Si instaló [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usted mismo y ejecuta scripts de R o Python en su propia instancia, normalmente ejecutar secuencias de comandos como administrador. Por lo tanto, tendrá permiso implícito en varias operaciones y todos los datos de la base de datos.

Sin embargo, la mayoría de los usuarios, no tiene estos permisos elevados. Por ejemplo, los usuarios de una organización que usa inicios de sesión SQL para tener acceso a la base de datos generalmente no tiene permisos elevados. Por lo tanto, para cada usuario que usa R o Python, debe conceder a los usuarios de Machine Learning Services el permiso para ejecutar scripts externos en cada base de datos donde se usa el idioma. A continuación, se indica cómo puede hacerlo.

```sql
USE <database_name>
GO
GRANT EXECUTE ANY EXTERNAL SCRIPT TO [UserName]
```

> [!NOTE]
> Permisos no son específicos del lenguaje de secuencia de comandos compatible. En otras palabras, no hay niveles de permisos independientes para el script de R en comparación con el script de Python. Si necesita mantener permisos independientes para estos idiomas, instalar R y Python en instancias independientes.

<a name="permissions-db"></a> 

## <a name="grant-databases-permissions"></a>Conceder permisos de las bases de datos

Mientras que un usuario ejecuta secuencias de comandos, el usuario deba leer datos de otras bases de datos. El usuario también podría necesitar crear nuevas tablas para almacenar resultados y escribir datos en tablas.

Para cada cuenta de usuario de Windows o inicio de sesión SQL que ejecuta scripts de R o Python, asegúrese de que tiene los permisos adecuados en la base de datos específica: `db_datareader` para leer datos, `db_datawriter` para guardar los objetos en la base de datos o `db_ddladmin` para crear objetos Por ejemplo, procedimientos almacenados o tablas que contiene había entrenado y datos serializados.

Por ejemplo, la siguiente [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción proporciona el inicio de sesión SQL *MySQLLogin* los derechos para ejecutar consultas de T-SQL en la *ML_Samples* base de datos. Para ejecutar esta instrucción, el inicio de sesión de SQL debe existir en el contexto de seguridad del servidor.

```sql
USE ML_Samples
GO
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'
```

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de los permisos incluidos en cada rol, consulte [roles de nivel de base de datos](../../relational-databases/security/authentication-access/database-level-roles.md).