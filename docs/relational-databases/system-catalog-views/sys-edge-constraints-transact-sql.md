---
title: Sys. edge_constraints (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/17/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.edge_constraints
- edge_constraints
- SQL Graph
- edge_constraints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.edge_constraints catalog view
ms.assetid: 0f782d2f-7126-46ab-85b7-bcba44862231
author: shkale-msft
ms.author: shkale
monikerRange: '>=sql-server-2017||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9e3e7068e18e5a0315936593fca071132d49e833
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85648907"
---
# <a name="sysedge_constraints-transact-sql"></a>Sys. edge_constraints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx.md](../../includes/applies-to-version/sqlserver2019.md)]

Contiene una fila por cada objeto que es una restricción perimetral. 
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**\<Columns inherited from sys.objects>**||Para obtener una lista de las columnas que hereda esta vista, vea [Sys. objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).|  
|**is_disabled**|**bit**|1 = la restricción perimetral está dessangrada.<br /><br /> 0 = la restricción perimetral está habilitada.|  
|**is_not_trusted**|**bit**|1 = el sistema no ha comprobado la restricción perimetral.<br /><br /> 0 = el sistema ha comprobado la restricción perimetral.|  
|**delete_referential_action**|**tinyint**|Acción referencial que se definió en esta restricción perimetral.<br /><br />0 = ninguna acción.|  
|**delete_referential_action_desc**|**nvarchar(60)**|Descripción de la acción referencial que se definió en esta restricción perimetral.<br /><br />NO_ACTION|  
|**is_system_named**|**bit**|1 = el sistema generó el nombre de la restricción perimetral.<br /><br />0 = el usuario proporcionó el nombre de la restricción perimetral.|  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte también  
 [Vistas de catálogo de objetos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Consultar las preguntas más frecuentes (P+F) del catálogo del sistema de SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
