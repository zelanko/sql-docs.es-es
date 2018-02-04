---
title: sys.trusted_assemblies (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- trusted_assemblies_TSQL
- trusted_assemblies
- sys.trusted_assemblies_TSQL
- sys.trusted_assemblies
dev_langs:
- TSQL
helpviewer_keywords:
- sys.trusted_assemblies
ms.assetid: 
caps.latest.revision: 
author: tmullaney
ms.author: thmullan;rickbyh
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 827e0d356114bf2254ebd265ca7ee29e0a00f595
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/03/2018
---
# <a name="systrustedassemblies-transact-sql"></a>sys.trusted_assemblies (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Contiene una fila por cada ensamblado de confianza para el servidor.

 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  


|Nombre de columna |Tipo de datos |Description |
|--- |--- |--- |
|hash |varbinary(8000) |SHA2_512 el hash del contenido del ensamblado. |
|description |nvarchar(4000) |Obtener descripción opcional definida por el usuario del ensamblado. Microsoft recomienda utilizar el nombre canónico que codifica el nombre simple, número de versión, referencia cultural, clave pública y arquitectura de ensamblado de confianza. Este valor unívocamente identifica el ensamblado en el lado de runtime (CLR) de lenguaje común y es el mismo que el valor de clr_name en sys.assemblies. |
|create_date |datetime2 |Fecha en que el ensamblado se agregó a la lista de ensamblados de confianza. |
|created_by |nvarchar (128) |Nombre de inicio de sesión de la entidad de seguridad que se agrega el ensamblado a la lista. |
| | | |


## <a name="remarks"></a>Comentarios  

Use **necesita agregar sp_add_trusted_assembly** y **necesita agregar sys.trusted_assemblies** agregar o quitar ensamblados de `sys.trusted_assemblies`.

## <a name="see-also"></a>Vea también  
  [sys.sp_add_trusted_assembly](../../relational-databases/system-stored-procedures/sys-sp-add-trusted-assembly-transact-sql.md) [sys.sp_drop_trusted_assembly](../../relational-databases/system-stored-procedures/sys-sp-drop-trusted-assembly-transact-sql.md) [DROP ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-assembly-transact-sql.md)  
  [sys.assemblies](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md)  
  [sys.dm_clr_loaded_assemblies](../../relational-databases/system-dynamic-management-views/sys-dm-clr-loaded-assemblies-transact-sql.md)  

