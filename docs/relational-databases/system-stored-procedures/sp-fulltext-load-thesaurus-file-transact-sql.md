---
title: sp_fulltext_load_thesaurus_file (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_fulltext_load_thesaurus_file
- sp_fulltext_load_thesaurus_file_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fulltext_load_thesaurus_file
- full-text indexes [SQL Server], thesaurus files
- thesaurus [full-text search], editing
ms.assetid: 73a309c3-6d22-42dc-a6fe-8a63747aa2e4
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d076bfde2e4dc4a71af558a08f197d20144ce9db
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47840979"
---
# <a name="spfulltextloadthesaurusfile-transact-sql"></a>sp_fulltext_load_thesaurus_file (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Hace que la instancia de servidor analice y cargue los datos del archivo de sinónimos correspondiente al idioma cuyo LCID se especifica. Este procedimiento almacenado es útil después de actualizar un archivo de sinónimos. Ejecutar **sp_fulltext_load_thesaurus_file** provoca una recompilación de consultas de texto completo que utilizan el diccionario de sinónimos del LCID especificado.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sys.sp_fulltext_load_thesaurus_file lcid [ , @loadOnlyIfNotLoaded  = action ]   
```  
  
## <a name="arguments"></a>Argumentos  
 *lcid*  
 Número entero que asigna el identificador de configuración regional (LCID) del idioma para el que desea lade la definición XML del diccionario de sinónimos. Para obtener los LCID de los idiomas que están disponibles en una instancia del servidor, use la [sys.fulltext_languages &#40;Transact-SQL&#41; ](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md) vista de catálogo.  
  
 **@loadOnlyIfNotLoaded** = *Acción*  
 Especifica si el archivo de diccionario de sinónimos se carga en las tablas de diccionario de sinónimos internas aun cuando ya se haya cargado. *acción* es uno de:  
  
|Valor|Definición|  
|-----------|----------------|  
|**0**|Se carga el archivo de diccionario de sinónimos sin tener en cuenta si ya está cargado. Este es el comportamiento predeterminado de **sp_fulltext_load_thesaurus_file**.|  
|1|Solo se carga el archivo de diccionario de sinónimos si todavía no está cargado.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 None  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Comentarios  
 Las consultas de texto completo que utilizan el diccionario de sinónimos cargan automáticamente los archivos de sinónimos. Para evitar este impacto en el rendimiento de la primera vez en consultas de texto completo, se recomienda que ejecute **sp_fulltext_load_thesaurus_file**.  
  
 Use [sp_fulltext_service](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)'**update_languages**' para actualizar la lista de idiomas registrados con búsqueda de texto completo.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor o el administrador del sistema puede ejecutar la **sp_fulltext_load_thesaurus_file** procedimiento almacenado.  
  
 Solo los administradores del sistema pueden actualizar, modificar o eliminar archivos de diccionarios de sinónimos.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-load-a-thesaurus-file-even-if-it-is-already-loaded"></a>A. Cargar un archivo de diccionario de sinónimos aunque esté cargado  
 En el ejemplo siguiente se analiza y carga el archivo de diccionario de sinónimos en inglés.  
  
```  
EXEC sys.sp_fulltext_load_thesaurus_file 1033;  
GO  
```  
  
### <a name="b-load-a-thesaurus-file-only-if-it-is-not-yet-loaded"></a>B. Cargar un archivo de diccionario de sinónimos si todavía no está cargado  
 El ejemplo siguiente analiza y carga el archivo de diccionario de sinónimos en árabe, a menos que ya esté cargado.  
  
```  
EXEC sys.sp_fulltext_load_thesaurus_file 1025, @loadOnlyIfNotLoaded = 1;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [FULLTEXTSERVICEPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/fulltextserviceproperty-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Configurar y administrar archivos de sinónimos para búsquedas de texto completo](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md)   
 [Configurar y administrar archivos de sinónimos para búsquedas de texto completo](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md)  
  
  
