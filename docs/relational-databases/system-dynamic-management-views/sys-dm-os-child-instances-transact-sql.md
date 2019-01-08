---
title: Sys.dm_os_child_instances (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_child_instances
- sys.dm_os_child_instances_TSQL
- dm_os_child_instances
- dm_os_child_instances_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- server state information [SQL Server]
- sys.dm_os_child_instances dynamic management view
- monitoring server health
ms.assetid: 1bef3074-0ccc-48fa-8f3d-14f3d99df86b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a57719becab0c7dda9d684e4de3218e29418b6a3
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/11/2018
ms.locfileid: "53203456"
---
# <a name="sysdmoschildinstances-transact-sql"></a>sys.dm_os_child_instances (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila por cada instancia de usuario creada a partir de la instancia del servidor primario.  
  
> **IMPORTANTE:** [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 La información devuelta de **sys.dm_os_child_instances** puede utilizarse para determinar el estado de cada instancia de usuario (heart_beat) y obtener el nombre de canalización (instance_pipe_name) que puede usarse para crear una conexión con el usuario Instancia mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o SQLCmd. Solo se puede conectar con una instancia de usuario después de que la inicie un proceso externo, como por ejemplo una aplicación cliente. Las herramientas de administración de SQL no pueden iniciar instancias de usuario.  
  
> **NOTA:** Las instancias de usuario son una característica exclusiva de [!INCLUDE[ssExpressEd11](../../includes/ssexpressed11-md.md)].  
> 
> **Tenga en cuenta** para llamarlo desde [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use el nombre **sys.dm_pdw_nodes_os_child_instances**.  
  
|columna|Data type|Descripción|  
|------------|---------------|-----------------|  
|**owning_principal_name**|**nvarchar(256)**|Nombre del usuario para el que se creó esta instancia.|  
|owning_principal_sid|nvarchar(256)|SID (identificador de seguridad) de la entidad de seguridad que posee esta instancia de usuario. Coincide con el identificador SID de Windows.|  
|owning_principal_sid_binary|varbinary(85)|Versión binaria del SID para el usuario propietario de la instancia de usuario.|  
|**instance_name**|**nvarchar(128)**|Nombre de esta instancia de usuario.|  
|**instance_pipe_name**|**nvarchar(260)**|Cuando se crea una instancia de usuario, se crea una canalización con nombre para que las aplicaciones se conecten a ella. Este nombre se puede utilizar en una cadena de conexión para conectarse a esta instancia de usuario.|  
|**os_process_id**|**Int**|Número del proceso de Windows para esta instancia de usuario.|  
|**os_process_creation_date**|**Fecha y hora**|Fecha y hora de la última vez que se inició el proceso de esta instancia de usuario.|  
|**heart_beat**|**nvarchar (5)**|Estado actual de esta instancia de usuario; puede ser ALIVE o DEAD.|  
|**pdw_node_id**|**int**|**Se aplica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> El identificador para el nodo en esta distribución.|  
  
## <a name="permissions"></a>Permisos  
 es necesario contar con el permiso VIEW SERVER STATE en el servidor.  
  
## <a name="remarks"></a>Comentarios  
 Para obtener más información acerca de la vista de administración dinámica, consulte [funciones y vistas de administración dinámica &#40;Transact-SQL&#41; ](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md) en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] libros en pantalla.  
  
## <a name="see-also"></a>Vea también  
 [Instancias de usuario para que no son administradores](https://msdn.microsoft.com/85385aae-10fb-4f8b-9eeb-cce2ee7da019)  
  
  



