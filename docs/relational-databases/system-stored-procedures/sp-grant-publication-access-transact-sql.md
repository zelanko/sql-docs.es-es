---
title: sp_grant_publication_access (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_grant_publication_access_TSQL
- sp_grant_publication_access
helpviewer_keywords: sp_grant_publication_access
ms.assetid: 17993952-def6-4a16-b1c1-323ec42967f8
caps.latest.revision: "31"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3a961e086d738d1784884142f22ed6dd45928897
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="spgrantpublicationaccess-transact-sql"></a>sp_grant_publication_access (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Agrega un inicio de sesión a la lista de acceso de la publicación. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_grant_publication_access [ @publication = ] 'publication', [ @login = ] 'login'   
    [ , [ @reserved = ] 'reserved' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication** =] **'***publicación***'**  
 Es el nombre de la publicación a la que se obtiene acceso. **'***publicación***'** es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@login** =] **'***inicio de sesión***'**  
 Es el identificador de inicio de sesión. **'***inicio de sesión***'** es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@reserved =**] **'***reservada***'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_grant_publication_access** se utiliza en instantáneas, transaccional y de mezcla.  
  
 Es posible llamar repetidamente a este procedimiento almacenado.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor o el **db_owner** rol fijo de base de datos puede ejecutar **sp_grant_publication_access**.  
  
## <a name="see-also"></a>Vea también  
 [sp_help_publication_access &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-publication-access-transact-sql.md)   
 [sp_revoke_publication_access &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-revoke-publication-access-transact-sql.md)   
 [Proteger el publicador](../../relational-databases/replication/security/secure-the-publisher.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
