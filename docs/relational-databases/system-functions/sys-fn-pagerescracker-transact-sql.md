---
title: Sys.fn_PageResCracker (Transact-SQL) | Microsoft Docs
description: Documentación de la función del sistema sys.fn_PageResCracker.
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
ms.openlocfilehash: a666e5d98d2c8ea0753981f05d1da20a6234251f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47833343"
---
# <a name="sysfnpagerescracker-transact-sql"></a>Sys.fn_PageResCracker (Transact-SQL)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Devuelve el `db_id`, `file_id`, y `page_id` para la dada `page_resource` valor. 
  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
sys.fn_PageResCracker ( page_resource )  
```  
  
## <a name="arguments"></a>Argumentos  
 *page_resource*  
 Es el formato hexadecimal de 8 bytes de un recurso de página de base de datos.
  
## <a name="tables-returned"></a>Tablas devueltas  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|db_id|**int**|Id. de base de datos|  
|file_id|**int**|Id. de archivo|  
|page_id|**int**|Identificador de página|  
  
## <a name="remarks"></a>Comentarios  
`sys.fn_PageResCracker` se utiliza para convertir la representación hexadecimal de 8 bytes de una página de base de datos en un conjunto de filas que contiene el identificador de la base de datos, archivo de identificador y el identificador de la página. Puede obtener un recurso de página válida desde el `page_resource` columna de la [sys.dm_exec_requests &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md) vista de administración dinámica o el [sys.sysprocesses &#40;&#41; ](../../relational-databases/system-compatibility-views/sys-sysprocesses-transact-sql.md) vista del sistema.  El uso principal de `sys.fn_PageResCracker` es facilitar las combinaciones entre estas vistas y [sys.dm_db_page_info &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-db-page-info-transact-sql.md) función de administración dinámica con el fin de obtener información acerca de la página, como la objeto al que pertenece.
  
## <a name="permissions"></a>Permisos  
 El usuario necesita tener el permiso VIEW SERVER STATE en el servidor.  
  
## <a name="examples"></a>Ejemplos  
El `sys.fn_PageResCracker` función puede utilizarse junto con [sys.dm_db_page_info &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-db-page-info-transact-sql.md) solucionar problemas de página relacionadas con esperas y bloqueos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  El script siguiente es un ejemplo de cómo puede usar estas funciones para recopilar información de la página de base de datos para todas las solicitudes activas que están esperando en algún tipo de recurso de página. 
  
```sql  
SELECT page_info.* 
FROM sys.dm_exec_requests AS d  
CROSS APPLY sys.fn_PageResCracker (d.page_resource) AS r  
CROSS APPLY sys.dm_db_page_info(r.db_id, r.file_id, r.page_id, 1) AS page_info
```  
  
## <a name="see-also"></a>Vea también  
 [Sys.dm_db_page_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-page-info-transact-sql.md)  
 [Sys.sysprocesses &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysprocesses-transact-sql.md)   
 [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
  
