---
title: sp_droplinkedsrvlogin (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_droplinkedsrvlogin_TSQL
- sp_droplinkedsrvlogin
dev_langs:
- TSQL
helpviewer_keywords:
- sp_droplinkedsrvlogin
ms.assetid: 75a4a040-72d5-4d29-8304-de0aa481ad4b
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 3040f585e10816d4f8664566be8af1523048db88
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82830137"
---
# <a name="sp_droplinkedsrvlogin-transact-sql"></a>sp_droplinkedsrvlogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Quita una asignación existente entre un inicio de sesión del servidor local que ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y un inicio de sesión en el servidor vinculado.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_droplinkedsrvlogin [ @rmtsrvname= ] 'rmtsrvname' ,   
   [ @locallogin= ] 'locallogin'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @rmtsrvname = ] 'rmtsrvname'`Es el nombre de un servidor vinculado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al que se aplica la asignación de inicio de sesión. *rmtsrvname* es de **tipo sysname**y no tiene ningún valor predeterminado. *rmtsrvname* ya debe existir.  
  
`[ @locallogin = ] 'locallogin'`Es el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Inicio de sesión en el servidor local que tiene una asignación al servidor vinculado *rmtsrvname*. *locallogin* es de **tipo sysname**y no tiene ningún valor predeterminado. Ya debe existir una asignación para *locallogin* a *rmtsrvname* . Si es NULL, se elimina la asignación predeterminada creada por **sp_addlinkedserver**, que asigna todos los inicios de sesión del servidor local a los inicios de sesión en el servidor vinculado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="remarks"></a>Observaciones  
 Cuando se elimina la asignación existente para un inicio de sesión, el servidor local utiliza la asignación predeterminada creada por **sp_addlinkedserver** cuando se conecta al servidor vinculado en nombre de ese inicio de sesión. Para cambiar la asignación predeterminada, use **sp_addlinkedsrvlogin**.  
  
 Si también se elimina la asignación predeterminada, solo los inicios de sesión a los que se haya asignado explícitamente una asignación de inicio de sesión al servidor vinculado, mediante **sp_addlinkedsrvlogin**, pueden tener acceso al servidor vinculado.  
  
 **sp_droplinkedsrvlogin** no se puede ejecutar desde una transacción definida por el usuario.  
  
## <a name="permissions"></a>Permisos  
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
  
## <a name="see-also"></a>Consulte también  
 [sp_addlinkedserver &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_addlinkedsrvlogin &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
