---
title: sp_polybase_join_group | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sp_polybase_join_group
helpviewer_keywords:
- PolyBase
ms.assetid: 48066431-fed2-4a8a-85af-ac704689e183
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: cffdf311abbac196b49a5174364d8f313275ad40
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43038968"
---
# <a name="sppolybasejoingroup-transact-sql"></a>sp_polybase_join_group (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Agrega una instancia de SQL Server como un nodo de proceso a un grupo de PolyBase para el cálculo de escalabilidad horizontal.  
  
 La instancia de SQL Server debe tener la [PolyBase](../../relational-databases/polybase/polybase-guide.md) característica instalada.  PolyBase permite la integración de orígenes de datos que no son de SQL Server, como Hadoop y Azure storage blob. Vea también [sp_polybase_leave_group &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-leave-group.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
sp_polybase_join_group (@head_node_address = N'head_node_address',  
    @dms_control_channel_port = dms_control_channel_port,  
    @head_node_sql_server_instance_name = head_node_sql_server_instance_name)  
[ ; ]          
```  
  
## <a name="arguments"></a>Argumentos  
 *@head_node_address* = N'*head_node_address*'  
 El nombre del equipo que hospeda el nodo principal de SQL Server del grupo de escalado horizontal de PolyBase. *@head_node_address* es nvarchar (255).  
  
 *@dms_control_channel_port* = dms_control_channel_port  
 El puerto donde se ejecuta el canal de control para el nodo principal de servicio de movimiento de datos de PolyBase. *@dms_control_channel_port* es un __int16 sin signo. El valor predeterminado es **16450**.  
  
 *@head_node_sql_server_instance_name* = head_node_sql_server_instance_name  
 El nombre de la instancia de SQL Server de nodo principal en el grupo de escalabilidad horizontal de PolyBase. *@head_node_sql_server_instance_name* es nvarchar(16).  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="permissions"></a>Permisos  
 Requiere el permiso CONTROL SERVER.  
  
## <a name="remarks"></a>Notas  
 Después de ejecutar el procedimiento almacenado, apagar el motor de PolyBase y reinicie el servicio de movimiento de datos de PolyBase en el equipo. Para comprobar la ejecute la DMV siguiente en el nodo principal: **sys.dm_exec_compute_nodes**.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo se une el equipo actual como un nodo de proceso a un grupo de PolyBase.  El nombre del nodo principal es **HST01** y el nombre de la instancia de SQL Server en el nodo principal es **MSSQLSERVER**.  
  
```  
EXEC sp_polybase_join_group N'HST01', 16450, N'MSSQLSERVER'   
```  
  
## <a name="see-also"></a>Vea también  
 [Introducción a PolyBase](../../relational-databases/polybase/get-started-with-polybase.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
