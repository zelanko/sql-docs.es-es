---
title: systranschemas (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- systranschemas
- systranschemas_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- systranschemas system table
ms.assetid: 864c3966-cb61-4f2b-8939-ccda112de853
author: stevestein
ms.author: sstein
ms.openlocfilehash: f3ba5516920cee6cb2f6f18f0120844e4320afe5
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2020
ms.locfileid: "85881191"
---
# <a name="systranschemas-transact-sql"></a>systranschemas (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  La tabla **systranschemas** se usa para realizar el seguimiento de los cambios de esquema en los artículos publicados en publicaciones transaccionales y de instantáneas. Esta tabla se almacena en las bases de datos de publicaciones y suscripciones.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**tabid**|**int**|Identifica el artículo de la tabla en la que se produjo el cambio de esquema.|  
|**LSN**|**binary**|Valor LSN al inicio del cambio de esquema.|  
|**endlsn**|**binary**|Valor LSN al final del cambio de esquema.|  
|**TypeId**|**int**|Tipo de cambio de esquema.|  
  
## <a name="see-also"></a>Consulte también  
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
