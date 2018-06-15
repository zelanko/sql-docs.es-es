---
title: IHextendedArticleView (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
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
- IHextendedArticleView_TSQL
- IHextendedArticleView
dev_langs:
- TSQL
helpviewer_keywords:
- IHextendedArticleView view
ms.assetid: 19ef0a12-3214-4bb0-9c25-a665897e65a2
caps.latest.revision: 11
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2e0bcc294189f4902fd8d39de230166e6956dd53
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "33010382"
---
# <a name="ihextendedarticleview-transact-sql"></a>IHextendedArticleView (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **IHextendedArticleView** vista expone información sobre los artículos de una publicación no es de SQL Server. Esta vista se almacena en la **distribución** base de datos.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|Identificador único del publicador.|  
|**publication_id**|**int**|Identificador único de la publicación.|  
|**article**|**sysname**|Nombre del artículo.|  
|**destination_object**|**sysname**|Nombre del objeto publicado en el suscriptor.|  
|**source_owner**|**sysname**|Propietario del objeto publicado en el publicador.|  
|**source_object**|**sysname**|Nombre del objeto publicado en el publicador.|  
|**Descripción**|**nvarchar(255)**|Descripción del artículo.|  
|**creation_script**|**nvarchar(255)**|Script de creación de esquemas para el artículo.|  
|**del_cmd**|**nvarchar(255)**|Comando ejecutado para DELETE.|  
|**filter**|**int**|Identificador para el procedimiento almacenado utilizado para definir la partición horizontal.|  
|**filter_clause**|**ntext**|Cláusula WHERE utilizada para filtrar horizontalmente el artículo.|  
|**ins_cmd**|**nvarchar(255)**|Comando ejecutado para INSERT.|  
|**pre_creation_cmd**|**tinyint**|Comando de creación previa para DROP TABLE, DELETE TABLE o TRUNCATE:<br /><br /> **0** = none.<br /><br /> **1** = QUITAR.<br /><br /> **2** = DELETE.<br /><br /> **3** = TRUNCATE.|  
|**status**|**tinyint**|La máscara de bits de las opciones y el estado del artículo, que puede ser el resultado de OR lógico bit a bit de uno o más de estos valores:<br /><br /> **1** = artículo está activo.<br /><br /> **8** = incluir el nombre de columna en las instrucciones INSERT.<br /><br /> **16** = utilizar instrucciones parametrizadas.<br /><br /> **24** = ambos incluyen el nombre de columna en las instrucciones INSERT y utilizar instrucciones con parámetros.<br /><br /> Por ejemplo, un artículo activo que utilizara instrucciones con parámetros tendría un valor de **17** en esta columna. Un valor de **0** significa que el artículo está inactivo y no se definen propiedades adicionales.|  
|**Tipo**|**tinyint**|Tipo de artículo.<br /><br /> **1** = artículo basado en registro.<br /><br /> **3** = artículo basado en registro con filtro manual.<br /><br /> **5** = artículo basado en registro con vista manual.<br /><br /> **7** = artículo basado en registro con filtro manual y vista manual.|  
|**upd_cmd**|**nvarchar(255)**|Comando ejecutado para UPDATE.|  
|**schema_option**|**binario**|Indica qué se va a convertir en script. Vea [sp_addarticle &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) para obtener una lista de opciones de esquema admitidas.|  
|**dest_owner**|**sysname**|Propietario del objeto publicado en la base de datos de destino.|  
  
## <a name="see-also"></a>Vea también  
 [Replicación de bases de datos heterogéneas](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
