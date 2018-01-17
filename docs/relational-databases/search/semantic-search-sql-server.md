---
title: "Búsqueda semántica (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: search
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-search
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- semantic search [SQL Server]
- semantic search [SQL Server], overview
- statistical semantic search [SQL Server]
- statistical semantic search [SQL Server], overview
ms.assetid: cd8faa9d-07db-420d-93f4-a2ea7c974b97
caps.latest.revision: "20"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 6bd21c1c3be6109431165eb0c7c17ad1cb88a1c6
ms.sourcegitcommit: d28d9e3413b6fab26599966112117d45ec2c7045
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/11/2018
---
# <a name="semantic-search-sql-server"></a>Búsqueda semántica (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] La búsqueda semántica estadística proporciona una visión general amplia de los documentos no estructurados almacenados en las bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante la extracción e indexación de *frases clave* estadísticamente pertinentes. Después, usa las frases clave para identificar e indizar *documentos que son similares o están relacionados*.  
  
##  <a name="whatcanido"></a> ¿Qué puede hacer con la búsqueda semántica?  
 La búsqueda semántica se basa en la características de búsqueda de texto completo existente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], pero habilita nuevos escenarios que van más allá de las búsquedas sintácticas de palabras clave. Mientras que la búsqueda de texto completo permite consultar las *palabras* de un documento, la búsqueda semántica permite consultar el *significado* del documento. Las soluciones que ahora son posibles incluyen la extracción automática de etiquetas, la detección de contenido relacionado y la navegación jerárquica en contenido similar. Por ejemplo, puede consultar el índice de frases clave para compilar la taxonomía de una organización o un corpus de documentos. O bien, puede consultar el índice de similitud de documentos para identificar currículos que coincidan con la descripción de un trabajo.  
  
 En los ejemplos siguientes se demuestran las capacidades de la búsqueda semántica. Al mismo tiempo, estos ejemplos muestran las tres funciones de conjunto de filas de Transact-SQL que se utilizan para consultar los índices semánticos y recuperar los resultados como datos estructurados.  
  
###  <a name="find1"></a> Find the key phrases in a document  
 La consulta siguiente obtiene las frases clave que se identificaron en el documento de ejemplo. Muestra los resultados en orden descendente por la puntuación que clasifica la importancia estadística de cada frase clave.
 
 Esta consulta llama a la función [semantickeyphrasetable](../../relational-databases/system-functions/semantickeyphrasetable-transact-sql.md).  
  
```sql  
SET @Title = 'Sample Document.docx'  
  
SELECT @DocID = DocumentID  
    FROM Documents  
    WHERE DocumentTitle = @Title  
  
SELECT @Title AS Title, keyphrase, score  
    FROM SEMANTICKEYPHRASETABLE(Documents, *, @DocID)  
    ORDER BY score DESC  
  
```  
  
###  <a name="find2"></a> Find similar or related documents  
 La consulta siguiente obtiene los documentos que se identificaron como similares al documento de ejemplo o relacionados con este. Muestra los resultados en orden descendente por la puntuación que clasifica la similitud de los dos documentos.
 
 Esta consulta llama a la función [semanticsimilaritytable](../../relational-databases/system-functions/semanticsimilaritytable-transact-sql.md).  
  
```vb  
SET @Title = 'Sample Document.docx'  
  
SELECT @DocID = DocumentID  
    FROM Documents  
    WHERE DocumentTitle = @Title  
  
SELECT @Title AS SourceTitle, DocumentTitle AS MatchedTitle,  
        DocumentID, score  
    FROM SEMANTICSIMILARITYTABLE(Documents, *, @DocID)  
    INNER JOIN Documents ON DocumentID = matched_document_key  
    ORDER BY score DESC  
  
```  
  
###  <a name="find3"></a> Find the key phrases that make documents similar or related  
 La consulta siguiente obtiene las frases clave que hacen a los dos documentos de ejemplo similares o relacionados entre sí. Muestra los resultados en orden descendente por la puntuación que clasifica el peso de cada frase clave.
 
 Esta consulta llama a la función [semanticsimilaritydetailstable](../../relational-databases/system-functions/semanticsimilaritydetailstable-transact-sql.md).  
  
```sql  
SET @SourceTitle = 'first.docx'  
SET @MatchedTitle = 'second.docx'  
  
SELECT @SourceDocID = DocumentID FROM Documents WHERE DocumentTitle = @SourceTitle  
SELECT @MatchedDocID = DocumentID FROM Documents WHERE DocumentTitle = @MatchedTitle  
  
SELECT @SourceTitle AS SourceTitle, @MatchedTitle AS MatchedTitle, keyphrase, score  
    FROM semanticsimilaritydetailstable(Documents, DocumentContent,  
        @SourceDocID, DocumentContent, @MatchedDocID)  
    ORDER BY score DESC  
  
```  
  
##  <a name="store"></a> Almacenar los documentos en SQL Server  
 Antes de poder indizar documentos con búsqueda semántica, tiene que almacenar los documentos en una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 La característica FileTable de SQL Server, convierte los archivos y documentos no estructurados en objetos de primera clase de la base de datos relacional. Como resultado, los desarrolladores de bases de datos pueden manipular documentos junto con datos estructurados en operaciones basadas en conjuntos de Transact-SQL.  
  
 Para más información sobre la característica FileTable, vea [FileTables &#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md). Para más información sobre la característica FILESTREAM, que es la opción para almacenar documentos en la base de datos, vea [FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md).  
  
##  <a name="reltasks"></a> Related tasks  
 [Instalar y configurar la búsqueda semántica](../../relational-databases/search/install-and-configure-semantic-search.md)  
 Describe los requisitos previos de la búsqueda semántica estadística y cómo instalarlos o comprobarlos.  
  
 [Habilitar la búsqueda semántica en tablas y columnas](../../relational-databases/search/enable-semantic-search-on-tables-and-columns.md)  
 Describe cómo habilitar o deshabilitar la indización semántica estadística de las columnas seleccionadas que contienen documentos o texto.  
  
 [Buscar frases clave en documentos con la búsqueda semántica](../../relational-databases/search/find-key-phrases-in-documents-with-semantic-search.md)  
 Describe cómo buscar las frases clave en documentos o columnas de texto configurados para la indización semántica estadística.  
  
 [buscar documentos similares y relacionados con la búsqueda semántica](../../relational-databases/search/find-similar-and-related-documents-with-semantic-search.md)  
 Describe cómo buscar documentos o valores de texto similares e información acerca de su similitud o relación en columnas configuradas para la indización semántica estadística.  
  
 [Administrar y supervisar la búsqueda semántica](../../relational-databases/search/manage-and-monitor-semantic-search.md)  
 Describe el proceso de indización semántica y las tareas relacionadas con la supervisión y la administración de índices.  
  
##  <a name="relcontent"></a> Related content  
 [DDL de búsqueda semántica, funciones, procedimientos almacenados y vistas](../../relational-databases/search/semantic-search-ddl-functions-stored-procedures-and-views.md)  
 Enumera las instrucciones Transact-SQL y los objetos de base de datos de SQL Server agregados o cambiados para admitir la búsqueda semántica estadística.  
  
  
