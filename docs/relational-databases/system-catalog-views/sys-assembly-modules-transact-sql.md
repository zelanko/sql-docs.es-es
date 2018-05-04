---
title: Sys.assembly_modules (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.assembly_modules
- sys.assembly_modules_TSQL
- assembly_modules
- assembly_modules_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.assembly_modules catalog view
ms.assetid: 5f9e644e-8065-49a2-b53d-db7df98f70d8
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 43ab83d17d9bca58790dc06b37ed46b157a97408
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sysassemblymodules-transact-sql"></a>sys.assembly_modules (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Devuelve una fila para cada función, procedimiento o desencadenador definido por un ensamblado de Common Language Runtime (CLR). Esta vista de catálogo asigna los procedimientos almacenados, desencadenadores o funciones CLR a su implementación subyacente. Los objetos de tipo TA, AF, PC, FS y FT tienen un módulo de ensamblado asociado. Para encontrar la asociación entre el objeto y el ensamblado, puede combinar esta vista de catálogo con otras. Por ejemplo, cuando se crea un procedimiento almacenado CLR, se representa mediante una fila de **sys.objects**, una fila en **sys.procedures** (que hereda de **sys.objects**), y una fila de **sys.assembly_modules**. El propio procedimiento almacenado está representado por los metadatos de **sys.objects** y **sys.procedures**. Se encontraron referencias a la implementación de CLR subyacente del procedimiento en **sys.assembly_modules**.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Número de identificación del objeto de SQL. Es único en una base de datos.|  
|**assembly_id**|**int**|Id. del ensamblado desde el que se creó este módulo.|  
|**assembly_class**|**sysname**|Nombre de la clase en el ensamblado que define este módulo.|  
|**assembly_method**|**sysname**|Nombre del método en el **assembly_class** que define este módulo.<br /><br /> Es NULL para las funciones de agregado (AF).|  
|**null_on_null_input**|**bit**|El módulo se ha declarado para generar una salida NULL para cualquier entrada NULL.|  
|**execute_as_principal_id**|**int**|Id. de la entidad de seguridad de base de datos en la que se produce el contexto de ejecución, tal como lo especifica la cláusula EXECUTE AS de la función, procedimiento almacenado o desencadenador CLR.<br /><br /> NULL = EXECUTE AS CALLER. Ésta es la opción predeterminada.<br /><br /> Id. de la entidad de seguridad de base de datos especificada = EXECUTE AS SELF, EXECUTE AS *nombre_usuario*, o EXECUTE AS *login_name*.<br /><br /> -2 = EXECUTE AS OWNER.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Object Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  (Vistas de catálogo de objetos [Transact-SQL])  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
