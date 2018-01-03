---
title: "QUITAR CREDENCIALES en el ámbito de base de datos (Transact-SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 02/27/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP DATABASE SCOPED CREDENTIAL
- DROP_DATABASE_SCOPED_CREDENTIAL_TSQL
helpviewer_keywords:
- DROP DATABASE SCOPED CREDENTIAL statement
- credential [SQL Server], DROP DATABASE SCOPED CREDENTIAL statement
ms.assetid: 319d59f4-fa82-47ca-869b-3a9cd52900b0
caps.latest.revision: "11"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 96016adf491a2869054068339a7fba64f8e7fedb
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/02/2018
---
# <a name="drop-database-scoped-credential-transact-sql"></a>QUITAR CREDENCIALES en el ámbito de base de datos (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Quita una credencial de ámbito de la base de datos del servidor.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DROP DATABASE SCOPED CREDENTIAL credential_name  
```  
  
## <a name="arguments"></a>Argumentos  
 *credential_name*  
 Es el nombre de la credencial de ámbito de la base de datos que se va a quitar del servidor.  
  
## <a name="remarks"></a>Comentarios  
 Para quitar el secreto asociado con una credencial de ámbito de la base de datos sin quitar la credencial de ámbito de la base de datos, utilice [ALTER CREDENTIAL](../../t-sql/statements/alter-credential-transact-sql.md).  
  
 Información sobre las credenciales de ámbito de la base de datos está visible en el [sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md) vista de catálogo.  
  
## <a name="permissions"></a>Permissions  
 Requiere `ALTER` permiso en la credencial.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se quita la credencial de ámbito de la base de datos denominada `SalesAccess`.  
  
```sql  
DROP DATABASE SCOPED CREDENTIAL AppCred;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Credenciales &#40; motor de base de datos &#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [CREAR CREDENCIAL en el ámbito de base de datos &#40; Transact-SQL &#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)   
 [ALTER CREDENTIAL en el ámbito de base de datos &#40; Transact-SQL &#41;](../../t-sql/statements/alter-database-scoped-credential-transact-sql.md)   
 [Sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [sys.credentials &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
  
  
