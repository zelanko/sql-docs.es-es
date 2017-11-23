---
title: sp_polybase_leave_group (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine-polybase
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sp_polybase_leave_group
- sp_polybase_leave_group_TSQL
helpviewer_keywords: sp_polybase_leave_group
ms.assetid: ef87a8f1-5407-47b5-b8bf-bd7d08c0f0fe
caps.latest.revision: "11"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f86b26be75bfc5311714c969c9d965152a8acf5f
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="polybase-stored-procedures---sppolybaseleavegroup"></a>Procedimientos almacenados de PolyBase - sp_polybase_leave_group
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Quita una instancia de SQL Server de un grupo de PolyBase para el cálculo de escalabilidad horizontal. 
 
 La instancia de SQL Server debe tener la [Guía de PolyBase](../../relational-databases/polybase/polybase-guide.md) característica instalada.  PolyBase permite la integración de orígenes de datos no es de SQL Server, como almacenamiento de blobs de Hadoop y Azure. Vea también [sp_polybase_join_group](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-join-group.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_polybase_leave_group;  
  
```  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso CONTROL SERVER.  
  
## <a name="remarks"></a>Comentarios  
 Solo puede quitar un nodo de proceso de un grupo.  
  
 Después de ejecutar el procedimiento almacenado, reinicie el motor y el servicio de movimiento de datos de PolyBase en el equipo. Para comprobar ejecute la DMV siguiente en el nodo principal: **sys.dm_exec_compute_nodes**.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo se quita la máquina actual de un grupo de PolyBase.  
  
```sql  
EXEC sp_polybase_leave_group ;  
```  
  
## <a name="see-also"></a>Vea también  
 [Introducción a PolyBase](../../relational-databases/polybase/get-started-with-polybase.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
