---
title: MSsub_identity_range (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSsub_identity_range_TSQL
- MSsub_identity_range
dev_langs:
- TSQL
helpviewer_keywords:
- MSsub_identity_range system table
ms.assetid: 26e20d28-14ed-44fc-af3b-4de386de4bb8
author: stevestein
ms.author: sstein
ms.openlocfilehash: 4ec1f915e7cc70cb2d8ed0f09a9b0394dc7e09aa
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68221965"
---
# <a name="mssub_identity_range-transact-sql"></a>MSsub_identity_range (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  En la tabla **MSsub_identity_range** se proporciona compatibilidad con la administración de intervalos de identidad para las suscripciones. Esta tabla se almacena en las bases de datos de suscripciones.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**objid**|**int**|Identificador de la tabla cuya columna de identidad se administra mediante la replicación.|  
|**variedad**|**BIGINT**|Controla el tamaño del intervalo de valores de identidad consecutivos que podrían asignarse al suscriptor en un ajuste.|  
|**last_seed**|**BIGINT**|Límite inferior del intervalo actual.|  
|**mínimo**|**int**|Valor de porcentaje que controla cuándo el Agente de distribución asigna un nuevo intervalo de identidad. Cuando se utiliza el porcentaje de valores especificado en *umbral* , el agente de distribución crea un nuevo intervalo de identidad.|  
  
## <a name="see-also"></a>Consulte también  
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
