---
title: Sys.database_credentials (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 02/27/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.database_credentials
- sys.database_credentials_TSQL
- database_credentials
- database_credentials_TSQL
helpviewer_keywords: sys.database_credentials catalog view
ms.assetid: 796322df-e62a-45bf-b519-89e1d521abce
caps.latest.revision: "8"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cc6e8fe546412d4549c0724b34e434994ffa744d
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="sysdatabasecredentials-transact-sql"></a>Sys.database_credentials (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  Devuelve una fila por cada base de datos con ámbito de credencial en la base de datos.  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Use [sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md) en su lugar.    
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|credential_id|**int**|Id. de la credencial de ámbito de la base de datos. Es único en la base de datos.|  
|name|**sysname**|Credencial con ámbito de nombre de la base de datos. Es único en la base de datos.|  
|credential_identity|**nvarchar(4000)**|Nombre de la identidad que se va a utilizar. Suele ser un usuario de Windows. No tiene que ser único.|  
|create_date|**datetime**|Hora en que se creó la credencial de ámbito de la base de datos.|  
|modify_date|**datetime**|Hora a la que se modificó por última vez la credencial de ámbito de la base de datos.|  
|target_type|**nvarchar (100)**|Credencial de ámbito del tipo de base de datos. Devuelve un valor NULL para la base de datos de credenciales con ámbito.|  
|target_id|**int**|Id. del objeto que está asignada la credencial de ámbito de la base de datos a. Credenciales con ámbito devuelve 0 para la base de datos|  
  
## <a name="permissions"></a>Permissions  
 Debe tener el permiso `CONTROL` para la base de datos.  
  
## <a name="see-also"></a>Vea también  
 [Credenciales &#40; motor de base de datos &#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [CREAR CREDENCIAL en el ámbito de base de datos &#40; Transact-SQL &#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)   
 [ALTER CREDENTIAL en el ámbito de base de datos &#40; Transact-SQL &#41;](../../t-sql/statements/alter-database-scoped-credential-transact-sql.md)   
 [ELIMINAR CREDENCIALES en el ámbito de base de datos &#40; Transact-SQL &#41;](../../t-sql/statements/drop-database-scoped-credential-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [sys.credentials &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
  
  
