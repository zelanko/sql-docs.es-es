---
title: sys.dm_os_virtual_address_dump (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_os_virtual_address_dump
- sys.dm_os_virtual_address_dump_TSQL
- sys.dm_os_virtual_address_dump
- dm_os_virtual_address_dump_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_virtual_address_dump dynamic management view
ms.assetid: 7b24ea55-3873-42fd-a86c-441c92eb6175
caps.latest.revision: 23
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: a0326ff840c6874a709541d25f9e8fb55ef3ba8d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmosvirtualaddressdump-transact-sql"></a>sys.dm_os_virtual_address_dump (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Devuelve información acerca de un intervalo de páginas en el espacio de direcciones virtual del proceso que llama.  
  
> [!NOTE]  
>  Esta información también se devuelve por la **VirtualQuery** API de Windows.  
  
> [!NOTE]  
>  Para llamar a esta desde [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use el nombre **sys.dm_pdw_nodes_os_virtual_address_dump**.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**region_base_address**|**varbinary (8)**|Puntero que señala la dirección base de la región de páginas. No admite valores NULL.|  
|**region_allocation_base_address**|**varbinary (8)**|Puntero que señala la dirección base de un intervalo de páginas asignada por la función API de Windows VirtualAlloc. La página apuntada por el miembro de BaseAddress está dentro de este intervalo de asignación. No admite valores NULL.|  
|**region_allocation_protection**|**varbinary (8)**|Atributos de protección cuando la región que asignó por primera vez. El valor puede ser:<br /><br /> -PAGE_READONLY<br />-PAGE_READWRITE<br />-PAGE_NOACCESS<br />-PAGE_WRITECOPY<br />-PAGE_EXECUTE<br />-PAGE_EXECUTE_READ<br />-PAGE_EXECUTE_READWRITE<br />-PAGE_EXECUTE_WRITECOPY<br />-PAGE_GUARD<br />-PAGE_NOCACHE<br /><br /> No admite valores NULL.|  
|**region_size_in_bytes**|**bigint**|Tamaño de la región, en bytes, empezando en la dirección base en la que todas las páginas tienen los mismos atributos. No admite valores NULL.|  
|**region_state**|**varbinary (8)**|Estado actual de la región. Es uno de los siguientes:<br /><br /> -MEM_COMMIT<br />-MEM_RESERVE<br />-MEM_FREE<br /><br /> No admite valores NULL.|  
|**region_current_protection**|**varbinary (8)**|Atributos de protección. El valor puede ser:<br /><br /> -PAGE_READONLY<br />-PAGE_READWRITE<br />-PAGE_NOACCESS<br />-PAGE_WRITECOPY<br />-PAGE_EXECUTE<br />-PAGE_EXECUTE_READ<br />-PAGE_EXECUTE_READWRITE<br />-PAGE_EXECUTE_WRITECOPY<br />-PAGE_GUARD<br />-PAGE_NOCACHE<br /><br /> No admite valores NULL.|  
|**region_type**|**varbinary (8)**|Identifica los tipos de páginas en la región. El valor puede ser uno de los siguientes:<br /><br /> -MEM_PRIVATE<br />-MEM_MAPPED<br />-MEM_IMAGE<br /><br /> No admite valores NULL.|  
|**pdw_node_id**|**int**|**Se aplica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> El identificador para el nodo que se encuentra en esta distribución.|  
  
## <a name="permissions"></a>Permissions  
 es necesario contar con el permiso VIEW SERVER STATE en el servidor.  
  
## <a name="see-also"></a>Vea también  
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Vistas de administración dinámica relacionadas con el sistema operativo SQL Server &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


