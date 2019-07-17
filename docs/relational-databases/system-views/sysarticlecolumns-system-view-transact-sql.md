---
title: sysarticlecolumns (vista del sistema) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysarticlecolumns
- sysarticlecolumns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysarticlecolumns view
ms.assetid: a8dd8d13-c827-45c4-87ba-802725301382
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8a0505b8316254090fe5f2310fa68011d8289679
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68129550"
---
# <a name="sysarticlecolumns-system-view-transact-sql"></a>sysarticlecolumns (vista del sistema) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **sysarticlecolumns** vista expone información adicional acerca de las columnas de los artículos publicados. Esta vista se almacena en la base de datos de distribución.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|Identifica un artículo.|  
|**colid**|**int**|Identifica una columna de un artículo.|  
|**is_udt**|**int**|Indica si la columna es una columna de un tipo de datos definido por el usuario (UDT). Un valor de **1** indica una columna UDT.|  
|**is_xml**|**int**|Indica si la columna es una **xml** columna. Un valor de **1** indica un **xml** columna.|  
|**is_max**|**int**|Indica si la columna es una columna de tipo de datos de valor grande (**varchar (max)** , **nvarchar (max)** o **varbinary (max)** ). Un valor de **1** indica una columna de valor grande.|  
  
## <a name="see-also"></a>Vea también  
 [sp_articlecolumn &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [sysarticlecolumns &#40;Transact-SQL&#41;](../../relational-databases/system-tables/sysarticlecolumns-transact-sql.md)  
  
  
