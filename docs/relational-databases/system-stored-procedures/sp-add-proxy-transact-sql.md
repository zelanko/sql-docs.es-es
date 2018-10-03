---
title: sp_add_proxy (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_proxy
- sp_add_proxy_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE PROXY statement
- sp_add_proxy
ms.assetid: cb59df37-f103-439b-bec1-2871fb669a8b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e9353e797f5ff84101726b0cfe7d12020f14fca3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47811453"
---
# <a name="spaddproxy-transact-sql"></a>sp_add_proxy (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Agrega el proxy del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especificado.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_add_proxy  
    [ @proxy_name = ] 'proxy_name' ,  
    [ @enabled = ] is_enabled ,  
    [ @description = ] 'description' ,  
    [ @credential_name = ] 'credential_name' ,  
    [ @credential_id = ] credential_id ,  
    [ @proxy_id = ] id OUTPUT   
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@proxy_name**=] **'***proxy_name***'**  
 Nombre del proxy que se va a crear. El *proxy_name* es **sysname**, su valor predeterminado es null. Cuando el *proxy_name* es NULL o una cadena vacía, el nombre de los valores predeterminados de proxy para el *user_name* proporcionado.  
  
 [ **@enabled** =] *is_enabled*  
 Especifica si el proxy está habilitado. El *is_enabled* marca es **tinyint**, su valor predeterminado es 1. Cuando *is_enabled* es **0**, el proxy no está habilitado y no puede utilizarse por un paso de trabajo.  
  
 [ **@description**=] **'***descripción***'**  
 Descripción del proxy. La descripción es **nvarchar (512)**, su valor predeterminado es null. La descripción permite documentar el proxy. El Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no le da otros usos. Por tanto, este argumento es opcional.  
  
 [ **@credential_name** =] **'***credential_name***'**  
 Nombre de la credencial para el proxy. El *credential_name* es **sysname**, su valor predeterminado es null. Cualquier *credential_name* o *credential_id* debe especificarse.  
  
 [ **@credential_id** =] *credential_id*  
 Número de identificación de la credencial para el proxy. El *credential_id* es **int**, su valor predeterminado es null. Cualquier *credential_name* o *credential_id* debe especificarse.  
  
 [ **@proxy_id**=] *id* salida  
 Número de identificación que se ha asignado al proxy si éste se ha creado correctamente.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Comentarios  
 Este procedimiento almacenado se debe ejecutar en el **msdb** base de datos.  
  
 Un proxy del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] administra la seguridad para los pasos de trabajo que afectan a los subsistemas que no sean [!INCLUDE[tsql](../../includes/tsql-md.md)]. Cada proxy se corresponde con unas credenciales de seguridad. Un proxy puede tener acceso a cualquier número de subsistemas.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de seguridad puede ejecutar este procedimiento.  
  
 Los miembros de la **sysadmin** rol fijo de seguridad puede crear pasos de trabajo que utilicen cualquier proxy. Use el procedimiento almacenado [sp_grant_login_to_proxy &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-grant-login-to-proxy-transact-sql.md) para conceder acceso de otros inicios de sesión al proxy.  
  
## <a name="examples"></a>Ejemplos  
 En este ejemplo se crea un proxy para la credencial `CatalogApplicationCredential`. El código da por supuesto que la credencial ya existe. Para obtener más información acerca de las credenciales, vea [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md).  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_proxy  
    @proxy_name = 'Catalog application proxy',  
    @enabled = 1,  
    @description = 'Maintenance tasks on catalog application.',  
    @credential_name = 'CatalogApplicationCredential' ;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [sp_grant_login_to_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grant-login-to-proxy-transact-sql.md)   
 [sp_revoke_login_from_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revoke-login-from-proxy-transact-sql.md)  
  
  
