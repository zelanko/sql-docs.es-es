---
title: sp_helpreplfailovermode (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_helpreplfailovermode
- sp_helpreplfailovermode_TSQL
helpviewer_keywords:
- sp_helpreplfailovermode
ms.assetid: d1090e42-6840-4bf6-9aa9-327fd8987ec2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: baeb94873abbd243803166b478a1e5e95b12c3cb
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47782033"
---
# <a name="sphelpreplfailovermode-transact-sql"></a>sp_helpreplfailovermode (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Muestra el modo de conmutación por error actual de una suscripción. Este procedimiento almacenado se ejecuta en el suscriptor de cualquier base de datos. Para obtener más información acerca de los modos de conmutación por error, consulte [suscripciones actualizables para la replicación transaccional](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helpreplfailovermode [ @publisher= ] 'publisher'   
    [ , [ @publisher_db = ] 'publisher_db' ]   
    [ , [ @publication = ] 'publication' ]   
    [ , [ @failover_mode_id= ] 'failover_mode_id'OUTPUT]   
    [ , [ @failover_mode = ] 'failover_mode'OUTPUT]   
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publisher=**] **'***publisher***'**  
 Es el nombre del publicador que participa en la actualización de este suscriptor. *publicador* es **sysname**, no tiene ningún valor predeterminado. El publicador debe estar configurado para publicación.  
  
 [  **@publisher_db =**] **'***publisher_db***'**  
 Es el nombre de la base de datos de publicación. *publisher_db* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@publication=**] **'***publicación***'**  
 Es el nombre de la publicación que participa en la actualización de este suscriptor. *publicación*es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@failover_mode_id=**] **'***failover_mode_id***' salida**  
 Devuelve el valor entero del modo de conmutación por error y es un **salida** parámetro. *failover_mode_id* es un **tinyint** con un valor predeterminado de **0**. Devuelve **0** para actualización inmediata y **1** actualización en cola.  
  
 [**@failover_mode=**] **'***failover_mode***' salida**  
 Devuelve el modo en que se realizan las modificaciones de datos en el suscriptor. *failover_mode* es un **nvarchar (10)** con el valor predeterminado es NULL. Es un **salida** parámetro.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**Inmediata**|Actualización inmediata: las actualizaciones del suscriptor se propagan inmediatamente al publicador utilizando un protocolo de confirmación en dos fases (2PC).|  
|**En la cola**|Actualización en cola: las actualizaciones realizadas en el suscriptor se almacenan en una cola.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_helpreplfailovermode** se utiliza en la replicación de instantáneas o replicación transaccional para las suscripciones que están habilitadas para actualización inmediata con actualización en cola como conmutación por error, en caso de error.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor o el **db_owner** rol fijo de base de datos se puede ejecutar **sp_helpreplfailovermode**.  
  
## <a name="see-also"></a>Vea también  
 [sp_setreplfailovermode &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-setreplfailovermode-transact-sql.md)  
  
  
