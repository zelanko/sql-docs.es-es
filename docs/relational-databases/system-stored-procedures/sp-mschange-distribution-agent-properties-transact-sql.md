---
title: sp_MSchange_distribution_agent_properties (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_MSchange_distribution_agent_properties
- sp_MSchange_distribution_agent_properties_TSQL
helpviewer_keywords:
- sp_MSchange_distribution_agent_properties
ms.assetid: 7dac5e68-bf84-433a-a531-66921f35126f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5b7ebae98b83c743fa2ea111a2809b3d1a043005
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52774137"
---
# <a name="spmschangedistributionagentproperties-transact-sql"></a>sp_MSchange_distribution_agent_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cambia las propiedades de un trabajo del agente de distribución que se ejecuta en un [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o versión posterior de distribuidor. Este procedimiento almacenado se utiliza para cambiar las propiedades cuando el publicador se ejecuta en una instancia de [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]. Este procedimiento almacenado se ejecuta en el distribuidor de la base de datos de distribución.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_MSchange_distribution_agent_properties [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'   
        , [ @subscriber = ] 'subscriber'   
        , [ @subscriber_db = ] 'subscriber_db'   
        , [ @property = ] 'property'   
        , [ @value = ] 'value' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@publisher** =] **'***publisher***'**  
 Es el nombre del publicador. *publicador* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@publisher_db=** ] **'***publisher_db***'**  
 Es el nombre de la base de datos de publicación. *publisher_db* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@publication =** ] **'***publicación***'**  
 Es el nombre de la publicación. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@subscriber=** ] **'***suscriptor***'**  
 Es el nombre del suscriptor. *suscriptor* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@subscriber_db=** ] **'***subscriber_db***'**  
 Es el nombre de la base de datos de suscripción. *subscriber_db* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@property =** ] **'***propiedad***'**  
 Es la propiedad de publicación que se va a cambiar. *propiedad* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@value =** ] **'***valor***'**  
 Es el nuevo valor de la propiedad. *valor* es **nvarchar (524)**, su valor predeterminado es null.  
  
 Esta tabla describe las propiedades del trabajo del Agente de distribución que se pueden cambiar y las restricciones en los valores de esas propiedades.  
  
|Property|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**distrib_job_login**||Inicio de sesión de la cuenta de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows en la que se ejecuta el agente.|  
|**distrib_job_password**||Contraseña de la cuenta de Windows en la que se ejecuta el trabajo del agente.|  
|**subscriber_catalog**||Catálogo que debe utilizarse al establecer una conexión con el proveedor OLE DB. *Esta propiedad sólo es válida para que no sean de* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *los suscriptores.*|  
|**subscriber_datasource**||Nombre del origen de datos tal y como lo entiende el proveedor OLE DB. *Esta propiedad sólo es válida para que no sean de* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *los suscriptores.*|  
|**subscriber_location**||Ubicación de la base de datos tal y como la interpreta el proveedor OLE DB. *Esta propiedad sólo es válida para que no sean de* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *los suscriptores.*|  
|**subscriber_login**||Inicio de sesión que se debe utilizar al conectarse a un suscriptor para sincronizar la suscripción.|  
|**subscriber_password**||Contraseña del suscriptor.<br /><br /> [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]|  
|**subscriber_provider**||Identificador de programación único (PROGID) mediante el cual se registra el proveedor OLE DB para los orígenes de datos que no son de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *Esta propiedad sólo es válida para que no sean de* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *los suscriptores.*|  
|**subscriber_providerstring**||Cadena de conexión específica del proveedor OLE DB que identifica el origen de datos. *Esta propiedad sólo es válida para que no son suscriptores de SQL Server.*|  
|**subscriber_security_mode**|**1**|Autenticación de Windows.<br /><br /> [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]|  
||**0**|Autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**propiedad subscriber_type**|**0**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] suscriptor|  
||**1**|Servidor del origen de datos ODBC|  
||**3**|Proveedor OLE DB|  
|**flujos de suscripción**||Indica el número de conexiones permitidas por Agente de distribución para aplicar lotes de cambios de forma paralela a un suscriptor. *No se admite para que no sean de* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *los suscriptores, los publicadores de Oracle o suscripciones punto a punto.*|  
  
> [!NOTE]  
>  Después de cambiar un inicio de sesión o una contraseña de agente, debe detener y reiniciar el agente para que el cambio surta efecto.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_MSchange_distribution_agent_properties** se utiliza en la replicación de instantáneas y transaccional.  
  
 Cuando el publicador se ejecuta en una instancia de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o una versión posterior, debe utilizar [sp_changesubscription](../../relational-databases/system-stored-procedures/sp-changesubscription-transact-sql.md) para cambiar las propiedades de un trabajo de agente de mezcla que sincronice una suscripción de inserción que se ejecuta en el distribuidor.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor en el distribuidor puede ejecutar **sp_MSchange_distribution_agent_properties**.  
  
## <a name="see-also"></a>Vea también  
 [sp_addpushsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md)   
 [sp_addsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)  
  
  
