---
title: IHsyscolumns (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-views
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- IHsyscolumns
- IHsyscolumns_TSQL
dev_langs: TSQL
helpviewer_keywords: IHsyscolumns view
ms.assetid: 263452f1-9708-48f0-9536-402a89e7f5bf
caps.latest.revision: "12"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 347a3b691f2933cc4e3fbedcb3ddb59171da0108
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="ihsyscolumns-transact-sql"></a>IHsyscolumns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **IHsyscolumns** vista expone información de columna para los artículos publicados desde una no - publicador de SQL Server. Esta vista se almacena en el distributiondatabase.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**Nombre**|**sysname**|Nombre de la columna o parámetro de procedimiento.|  
|**id**|**int**|Id. de objeto de la tabla a la que pertenece esta columna o Id. del procedimiento almacenado al que está asociado este parámetro.|  
|**alguno**|**tinyint**|El tipo de almacenamiento físico de [sys.systypes &#40; Transact-SQL &#41; ](../../relational-databases/system-compatibility-views/sys-systypes-transact-sql.md).|  
|**typestat**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**xusertype**|**tinyint**|Id. del tipo de datos extendido definido por el usuario.|  
|**longitud**|**bigint**|La longitud máxima de almacenamiento físico de [sys.systypes &#40; Transact-SQL &#41; ](../../relational-databases/system-compatibility-views/sys-systypes-transact-sql.md).|  
|**xprec**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**XScale**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**colid**|**int**|Id. de la columna o parámetro.|  
|**XOffset**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**bitpos**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**reservado**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**colstat**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**cdefault**|**int**|El identificador del valor predeterminado para esta columna.|  
|**dominio**|**int**|El identificador de la regla o restricción CHECK para esta columna.|  
|**número**|**int**|El número de subprocedimiento cuando el procedimiento está agrupado (**0** para las entradas).|  
|**colorder**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**autoval**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**desplazamiento**|**int**|Desplazamiento en la fila en la que aparece esta columna.|  
|**collationid**|**int**|El identificador de la intercalación de la columna. Es NULL para las columnas no basadas en caracteres.|  
|**idioma**|**int**|Identificador de idioma de la columna.|  
|**status**|**int**|El mapa de bits utilizado para describir una propiedad de la columna o el parámetro:<br /><br /> **0 x 08** = columna permite valores null.<br /><br /> **0 x 10** = relleno ANSI activado al **varchar** o **varbinary** se han agregado las columnas. Se conservan los espacios en blanco **varchar** y se conservan los ceros finales **varbinary** columnas.<br /><br /> **0 x 40** = parámetro es un parámetro de salida.<br /><br /> **0 x 80** = columna es una columna de identidad.|  
|**tipo**|**int**|El tipo de almacenamiento físico de [sys.systypes &#40; Transact-SQL &#41; ](../../relational-databases/system-compatibility-views/sys-systypes-transact-sql.md).|  
|**usertype**|**tinyint**|El identificador del tipo de datos definido por el usuario desde [sys.systypes &#40; Transact-SQL &#41; ](../../relational-databases/system-compatibility-views/sys-systypes-transact-sql.md).|  
|**printfmt**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**Prec**|**int**|Nivel de precisión de esta columna.|  
|**escala**|**int**|Escala de esta columna.|  
|**es calculado**|**int**|Marca que especifica si es una columna calculada:<br /><br /> **0** = no calculada.<br /><br /> **1** = calculada.|  
|**isoutparam**|**int**|Indica si el parámetro de procedimiento es un parámetro de salida:<br /><br /> **1** = true.<br /><br /> **0** = false.|  
|**IsNullable**|**int**|Indica si la columna admite valores NULL:<br /><br /> **1** = true.<br /><br /> **0** = false.|  
|**intercalación**|**int**|El nombre de la intercalación de la columna. Es NULL para las columnas no basadas en caracteres.|  
|**tdscollation**|**int**|Nombre de la intercalación de la columna cuando se devuelve en un flujo TDS.|  
  
## <a name="see-also"></a>Vea también  
 [Replicación de bases de datos heterogéneas](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Tablas de replicación &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40; Transact-SQL &#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)  
  
  
