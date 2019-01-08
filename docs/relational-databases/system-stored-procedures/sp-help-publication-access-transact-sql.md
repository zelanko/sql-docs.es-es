---
title: sp_help_publication_access (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_help_publication_access
- sp_help_publication_access_TSQL
helpviewer_keywords:
- sp_help_publication_access
ms.assetid: 9408fa13-54a0-4cb1-8fb0-845e5536ef50
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d9c6a12ae648ab11fbdf28f04e6c29733fad8ce0
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52786377"
---
# <a name="sphelppublicationaccess-transact-sql"></a>sp_help_publication_access (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve una lista de todos los inicios de sesión concedidos para una publicación. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_help_publication_access [ @publication = ] 'publication'  
    [ , [ @return_granted = ] 'return_granted' ]   
    [ , [ @login = ] 'login' ]  
    [ , [ @initial_list = ] initial_list ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication=**] **'***publicación***'**  
 Es el nombre de la publicación a la que se obtiene acceso. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@return_granted=**] **'***return_granted***'**  
 Es el identificador de inicio de sesión. *return_granted* es **bit**, su valor predeterminado es 1. Si **0** se especifica y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se utiliza la autenticación, se devuelven los inicios de sesión disponibles que aparecen en el publicador pero no en el distribuidor. Si **0** se especifica y se utiliza la autenticación de Windows, los inicios de sesión que se han denegado específicamente no tengan acceso a cualquiera al publicador o distribuidor se devuelven.  
  
 [  **@login=**] **'***inicio de sesión***'**  
 Es el identificador de inicio de sesión de seguridad estándar. *inicio de sesión* es **sysname**, su valor predeterminado es **%**.  
  
 [  **@initial_list =**] *initial_list*  
 Especifica si se van a devolver todos los miembros con acceso de publicación o solo aquellos que disponían de acceso antes de la adición de nuevos miembros a la lista. *initial_list* es de tipo bit, su valor predeterminado es **0**.  
  
 **1** devuelve información para todos los miembros de la **sysadmin** rol fijo de servidor con los inicios de sesión válidos en el distribuidor que existía cuando se creó la publicación, así como el inicio de sesión actual.  
  
 **0** devuelve información para todos los miembros de la **sysadmin** rol fijo de servidor con los inicios de sesión válidos en el distribuidor que existía cuando se creó la publicación, así como todos los usuarios en la lista de acceso de publicación que no pertenecen a la **sysadmin** rol fijo de servidor.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**LoginName**|**nvarchar(256)**|Nombre de inicio de sesión real.|  
|**isntname**|**int**|**0** = inicio de sesión no es un usuario de Windows.<br /><br /> **1** = inicio de sesión es un usuario de Windows.|  
|**isntgroup**|**int**|**0** = inicio de sesión no es un grupo de Windows.<br /><br /> **1** = inicio de sesión es un grupo de Windows.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_help_publication_access** se utiliza en todos los tipos de replicación.  
  
 Cuando ambos **Isntname** y **Isntgroup** en el resultado son conjunto **0**, se supone que el inicio de sesión es un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicio de sesión.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor o el **db_owner** rol fijo de base de datos se puede ejecutar **sp_help_publication_access**.  
  
## <a name="see-also"></a>Vea también  
 [sp_grant_publication_access &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grant-publication-access-transact-sql.md)   
 [sp_revoke_publication_access &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revoke-publication-access-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
