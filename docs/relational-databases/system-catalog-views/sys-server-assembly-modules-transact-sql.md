---
title: Sys.server_assembly_modules (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- server_assembly_modules_TSQL
- sys.server_assembly_modules
- server_assembly_modules
- sys.server_assembly_modules_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_assembly_modules catalog view
ms.assetid: af799e38-2d16-49b2-bcf5-6f9199af899e
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 53e1bb84d002322cd4bb9b1443502be0eae47e24
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sysserverassemblymodules-transact-sql"></a>sys.server_assembly_modules (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una fila por cada módulo de ensamblado de los desencadenadores de nivel de servidor de tipo TA. Esta vista asigna los desencadenadores de ensamblado a la implementación CLR subyacente. Puede combinar esta relación para **sys.server_triggers**. El ensamblado deben cargarse en el **maestro** base de datos. La tupla (object_id) es la clave para la relación.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Se trata de una referencia FOREIGN KEY al objeto en el que se define este módulo de ensamblado.|  
|**assembly_id**|**int**|Id. del ensamblado desde el que se creó este módulo. El ensamblado debe estar cargado en la base de datos maestra.|  
|**assembly_class**|**sysname**|Nombre de la clase del ensamblado que define este módulo.|  
|**assembly_method**|**sysname**|Nombre del método de la clase que define este módulo. Es NULL para las funciones de agregado (AF).|  
|**execute_as_principal_id**|**int**|Id. de la entidad de seguridad de servidor EXECUTE AS.<br /><br /> NULL de manera predeterminada o si EXECUTE AS CALLER.<br /><br /> Id. de la entidad de seguridad especificada si EXECUTE AS SELF ejecutar AS \<principal >.<br /><br /> -2 = EXECUTE AS OWNER.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Vistas de catálogo del objeto &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  
  
  
