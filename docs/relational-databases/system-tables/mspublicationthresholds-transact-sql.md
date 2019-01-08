---
title: MSpublicationthresholds (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- mspublicationthresholds
- mspublicationthresholds_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSpublicationthresholds system table
ms.assetid: 9da3879f-b1f4-4ab4-abd4-a9a8ac395eba
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cec59e0b5cb933822790a1f2497ca1bd5a3cbb2e
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52794171"
---
# <a name="mspublicationthresholds-transact-sql"></a>MSpublicationthresholds (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **MSpublicationthresholds** tabla se utiliza para realizar un seguimiento de las métricas de rendimiento de replicación para una publicación, con una fila por cada valor de umbral que se está supervisando. Esta tabla se almacena en la base de datos de distribución.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**publication_id**|**int**|Identifica la publicación para la que se ha establecido un umbral.|  
|**metric_id**|**int**|Identifica una métrica de rendimiento de replicación que se está supervisa como se define en el [MSreplmonthresholdmetrics](../../relational-databases/system-tables/msreplmonthresholdmetrics-transact-sql.md) tabla del sistema.|  
|**value**|**sql_variant**|El valor del umbral de la métrica que se está supervisando.|  
|**shouldalert**|**bit**|Un valor de **1** indica que se debe generar una alerta cuando la métrica supera el umbral definido.|  
|**IsEnabled**|**bit**|Un valor de **1** indica que la supervisión está habilitada para esta métrica de rendimiento de replicación.|  
  
## <a name="see-also"></a>Vea también  
 [Las tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
