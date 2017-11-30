---
title: sp_droplinkedsrvlogin (Transact-SQL) | Documentos de Microsoft
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
- sp_droplinkedsrvlogin_TSQL
- sp_droplinkedsrvlogin
dev_langs: TSQL
helpviewer_keywords: sp_droplinkedsrvlogin
ms.assetid: 75a4a040-72d5-4d29-8304-de0aa481ad4b
caps.latest.revision: "21"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a0d9e2ed37bd70dda7d1cf47f78a7f1c28692a0f
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2017
---
# <a name="spdroplinkedsrvlogin-transact-sql"></a>sp_droplinkedsrvlogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Quita una asignación existente entre un inicio de sesión del servidor local que ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y un inicio de sesión en el servidor vinculado.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_droplinkedsrvlogin [ @rmtsrvname= ] 'rmtsrvname' ,   
   [ @locallogin= ] 'locallogin'  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@rmtsrvname =** ] **'***rmtsrvname***'**  
 Es el nombre de un servidor vinculado que la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se aplica la asignación de inicio de sesión. *rmtsrvname* es **sysname**, no tiene ningún valor predeterminado. *rmtsrvname* ya debe existir.  
  
 [  **@locallogin =** ] **'***locallogin***'**  
 Es el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicio de sesión en el servidor local que tiene una asignación para el servidor vinculado *rmtsrvname*. *locallogin* es **sysname**, no tiene ningún valor predeterminado. Una asignación para *locallogin* a *rmtsrvname* ya debe existir. Si es NULL, la asignación predeterminada creada por **sp_addlinkedserver**, que asigna todos los inicios de sesión en el servidor local a inicios de sesión en el servidor vinculado, se elimina.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="remarks"></a>Comentarios  
 Cuando la asignación existente para un inicio de sesión se elimina, el servidor local utiliza la asignación predeterminada creada por **sp_addlinkedserver** cuando se conecta al servidor vinculado en nombre de ese inicio de sesión. Para cambiar la asignación predeterminada, use **sp_addlinkedsrvlogin**.  
  
 Si también se elimina la asignación predeterminada, solo los inicios de sesión que se les ha asignado explícitamente una asignación de inicio de sesión para el servidor vinculado, mediante el uso de **sp_addlinkedsrvlogin**, puede tener acceso al servidor vinculado.  
  
 **sp_droplinkedsrvlogin** no se puede ejecutar desde una transacción definida por el usuario.  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso ALTER ANY LOGIN en el servidor.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-removing-the-login-mapping-for-an-existing-user"></a>A. Quitar la asignación de inicio de sesión a un usuario existente  
 En el siguiente ejemplo se quita la asignación del inicio de sesión `Mary` del servidor local al servidor vinculado `Accounts`. Por tanto, el inicio de sesión `Mary` usa la asignación de inicio de sesión predeterminada.  
  
```  
EXEC sp_droplinkedsrvlogin 'Accounts', 'Mary';  
```  
  
### <a name="b-removing-the-default-login-mapping"></a>B. Quitar la asignación de inicio de sesión predeterminada  
 En el siguiente ejemplo se quita la asignación de inicio de sesión predeterminada creada originalmente al ejecutar `sp_addlinkedserver` en el servidor vinculado `Accounts`.  
  
```  
EXEC sp_droplinkedsrvlogin 'Accounts', NULL;  
```  
  
## <a name="see-also"></a>Vea también  
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_addlinkedsrvlogin &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
