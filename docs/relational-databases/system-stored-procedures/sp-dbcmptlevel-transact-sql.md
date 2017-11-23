---
title: sp_dbcmptlevel (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_dbcmptlevel
- sp_dbcmptlevel_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_dbcmptlevel
ms.assetid: 508c686d-2bd4-41ba-8602-48ebca266659
caps.latest.revision: "110"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fba712ff23978ec3af33e481b947b1e1eca7d0f9
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="spdbcmptlevel-transact-sql"></a>sp_dbcmptlevel (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Configura varios comportamientos de la base de datos de manera que sean compatibles con la versión especificada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]Use [nivel de compatibilidad de ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)en su lugar.  
  
||  
|-|  
|**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_dbcmptlevel [ [ @dbname = ] name ]   
    [ , [ @new_cmptlevel = ] version ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@dbname=** ] *nombre*  
 Es el nombre de la base de datos cuyo nivel de compatibilidad se va a cambiar. Los nombres de base de datos deben cumplir las reglas de los identificadores. *nombre* es **sysname**, su valor predeterminado es null.  
  
 [  **@new_cmptlevel=** ] *versión*  
 Es la versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con la que se va a hacer compatible la base de datos. *versión* es **tinyint**, su valor predeterminado es null. Debe tener uno de los siguientes valores:  
  
 **90** = [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]  
  
 **100** = [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
 **110** = [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
 **120** = [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
 **130** = [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Si se especifica ningún parámetro o si la *nombre* no se especifica el parámetro, **sp_dbcmptlevel** devuelve un error.  
  
 Si *nombre* se especifica sin *versión*, [!INCLUDE[ssDE](../../includes/ssde-md.md)] devuelve un mensaje que muestra el nivel de compatibilidad actual de la base de datos especificada.  
  
## <a name="remarks"></a>Comentarios  
 Para obtener una descripción de los niveles de compatibilidad, vea [nivel de compatibilidad de ALTER DATABASE &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
## <a name="permissions"></a>Permissions  
 Solo el propietario de la base de datos, los miembros de la **sysadmin** fija de servidor sysadmin y la **db_owner** rol fijo de base (si va a cambiar la base de datos actual) puede ejecutar este procedimiento.  
  
## <a name="see-also"></a>Vea también  
 [Motor de base de datos almacenados procedimientos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [Palabras clave reservadas &#40;Transact-SQL&#41;](../../t-sql/language-elements/reserved-keywords-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
