---
description: buscar documentos similares y relacionados con la búsqueda semántica
title: Búsqueda de documentos similares y relacionados con la búsqueda semántica
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- semantic search [SQL Server], document similarity queries
ms.assetid: 9f527883-031b-442f-8e95-24bc0151ecbf
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.custom: seo-lt-2019
ms.openlocfilehash: b0df002c1d170061d6db8b6ee1ba53611e869603
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88498609"
---
# <a name="find-similar-and-related-documents-with-semantic-search"></a>buscar documentos similares y relacionados con la búsqueda semántica
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Describe cómo buscar documentos o valores de texto similares e información acerca de su similitud o relación en columnas configuradas para la indización semántica estadística.  
   
##  <a name="find-similar-or-related-documents-with-semanticsimilaritytable"></a><a name="HowToQuerySimilar"></a> Buscar documentos similares o relacionados con SEMANTICSIMILARITYTABLE  
 Para identificar documentos similares o relacionados en una columna específica, consulte la función [semanticsimilaritytable &#40;Transact-SQL&#41;](../../relational-databases/system-functions/semanticsimilaritytable-transact-sql.md).  
  
 **SEMANTICSIMILARITYTABLE** devuelve una tabla de cero, una o más filas cuyo contenido de la columna especificada es similar semánticamente al documento indicado. Se puede hacer referencia a esta función de conjunto de filas en la cláusula FROM de una instrucción SELECT como un nombre de tabla normal.  
  
 No se puede consultar en varias columnas para documentos similares. La función **SEMANTICSIMILARITYTABLE** solo recupera resultados de la misma columna que la columna de origen, que se identifica mediante el argumento **source_key** .  
  
 Para obtener información detallada sobre los parámetros requeridos por la función **SEMANTICSIMILARITYTABLE** y sobre la tabla de resultados que devuelve, vea [semanticsimilaritytable &#40;Transact-SQL&#41;](../../relational-databases/system-functions/semanticsimilaritytable-transact-sql.md).  
  
> [!IMPORTANT]  
>  Las columnas de destino deben tener habilitada la indización de texto completo y semántica.  
  
###  <a name="example-find-the-top-documents-that-are-similar-to-another-document"></a><a name="HowToIdentifySimilar"></a> Ejemplo: búsqueda de lo principales documentos que son similares a otro documento.  
 En el ejemplo siguiente se recuperan los 10 candidatos principales que son similares al candidato especificado por *\@CandidateID* de la tabla HumanResources.JobCandidate de la base de datos de ejemplo AdventureWorks2012.  
  
```scr  
SELECT TOP(10) KEY_TBL.matched_document_key AS Candidate_ID  
FROM SEMANTICSIMILARITYTABLE  
    (  
    HumanResources.JobCandidate,  
    Resume,  
    @CandidateID  
    ) AS KEY_TBL  
ORDER BY KEY_TBL.score DESC;  
GO  
```  
  
##  <a name="find-info-about-how-documents-are-similar-or-related-with-semanticsimilaritydetailstable"></a><a name="HowToQuerySimilarity"></a>Buscar información sobre la similitud o relación de los documentos con SEMANTICSIMILARITYDETAILSTABLE  
 Para obtener información sobre las frases clave que hacen que los documentos sean similares o relacionados, puede consultar la función [semanticsimilaritydetailstable &#40;Transact-SQL&#41;](../../relational-databases/system-functions/semanticsimilaritydetailstable-transact-sql.md).  
  
 **SEMANTICSIMILARITYDETAILSTABLE** devuelve una tabla de cero, una o más filas de frases clave comunes en dos documentos (un documento de origen y un documento coincidente) cuyo contenido es similar semánticamente. Se puede hacer referencia a esta función de conjunto de filas en la cláusula FROM de una instrucción SELECT como un nombre de tabla normal.  
  
 Para obtener información detallada sobre los parámetros requeridos por la función **SEMANTICSIMILARITYDETAILSTABLE** y sobre la tabla de resultados que devuelve, vea [semanticsimilaritydetailstable &#40;Transact-SQL&#41;](../../relational-databases/system-functions/semanticsimilaritydetailstable-transact-sql.md).  
  
> [!IMPORTANT]  
>  Las columnas de destino deben tener habilitada la indización de texto completo y semántica.  
  
###  <a name="example-find-the-top-key-phrases-that-are-similar-between-documents"></a><a name="HowToSimilarPhrases"></a> Ejemplo: búsqueda de las frases clave destacadas que sean similares entre documentos  
 En el ejemplo siguiente se recuperan las 5 frases clave que tienen la máxima puntuación de similitud entre los candidatos especificados en la tabla **HumanResources.JobCandidate** de la base de datos de ejemplo AdventureWorks2012.  
  
```sql  
SELECT TOP(5) KEY_TBL.keyphrase, KEY_TBL.score  
FROM SEMANTICSIMILARITYDETAILSTABLE  
    (  
    HumanResources.JobCandidate,  
    Resume, @CandidateID,  
    Resume, @MatchedID  
    ) AS KEY_TBL  
ORDER BY KEY_TBL.score DESC;  
GO  
```  
  
  
