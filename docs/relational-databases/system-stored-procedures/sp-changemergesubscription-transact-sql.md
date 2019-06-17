---
title: sp_changemergesubscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changemergesubscription_TSQL
- sp_changemergesubscription
helpviewer_keywords:
- sp_changemergesubscription
ms.assetid: fd820f35-c189-4e2d-884d-b60c1c469f58
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3b37e09147652e856ac0c4c8160c1d7d3caf6f6d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62993127"
---
# <a name="spchangemergesubscription-transact-sql"></a>sp_changemergesubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cambia las propiedades seleccionadas de una suscripción de inserción de mezcla. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
> [!IMPORTANT]  
>  Al configurar un publicador con un distribuidor remoto, los valores suministrados para todos los parámetros, incluidos *job_login* y *job_password*, se envían al distribuidor como texto sin formato. Antes de ejecutar este procedimiento almacenado, se recomienda cifrar la conexión entre el publicador y su distribuidor remoto. Para obtener más información, vea [Habilitar conexiones cifradas en el motor de base de datos &#40;Administrador de configuración de SQL Server&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_changemergesubscription [ [ @publication= ] 'publication' ]  
    [ , [ @subscriber= ] 'subscriber'  
    [ , [ @subscriber_db= ] 'subscriber_db' ]  
    [ , [ @property= ] 'property' ]  
    [ , [ @value= ] 'value' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'` Es el nombre de la publicación que se va a cambiar. *publicación* es **sysname**, su valor predeterminado es null. La publicación ya debe existir y ajustarse a las reglas para los identificadores.  
  
`[ @subscriber = ] 'subscriber'` Es el nombre del suscriptor. *suscriptor* es **sysname**, su valor predeterminado es null.  
  
`[ @subscriber_db = ] 'subscriber_db'` Es el nombre de la base de datos de suscripción. *subscriber_db*es **sysname**, su valor predeterminado es null.  
  
`[ @property = ] 'property'` Es la propiedad para cambiar para la publicación indicada. *propiedad* es **sysname**, y puede tener uno de los valores de la tabla.  
  
`[ @value = ] 'value'` Es el nuevo valor para el elemento especificado *propiedad*. *valor* es **nvarchar (255)** , y puede tener uno de los valores de la tabla.  
  
|Property|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**description**||Descripción de esta suscripción de mezcla.|  
|**priority**||Es la prioridad de la suscripción. La prioridad la utiliza el solucionador predeterminado para elegir un ganador cuando se detectan conflictos.|  
|**merge_job_login**||Inicio de sesión de la cuenta de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows en la que se ejecuta el agente.|  
|**merge_job_password**||Contraseña de la cuenta de Windows con la que se ejecuta el agente.|  
|**publisher_security_mode**|**1**|Se utiliza la autenticación de Windows para la conexión con el publicador.|  
||**0**|Se utiliza la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para la conexión con el publicador.|  
|**publisher_login**||Nombre de inicio de sesión en el publicador.|  
|**publisher_password**||Contraseña segura para el inicio de sesión del publicador que se ha proporcionado.|  
|**subscriber_security_mode**|**1**|Se utiliza la autenticación de Windows para la conexión con el suscriptor.|  
||**0**|Se utiliza la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para la conexión con el suscriptor.|  
|**subscriber_login**||Nombre de inicio de sesión del suscriptor.|  
|**subscriber_password**||Contraseña segura para el inicio de sesión del suscriptor que se ha proporcionado.|  
|**sync_type**|**automatic**|El esquema y los datos iniciales de las tablas publicadas se transfieren primero al suscriptor.|  
||**Ninguno**|El suscriptor ya tiene el esquema y los datos iniciales de las tablas publicadas; los datos y las tablas del sistema se transfieren siempre.|  
|**use_interactive_resolver**|**true**|Permite que los conflictos se resuelvan de forma interactiva para todos los artículos que lo permitan.|  
||**false**|Los conflictos se resuelven de forma automática mediante un solucionador predeterminado o personalizado.|  
|NULL (predeterminado)|NULL (predeterminado)||  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_changemergesubscription** se utiliza en la replicación de mezcla.  
  
 Después de cambiar un inicio de sesión o una contraseña de agente, debe detener y reiniciar el agente para que el cambio surta efecto.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor o **db_owner** rol fijo de base de datos se puede ejecutar **sp_changemergesubscription**.  
  
## <a name="see-also"></a>Vea también  
 [sp_addmergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)   
 [sp_dropmergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql.md)   
 [sp_helpmergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
