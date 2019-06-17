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
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ef59338f86601316a71ae4f97004dc9beceb015f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "64945634"
---
# <a name="sysfulltextlanguages-transact-sql"></a>sys.fulltext_languages (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Esta vista de catálogo contiene una fila por cada idioma cuyos separadores de palabras estén registrados en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Cada fila muestra el LCID y el nombre del idioma. Cuando se registran separadores de palabras para un lenguaje de su otros recursos lingüísticos-lematizadores, palabras irrelevantes (palabras irrelevantes) y archivos se convierten en el diccionario de sinónimos disponibles para las operaciones de indización y de consulta de texto completo. El valor de **nombre** o **lcid** se pueden especificar en las consultas de texto completo y el índice de texto completo [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucciones.  
   
|columna|Data type|Descripción|  
|------------|---------------|-----------------|  
|**lcid**|**int**|Identificador de configuración regional (LCID) de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows para el idioma.|  
|**Nombre**|**sysname**|Es el valor del alias en [sys.syslanguages](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md) corresponde al valor de **lcid** o la representación de cadena del LCID numérico.|  
  
## <a name="values-returned-for-default-languages"></a>Valores devueltos para los idiomas predeterminados  
 En la tabla siguiente se muestran los valores para los idiomas cuyos separadores de palabras están registrados de forma predeterminada.  
  
|Language|LCID|  
|--------------|----------|  
|Árabe|1025|  
|Bengali (India)|1093|  
|British English|2057|  
|Búlgaro|1026|  
|Catalán|1027|  
|Chino (RAE de Hong Kong, RPC)|3076|  
|Chino (RAE de Macao)|5124|  
|Chinese (Singapore)|4100|  
|Croata|1050|  
|Czech|1029|  
|Danish|1030|  
|Neerlandés|1043|  
|Inglés|3082|  
|Francés|1036|  
|German|1031|  
|**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Greek|1032|  
|Gujarati|1095|  
|Hebreo|1037|  
|Hindi|1081|  
|Islandés|1039|  
|Indonesio|1057|  
|Italiano|1040|  
|Japonés|1041|  
|Canarés|1099|  
|Coreano|1042|  
|Letón|1062|  
|Lituano|1063|  
|Malay - Malaysia|1086|  
|Malayalam|1100|  
|Maratí|1102|  
|Neutro|0|  
|Norwegian (Bokmål)|1044|  
|**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Polaco|1045|  
|Portuguese (Brazil)|1046|  
|Portuguese (Portugal)|2070|  
|Punjabí|1094|  
|Rumano|1048|  
|Ruso|1049|  
|Serbian (Cyrillic)|3098|  
|Serbian (Latin)|2074|  
|Chino simplificado|2052|  
|Eslovaco|1051|  
|Esloveno|1060|  
|Español|3082|  
|Sueco|1053|  
|Tamil|1097|  
|Telugu|1098|  
|Tailandés|1054|  
|Chino tradicional|1028|  
|**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Turco|1055|  
|Ucraniano|1058|  
|Urdu|1056|  
|Vietnamita|1066|  
  
## <a name="remarks"></a>Comentarios  
 Para actualizar la lista de idiomas registrados con búsqueda de texto completo, use [sp_fulltext_service](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)'**update_languages**'.  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [sp_fulltext_load_thesaurus_file &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-load-thesaurus-file-transact-sql.md)   
 [sp_fulltext_service &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)   
 [Configurar y administrar separadores de palabras y lematizadores para la búsqueda](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)   
 [Configurar y administrar archivos de sinónimos para búsquedas de texto completo](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md)   
 [Configurar y administrar palabras irrelevantes y listas de palabras irrelevantes para la búsqueda de texto completo](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)   
 [Actualizar la búsqueda de texto completo](../../relational-databases/search/upgrade-full-text-search.md)  
  
  
