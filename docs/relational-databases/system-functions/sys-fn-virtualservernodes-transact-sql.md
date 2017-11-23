---
title: Sys.fn_virtualservernodes (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, pdw
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- fn_virtualservernodes
- fn_virtualservernodes_TSQL
dev_langs: TSQL
helpviewer_keywords:
- nodes [Faillover Clustering], virtual servers
- nodes [Faillover Clustering]
- virtual servers [Faillover Clustering]
- failover clustering [SQL Server], nodes
- fn_virtualservernodes function
- sys.fn_virtualservernodes function
ms.assetid: 257f3b8d-93c0-4444-87f1-ea211bd8cad0
caps.latest.revision: "25"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 404c45f4aa245d6aeba40ee11bdb6cf4ad98576e
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="sysfnvirtualservernodes-transact-sql"></a>sys.fn_virtualservernodes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  Devuelve una lista de nodos de la instancia en clúster de conmutación por error en los que se puede ejecutar una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta información es útil en entornos de clústeres de conmutación por error.  
  
> [!IMPORTANT]  
>  Esto [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] función del sistema se incluye por compatibilidad con versiones anteriores. Se recomienda que use [sys.dm_os_cluster_nodes &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-cluster-nodes-transact-sql.md) en su lugar.  
  
||  
|-|  
|**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
fn_virtualservernodes()  
```  
  
## <a name="tables-returned"></a>Tablas devueltas  
 Si el servidor actual es un servidor agrupado, **fn_virtualservernodes** devuelve una lista de nodos de la instancia de clúster de conmutación por error en el que este instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se ha definido.  
  
 Si la instancia del servidor actual no es un servidor agrupado, **fn_virtualservernodes** devuelve un conjunto de filas vacío.  
  
## <a name="permissions"></a>Permissions  
 El usuario debe tener el permiso VIEW SERVER STATE para la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se utiliza `fn_virtualservernodes` para realizar una consulta en una instancia de servidor en clúster:  
  
```  
SELECT * FROM fn_virtualservernodes();  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 NodeName  
  
 -------\-  
  
 SS3-CLUSN1  
  
 SS3-CLUSN2  
  
## <a name="see-also"></a>Vea también  
 [Sys.dm_os_cluster_nodes &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-cluster-nodes-transact-sql.md)   
 [Sys.fn_servershareddrives &#40; Transact-SQL &#41;](../../relational-databases/system-functions/sys-fn-servershareddrives-transact-sql.md)  
  
  
