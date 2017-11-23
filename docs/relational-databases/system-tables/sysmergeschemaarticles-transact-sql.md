---
title: sysmergeschemaarticles (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sysmergeschemaarticles_TSQL
- sysmergeschemaarticles
dev_langs: TSQL
helpviewer_keywords: sysmergeschemaarticles system table
ms.assetid: b5085979-2f76-48e1-bf3b-765a84003dd9
caps.latest.revision: "27"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 13a3104b8f457cf4c9d223630739e3cf6eb76ee8
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="sysmergeschemaarticles-transact-sql"></a>sysmergeschemaarticles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Realiza un seguimiento de los artículos solo de esquema de la replicación de mezcla. Esta tabla se almacena en las bases de datos de publicación y de suscripciones.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**Nombre**|**sysname**|Nombre del artículo solo de esquema de la publicación de combinación.|  
|**tipo**|**tinyint**|Indica el tipo de artículo solo de esquema, que puede ser uno de los siguientes:<br /><br /> **0 x 20** = artículo de solo de esquema de procedimiento almacenado.<br /><br /> **0 x 40** = artículo solo de esquema de vista o un artículo de vista indizada solo de esquema.|  
|**ObjID**|**int**|Identificador de objeto del objeto base del artículo. Puede ser el identificador de objeto de un procedimiento, una vista, una vista indizada o una función de usuario.|  
|**artid**|**uniqueidentifier**|El identificador de artículo.|  
|**Descripción**|**nvarchar(255)**|Descripción del artículo.|  
|**pre_creation_command**|**tinyint**|Acción predeterminada que se debe realizar cuando se crea el artículo en la base de datos de suscripciones.<br /><br /> **0 =** ninguno: si la tabla ya existe en el suscriptor, se realiza ninguna acción.<br /><br /> **1** = drop: quita la tabla antes de volver a crearla.<br /><br /> **2** = delete: emite una eliminación basada en la cláusula WHERE del filtro de subconjunto.<br /><br /> **3** = Truncate-igual que **2**, pero elimina páginas en lugar de filas. Sin embargo, no precisa la cláusula WHERE.|  
|**pubid**|**uniqueidentifier**|El identificador único de la publicación.|  
|**status**|**tinyint**|Indica el estado del artículo solo de esquema, que puede ser uno de los siguientes:<br /><br /> **1** = Unsynced - el script de procesamiento inicial para publicar la próxima vez que se ejecuta el agente de instantáneas de las ejecuciones de la tabla.<br /><br /> **2** = active - se ha ejecutado la secuencia de comandos de procesamiento inicial para publicar la tabla.<br /><br /> **5** = New_inactive - va a agregar.<br /><br /> **6** = New_active - va a agregar.|  
|**creation_script**|**nvarchar(255)**|La ruta de acceso y el nombre de un script de creación previa opcional del esquema del artículo que se utiliza para crear la tabla de destino.|  
|**schema_option**|**binary (8)**|El mapa de bits de la opción de generación de esquemas del artículo solo de esquema específico, que puede ser el resultado de OR lógico bit a bit de uno o más de estos valores:<br /><br /> **0 x 00** = disable scripting del agente de instantáneas y utiliza la secuencia CreationScript.<br /><br /> **0 x 01** = genera la creación del objeto (CREATE TABLE, CREATE PROCEDURE etc.).<br /><br /> **0 x 10** = generar un índice clúster correspondiente.<br /><br /> **0 x 20** = convierten tipos de datos definidos por el usuario para tipos de datos base.<br /><br /> **0 x 40** = índice no clúster correspondiente de generar o índices.<br /><br /> **0 x 80** = incluir integridad referencial declarada para las claves principales.<br /><br /> **0 x 100** = los desencadenadores de usuario replicar en un artículo de tabla, si ha definido.<br /><br /> **0 x 200** = replicar restricciones foreign key. Si la tabla a la que se hace referencia no forma parte de una publicación, no se replica ninguna restricción de clave externa de una tabla publicada.<br /><br /> **0 x 400** = restricciones check replicar.<br /><br /> **0 x 800** = replicar los valores predeterminados.<br /><br /> **0 x 1000** = replicar intercalación de columna.<br /><br /> **0 x 2000** = replica propiedades extendidas asociadas con el objeto de origen del artículo publicado.<br /><br /> **0 x 4000** = replicar claves únicas si están definidas en un artículo de tabla.<br /><br /> **0 x 8000** = replica artículo de una clave principal y las claves únicas de una tabla como restricciones mediante instrucciones ALTER TABLE.<br /><br /> Para obtener más información sobre posibles valores de **schema_option**, consulte [sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md).|  
|**destination_object**|**sysname**|Nombre del objeto de destino en la base de datos de suscripciones. Este valor se aplica únicamente a los artículos solo de esquema, como procedimientos almacenados, vistas y UDF.|  
|**destination_owner**|**sysname**|El propietario del objeto en la base de datos de suscripción, si no lo es **dbo**.|  
  
## <a name="see-also"></a>Vea también  
 [Tablas de replicación &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
