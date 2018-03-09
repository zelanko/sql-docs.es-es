---
title: MSpublications (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSpublications
- MSpublications_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSpublications system table
ms.assetid: 7a0b3457-7265-4f24-a255-7f055d908f20
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9541a06cddbfad77ab404c6780076c633989a5e8
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="mspublications-transact-sql"></a>MSpublications (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **MSpublications** tabla contiene una fila por cada publicación que replica un publicador. Esta tabla se almacena en la base de datos de distribución.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**iddeeditor**|**smallint**|El identificador del publicador.|  
|**publisher_db**|**sysname**|Nombre de la base de datos del publicador.|  
|**publicación**|**sysname**|Nombre de la publicación.|  
|**publication_id**|**int**|Id. de la publicación.|  
|**publication_type**|**int**|Tipo de publicación:<br /><br /> **0** = transaccional.<br /><br /> **1** = instantánea.<br /><br /> **2** = la mezcla.|  
|**thirdparty_flag**|**bit**|Indica si una publicación es un [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos:<br /><br /> **0** = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> **1** = origen de datos distinto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**independent_agent**|**bit**|Indica si hay un agente de distribución independiente para esta publicación.|  
|**immediate_sync**|**bit**|Indica si los archivos de sincronización se crean o se vuelven a crear cada vez que se ejecuta el Agente de instantáneas.|  
|**allow_push**|**bit**|Indica si es posible crear suscripciones de inserción para la publicación indicada.|  
|**allow_pull**|**bit**|Indica si es posible crear suscripciones de extracción para la publicación indicada.|  
|**allow_anonymous**|**bit**|Indica si es posible crear suscripciones anónimas para la publicación indicada.|  
|**Descripción**|**nvarchar(255)**|Descripción de la publicación.|  
|**$vendor_name**|**nvarchar (100)**|Nombre del proveedor si el publicador no es una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**retención**|**int**|Período de retención de la publicación, expresado en horas.|  
|**sync_method**|**int**|Método de sincronización:<br /><br /> **0** = nativo (produce una salida de copia masiva en modo nativo de todas las tablas).<br /><br /> **1** = carácter (produce una salida de copia masiva en modo carácter de todas las tablas).<br /><br /> **3** = simultáneo (produce salida de copia masiva en modo nativo de todas las tablas, pero no bloquea la tabla durante la instantánea).<br /><br /> **4** = Concurrent_c (produce una salida de copia masiva en modo carácter de todas las tablas, pero no bloquea la tabla durante la instantánea)<br /><br /> Los valores **3** y **4** están disponibles para la replicación transaccional y la replicación de mezcla, pero no para replicación de instantáneas.|  
|**allow_subscription_copy**|**bit**|Habilita o deshabilita la funcionalidad de copia de las bases de datos de suscripciones suscritas a esta publicación. **0** significa que la copia está deshabilitada, y **1** significa que está habilitada.|  
|**thirdparty_options**|**int**|Especifica si la presentación de una publicación en la carpeta de replicación de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] se suprime:<br /><br /> **0** = muestra una publicación heterogénea en la carpeta de replicación en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].<br /><br /> **1** = suprime la visualización de una publicación heterogénea en la carpeta de replicación en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].|  
|**allow_queued_tran**|**bit**|Especifica si la publicación admite la actualización en cola:<br /><br /> **0 =** publicación es distinta en la cola.<br /><br /> **1** = publicación está en cola.|  
|**Opciones**|**int**|No hay información disponible para esta versión.|  
  
## <a name="see-also"></a>Vea también  
 [Tablas de replicación &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
