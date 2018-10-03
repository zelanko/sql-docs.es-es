---
title: Búsqueda de texto completo y funciones de búsqueda semántica (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- semantic search [SQL Server], system functions
ms.assetid: a61a3694-7604-4583-962e-fc30f771c6fa
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5f2a6364d002200cea1c04b35216dcec6dc0743d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47780993"
---
# <a name="full-text-search-and-semantic-search-functions-transact-sql"></a>Funciones de búsqueda de texto completo y de búsqueda semántica (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  En esta sección se describen las funciones del sistema relacionadas con la búsqueda semántica y de texto completo.  
  
## <a name="full-text-search-functions"></a>Funciones de búsqueda de texto completo  
 [CONTAINSTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)  
 Devuelve una tabla con cero, una o más filas para las columnas que contienen coincidencias exactas o aproximadas (menos precisas) de palabras o frases únicas, palabras próximas a otra dada (dentro de una distancia determinada) o coincidencias ponderadas.  
  
 [FREETEXTTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/freetexttable-transact-sql.md)  
 Devuelve una tabla de cero, uno o más filas para las columnas que contienen valores que coinciden con el significado y no solo literalmente, del texto especificado *cadena_freetext*.  
  
## <a name="semantic-search-functions"></a>Funciones de búsqueda semántica  
 [semantickeyphrasetable &#40;Transact-SQL&#41;](../../relational-databases/system-functions/semantickeyphrasetable-transact-sql.md)  
 Devuelve una tabla con cero, una o más filas para las frases clave asociadas a columnas de la tabla especificada.  
  
 [semanticsimilaritydetailstable &#40;Transact-SQL&#41;](../../relational-databases/system-functions/semanticsimilaritydetailstable-transact-sql.md)  
 Devuelve una tabla de cero, una o más filas de frases clave comunes en dos documentos (un documento origen y un documento coincidente) cuyo contenido es similar semánticamente.  
  
 [semanticsimilaritytable &#40;Transact-SQL&#41;](../../relational-databases/system-functions/semanticsimilaritytable-transact-sql.md)  
 Devuelve una tabla de cero, una, o más filas para las columnas cuyo contenido es similar semánticamente a un documento especificado.  
  
  
