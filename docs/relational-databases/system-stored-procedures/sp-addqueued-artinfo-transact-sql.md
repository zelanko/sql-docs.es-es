---
title: sp_addqueued_artinfo (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
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
- sp_addqueued_artinfo
- sp_addqueued_artinfo_TSQL
helpviewer_keywords:
- sp_addqueued_artinfo
ms.assetid: decdb6eb-3dcd-4053-a21d-fd367c3fbafb
caps.latest.revision: 20
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 1bb30e29e1e3dc8d23dfff4a105d835470e51ea9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="spaddqueuedartinfo-transact-sql"></a>sp_addqueued_artinfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  
  
> [!IMPORTANT]  
>  El [sp_script_synctran_commands](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md) procedimiento debe usarse en lugar de **sp_addqueued_artinfo**. [sp_script_synctran_commands](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md) genera un script que contiene el **sp_addqueued_artinfo** y **sp_addsynctrigger** llamadas.  
  
 Crea el [MSsubscription_articles](../../relational-databases/system-tables/mssubscription-articles-transact-sql.md) tabla del suscriptor que se usa para realizar un seguimiento de información de suscripción de artículo (actualización en cola y actualización inmediata con actualización en cola como conmutación por error). Este procedimiento almacenado se ejecuta en el suscriptor de la base de datos de suscripción.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_addqueued_artinfo [ @artid= ] 'artid'  
        , [ @article= ] 'article'  
        , [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'  
        , [ @dest_table= ] 'dest_table'  
        , [ @owner = ] 'owner'  
        , [ @cft_table= ] 'cft_table'  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@artid=** ] **'***artid***'**  
 Es el nombre del id. de artículo. *artid* es **int**, no tiene ningún valor predeterminado  
  
 [  **@article=**] **'***artículo***'**  
 Es el nombre del artículo que se va a agregar al script. *artículo* es **sysname**, no tiene ningún valor predeterminado  
  
 [  **@publisher=**] **'***publisher***'**  
 Es el nombre del servidor del publicador. *Publisher* es **sysname**, no tiene ningún valor predeterminado.  
  
 [ **@publisher_db=**] **'***publisher_db***'**  
 Es el nombre de la base de datos del publicador. *publisher_db* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@publication=**] **'***publicación***'**  
 Es el nombre de la publicación de la que se va a crear un script. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@dest_table=** ] *'dest_table ***'**  
 Es el nombre de la tabla de destino. *dest_table* es **sysname**, no tiene ningún valor predeterminado.  
  
 [ **@owner =** ] **'***propietario***'**  
 Es el propietario de la suscripción. *propietario* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@cft_table=** ] **'***cft_table***'**  
 Nombre de la tabla de conflictos de actualización en cola de este artículo. *cft_table*es **sysname**, no tiene ningún valor predeterminado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_addqueued_artinfo** es utilizado por el agente de distribución como parte de la inicialización de la suscripción. Los usuarios no suelen ejecutar este procedimiento almacenado, pero puede resultar útil si el usuario debe configurar manualmente una suscripción.  
  
 [sp_script_synctran_commands](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md) en lugar de **sp_addqueued_artinfo**.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor o **db_owner** rol fijo de base de datos puede ejecutar **sp_addqueued_artinfo**.  
  
## <a name="see-also"></a>Vea también  
 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [sp_script_synctran_commands &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md)   
 [MSsubscription_articles &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mssubscription-articles-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
