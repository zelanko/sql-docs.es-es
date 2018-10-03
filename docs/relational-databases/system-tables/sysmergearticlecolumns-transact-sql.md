---
title: sysmergearticlecolumns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sysmergearticlecolumns
- sysmergearticlecolumns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmergearticlecolumns system table
ms.assetid: 1ad8663f-a624-42a2-8641-fefac3433c97
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 64d4ff2edd683b4da4944fb71244f1d97458b44f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47801941"
---
# <a name="sysmergearticlecolumns-transact-sql"></a>sysmergearticlecolumns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **sysmergearticlecolumns** tabla contiene una fila por cada columna de tabla que se publica en una publicación de combinación y asigna cada columna en su artículo de mezcla. Esta tabla se almacena en la base de datos de publicación.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|Identifica un artículo.|  
|**colid**|**smallint**|Identifica una columna de un artículo.|  
  
## <a name="see-also"></a>Vea también  
 [Las tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
