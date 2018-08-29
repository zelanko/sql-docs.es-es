---
title: sp_replmonitorhelppublisher (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
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
- sp_replmonitorhelppublisher_TSQL
- sp_replmonitorhelppublisher
helpviewer_keywords:
- sp_replmonitorhelppublisher
ms.assetid: 171501fe-4b74-4647-96c3-7691c777e01b
caps.latest.revision: 27
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9f2b7593890e4c3bab83855e74bb370e1411e74d
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43028230"
---
# <a name="spreplmonitorhelppublisher-transact-sql"></a>sp_replmonitorhelppublisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve información sobre el estado actual para uno o más publicadores asociados a un distribuidor. Este procedimiento almacenado, que se utiliza para supervisar la replicación, se ejecuta en el distribuidor en la base de datos de distribución.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_replmonitorhelppublisher [ [ @publisher = ] 'publisher' ]  
    [ , [ @refreshpolicy = ] refreshpolicy ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@publisher** =] **'***publisher***'**  
 Es el nombre del publicador cuyo estado se está supervisando. *publicador* es **sysname**, su valor predeterminado es null. Si el valor es NULL, se devuelve información para todos los publicadores que utilizan el distribuidor.  
  
 [  **@refreshpolicy=** ] *refreshpolicy*  
 Exclusivamente para uso interno.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**publicador**|**sysname**|Es el nombre de un publicador.|  
|**distribution_db**|**sysname**|Es el nombre de la base de datos de distribución utilizada por un publicador.|  
|**status**|**int**|Estado máximo de todos los agentes de replicación asociados a las publicaciones de este publicador, el cual puede ser uno de los valores siguientes.<br /><br /> **1** = iniciado<br /><br /> **2** = se ha realizado correctamente<br /><br /> **3** = en curso<br /><br /> **4** = inactivo<br /><br /> **5** = reintentando<br /><br /> **6** = error|  
|**Advertencia**|**int**|Advertencia de umbral máximo generada por una suscripción perteneciente a una publicación de este publicador, la cual puede ser el resultado lógico OR de uno o más de estos valores.<br /><br /> **1** = expiration: una suscripción a una publicación transaccional no se sincronizó dentro del umbral del período de retención.<br /><br /> **2** = latency: el tiempo necesario para replicar datos desde un publicador transaccional al suscriptor supera el umbral, en segundos.<br /><br /> **4** = mergeexpiration: una suscripción a una publicación de mezcla no se sincronizó dentro del umbral del período de retención.<br /><br /> **8** = mergefastrunduration: el tiempo necesario para completar la sincronización de una suscripción de mezcla supera el umbral, en segundos, a través de una conexión de red rápida.<br /><br /> **16** = mergeslowrunduration: el tiempo necesario para completar la sincronización de una suscripción de mezcla supera el umbral, en segundos, a través de una conexión de red lenta o telefónico.<br /><br /> **32** = mergefastrunspeed: la tasa de entrega de filas durante la sincronización de una suscripción de mezcla no ha podido mantener la tasa de umbral, en filas por segundo, a través de una conexión de red rápida.<br /><br /> **64** = mergeslowrunspeed: la tasa de entrega de filas durante la sincronización de una suscripción de mezcla no ha podido mantener la tasa de umbral, en filas por segundo, a través de una conexión de red lenta o telefónico.|  
|**publicationcount**|**int**|Es el número de publicaciones pertenecientes al publicador.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Notas  
 **sp_replmonitorhelppublisher** se utiliza con todos los tipos de replicación.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor en el distribuidor o los miembros de la **db_owner** o **replmonitor** pueden roles fijos de base de datos en la base de datos de distribución ejecutar **sp_replmonitorhelppublisher**.  
  
## <a name="see-also"></a>Vea también  
 [Supervisar la replicación mediante programación](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
