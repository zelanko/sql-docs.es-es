---
title: sys.assemblies (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.assemblies
- assemblies_TSQL
- sys.assemblies_TSQL
- assemblies
dev_langs:
- TSQL
helpviewer_keywords:
- sys.assemblies catalog view
ms.assetid: e321753f-293f-42ab-b225-d118713df40b
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 335b536d3356f5bfefa6cf5efd71b34327c79708
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62706081"
---
# <a name="sysassemblies-transact-sql"></a>sys.assemblies (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Devuelve una fila para cada ensamblado.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**Nombre**|**sysname**|Nombre del ensamblado. Es único en la base de datos.|  
|**principal_id**|**int**|Id. de la entidad de seguridad propietaria de este ensamblado.|  
|**assembly_id**|**int**|Número de identificación del ensamblado. Es único en una base de datos.|  
|**clr_name**|**nvarchar(4000)**|Cadena canónica que codifica el nombre sencillo, número de versión, referencia cultural, clave pública y arquitectura del ensamblado. Este valor identifica de forma única el ensamblado en Common Language Runtime (CLR).|  
|**permission_set**|**tinyint**|Conjunto de permisos y nivel de seguridad del ensamblado.<br /><br /> 1 = Acceso seguro<br /><br /> 2 = Acceso externo<br /><br /> 3 = Acceso no seguro|  
|**permission_set_desc**|**nvarchar(60)**|Descripción del conjunto de permisos y nivel de seguridad del ensamblado.<br /><br /> SAFE_ACCESS<br /><br /> EXTERNAL_ACCESS<br /><br /> UNSAFE_ACCESS|  
|**is_visible**|**bit**|1 = El ensamblado está visible para registrar puntos de entrada de [!INCLUDE[tsql](../../includes/tsql-md.md)].<br /><br /> 0 = El ensamblado está destinado únicamente a autores de llamadas administrados. Es decir, el ensamblado proporciona una implementación interna para otros ensamblados de la base de datos.|  
|**create_date**|**datetime**|Fecha en que se creó o se registró el ensamblado.|  
|**modify_date**|**datetime**|Fecha en que se modificó el ensamblado.|  
|**is_user_defined**|**bit**|Indica el origen del ensamblado.<br /><br /> 0 = ensamblados definidos por el sistema (como Microsoft.SqlServer.Types para el **hierarchyid** tipo de datos)<br /><br /> 1 = Ensamblados definidos por el usuario.|  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo del ensamblado CLR &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/clr-assembly-catalog-views-transact-sql.md)   
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [ASSEMBLYPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/assemblyproperty-transact-sql.md)  
  
  
