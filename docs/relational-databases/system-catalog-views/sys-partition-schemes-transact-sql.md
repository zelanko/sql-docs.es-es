---
title: Sys.partition_schemes (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- partition_schemes_TSQL
- partition_schemes
- sys.partition_schemes_TSQL
- sys.partition_schemes
dev_langs: TSQL
helpviewer_keywords: sys.partition_schemes catalog view
ms.assetid: ed557fd5-12b0-4cef-9e4f-440b02e99d1f
caps.latest.revision: "37"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5c77fcc9083c46921197554b256ca1af46e159e5
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="syspartitionschemes-transact-sql"></a>sys.partition_schemes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Contiene una fila por cada espacio de datos que es un esquema de partición, con **tipo** = PS.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**\<hereda columnas >**||Hereda columnas de [sys.data_spaces &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md).|  
|**function_id**|**int**|Id. de función de la partición utilizado en el esquema.|  
  
 Para obtener una lista de columnas que hereda esta vista, consulte [sys.data_spaces &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer al rol **public** . Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Preguntas frecuentes sobre consultas del catálogo de sistema de SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
