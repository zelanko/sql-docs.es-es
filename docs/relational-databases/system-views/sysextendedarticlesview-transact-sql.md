---
title: sysextendedarticlesview (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sysextendedarticlesview_TSQL
- sysextendedarticlesview
dev_langs:
- TSQL
helpviewer_keywords:
- sysextendedarticlesview view
ms.assetid: 8bdd22f7-c268-49b6-820c-3fe603feb128
caps.latest.revision: 11
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 71faf31a4a38501c3a771b46ee680a1490fd05ac
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sysextendedarticlesview-transact-sql"></a>sysextendedarticlesview (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **sysextendedarticlesview** vista proporciona información sobre los artículos publicados. Esta vista se almacena en la base de datos de distribución.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|La columna de identidad que proporciona un número de identificación único para el artículo.|  
|**creation_script**|**nvarchar(255)**|Script de creación de esquemas para el artículo.|  
|**del_cmd**|**nvarchar(255)**|Comando para ejecutar con DELETE; en caso contrario, se construye a partir del registro.|  
|**Descripción**|**nvarchar(255)**|La entrada descriptiva del artículo.|  
|**dest_table**|**nvarchar(128)**|Nombre de la tabla de destino.|  
|**filter**|**int**|Identificador de objeto del procedimiento almacenado utilizado para la partición horizontal.|  
|**filter_clause**|**ntext**|La cláusula WHERE del artículo, utilizada para el filtrado horizontal.|  
|**ins_cmd**|**nvarchar(255)**|Comando que se ejecuta con INSERT.|  
|**Nombre**|**nvarchar(128)**|El nombre asociado al artículo, único en la publicación.|  
|**ObjID**|**int**|El Id. de objeto de la tabla publicada.|  
|**pubid**|**int**|Id. de la publicación a la que pertenece el artículo.|  
|**pre_creation_cmd**|**tinyint**|El comando anterior a la creación para DROP TABLE, DELETE TABLE o TRUNCATE:<br /><br /> **0** = none.<br /><br /> **1** = QUITAR.<br /><br /> **2** = DELETE.<br /><br /> **3** = TRUNCATE.|  
|**status**|**int**|La máscara de bits de las opciones y el estado del artículo, que puede ser el resultado de OR lógico bit a bit de uno o más de estos valores:<br /><br /> **1** = artículo está activo.<br /><br /> **8** = incluir el nombre de columna en las instrucciones INSERT.<br /><br /> **16** = utilizar instrucciones parametrizadas.<br /><br /> **24** = ambos incluyen el nombre de columna en las instrucciones INSERT y utilizar instrucciones con parámetros.<br /><br /> Por ejemplo, un artículo activo que utilice instrucciones con parámetros tendrá un valor de 17 en esta columna. Un valor de 0 significa que el artículo no está activo y no tiene otras propiedades definidas.|  
|**sync_objid**|**int**|El Id. de la tabla o vista que representa la definición del artículo.|  
|**Tipo**|**tinyint**|Tipo de artículo:<br /><br /> **1** = artículo basado en registro.<br /><br /> **3** = artículo basado en registro con filtro manual.<br /><br /> **5** = artículo basado en registro con vista manual.<br /><br /> **7** = artículo basado en registro con filtro manual y vista manual.|  
|**upd_cmd**|**nvarchar(255)**|Comando para ejecutar con UPDATE; en caso contrario, se construye a partir del registro.|  
|**schema_option**|**binario**|Indica qué propiedades del objeto publicado se convierten en script en la instantánea. Para obtener una lista de opciones de esquemas admitidas, consulte [sp_addarticle](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md).|  
|**dest_owner**|**nvarchar(128)**|Propietario de la tabla de la base de datos de destino.|  
|**ins_scripting_proc**|**int**|Identificador de objeto del procedimiento almacenado o script personalizados que se ejecutan al replicar una instrucción INSERT.|  
|**del_scripting_proc**|**int**|Identificador de objeto del procedimiento almacenado o script personalizados que se ejecutan al replicar una instrucción DELETE.|  
|**upd_scripting_proc**|**int**|Identificador de objeto del procedimiento almacenado o script personalizados que se ejecutan al replicar una instrucción UPDATE.|  
|**custom_script**|**int**|Identificador de objeto del procedimiento o script personalizados que se ejecutan cuando finaliza un desencadenador DDL.|  
|**fire_triggers_on_snapshot**|**int**|Indica si los desencadenadores replicados se ejecutan al aplicar la instantánea. Puede tener uno de estos valores:<br /><br /> **0** = no se ejecutan desencadenadores.<br /><br /> **1** = desencadenadores se ejecutan.|  
  
## <a name="see-also"></a>Vea también  
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_addarticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_changearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_helparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [sysarticles &#40;Transact-SQL&#41;](../../relational-databases/system-tables/sysarticles-transact-sql.md)  
  
  
