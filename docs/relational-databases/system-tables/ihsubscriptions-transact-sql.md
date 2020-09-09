---
description: IHsubscriptions (Transact-SQL)
title: IHsubscriptions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHsubscriptions_TSQL
- IHsubscriptions
dev_langs:
- TSQL
helpviewer_keywords:
- IHsubscriptions system table
ms.assetid: 9ec21119-35f1-4e39-abaa-b2c790c485b1
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b8dafdba96014fe7c60524a34d76d8bc36792762
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540944"
---
# <a name="ihsubscriptions-transact-sql"></a>IHsubscriptions (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  La tabla del sistema **IHsubscriptions** contiene una fila por cada suscripción a una publicación de un publicador que no es de SQL Server mediante el distribuidor actual. Esta tabla se almacena en la base de datos de distribución.  
  
## <a name="definition"></a>Definición  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**article_id**|**int**|Identifica un artículo publicado de forma exclusiva.|  
|**srvid**|**smallint**|Id. de servidor del suscriptor.|  
|**dest_db**|**sysname**|El nombre de la base de datos de destino|  
|**login_name**|**sysname**|El nombre de inicio de sesión utilizado al agregar la suscripción.|  
|**distribution_jobid**|**binario (16)**|El Id. de trabajo del Agente de distribución.|  
|**timestamp**|**timestamp**|Fecha y la hora de creación de la suscripción.|  
|**queued_reinit**|**bit**|Especifica si el artículo está marcado para inicialización o reinicialización. Un valor de **1** especifica que el artículo suscrito está marcado para inicialización o reinicialización.|  
|**status**|**tinyint**|El estado de la suscripción:<br /><br /> **0** = inactivo.<br /><br /> **1** = suscrito.<br /><br /> **2** = activo.|  
|**sync_type**|**tinyint**|El tipo de sincronización inicial:<br /><br /> **1** = automático.<br /><br /> **2** = ninguno.|  
|**subscription_type**|**int**|El tipo de suscripción:<br /><br /> **0** = inserciones: el agente de distribución se ejecuta en el suscriptor.<br /><br /> **1** = extracción: el agente de distribución se ejecuta en el distribuidor.|  
|**update_mode**|**tinyint**|Modo de actualización:<br /><br /> **0** = solo lectura.<br /><br /> **1** = actualización inmediata.|  
|**loopback_detection**|**bit**|Se aplica a las suscripciones que forman parte de una topología de replicación transaccional bidireccional. La detección de bucles de retorno determina si el Agente de distribución envía las transacciones originadas en el suscriptor al mismo suscriptor:<br /><br /> **0** = devuelve.<br /><br /> **1** = no devuelve.|  
  
## <a name="see-also"></a>Vea también  
 [Replicación de bases de datos heterogéneas](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_addsubscription &#40;&#41;de Transact-SQL ](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)   
 [sp_helpsubscription &#40;&#41;de Transact-SQL ](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)  
  
  
