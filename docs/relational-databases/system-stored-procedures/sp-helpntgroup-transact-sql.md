---
title: sp_helpntgroup (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/10/2016
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
- sp_helpntgroup
- sp_helpntgroup_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpntgroup
ms.assetid: 02b4f7c1-480a-436c-8bae-7a2488be45d2
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 5c2128c95c4729d087a0e9bb9c8553d71600af14
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sphelpntgroup-transact-sql"></a>sp_helpntgroup (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Presenta información acerca de grupos de Windows que tienen cuentas en la base de datos actual.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helpntgroup [ [ @ntname= ] 'name' ]   
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@ntname =** ] **'***nombre***'**  
 Es el nombre del grupo de Windows. *nombre* es **sysname**, su valor predeterminado es null. *nombre* debe ser un grupo de Windows válido con acceso a la base de datos actual. Si *nombre* no se especifica, se incluyen todos los grupos de Windows con acceso a la base de datos actual en la salida.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**NTGroupName**|**sysname**|Nombre del grupo de Windows.|  
|**NTGroupId**|**smallint**|Id. del grupo.|  
|**SID**|**varbinary(85)**|Identificador de seguridad (SID) de **NTGroupName**.|  
|**HasDbAccess**|**int**|1 = el grupo de Windows tiene permiso de acceso a la base de datos.|  
  
## <a name="remarks"></a>Comentarios  
 Para ver una lista de los [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] roles en la base de datos actual, use **sp_helprole**.  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer al rol **public** .  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se presenta la lista de los grupos de Windows con acceso a la base de datos actual.  
  
```  
EXEC sp_helpntgroup;  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados de seguridad &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_grantdbaccess &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantdbaccess-transact-sql.md)   
 [sp_helprole &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helprole-transact-sql.md)   
 [sp_revokedbaccess &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokedbaccess-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
