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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 65d174c38d4d6fe22c73b16af40bcee9d4ff63a3
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82833142"
---
# <a name="mspublisher_databases-transact-sql"></a>MSpublisher_databases (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  La tabla **MSpublisher_databases** contiene una fila por cada par de publicador y base de datos del publicador que presta servicio el distribuidor local. Esta tabla se almacena en la base de datos de distribución.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|IDENTIFICADOR del publicador.|  
|**publisher_db**|**sysname**|Nombre de la base de datos del publicador.|  
|**id**|**int**|Id. de la fila.|  
|**publisher_engine_edition**|**int**|Edición del publicador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], que puede ser una de las siguientes:<br /><br /> **10** = edición personal<br /><br /> **11** = Desktop Engine (MSDE)<br /><br /> **20** = estándar<br /><br /> **21** = grupo de trabajo<br /><br /> **30** = Enterprise (evaluación)<br /><br /> **31** = desarrollador<br /><br /> **40** = Express (Express no puede ser un publicador. Este valor está presente por integridad.)|  
  
## <a name="see-also"></a>Consulte también  
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
