---
description: sys.assembly_types (Transact-SQL)
title: Sys. assembly_types (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- assembly_types
- sys.assembly_types
- sys.assembly_types_TSQL
- assembly_types_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.assembly_types catalog view
ms.assetid: 35f0384f-7a6d-41b1-9461-f1406d68f317
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 06eb2eb4fe6b0983b798ea38fa98057be73af77a
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545102"
---
# <a name="sysassembly_types-transact-sql"></a>sys.assembly_types (Transact-SQL)
[!INCLUDE [sql-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdbmi-asa-pdw.md)]

  Contiene una fila por cada tipo definido por el usuario que se define en un ensamblado CLR. El siguiente **Sys. assembly_types** aparece en la lista de columnas heredadas (vea [Sys. Types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)) después de **rule_object_id**.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**assembly_id**|**int**|Id. del ensamblado a partir del cual se crea el tipo.|  
|**assembly_class**|**sysname**|Nombre de la clase en el ensamblado que define este tipo.|  
|**is_binary_ordered**|**bit**|La ordenación de bytes de este tipo es equivalente a la ordenación mediante operadores de comparación en el tipo.|  
|**is_fixed_length**|**bit**|La longitud del tipo es siempre igual que max_length.|  
|**prog_id**|**nvarchar(40)**|Id. de programa del tipo según se expone para COM.|  
|**assembly_qualified_name**|**nvarchar(4000)**|Nombre de tipo calificado de ensamblado. El nombre tiene un formato adecuado para pasar a Type.GetType().|  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte también  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Vistas de catálogo de tipos escalares &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/scalar-types-catalog-views-transact-sql.md)  
  
  
