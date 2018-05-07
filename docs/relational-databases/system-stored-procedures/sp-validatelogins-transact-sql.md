---
title: sp_validatelogins (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_validatelogins
- sp_validatelogins_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_validatelogins
ms.assetid: 6ac52e21-e20d-469b-ad40-5aa091e06b61
caps.latest.revision: 25
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: f8bfcefdd3b43e8a52fce6514583a47ed6aa4119
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="spvalidatelogins-transact-sql"></a>sp_validatelogins (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ofrece información acerca de los usuarios y grupos de Windows asignados a entidades de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que ya no existen en el entorno de Windows.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_validatelogins  
```  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**SID**|**varbinary(85)**|Identificador de seguridad (SID) de Windows del usuario o grupo de Windows.|  
|**Inicio de sesión de NT**|**sysname**|Nombre del usuario o grupo de Windows.|  
  
## <a name="remarks"></a>Comentarios  
 Si la entidad de seguridad a nivel de servidor huérfana es propietaria de un usuario de base de datos, es necesario quitar el usuario de la base de datos antes de quitar la entidad de seguridad de servidor huérfana. Para quitar un usuario de base de datos, use [DROP USER](../../t-sql/statements/drop-user-transact-sql.md). Si la entidad de seguridad a nivel de servidor es propietaria de elementos protegibles en la base de datos, la propiedad de estos elementos debe transferirse o quitarse. Para transferir la propiedad de elementos protegibles de base de datos, utilice [ALTER AUTHORIZATION](../../t-sql/statements/alter-authorization-transact-sql.md).  
  
 Para quitar las asignaciones a los usuarios de Windows y grupos que ya no existen, utilice [DROP LOGIN](../../t-sql/statements/drop-login-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer a la **sysadmin** o **securityadmin** rol fijo de servidor.  
  
## <a name="examples"></a>Ejemplos  
 En este ejemplo se muestran los usuarios y los grupos de Windows que ya no existen pero que siguen disponiendo de acceso a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
EXEC sp_validatelogins;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Procedimientos almacenados de seguridad &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [Eliminar usuario & #40; Transact-SQL & #41;](../../t-sql/statements/drop-user-transact-sql.md)   
 [QUITAR el inicio de sesión & #40; Transact-SQL & #41;](../../t-sql/statements/drop-login-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)  
  
  
