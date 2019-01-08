---
title: sp_reinitsubscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_reinitsubscription
- sp_reinitsubscription_TSQL
helpviewer_keywords:
- sp_reinitsubscription
ms.assetid: d56ae218-6128-4ff9-b06c-749914505c7b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: da8e0d9ab1959251bf5e41e35e4b3d647e072d8a
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/11/2018
ms.locfileid: "53207342"
---
# <a name="spreinitsubscription-transact-sql"></a>sp_reinitsubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Marca las suscripciones para reinicialización. Este procedimiento almacenado se ejecuta en el publicador para suscripciones de inserción.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_reinitsubscription [ [ @publication = ] 'publication' ]  
    [ , [ @article = ] 'article' ]  
        , [ @subscriber = ] 'subscriber'  
    [ , [ @destination_db = ] 'destination_db']  
    [ , [ @for_schema_change = ] 'for_schema_change']  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @ignore_distributor_failure = ] ignore_distributor_failure ]   
    [ , [ @invalidate_snapshot = ] invalidate_snapshot ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication=**] **'***publicación***'**  
 Es el nombre de la publicación. *publicación* es **sysname**, con un valor predeterminado es all.  
  
 [  **@article=**] **'***artículo***'**  
 Es el nombre del artículo. *artículo* es **sysname**, con un valor predeterminado es all. Para una publicación de actualización inmediata, *artículo* debe ser **todas**; en caso contrario, el procedimiento almacenado omite la publicación y notifica un error.  
  
 [  **@subscriber=**] **'***suscriptor***'**  
 Es el nombre del suscriptor. *suscriptor* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@destination_db=**] **'***destination_db***'**  
 Es el nombre de la base de datos de destino. *destination_db* es **sysname**, con un valor predeterminado es all.  
  
 [  **@for_schema_change=**] **'***for_schema_change***'**  
 Indica si la reinicialización se produce como resultado de un cambio de esquema en la base de datos de publicación. *for_schema_change* es **bit**, su valor predeterminado es 0. Si **0**, las suscripciones activas para las publicaciones que permiten la actualización inmediata se reactivan siempre y cuando toda la publicación y no solo algunos de los artículos se reinicialicen. Esto significa que la reinicialización se produce como resultado de un cambio de esquema. Si **1**, las suscripciones activas no se reactivan hasta que se ejecuta el agente de instantáneas.  
  
 [  **@publisher=** ] **'***publisher***'**  
 Especifica que no es [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publisher. *publicador* es **sysname**, su valor predeterminado es null.  
  
> [!NOTE]  
>  *publicador* no debe usarse para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicadores.  
  
 [  **@ignore_distributor_failure=** ] *ignore_distributor_failure*  
 Permite la reinicialización incluso si el distribuidor no existe o está sin conexión. *ignore_distributor_failure* es **bit**, su valor predeterminado es 0. Si **0**, reinicialización se produce un error si el distribuidor no existe o está sin conexión.  
  
 [  **@invalidate_snapshot=** ] *invalidate_snapshot*  
 Invalida la instantánea de publicación existente. *invalidate_snapshot* es **bit**, su valor predeterminado es 0. Si **1**, se genera una nueva instantánea para la publicación.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_reinitsubscription** se utiliza en la replicación transaccional.  
  
 **sp_reinitsubscription** no se admite para la replicación transaccional punto a punto.  
  
 Para aquellas suscripciones en las que se aplica automáticamente la instantánea inicial y en las que la publicación no admite suscripciones actualizables, es necesario ejecutar el Agente de instantáneas después de ejecutar el procedimiento almacenado a fin de que el esquema y los archivos del programa de copia masiva estén preparados; a continuación, los Agentes de distribución estarán preparados para volver a sincronizar las suscripciones.  
  
 Para aquellas suscripciones en las que la instantánea inicial se aplica automáticamente y en las que la publicación admite suscripciones actualizables, el Agente de distribución vuelve a sincronizar la suscripción utilizando el esquema y los archivos del programa de copia masiva más recientes creados previamente por el Agente de instantáneas. El agente de distribución vuelve a sincronizar la suscripción inmediatamente después de que el usuario ejecuta **sp_reinitsubscription**, si el agente de distribución no está ocupado; de lo contrario, la sincronización puede producir cuando el intervalo de mensaje () especificado por el parámetro de línea de comandos del agente de distribución: **MessageInterval**).  
  
 **sp_reinitsubscription** no tiene ningún efecto en las suscripciones donde se aplica manualmente la instantánea inicial.  
  
 Para volver a sincronizar las suscripciones anónimas a una publicación, pase **todas** o NULL como *suscriptor*.  
  
 La replicación transaccional admite la reinicialización de suscripciones en el nivel del artículo. La instantánea del artículo se volverá a aplicar en el suscriptor durante la siguiente sincronización una vez que se haya marcado el artículo para reinicializarlo. Sin embargo, si hay artículos dependientes a los que también está suscrito el mismo suscriptor, se puede generar un error al volver a aplicar la instantánea en el artículo, a menos que los artículos dependientes de la publicación se reinicialicen también automáticamente en determinadas circunstancias:  
  
-   Si el comando de creación previa del artículo es 'drop', los artículos de vistas y procedimientos almacenados enlazados a un esquema del objeto base de ese artículo también se marcan para reinicializarlos.  
  
-   Si la opción de esquema del artículo incluye scripting de integridad referencial declarada en las claves principales, los artículos que tienen tablas base con relaciones de clave externa con tablas base del artículo reinicializado también se marcan para reinicializarlos.  
  
## <a name="example"></a>Ejemplo  
 [!code-sql[HowTo#sp_reinittranpushsub](../../relational-databases/replication/codesnippet/tsql/sp-reinitsubscription-tr_1.sql)]  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor, los miembros de la **db_owner** rol fijo de base de datos o el creador de la suscripción puede ejecutar **sp_reinitsubscription** .  
  
## <a name="see-also"></a>Vea también  
 [Reinicializar una suscripción](../../relational-databases/replication/reinitialize-a-subscription.md)   
 [Reinicializar suscripciones](../../relational-databases/replication/reinitialize-subscriptions.md)   
 [Procedimientos almacenados de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
