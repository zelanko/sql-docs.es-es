---
title: sys.fulltext_languages (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fulltext_languages
- sys.fulltext_languages_TSQL
- fulltext_languages
- fulltext_languages_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- languages [full-text search]
- sys.fulltext_languages catalog view
ms.assetid: 2ed6b53d-1cf2-4763-9d58-36ea24a610ef
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e5af224150508f048d91345cba595517209f824d
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/13/2019
ms.locfileid: "73981776"
---
# <a name="sysfulltext_languages-transact-sql"></a>sys.fulltext_languages (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Esta vista de catálogo contiene una fila por cada idioma cuyos separadores de palabras estén registrados en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Cada fila muestra el LCID y el nombre del idioma. Cuando se registran separadores de palabras para un idioma, los demás recursos lingüísticos (lematizadores, palabras irrelevantes (palabras irrelevantes) y archivos de Diccionario de sinónimos) están disponibles para las operaciones de indización y consulta de texto completo. El valor de **Name** o **LCID** se puede especificar en las instrucciones de las consultas de texto completo y el índice de texto completo [!INCLUDE[tsql](../../includes/tsql-md.md)].  
   
|Columna|Tipo de datos|Descripción|  
|------------|---------------|-----------------|  
|**lcid**|**int**|Identificador de configuración regional (LCID) de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows para el idioma.|  
|**Nombre**|**sysname**|Es el valor del alias en [Sys. syslanguages](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md) que corresponde al valor de **LCID** o la representación de cadena del LCID numérico.|  
  
## <a name="values-returned-for-default-languages"></a>Valores devueltos para los idiomas predeterminados  
 En la tabla siguiente se muestran los valores para los idiomas cuyos separadores de palabras están registrados de forma predeterminada.  
  
|Lenguaje|LCID|  
|--------------|----------|  
|Arabic|1025|  
|Bengali (India)|1093|  
|British English|2057|  
|Bulgarian|1026|  
|Catalan|1027|  
|Chino (Hong Kong ZAE, RPC)|3076|  
|Chinese (Macao SAR)|5124|  
|Chinese (Singapore)|4100|  
|Croatian|1050|  
|Czech|1029|  
|Danés|1030|  
|Dutch|1043|  
|English|3082|  
|French|1036|  
|German|1031|  
|**Válido para** : [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y versiones posteriores.<br /><br /> Greek|1032|  
|Gujarati|1095|  
|Hebrew|1037|  
|Hindi|1081|  
|Icelandic|1039|  
|Indonesian|1057|  
|Italian|1040|  
|Japanese|1041|  
|Canarés|1099|  
|Korean|1042|  
|Latvian|1062|  
|Lithuanian|1063|  
|Malay - Malaysia|1086|  
|Malayalam|1100|  
|Maratí|1102|  
|Neutral|0|  
|Norwegian (Bokmål)|1044|  
|**Válido para** : [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y versiones posteriores.<br /><br /> Polish|1045|  
|Portuguese (Brazil)|1046|  
|Portuguese (Portugal)|2070|  
|Punjabi|1094|  
|Rumano|1048|  
|Russian|1049|  
|Serbian (Cyrillic)|3098|  
|Serbian (Latin)|2074|  
|Simplified Chinese|2052|  
|Slovak|1051|  
|Slovenian|1060|  
|Spanish|3082|  
|Swedish|1053|  
|Tamil|1097|  
|Telugu|1098|  
|Thai|1054|  
|Traditional Chinese|1028|  
|**Válido para** : [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y versiones posteriores.<br /><br /> Turkish|1055|  
|Ukrainian|1058|  
|Urdu|1056|  
|Vietnamese|1066|  
  
## <a name="remarks"></a>Remarks  
 Para actualizar la lista de idiomas registrados en la búsqueda de texto completo, use [sp_fulltext_service](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)"**update_languages**".  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [sp_fulltext_load_thesaurus_file &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-load-thesaurus-file-transact-sql.md)   
 [sp_fulltext_service &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)   
 [Configurar y administrar separadores de palabras y lematizadores para la búsqueda](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)   
 [Configurar y administrar archivos de sinónimos para la búsqueda de texto completo](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md)   
 [Configurar y administrar palabras irrelevantes y listas de palabras irrelevantes para la búsqueda de texto completo](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)   
 [Actualizar la búsqueda de texto completo](../../relational-databases/search/upgrade-full-text-search.md)  
  
  
