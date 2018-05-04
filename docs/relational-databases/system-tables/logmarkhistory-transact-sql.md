---
title: logmarkhistory (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- logmarkhistory
- logmarkhistory_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- logmarkhistory system table
ms.assetid: 5c1becc5-f34e-4869-bf69-dfafab684540
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6cd97bf488bfdd98868ce6c3ca9c68b08e38d0a5
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="logmarkhistory-transact-sql"></a>logmarkhistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una fila por cada transacción marcada que se ha confirmado. Esta tabla se almacena en la **msdb** base de datos.  
  

|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**database_name**|**nvarchar(128)**|Base de datos local donde tiene lugar la transacción marcada.|  
|**nombre_de_marca**|**nvarchar(128)**|Nombre proporcionado por el usuario para la transacción marcada.|  
|**Descripción**|**nvarchar(255)**|Descripción proporcionada por el usuario para la transacción marcada. Puede ser NULL.|  
|**user_name**|**nvarchar(128)**|Nombre de usuario de la base de datos que llevó a cabo la transacción marcada. Puede ser NULL.|  
|**LSN**|**numeric(25,0)**|Número de secuencia de registro de la transacción donde tuvo lugar la marca.|  
|**mark_time**|**datetime**|Hora de la confirmación de la transacción marcada (hora local).|  
  
## <a name="see-also"></a>Vea también  
 [Restaurar una base de datos en una transacción marcada &#40;SQL Server Management Studio&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-marked-transaction-sql-server-management-studio.md)   
 [Usar transacciones marcadas para recuperar bases de datos relacionadas sistemáticamente &#40;modelo de recuperación completa&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md)   
 [Tablas del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
