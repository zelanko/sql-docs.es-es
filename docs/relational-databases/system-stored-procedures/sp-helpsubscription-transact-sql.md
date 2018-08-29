---
title: sp_helpsubscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_helpsubscription_TSQL
- sp_helpsubscription
helpviewer_keywords:
- sp_helpsubscription
ms.assetid: ff96bcbf-e2b9-4da8-8515-d80d4ce86c16
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e44e5ce6dac4f04703925b7f216e039acf8ae6cc
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43019349"
---
# <a name="sphelpsubscription-transact-sql"></a>sp_helpsubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Presenta la información de suscripción asociada con una publicación particular, un artículo, un suscriptor o un conjunto de suscripciones. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicaciones.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helpsubscription [ [ @publication = ] 'publication' ]   
    [ , [ @article = ] 'article' ]  
    [ , [ @subscriber = ] 'subscriber' ]  
    [ , [ @destination_db = ] 'destination_db' ]   
    [ , [ @found=] found OUTPUT ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication =** ] **'***publicación***'**  
 Es el nombre de la publicación asociada. *publicación* es **sysname**, su valor predeterminado es **%**, que devuelve información de todas las suscripciones para este servidor.  
  
 [  **@article=** ] **'***artículo***'**  
 Es el nombre del artículo. *artículo* es **sysname**, su valor predeterminado es **%**, que devuelve información de todas las suscripciones para las publicaciones y suscriptores seleccionados. Si **todas**, se devuelve una sola entrada por cada suscripción completa en una publicación.  
  
 [  **@subscriber=** ] **'***suscriptor***'**  
 Es el nombre del suscriptor acerca del cual se obtendrá la información de suscripción. *suscriptor* es **sysname**, su valor predeterminado es **%**, que devuelve información de todas las suscripciones para las publicaciones y artículos seleccionados.  
  
 [  **@destination_db=** ] **'***destination_db***'**  
 Es el nombre de la base de datos de destino. *destination_db* es **sysname**, su valor predeterminado es **%**.  
  
 [  **@found=** ] **'***encuentra***'** salida  
 Es una marca para indicar que se devuelven filas. *se encontró*es **int** y un parámetro OUTPUT y su valor predeterminado es 23456.  
  
 **1** indica que se encuentra la publicación.  
  
 **0** indica que no se encuentra la publicación.  
  
 [ **@publisher**=] **'***publisher***'**  
 Es el nombre del publicador. *publicador* es **sysname**y el valor predeterminado es el nombre del servidor actual.  
  
> [!NOTE]  
>  *publicador* no debe especificarse, excepto cuando es un publicador de Oracle.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**suscriptor**|**sysname**|Nombre del suscriptor.|  
|**publicación**|**sysname**|Nombre de la publicación.|  
|**article**|**sysname**|Nombre del artículo.|  
|**base de datos de destino**|**sysname**|Nombre de la base de datos de destino a la que se envían los datos duplicados.|  
|**estado de la suscripción**|**tinyint**|Estado de la suscripción:<br /><br /> **0** = inactivo<br /><br /> **1** = suscrito<br /><br /> **2** = activo|  
|**tipo de sincronización**|**tinyint**|Tipo de sincronización de suscripción:<br /><br /> **1** = automática<br /><br /> **2** = ninguno|  
|**tipo de suscripción**|**int**|Tipo de suscripción:<br /><br /> **0** = inserción<br /><br /> **1** = extracción<br /><br /> **2** = anónima|  
|**suscripción completa**|**bit**|Indica si la suscripción es a todos los artículos de la publicación:<br /><br /> **0** = No<br /><br /> **1** = Sí|  
|**nombre de la suscripción**|**nvarchar(255)**|Nombre de la suscripción.|  
|**modo de actualización**|**int**|**0** = solo lectura<br /><br /> **1** = la suscripción de actualización inmediata|  
|**Id. de trabajo de distribución**|**binary (16)**|Id. de trabajo del agente de distribución.|  
|**loopback_detection**|**bit**|La detección de bucles de retorno determina si el Agente de distribución envía las transacciones originadas en el suscriptor al mismo suscriptor:<br /><br /> **0** = las envía.<br /><br /> **1** = no no volver a enviar.<br /><br /> Se utilizan con replicación transaccional bidireccional. Para más información, consulte [Bidirectional Transactional Replication](../../relational-databases/replication/transactional/bidirectional-transactional-replication.md).|  
|**offload_enabled**|**bit**|Especifica si se ha establecido que la descarga de un agente de duplicación se lleve a cabo en el suscriptor.<br /><br /> Si **0**, agente se ejecuta en el publicador.<br /><br /> Si **1**, se ejecuta el agente en el suscriptor.|  
|**offload_server**|**sysname**|Nombre del servidor habilitado para la activación remota de agentes. Si es NULL, a continuación, el actual offload_server de [MSdistribution_agents](../../relational-databases/system-tables/msdistribution-agents-transact-sql.md) se utiliza la tabla.|  
|**dts_package_name**|**sysname**|Especifica el nombre del paquete de Servicios de transformación de datos (DTS).|  
|**dts_package_location**|**int**|Ubicación del paquete DTS, si se asigna uno a la suscripción. Si hay un paquete, un valor de **0** especifica la ubicación del paquete en el **distribuidor**. Un valor de **1** especifica la **suscriptor**.|  
|**subscriber_security_mode**|**smallint**|Es el modo de seguridad en el suscriptor, donde **1** significa autenticación de Windows y **0** significa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación.|  
|**subscriber_login**|**sysname**|Es el nombre de inicio de sesión del suscriptor.|  
|**subscriber_password**||La contraseña real del suscriptor no se devuelve nunca. El resultado se enmascara mediante una "**\*\*\*\*\*\***" cadena.|  
|**job_login**|**sysname**|Nombre de la cuenta de Windows en la que se ejecuta el Agente de distribución.|  
|**job_password**||La contraseña real del trabajo no se devuelve nunca. El resultado se enmascara mediante una "**\*\*\*\*\*\***" cadena.|  
|**distrib_agent_name**|**Nvarchar (100)**|Nombre del trabajo del agente que sincroniza la suscripción.|  
|**propiedad subscriber_type**|**tinyint**|Tipo de suscriptor, que puede ser uno de los siguientes:<br /><br /> **0** = suscriptor de SQL Server<br /><br /> **1** = servidor de origen de datos ODBC<br /><br /> **2** = base de datos Microsoft JET (desusado)<br /><br /> **3** = proveedor OLE DB|  
|**subscriber_provider**|**sysname**|Identificador de programación único (PROGID) mediante el cual se registra el proveedor OLE DB para los orígenes de datos que no son de SQL Server.|  
|**subscriber_datasource**|**nvarchar(4000)**|Nombre del origen de datos tal y como lo entiende el proveedor OLE DB.|  
|**subscriber_providerstring**|**nvarchar(4000)**|Cadena de conexión específica del proveedor OLE DB que identifica el origen de datos.|  
|**subscriber_location**|**nvarchar(4000)**|Ubicación de la base de datos tal y como la entiende el proveedor OLE DB|  
|**subscriber_catalog**|**sysname**|Catálogo que debe utilizarse al establecer una conexión con el proveedor OLE DB.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Notas  
 **sp_helpsubscription** se utiliza en la replicación de instantáneas y transaccional.  
  
## <a name="permissions"></a>Permisos  
 De forma predeterminada, los permisos de ejecución corresponden al rol **public** . Los usuarios solo reciben información de las suscripciones que hayan creado. Se devuelve información sobre todas las suscripciones a los miembros de la **sysadmin** rol fijo de servidor en el publicador o los miembros de la **db_owner** rol fijo de base de datos en la base de datos de publicación.  
  
## <a name="see-also"></a>Vea también  
 [sp_addsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)   
 [sp_changesubstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changesubstatus-transact-sql.md)   
 [sp_dropsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
