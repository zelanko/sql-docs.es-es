---
title: ALTER FULLTEXT STOPLIST (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER FULLTEXT STOPLIST
- ALTER_FULLTEXT_STOPLIST_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- stoplists [full-text search]
- full-text search [SQL Server], stoplists
- ALTER FULLTEXT STOPLIST statement
- full-text search [SQL Server], stopwords
- stopwords [full-text search]
ms.assetid: f6ad87d5-6a34-435a-8456-8244947c5c83
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 20947c0331f9713a937e0a7de8efb1f2fc9f753c
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="alter-fulltext-stoplist-transact-sql"></a>ALTER FULLTEXT STOPLIST (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Inserta o elimina una palabra irrelevante en la lista de palabras irrelevantes de texto completo predeterminada de la base de datos actual.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
ALTER FULLTEXT STOPLIST stoplist_name  
{   
        ADD [N] 'stopword' LANGUAGE language_term    
  | DROP   
    {  
        'stopword' LANGUAGE language_term   
      | ALL LANGUAGE language_term   
      | ALL  
     }  
;  
```  
  
## <a name="arguments"></a>Argumentos  
 *stoplist_name*  
 Es el nombre de la lista de palabras irrelevantes que se está modificando. *stoplist_name* puede tener un máximo de 128 caracteres.  
  
 **'** *palabra irrelevante* **'**  
 Es una cadena que podría ser una palabra con significado lingüístico en el idioma especificado o un token que no tiene un significado lingüístico. *palabra irrelevante* está limitado a la longitud máxima del token (64 caracteres). Una palabra irrelevante se puede especificar en forma de cadena Unicode.  
  
 IDIOMA *language_term*  
 Especifica el idioma que desea asociar a la *palabra irrelevante* que se va a agregar o quitar.  
  
 *language_term* se puede especificar como una cadena, entero o un valor hexadecimal correspondiente al identificador de configuración regional (LCID) del idioma, como se indica a continuación:  
  
|Formato|Description|  
|------------|-----------------|  
|String|*language_term* corresponde a la **alias** valor de columna en la [sys.syslanguages (Transact-SQL)](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md) vista de compatibilidad. La cadena debe incluirse entre comillas simples, como en **'***language_term***'**.|  
|Integer|*language_term* es el LCID del idioma.|  
|Hexadecimal|*language_term* 0 x seguido del valor hexadecimal del LCID. El valor hexadecimal no puede superar los ocho dígitos, incluidos los ceros a la izquierda. Si el valor está en formato de juego de caracteres de doble byte (DBCS), SQL Server lo convertirá a Unicode.|  
  
 AGREGAR **'***palabra irrelevante***'** LENGUAJE *language_term*  
 Agrega una palabra irrelevante a la lista de palabras irrelevantes para el idioma especificado por idioma *language_term*.  
  
 Si la combinación especificada de la palabra clave y del valor LCID del idioma no es única en la lista de palabras irrelevantes, se devuelve un error.  Si el valor LCID no corresponde a un idioma registrado, se genera un error.  
  
 DROP { **'***palabra irrelevante***'** LENGUAJE *language_term* | Todos los idiomas *language_term* | ALL}  
 Quita una palabra de la lista de palabras irrelevantes.  
  
 **'** *palabra irrelevante* **'** LENGUAJE *language_term*  
 Quita la palabra irrelevante especificada para el idioma especificado por *language_term*.  
  
 Todos los idiomas *language_term*  
 Quita todas las palabras irrelevantes para el idioma especificado por *language_term*.  
  
 ALL  
 Quita todas las palabras irrelevantes de la lista de palabras irrelevantes.  
  
## <a name="remarks"></a>Comentarios  
 CREATE FULLTEXT STOPLIST solo se admite para el nivel de compatibilidad 100 y posterior. Para los niveles de compatibilidad 80 y 90, la lista de palabras irrelevantes del sistema siempre se asigna a la base de datos.  
  
## <a name="permissions"></a>Permissions  
 Para designar una lista de palabras irrelevantes como la lista predeterminada de la base de datos, se requiere el permiso ALTER DATABASE. Para modificar una lista de palabras irrelevantes es necesario ser el propietario de la lista de palabras irrelevantes o la pertenencia a la **db_owner** o **db_ddladmin** funciones fijas de base de datos.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se modifica la lista de palabras irrelevantes `CombinedFunctionWordList`, agregando la palabra 'en', primero para español y, a continuación, para francés.  
  
```  
ALTER FULLTEXT STOPLIST CombinedFunctionWordList ADD 'en' LANGUAGE 'Spanish';  
ALTER FULLTEXT STOPLIST CombinedFunctionWordList ADD 'en' LANGUAGE 'French';  
```  
  
## <a name="see-also"></a>Vea también  
 [Crear lista de palabras IRRELEVANTES de texto completo &#40; Transact-SQL &#41;](../../t-sql/statements/create-fulltext-stoplist-transact-sql.md)   
 [DROP FULLTEXT STOPLIST &#40; Transact-SQL &#41;](../../t-sql/statements/drop-fulltext-stoplist-transact-sql.md)   
 [Configurar y administrar palabras irrelevantes y listas de palabras irrelevantes para la búsqueda de texto completo](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)   
 [Sys.fulltext_stoplists &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql.md)   
 [Sys.fulltext_stopwords &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql.md)   
 [Configurar y administrar palabras irrelevantes y listas de palabras irrelevantes para la búsqueda de texto completo](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)  
  
  
