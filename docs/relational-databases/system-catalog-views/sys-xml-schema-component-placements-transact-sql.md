---
title: Sys.xml_schema_component_placements (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.xml_schema_component_placements
- xml_schema_component_placements_TSQL
- xml_schema_component_placements
- sys.xml_schema_component_placements_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.xml_schema_component_placements catalog view
ms.assetid: 2d3c8828-e4b3-423d-bf11-990464c1341b
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 78403dd04dc4fb1e531032c9f80639134f58b6ef
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47818283"
---
# <a name="sysxmlschemacomponentplacements-transact-sql"></a>sys.xml_schema_component_placements (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila por ubicación de componentes del esquema XML.  
   
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**xml_component_id**|**int**|Id. del componente del esquema XML propietario de esta ubicación.|  
|**placement_id**|**int**|Id. de la ubicación. Es exclusiva en el propietario del componente del esquema XML.|  
|**placed_xml_component_id**|**int**|Id. del componente del esquema XML ubicado.|  
|**is_default_fixed**|**bit**|1 = el valor predeterminado es un valor fijo. Este valor no se puede anular en una instancia de XML.<br /><br /> 0 = El valor se puede omitir. (predeterminado)|  
|**min_occurrences**|**int**|Número mínimo de casos de componentes ubicados.|  
|**max_occurrences**|**int**|Número máximo de casos de componentes ubicados.|  
|**default_value**|**nvarchar (4000)**|Valor predeterminado si se proporciona uno. Si no se ofrece otro valor predeterminado, es NULL.|  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Los esquemas XML &#40;sistema de tipo XML&#41; vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
