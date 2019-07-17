---
title: sp_link_publication (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_link_publication_TSQL
- sp_link_publication
helpviewer_keywords:
- sp_link_publication
ms.assetid: 1945ed24-f9f1-4af6-94ca-16d8e864706e
author: stevestein
ms.author: sstein
ms.openlocfilehash: 17c1c2a5ccb7ef9e7c4a3d843f63edde1f134016
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68139895"
---
# <a name="splinkpublication-transact-sql"></a>sp_link_publication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Establece la información de configuración y de seguridad que utilizan los desencadenadores de sincronización de las suscripciones de actualización inmediata al conectar con el publicador. Este procedimiento almacenado se ejecuta en el suscriptor de la base de datos de suscripción.  
  
> [!IMPORTANT]
>  Al configurar un publicador con un distribuidor remoto, los valores suministrados para todos los parámetros, incluidos *job_login* y *job_password*, se envían al distribuidor como texto sin formato. Antes de ejecutar este procedimiento almacenado, se recomienda cifrar la conexión entre el publicador y su distribuidor remoto. Para obtener más información, vea [Habilitar conexiones cifradas en el motor de base de datos &#40;Administrador de configuración de SQL Server&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
> 
> [!IMPORTANT]
>  Bajo ciertas condiciones, este procedimiento almacenado puede producir un error si el suscriptor se está ejecutando [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 1 o posterior y el publicador está ejecutando una versión anterior. Si el procedimiento almacenado genera un error en este escenario, actualice el publicador al Service Pack 1 de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o posterior.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_link_publication [ @publisher = ] 'publisher'   
        , [ @publisher_db = ] 'publisher_db'   
        , [ @publication = ] 'publication'   
        , [ @security_mode = ] security_mode  
    [ , [ @login = ] 'login' ]  
    [ , [ @password = ]'password' ]  
    [ , [ @distributor = ] 'distributor' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publisher = ] 'publisher'` Es el nombre del publicador para vincular a. *publicador* es **sysname**, no tiene ningún valor predeterminado.  
  
`[ @publisher_db = ] 'publisher_db'` Es el nombre de la base de datos del publicador para vincular a. *publisher_db* es **sysname**, no tiene ningún valor predeterminado.  
  
`[ @publication = ] 'publication'` Es el nombre de la publicación para vincular a. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
`[ @security_mode = ] security_mode` Es el modo de seguridad utilizado por el suscriptor para conectarse a un publicador remoto para la actualización inmediata. *security_mode* es **int**, y puede tener uno de estos valores. [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**0**|Usa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación con el inicio de sesión especificado en este procedimiento almacenado como *inicio de sesión* y *contraseña*.<br /><br /> Nota: En versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esta opción se utiliza para especificar una llamada dinámica de procedimiento remoto (RPC).|  
|**1**|Utiliza el contexto de seguridad (autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o autenticación de Windows) del usuario que realiza el cambio en el suscriptor.<br /><br /> Nota: Esta cuenta también debe existir en el publicador con privilegios suficientes. Al usar la autenticación de Windows, se debe admitir la delegación de cuentas de seguridad.|  
|**2**|Utiliza una existente, definido por el usuario inicio de sesión vinculado creado mediante **sp_link_publication**.|  
  
`[ @login = ] 'login'` Es el inicio de sesión. *login* es de tipo **sysname** y su valor predeterminado es NULL. Este parámetro debe especificarse cuando *security_mode* es **0**.  
  
`[ @password = ] 'password'` Es la contraseña. *contraseña* es **sysname**, su valor predeterminado es null. Este parámetro debe especificarse cuando *security_mode* es **0**.  
  
`[ @distributor = ] 'distributor'` Es el nombre del distribuidor. *distribuidor* es **sysname**, su valor predeterminado es null.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_link_publication** utiliza suscripciones de actualización inmediata en la replicación transaccional.  
  
 **sp_link_publication** puede utilizarse para las suscripciones de inserción y extracción. Se puede llamar antes o después de haber creado la suscripción. Se inserta una entrada o se actualiza en el [MSsubscription_properties &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/mssubscription-properties-transact-sql.md) tabla del sistema.  
  
 Para las suscripciones de inserción, la entrada puede limpiarse por [sp_subscription_cleanup &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql.md). Para las suscripciones de extracción, la entrada puede limpiarse por [sp_droppullsubscription &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-droppullsubscription-transact-sql.md) o [sp_subscription_cleanup &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql.md). También puede llamar a **sp_link_publication** con una contraseña NULL para borrar la entrada en el [MSsubscription_properties &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/mssubscription-properties-transact-sql.md) tabla del sistema por motivos de seguridad.  
  
 El modo predeterminado que utiliza un suscriptor de actualización inmediata cuando se conecta al publicador no permite una conexión mediante la autenticación de Windows. Para conectar con un modo de autenticación de Windows, se deberá configurar un servidor vinculado como publicador, y el suscriptor de actualización inmediata debe utilizar esta conexión cuando actualice el suscriptor. Esto requiere la **sp_link_publication** se ejecuten con *security_mode* = **2**. Al usar la autenticación de Windows, se debe admitir la delegación de cuentas de seguridad.  
  
## <a name="example"></a>Ejemplo  
 [!code-sql[HowTo#sp_addtranpullsubscriptionagent_failover](../../relational-databases/replication/codesnippet/tsql/sp-link-publication-tran_1.sql)]  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor puede ejecutar **sp_link_publication**.  
  
## <a name="see-also"></a>Vea también  
 [sp_droppullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droppullsubscription-transact-sql.md)   
 [sp_helpsubscription_properties &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)   
 [sp_subscription_cleanup &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
