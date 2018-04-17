---
title: sp_helprolemember (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_helprolemember_TSQL
- sp_helprolemember
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helprolemember
ms.assetid: 42797510-aa5d-4564-85ac-27418419af9c
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d6fc001d0153ece51fc2ceed8cae2b12071af5e5
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sphelprolemember-transact-sql"></a>sp_helprolemember (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve información acerca de los miembros directos de un rol de la base de datos actual.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helprolemember [ [ @rolename = ] 'role' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@rolename =** ] **'** *rol* **'**  
 Es el nombre de un rol en la base de datos actual. *rol* es **sysname**, su valor predeterminado es null. *rol* debe existir en la base de datos actual. Si *rol* no se especifica, se devuelven todas las funciones que contienen al menos un miembro de la base de datos actual.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**DbRole**|**sysname**|Nombre del rol en la base de datos actual.|  
|**Nombre de usuario registrado**|**sysname**|Nombre de un miembro de **DbRole.**|  
|**MemberSID**|**varbinary(85)**|Identificador de seguridad de **MemberName.**|  
  
## <a name="remarks"></a>Comentarios  
 Si la base de datos contiene roles anidados, **MemberName** puede ser el nombre de un rol. **sp_helprolemember** no muestra la pertenencia obtenida con roles anidados. Por ejemplo, si User1 es miembro de Role1 y Role1 es miembro de Role2, `EXEC sp_helprolemember 'Role2'`, devolverá Role1, pero no los miembros de Role1 (User1 en este ejemplo). Para devolver pertenencias anidadas, debe ejecutar **sp_helprolemember** repetidamente para cada rol anidado.  
  
 Use **sp_helpsrvrolemember** para mostrar los miembros del rol fijo de servidor.  
  
 Use [IS_ROLEMEMBER &#40;Transact-SQL&#41; ](../../t-sql/functions/is-rolemember-transact-sql.md) para comprobar la pertenencia a roles para un usuario especificado.  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer al rol **public** .  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se muestran los miembros del rol `Sales`.  
  
```  
EXEC sp_helprolemember 'Sales';  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados de seguridad &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sp_droprolemember & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md)   
 [sp_helprole &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helprole-transact-sql.md)   
 [sp_helpsrvrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsrvrolemember-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
