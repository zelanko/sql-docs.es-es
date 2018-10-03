---
title: Sys.trusted_assemblies (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql
ms.technology: system-objects
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
ms.assetid: ''
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5830d394330778fae6aab795286c7fbc9e211072
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47710723"
---
# <a name="systrustedassemblies-transact-sql"></a>sys.trusted_assemblies (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Contiene una fila para cada ensamblado de confianza para el servidor.

 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  


|Nombre de columna |Tipo de datos |Descripción |
|--- |--- |--- |
|hash |varbinary (8000) |SHA2_512 hash del contenido del ensamblado. |
|description |nvarchar(4000) |Descripción de definido por el usuario opcional del ensamblado. Microsoft recomienda usar el nombre canónico que codifica el nombre simple, número de versión, referencia cultural, clave pública y la arquitectura de ensamblado de confianza. Forma exclusiva este valor identifica el ensamblado del lado common language runtime (CLR) y es el mismo que el valor de clr_name en sys.assemblies. |
|create_date |datetime2 |Fecha en que el ensamblado se agregó a la lista de ensamblados de confianza. |
|created_by |nvarchar(128) |Nombre de inicio de sesión de la entidad de seguridad que agrega el ensamblado a la lista. |
| | | |


## <a name="remarks"></a>Comentarios  

Use **deba agregar sp_add_trusted_assembly** y **deba agregar sys.trusted_assemblies** agregar o quitar ensamblados de `sys.trusted_assemblies`.

## <a name="see-also"></a>Vea también  
  [sys.sp_add_trusted_assembly](../../relational-databases/system-stored-procedures/sys-sp-add-trusted-assembly-transact-sql.md) [sys.sp_drop_trusted_assembly](../../relational-databases/system-stored-procedures/sys-sp-drop-trusted-assembly-transact-sql.md) [DROP ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-assembly-transact-sql.md)  
  [sys.assemblies](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md)  
  [sys.dm_clr_loaded_assemblies](../../relational-databases/system-dynamic-management-views/sys-dm-clr-loaded-assemblies-transact-sql.md)  

