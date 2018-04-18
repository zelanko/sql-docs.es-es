---
title: Sys.xml_schema_facets (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/10/2016
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
- sys.xml_schema_facets
- xml_schema_facets_TSQL
- sys.xml_schema_facets_TSQL
- xml_schema_facets
dev_langs:
- TSQL
helpviewer_keywords:
- sys.xml_schema_facets catalog view
ms.assetid: 4402dde9-1877-4872-8550-140dc2a177d2
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e09cbbbc7e85610f202061dcf1a4ee10c27c406d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sysxmlschemafacets-transact-sql"></a>sys.xml_schema_facets (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila por faceta (restricción) de una definición de tipo xml (corresponde a **sys.xml_types**).  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**xml_component_id**|**int**|Id. del componente (tipo) XML al que pertenece este aspecto.|  
|**facet_id**|**int**|Id. (ordinal en base 1) del aspecto, único en el identificador del componente.|  
|**tipo**|**char(2)**|Tipo de aspecto:<br /><br /> LG = Longitud<br /><br /> LN = Longitud mínima<br /><br /> LX = Longitud máxima<br /><br /> PT = Patrón (expresión normal)<br /><br /> EU = Enumeración<br /><br /> IN = Valor inclusivo mínimo<br /><br /> IX = Valor inclusivo máximo<br /><br /> EN = Valor exclusivo mínimo<br /><br /> EX = Valor exclusivo máximo<br /><br /> DT = Dígitos totales<br /><br /> DF = Dígitos de fracción<br /><br /> WS = Normalización de espacio en blanco|  
|**kind_desc**|**nvarchar (60)**|Descripción del tipo de aspecto:<br /><br /> LENGTH<br /><br /> MINIMUM_LENGTH<br /><br /> MAXIMUM_LENGTH<br /><br /> PATTERN<br /><br /> ENUMERATION<br /><br /> MINIMUM_INCLUSIVE_VALUE<br /><br /> MAXIMUM_INCLUSIVE_VALUE<br /><br /> MINIMUM_EXCLUSIVE_VALUE<br /><br /> MAXIMUM_EXCLUSIVE_VALUE<br /><br /> TOTAL_DIGITS<br /><br /> FRACTION_DIGITS<br /><br /> WHITESPACE_NORMALIZATION|  
|**is_fixed**|**bit**|1 = El aspecto tiene un valor fijo, especificado previamente.<br /><br /> 0 = No tiene un valor fijo. (predeterminado).|  
|**value**|**nvarchar (4000)**|Valor fijo, especificado previamente del aspecto.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Esquemas XML &#40;sistema de tipo XML&#41; vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
