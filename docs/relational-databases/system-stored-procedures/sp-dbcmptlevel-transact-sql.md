---
title: sp_dbcmptlevel (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dbcmptlevel
- sp_dbcmptlevel_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dbcmptlevel
ms.assetid: 508c686d-2bd4-41ba-8602-48ebca266659
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0f6ffcb7a43fbfc2a840cbbbeb95de4bbb875cbe
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68108208"
---
# <a name="sp_dbcmptlevel-transact-sql"></a>sp_dbcmptlevel (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Configura varios comportamientos de la base de datos de manera que sean compatibles con la versión especificada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]Use en su lugar el [nivel de compatibilidad ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_dbcmptlevel [ [ @dbname = ] name ]   
    [ , [ @new_cmptlevel = ] version ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @dbname = ] name`Es el nombre de la base de datos para la que se va a cambiar el nivel de compatibilidad. Los nombres de base de datos deben cumplir las reglas de los identificadores. *Name* es de **tipo sysname y su**valor predeterminado es NULL.  
  
`[ @new_cmptlevel = ] version`Es la versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con la que se va a hacer compatible la base de datos. la *versión* es de **tinyint**y su valor predeterminado es NULL. Debe tener uno de los siguientes valores:  
  
 **90** = [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]  
  
 **100** = [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
 **110** = [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
 **120** = [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
 **130** = [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Si no se especifican parámetros o si no se especifica el parámetro *Name* , **sp_dbcmptlevel** devuelve un error.  
  
 Si se especifica *Name* sin la *versión*, [!INCLUDE[ssDE](../../includes/ssde-md.md)] el devuelve un mensaje que muestra el nivel de compatibilidad actual de la base de datos especificada.  
  
## <a name="remarks"></a>Observaciones  
 Para obtener una descripción de los niveles de compatibilidad, vea [nivel de compatibilidad de Alter database &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
## <a name="permissions"></a>Permisos  
 Solo el propietario de la base de datos, los miembros del rol fijo de servidor **sysadmin** y el rol fijo de base de datos **db_owner** (si va a cambiar la base de datos actual) pueden ejecutar este procedimiento.  
  
## <a name="see-also"></a>Consulte también  
 [Motor de base de datos procedimientos almacenados &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [Palabras clave reservadas &#40;Transact-SQL&#41;](../../t-sql/language-elements/reserved-keywords-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
