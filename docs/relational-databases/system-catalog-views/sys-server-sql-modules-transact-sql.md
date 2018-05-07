---
title: Sys.server_sql_modules (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.server_sql_modules
- sys.server_sql_modules_TSQL
- server_sql_modules_TSQL
- server_sql_modules
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_sql_modules catalog view
ms.assetid: 9ef9a8b9-c470-4a61-b0c4-ee24ad871d63
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: da09ea47bc62839239630029cbdd054c498b0f4a
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="sysserversqlmodules-transact-sql"></a>sys.server_sql_modules (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene el conjunto de módulos SQL para los desencadenadores de nivel de servidor de tipo TR. Puede combinar esta relación con sys.server_triggers. La tupla (object_id) es la clave de la relación.  
  
|Nombre de la columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Se trata de una referencia FOREIGN KEY al desencadenador de nivel de servidor en el que se define este módulo.|  
|**Definición**|**nvarchar(max)**|Texto SQL que define este módulo.<br /><br /> NULL = Cifrado.|  
|**uses_ansi_nulls**|**bit**|El módulo fue creado con la opción de conjunto ANSI NULLS establecida en ON.|  
|**uses_quoted_identifier**|**bit**|El módulo fue creado con la opción de conjunto QUOTED IDENTIFIER establecida en ON.|  
|**execute_as_principal_id**|**int**|Id. de la entidad de seguridad de servidor EXECUTE AS.<br /><br /> NULL de manera predeterminada o si EXECUTE AS CALLER <br /><br /> Id. de la entidad de seguridad especificada si EXECUTE AS SELF ejecutar AS principal-2 = EXECUTE AS OWNER.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
