---
title: Sys. fn_PageResCracker (Transact-SQL) | Microsoft Docs
description: Documentación de la función del sistema sys. fn_PageResCracker.
ms.custom: ''
ms.date: 09/18/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_PageResCracker
- sys.fn_PageResCracker_TSQL
- fn_PageResCracker_TSQL
- sys.fn_PageResCracker
- sys.dm_db_page_info
dev_langs:
- TSQL
helpviewer_keywords:
- fn_PageResCracker function
- page_resource
- sys.fn_PageResCracker function
- sys.dm_db_page_info
- page info
author: bluefooted
ms.author: pamela
manager: amitban
ms.openlocfilehash: 6d8203979a0afdca1ae78b9bd51723c906c40ea2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "68267071"
---
# <a name="sysfn_pagerescracker-transact-sql"></a>Sys. fn_PageResCracker (Transact-SQL)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Devuelve `db_id`, `file_id`y `page_id` para el valor especificado. `page_resource` 
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
```  
sys.fn_PageResCracker ( page_resource )  
```  
  
## <a name="arguments"></a>Argumentos  
*page_resource*    
Es el formato hexadecimal de 8 bytes de un recurso de página de base de datos.
  
## <a name="tables-returned"></a>Tablas devueltas  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|db_id|**int**|Identificador de base de datos|  
|file_id|**int**|Id. de archivo|  
|page_id|**int**|Identificador de página|  
  
## <a name="remarks"></a>Observaciones  
`sys.fn_PageResCracker`se utiliza para convertir la representación hexadecimal de 8 bytes de una página de base de datos en un conjunto de filas que contiene el identificador de base de datos, el identificador de archivo y el ID. de página de la página.   

Puede obtener un recurso de página válido de la `page_resource` columna de la vista de administración dinámica [sys. dm_exec_requests &#40;transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md) o la vista del sistema [Sys. sysprocesses &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysprocesses-transact-sql.md) . Si se usa un recurso de página no válido, el valor devuelto es NULL.  
El uso principal de `sys.fn_PageResCracker` es facilitar las combinaciones entre estas vistas y la función de administración dinámica [sys. dm_db_page_info &#40;TRANSACT-&#41;SQL](../../relational-databases/system-dynamic-management-views/sys-dm-db-page-info-transact-sql.md) para obtener información acerca de la página, como el objeto al que pertenece.
  
## <a name="permissions"></a>Permisos  
El usuario necesita `VIEW SERVER STATE` el permiso en el servidor.  
  
## <a name="examples"></a>Ejemplos  
La `sys.fn_PageResCracker` función se puede usar junto con [sys. dm_db_page_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-page-info-transact-sql.md) para solucionar problemas de esperas y bloqueos relacionados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]con las páginas en.  El script siguiente es un ejemplo de cómo puede usar estas funciones para recopilar información de la página de base de datos para todas las solicitudes activas que están esperando actualmente algún tipo de recurso de página. 
  
```sql  
SELECT page_info.* 
FROM sys.dm_exec_requests AS d  
CROSS APPLY sys.fn_PageResCracker (d.page_resource) AS r  
CROSS APPLY sys.dm_db_page_info(r.db_id, r.file_id, r.page_id, 1) AS page_info
```  
  
## <a name="see-also"></a>Consulte también  
 [Sys. dm_db_page_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-page-info-transact-sql.md)  
 [Sys. sysprocesses &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysprocesses-transact-sql.md)   
 [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
  
