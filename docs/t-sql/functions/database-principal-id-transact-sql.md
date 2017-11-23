---
title: DATABASE_PRINCIPAL_ID (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DATABASE_PRINCIPAL_ID_TSQL
- DATABASE_PRINCIPAL_ID
dev_langs: TSQL
helpviewer_keywords:
- identification numbers [SQL Server], principals
- principal ID numbers [SQL Server]
- DATABASE_PRINCIPAL_ID function
- IDs [SQL Server], principals
ms.assetid: 908c7dd8-c10b-4658-92f6-0224f9835dd9
caps.latest.revision: "28"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 44f4bd65c93fc0c6ed0fd069946fabaedd1e0943
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="databaseprincipalid-transact-sql"></a>DATABASE_PRINCIPAL_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Devuelve el número de Id. de una entidad de seguridad de la base de datos actual. Para obtener más información acerca de las entidades, consulte [entidades de seguridad &#40; motor de base de datos &#41;](../../relational-databases/security/authentication-access/principals-database-engine.md).
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
DATABASE_PRINCIPAL_ID ( 'principal_name' )  
```  
  
## <a name="arguments"></a>Argumentos  
*principal_name*  
Es una expresión de tipo **sysname** que representa la entidad de seguridad.  
Cuando *principal_name* es se omite, se devuelve el identificador del usuario actual. Es obligatorio utilizar paréntesis.
  
## <a name="return-types"></a>Tipos de valor devuelto
**int**  
NULL cuando la entidad de base de datos no existe
  
## <a name="remarks"></a>Comentarios  
DATABASE_PRINCIPAL_ID se puede utilizar en una lista de selección, en una cláusula WHERE o en cualquier lugar en el que se permita una expresión. Para obtener más información, vea [Expresiones &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md).
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-retrieving-the-id-of-the-current-user"></a>A. Recuperar el Id. del usuario actual  
En el siguiente ejemplo se devuelve el Id. de la entidad de seguridad de base de datos del usuario actual.
  
```sql
SELECT DATABASE_PRINCIPAL_ID();  
GO  
```  
  
### <a name="b-retrieving-the-id-of-a-specified-database-principal"></a>B. Recuperar el Id. de la entidad de seguridad de base de datos especificada  
En el siguiente ejemplo se devuelve el Id. de la entidad de seguridad de base de datos del rol de base de datos `db_owner`.
  
```sql
SELECT DATABASE_PRINCIPAL_ID('db_owner');  
GO  
```  
  
## <a name="see-also"></a>Vea también
[Entidades de seguridad &#40;motor de base de datos&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
[Jerarquía de permisos &#40;motor de base de datos&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)  
[sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)
  
  
