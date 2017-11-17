---
title: USE (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 11/28/2016
ms.prod: sql-non-specified
ms.prod_service: pdw, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- USE_TSQL
- USE
dev_langs:
- TSQL
helpviewer_keywords:
- USE statement
- database context [SQL Server]
- context changes [SQL Server]
- modifying database context
ms.assetid: c05acac8-c063-4770-8e36-d7f71d500b10
caps.latest.revision: 40
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: 3bd8f0900e3b942fb42b15deb5dbf293f168cba8
ms.contentlocale: es-es
ms.lasthandoff: 10/24/2017

---
# <a name="use-transact-sql"></a>USE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  Cambia el contexto de la base de datos al de la base de datos especificada o a la instantánea en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
USE { database_name }   
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 *database_name*  
 Es el nombre de la base de datos o instantánea de base de datos a la que se cambia el contexto de usuario. Base de datos y nombres de instantánea de base de datos deben cumplir las reglas de [identificadores](../../relational-databases/databases/database-identifiers.md).  
  
 En [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], el parámetro de base de datos solo puede hacer referencia a la base de datos actual. Si se proporciona una base de datos que no sea la base de datos actual, el `USE` instrucción no cambia entre bases de datos y se devuelve el código de error 40508. Para cambiar de base de datos, debe conectarse directamente a la base de datos. La instrucción USE se marca como no es aplicable a la base de datos de SQL en la parte superior de esta página, porque, aunque puede tener la `USE` instrucción en un lote, no hace nada.
  
## <a name="remarks"></a>Comentarios  
 Cuando un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se conecta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el inicio de sesión se conecta automáticamente a su base de datos predeterminada y adquiere el contexto de seguridad de un usuario de la base de datos. Si no se ha creado ningún usuario de la base de datos para el inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el inicio de sesión se conecta como guest. Si el usuario de la base de datos no tiene permiso CONNECT en la base de datos, la instrucción USE no funcionará correctamente. Si no se ha asignado ninguna base de datos predeterminada al inicio de sesión, su base de datos predeterminada se establecerá en master.  
  
 USE se ejecuta en tiempo de compilación y de ejecución, y surte efecto inmediatamente. Por lo tanto, las instrucciones que aparecen en un lote después de la instrucción USE se ejecutan en la base de datos especificada.  
  
## <a name="permissions"></a>Permissions  
 Requiere permiso CONNECT en la base de datos de destino.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se cambia el contexto de la base de datos al de la base de datos `AdventureWorks2012`.  
  
```  
USE AdventureWorks2012;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [Entidades de seguridad &#40;motor de base de datos&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [CREATE DATABASE &#40;Transact-SQL de SQL Server&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [DROP DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)   
 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)  
  
  



