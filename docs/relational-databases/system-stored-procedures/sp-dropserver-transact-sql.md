---
title: sp_dropserver (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_dropserver_TSQL
- sp_dropserver
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dropserver
ms.assetid: 0fc83e35-0caa-49a3-a4b6-a1890d4f46ef
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 82f030a0f35a75bb1494035c9db8cd0ae0f002c0
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="spdropserver-transact-sql"></a>sp_dropserver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  Quita un servidor de la lista de servidores remotos y vinculados conocidos de la instancia local de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
[!INCLUDE[ssMIlimitation](../../includes/sql-db-mi-limitation.md)]

 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_dropserver [ @server = ] 'server'   
     [ , [ @droplogins = ] { 'droplogins' | NULL} ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@server =** ] **'***server***'**  
 Es el servidor que se va a quitar. *server* es de tipo **sysname**y no tiene ningún valor predeterminado. *servidor* debe existir.  
  
 [  **@droplogins =** ] **'droplogins'** | ES NULL  
 Indica que los inicios de sesión de servidor remoto o vinculado para *server* también deben quitarse si **droplogins** se especifica. **@droplogins** es **char (10)**, su valor predeterminado es null.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="remarks"></a>Comentarios  
 Si ejecuta **sp_dropserver** en un servidor que esté asociada a las entradas de inicio de sesión de servidor remoto o vinculado o se configura como un publicador de replicación, se devuelve un mensaje de error. Para quitar todos los inicios de sesión de servidor remoto o vinculado de un servidor al quitar el servidor, use la **droplogins** argumento.  
  
 **sp_dropserver** no se puede ejecutar dentro de una transacción definida por el usuario.  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso ALTER ANY LINKED SERVER en el servidor.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se quita el servidor remoto `ACCOUNTS` y todos los inicios de sesión remotos asociados de la instancia local de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
sp_dropserver 'ACCOUNTS', 'droplogins';  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados de seguridad &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)   
 [sp_dropremotelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropremotelogin-transact-sql.md)   
 [sp_helpremotelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpremotelogin-transact-sql.md)   
 [sp_helpserver & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
