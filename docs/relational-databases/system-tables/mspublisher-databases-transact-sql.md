---
title: MSpublisher_databases (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSpublisher_databases
- MSpublisher_databases_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSpublisher_databases system table
ms.assetid: 59b0166e-a64c-46b8-befc-c222fa1ccce2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5c9ceb08b4757af09cfc5eba8c4d9f26da3cf931
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52817717"
---
# <a name="mspublisherdatabases-transact-sql"></a>MSpublisher_databases (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **MSpublisher_databases** tabla contiene una fila por cada par de base de datos del publicador y publicador da servido el distribuidor local. Esta tabla se almacena en la base de datos de distribución.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|El ID. del publicador.|  
|**publisher_db**|**sysname**|Nombre de la base de datos del publicador.|  
|**id**|**int**|Id. de la fila.|  
|**publisher_engine_edition**|**int**|Edición del publicador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], que puede ser una de las siguientes:<br /><br /> **10** = personal Edition<br /><br /> **11** = desktop Engine (MSDE)<br /><br /> **20** = estándar<br /><br /> **21** = grupo de trabajo<br /><br /> **30** = Enterprise (evaluación)<br /><br /> **31** = para desarrolladores<br /><br /> **40** = express (Express no puede ser un publicador. Este valor está presente por integridad.)|  
  
## <a name="see-also"></a>Vea también  
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
