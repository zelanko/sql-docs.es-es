---
title: Sys.securable_classes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/01/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- securable_classes_TSQL
- securable_classes
- sys.securable_classes_TSQL
- sys.securable_classes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.securable_classes catalog view
ms.assetid: ae2bf589-17be-4cad-b5d5-05a34173b32d
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 44a9a7268c58ee87c21ae399021e7f0530d9e0c2
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2018
ms.locfileid: "39551945"
---
# <a name="syssecurableclasses-transact-sql"></a>sys.securable_classes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve una lista de las clases protegibles.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**class_desc**|**sysname**|Nombre de la clase.|  
|**class**|**int**|Designación numérica de la clase.|  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve las clases protegibles admitidas por esta instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```sql  
SELECT * FROM sys.securable_classes ORDER BY class;  
```  
  
## <a name="see-also"></a>Vea también  
 [Elementos protegibles](../../relational-databases/security/securables.md)  
  
  
