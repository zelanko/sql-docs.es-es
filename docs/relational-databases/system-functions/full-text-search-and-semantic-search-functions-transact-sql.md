---
title: Búsqueda de texto completo y funciones de búsqueda semántica (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- semantic search [SQL Server], system functions
ms.assetid: a61a3694-7604-4583-962e-fc30f771c6fa
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 70e9351761332d534f612cfe77d20c301a9423cb
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="full-text-search-and-semantic-search-functions-transact-sql"></a>Funciones de búsqueda de texto completo y de búsqueda semántica (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  En esta sección se describen las funciones del sistema relacionadas con la búsqueda semántica y de texto completo.  
  
## <a name="full-text-search-functions"></a>Funciones de búsqueda de texto completo  
 [CONTAINSTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)  
 Devuelve una tabla con cero, una o más filas para las columnas que contienen coincidencias exactas o aproximadas (menos precisas) de palabras o frases únicas, palabras próximas a otra dada (dentro de una distancia determinada) o coincidencias ponderadas.  
  
 [FREETEXTTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/freetexttable-transact-sql.md)  
 Devuelve una tabla de cero, uno o más filas para las columnas que contienen valores que coinciden con el significado y no solo literalmente, del texto especificado *freetext_string*.  
  
## <a name="semantic-search-functions"></a>Funciones de búsqueda semántica  
 [semantickeyphrasetable &#40;Transact-SQL&#41;](../../relational-databases/system-functions/semantickeyphrasetable-transact-sql.md)  
 Devuelve una tabla con cero, una o más filas para las frases clave asociadas a columnas de la tabla especificada.  
  
 [semanticsimilaritydetailstable &#40;Transact-SQL&#41;](../../relational-databases/system-functions/semanticsimilaritydetailstable-transact-sql.md)  
 Devuelve una tabla de cero, una o más filas de frases clave comunes en dos documentos (un documento origen y un documento coincidente) cuyo contenido es similar semánticamente.  
  
 [semanticsimilaritytable &#40;Transact-SQL&#41;](../../relational-databases/system-functions/semanticsimilaritytable-transact-sql.md)  
 Devuelve una tabla de cero, una, o más filas para las columnas cuyo contenido es similar semánticamente a un documento especificado.  
  
  
