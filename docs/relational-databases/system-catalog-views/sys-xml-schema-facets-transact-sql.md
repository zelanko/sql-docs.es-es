---
title: Sys.xml_schema_facets (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.xml_schema_facets
- xml_schema_facets_TSQL
- sys.xml_schema_facets_TSQL
- xml_schema_facets
dev_langs: TSQL
helpviewer_keywords: sys.xml_schema_facets catalog view
ms.assetid: 4402dde9-1877-4872-8550-140dc2a177d2
caps.latest.revision: "33"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: df9761b05605282e125c9fee091cde0dfa345012
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="sysxmlschemafacets-transact-sql"></a>sys.xml_schema_facets (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila por faceta (restricción) de una definición de tipo xml (corresponde a **sys.xml_types**).  
  
||  
|-|  
|**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**xml_component_id**|**int**|Id. del componente (tipo) XML al que pertenece este aspecto.|  
|**facet_id**|**int**|Id. (ordinal en base 1) del aspecto, único en el identificador del componente.|  
|**tipo**|**Char(2)**|Tipo de aspecto:<br /><br /> LG = Longitud<br /><br /> LN = Longitud mínima<br /><br /> LX = Longitud máxima<br /><br /> PT = Patrón (expresión normal)<br /><br /> EU = Enumeración<br /><br /> IN = Valor inclusivo mínimo<br /><br /> IX = Valor inclusivo máximo<br /><br /> EN = Valor exclusivo mínimo<br /><br /> EX = Valor exclusivo máximo<br /><br /> DT = Dígitos totales<br /><br /> DF = Dígitos de fracción<br /><br /> WS = Normalización de espacio en blanco|  
|**kind_desc**|**nvarchar (60)**|Descripción del tipo de aspecto:<br /><br /> LENGTH<br /><br /> MINIMUM_LENGTH<br /><br /> MAXIMUM_LENGTH<br /><br /> PATTERN<br /><br /> ENUMERATION<br /><br /> MINIMUM_INCLUSIVE_VALUE<br /><br /> MAXIMUM_INCLUSIVE_VALUE<br /><br /> MINIMUM_EXCLUSIVE_VALUE<br /><br /> MAXIMUM_EXCLUSIVE_VALUE<br /><br /> TOTAL_DIGITS<br /><br /> FRACTION_DIGITS<br /><br /> WHITESPACE_NORMALIZATION|  
|**is_fixed**|**bit**|1 = El aspecto tiene un valor fijo, especificado previamente.<br /><br /> 0 = No tiene un valor fijo. (predeterminado).|  
|**valor**|**nvarchar (4000)**|Valor fijo, especificado previamente del aspecto.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Esquemas XML &#40; Sistema de tipo XML &#41; Vistas de catálogo &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
