---
title: sp_changesubscription (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 10/28/2015
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- changesubscription
- sp_changesubscription
- changesubscription_TSQL
- sp_changesubscription_TSQL
helpviewer_keywords:
- sp_changesubscription
ms.assetid: f9d91fe3-47cf-4915-b6bf-14c9c3d8a029
caps.latest.revision: 40
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 47ce4c99261b7b7fd5ee7b3af4636d5ced5cf4f2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="spchangesubscription-transact-sql"></a>sp_changesubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cambia las propiedades de una suscripción de inserción transaccional o de instantáneas o de una suscripción de extracción relacionada con la replicación transaccional de actualización en cola. Para cambiar las propiedades de todos los demás tipos de suscripciones de extracción, utilice [sp_change_subscription_properties &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md). **sp_changesubscription** se ejecuta en el publicador de la base de datos de publicación.  
  
> [!IMPORTANT]  
>  Al configurar un publicador con un distribuidor remoto, los valores suministrados para todos los parámetros, incluidos *job_login* y *job_password*, se envían al distribuidor como texto sin formato. Antes de ejecutar este procedimiento almacenado, se recomienda cifrar la conexión entre el publicador y su distribuidor remoto. Para obtener más información, vea [Habilitar conexiones cifradas en el motor de base de datos &#40;Administrador de configuración de SQL Server&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_changesubscription [ @publication = ] 'publication'  
        , [ @article = ] 'article'  
        , [ @subscriber = ] 'subscriber'  
        , [ @destination_db = ] 'destination_db'  
        , [ @property = ] 'property'  
        , [ @value = ] 'value'  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@publication**=] **'***publicación***'**  
 Es el nombre de la publicación que se va a cambiar. *publicación*es **sysname**, no tiene ningún valor predeterminado  
  
 [ **@article** =] **'***artículo***'**  
 Es el nombre del artículo que se va a cambiar. *artículo* es **sysname**, no tiene ningún valor predeterminado.  
  
 [ **@subscriber** =] **'***suscriptor***'**  
 Es el nombre del suscriptor. *suscriptor* es **sysname**, no tiene ningún valor predeterminado.  
  
 [ **@destination_db** =] **'***destination_db***'**  
 Es el nombre de la base de datos de suscripción. *destination_db* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@property=**] **'***propiedad***'**  
 Es la propiedad que se va a cambiar para la suscripción especificada. *propiedad* es **nvarchar (30)**, y puede tener uno de los valores de la tabla.  
  
 [  **@value=**] **'***valor***'**  
 Es el nuevo valor para el elemento especificado *propiedad*. *valor* es **nvarchar (4000)**, y puede tener uno de los valores de la tabla.  
  
|Propiedad|Value|Description|  
|--------------|-----------|-----------------|  
|**distrib_job_login**||Inicio de sesión de la cuenta de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows en la que se ejecuta el agente.|  
|**distrib_job_password**||Contraseña de la cuenta de Windows con la que se ejecuta el agente.|  
|**subscriber_catalog**||Catálogo que debe utilizarse al establecer una conexión con el proveedor OLE DB. Solo es válida para esta propiedad no es[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] los suscriptores.|  
|**subscriber_datasource**||Nombre del origen de datos tal y como lo entiende el proveedor OLE DB. *Solo es válida para esta propiedad no es* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *los suscriptores.*|  
|**subscriber_location**||Ubicación de la base de datos tal y como la interpreta el proveedor OLE DB. *Solo es válida para esta propiedad no es* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *los suscriptores.*|  
|**subscriber_login**||Nombre de inicio de sesión del suscriptor.|  
|**subscriber_password**||Contraseña segura para el inicio de sesión que se ha proporcionado.|  
|**subscriber_security_mode**|**1**|Se utiliza la autenticación de Windows para la conexión con el suscriptor.|  
||**0**|Se utiliza la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para la conexión con el suscriptor.|  
|**subscriber_provider**||Identificador de programación único (PROGID) mediante el cual se registra el proveedor OLE DB para los orígenes de datos que no son de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *Solo es válida para esta propiedad no es* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *los suscriptores.*|  
|**subscriber_providerstring**||Cadena de conexión específica del proveedor OLE DB que identifica el origen de datos. *Solo es válida para esta propiedad no es* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *los suscriptores.*|  
|**flujos de suscripción**||Es el número de conexiones permitidas por Agente de distribución para aplicar lotes de cambios en paralelo a un suscriptor. Un intervalo de valores de **1** a **64** es compatible con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicadores. Esta propiedad debe ser **0** para no[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] los suscriptores, los publicadores de Oracle o suscripciones punto a punto.|  
|**propiedad subscriber_type**|**1**|Servidor del origen de datos ODBC|  
||**3**|Proveedor OLE DB|  
|**con optimización para memoria**|**bit**|Indica que la suscripción admite tablas optimizadas en memoria. *memory_optimized* es **bits**, donde 1 es igual a true (la suscripción es compatible con tablas optimizadas en memoria).|  
  
 [  **@publisher =** ] **'***publisher***'**  
 Especifica un publicador que no es de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *Publisher* es **sysname**, su valor predeterminado es null.  
  
> [!NOTE]  
>  *Publisher* no se debe especificar para una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publisher.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_changesubscription** se utiliza en la replicación de instantáneas y transaccional.  
  
 **sp_changesubscription** solo se puede utilizar para modificar las propiedades de las suscripciones de inserción o extracción relacionadas con la replicación transaccional de actualización en cola. Para cambiar las propiedades de todos los demás tipos de suscripciones de extracción, utilice [sp_change_subscription_properties &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md).  
  
 Después de cambiar un inicio de sesión o una contraseña de agente, debe detener y reiniciar el agente para que el cambio surta efecto.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor o **db_owner** rol fijo de base de datos puede ejecutar **sp_changesubscription**.  
  
## <a name="see-also"></a>Vea también  
 [sp_addsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)   
 [sp_dropsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)  
  
  
