---
title: sys.fulltext_catalogs (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fulltext_catalogs_TSQL
- sys.fulltext_catalogs
- fulltext_catalogs
- fulltext_catalogs_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fulltext_catalogs catalog view
ms.assetid: cf1489ff-4819-41fa-a62a-4ed797a16207
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
manager: craigg
ms.openlocfilehash: 0183694382851f023c9f6863848a3e525cc0b7aa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "64945617"
---
# <a name="sysfulltextcatalogs-transact-sql"></a>sys.fulltext_catalogs (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una fila para cada catálogo de texto completo.  
  
> [!NOTE]  
>  Las columnas siguientes se quitarán en una versión futura de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **data_space_id**, **file_id**, y **ruta de acceso**. No utilice estas columnas en nuevos trabajos de desarrollo y modifique lo antes posible las aplicaciones que actualmente usan cualquiera de estas columnas.  
 
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|fulltext_catalog_id|**int**|Id. del catálogo de texto completo. Es único en los catálogos de texto completo de la base de datos.|  
|NAME|**sysname**|Nombre del catálogo. Es único en la base de datos.|  
|path|**nvarchar(260)**|Nombre del directorio de catálogos en el sistema de archivos.|  
|is_default|**bit**|Catálogo de texto completo predeterminado.<br /><br /> True = Es predeterminado.<br /><br /> False = No es predeterminado.|  
|is_accent_sensitivity_on|**bit**|Opción de distinción de acentos del catálogo.<br /><br /> True = Distinción de acentos.<br /><br /> False = Sin distinción de acentos.|  
|data_space_id|**int**|Grupo de archivos donde se creó este catálogo.|  
|file_id|**int**|Identificador de archivo del archivo de texto completo asociado al catálogo.|  
|principal_id|**int**|Identificador de la entidad de seguridad de base de datos que posee el catálogo de texto completo.|  
|is_importing|**bit**|Indica si se va a importar el catálogo de texto completo:<br /><br /> 1 = Se va a importar el catálogo.<br /><br /> 2 = No se va a importar el catálogo.|  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [CREATE FULLTEXT CATALOG &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)   
 [ALTER FULLTEXT CATALOG &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-catalog-transact-sql.md)   
 [DROP FULLTEXT CATALOG &#40;Transact-SQL&#41;](../../t-sql/statements/drop-fulltext-catalog-transact-sql.md)  
  
  
