---
description: MSpublicationthresholds (Transact-SQL)
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 799c068d066fdab518a355552ead5ed5a9fde8af
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88427657"
---
# <a name="mspublicationthresholds-transact-sql"></a>MSpublicationthresholds (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  La tabla **MSpublicationthresholds** se utiliza para realizar el seguimiento de las métricas de rendimiento de la replicación de una publicación, con una fila por cada valor de umbral que se está supervisando. Esta tabla se almacena en la base de datos de distribución.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**publication_id**|**int**|Identifica la publicación para la que se ha establecido un umbral.|  
|**metric_id**|**int**|Identifica una métrica de rendimiento de replicación que se está supervisando según se define en la tabla del sistema [MSreplmonthresholdmetrics](../../relational-databases/system-tables/msreplmonthresholdmetrics-transact-sql.md) .|  
|**value**|**sql_variant**|El valor del umbral de la métrica que se está supervisando.|  
|**shouldalert**|**bit**|Un valor de **1** indica que se debe generar una alerta cuando la métrica supera el umbral definido.|  
|**IsEnabled**|**bit**|Un valor de **1** indica que la supervisión está habilitada para esta métrica de rendimiento de replicación.|  
  
## <a name="see-also"></a>Consulte también  
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
