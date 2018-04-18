---
title: MSmerge_settingshistory (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSmerge_settingshistory
- MSmerge_settingshistory_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_settingshistory system table
ms.assetid: 0bdf2d5f-5502-44cd-aa9d-2d5006ad20ce
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9e01e404abe840e8ddea6514694f430e8097c518
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="msmergesettingshistory-transact-sql"></a>MSmerge_settingshistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **MSmerge_settingshistory** tabla se utiliza para mantener un historial de los cambios realizados a las propiedades de publicaciones y artículos para replicación de mezcla, con una fila por cada cambio realizado en una topología de replicación de mezcla. Esta tabla también almacena información acerca de cuándo se establecieron los valores de propiedad iniciales. Esta tabla se almacena en las bases de datos de publicación y de suscripciones.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**EventTime**|**datetime**|Fecha y hora del evento.|  
|**pubid**|**uniqueidentifier**|Número de identificación único de una determinada publicación.|  
|**artid**|**uniqueidentifier**|El número de identificación único del artículo indicado.|  
|**EventType**|**tinyint**|Especifica el tipo de evento que se va a registrar, que puede ser uno de los siguientes:<br /><br /> **1** : inicial de la configuración de la propiedad nivel de publicación.<br /><br /> **2** -cambiar en una propiedad de publicación.<br /><br /> **101** -inicial de la configuración de la propiedad de artículo.<br /><br /> **102** -cambiar en una propiedad del artículo.|  
|**propertyname**|**sysname**|Nombre de la propiedad establecida o cambiada.|  
|**previousvalue**|**sysname**|Valor de la propiedad anterior si se ha cambiado la propiedad.|  
|**NewValue**|**sysname**|Valor cambiado o creado en la propiedad.|  
|**eventText**|**nvarchar(2000)**|Cadena de caracteres que describe el evento.|  
  
## <a name="see-also"></a>Vea también  
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
