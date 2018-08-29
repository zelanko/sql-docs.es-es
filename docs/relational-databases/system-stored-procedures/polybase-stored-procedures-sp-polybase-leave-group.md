---
title: sp_polybase_leave_group (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
f1_keywords:
- sp_polybase_leave_group
- sp_polybase_leave_group_TSQL
helpviewer_keywords:
- sp_polybase_leave_group
ms.assetid: ef87a8f1-5407-47b5-b8bf-bd7d08c0f0fe
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 43f155de0eb81918d5129d404e7cd2f236957152
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43037908"
---
# <a name="sppolybaseleavegroup-transact-sql"></a>sp_polybase_leave_group (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Quita una instancia de SQL Server de un grupo de PolyBase para el cálculo de escalabilidad horizontal. 
 
 La instancia de SQL Server debe tener la [Guía de PolyBase](../../relational-databases/polybase/polybase-guide.md) característica instalada.  PolyBase permite la integración de orígenes de datos que no son de SQL Server, como Hadoop y Azure storage blob. Vea también [sp_polybase_join_group](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-join-group.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_polybase_leave_group;  
  
```  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="permissions"></a>Permisos  
 Requiere el permiso CONTROL SERVER.  
  
## <a name="remarks"></a>Notas  
 Solo puede quitar un nodo de proceso de un grupo.  
  
 Después de ejecutar el procedimiento almacenado, reinicie el motor de PolyBase y el servicio de movimiento de datos de PolyBase en el equipo. Para comprobar la ejecute la DMV siguiente en el nodo principal: **sys.dm_exec_compute_nodes**.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo se quita la máquina actual de un grupo de PolyBase.  
  
```sql  
EXEC sp_polybase_leave_group ;  
```  
  
## <a name="see-also"></a>Vea también  
 [Introducción a PolyBase](../../relational-databases/polybase/get-started-with-polybase.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
