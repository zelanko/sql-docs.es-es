---
title: "Administración y supervisión de la búsqueda semántica | Microsoft Docs"
ms.custom: 
ms.date: 03/20/2017
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
- semantic search [SQL Server], managing
- semantic search [SQL Server], monitoring
ms.assetid: eb5c3b29-da70-42aa-aa97-7d35a3f1eb98
caps.latest.revision: "19"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f6613fd3036a141f018082f988aa4c3365d0325b
ms.sourcegitcommit: d28d9e3413b6fab26599966112117d45ec2c7045
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/11/2018
---
# <a name="manage-and-monitor-semantic-search"></a>Administrar y supervisar la búsqueda semántica
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Describe el proceso de indexación semántica y las tareas relacionadas con la administración y supervisión de los índices.  
  
##  <a name="HowToMonitorStatus"></a> Comprobación del estado de la indización semántica  
### <a name="is-the-first-phase-of-semantic-indexing-complete"></a>¿Se ha completado la primera fase de la indización semántica?
 Consulte la vista de administración dinámica [sys.dm_fts_index_population &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql.md) y compruebe las columnas **status** y **status_description**.  
  
 La primera fase de la indización incluye el rellenado del índice de palabras clave de texto completo y el índice semántico de frases clave, así como la extracción de datos de similitud de documentos.  
  
```sql  
USE database_name  
GO  
  
SELECT * FROM sys.dm_fts_index_population WHERE table_id = OBJECT_ID('table_name')  
GO  
```  
  
### <a name="is-the-second-phase-of-semantic-indexing-complete"></a>¿Se ha completado la segunda fase de la indización semántica?
 Consulte la vista de administración dinámica [sys.dm_fts_semantic_similarity_population &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-semantic-similarity-population-transact-sql.md) y compruebe las columnas **status** y **status_description**.  
  
 La segunda fase de la indicación incluye el rellenado del índice semántico de similitud de documentos.  
  
```wql  
USE database_name  
GO  
  
SELECT * FROM sys.dm_fts_semantic_similarity_population WHERE table_id = OBJECT_ID('table_name')  
GO  
```  
  
##  <a name="HowToCheckSize"></a> Comprobación del tamaño de los índices semánticos  
### <a name="what-is-the-logical-size-of-a-semantic-key-phrase-index-or-a-semantic-document-similarity-index"></a>¿Cuál es el tamaño lógico de un índice semántico de frases clave o un índice semántico de similitud de documentos?
 Consulte la vista de administración dinámica [sys.dm_db_fts_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-fts-index-physical-stats-transact-sql.md).  
  
 El tamaño lógico se muestra en el número de páginas de índice.  
  
```sql  
USE database_name  
GO  
  
SELECT * FROM sys.dm_db_fts_index_physical_stats WHERE object_id = OBJECT_ID('table_name')  
GO  
```  
  
### <a name="what-is-the-total-size-of-the-full-text-and-semantic-indexes-for-a-full-text-catalog"></a>¿Cuál es el tamaño total de los índices de texto completo y semántico de un catálogo de texto completo?  
 Consulte la propiedad **IndexSize** de la función de metadatos [FULLTEXTCATALOGPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/fulltextcatalogproperty-transact-sql.md).  
  
```sql  
SELECT FULLTEXTCATALOGPROPERTY('catalog_name', 'IndexSize')  
GO  
```  
  
### <a name="how-many-items-are-indexed-in-the-full-text-and-semantic-indexes-for-a-full-text-catalog"></a>¿Cuántos elementos se indizan en los índices de texto completo y semántico de un catálogo de texto completo?  
 Consulte la propiedad **ItemCount** de la función de metadatos [FULLTEXTCATALOGPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/fulltextcatalogproperty-transact-sql.md).  
  
```sql  
SELECT FULLTEXTCATALOGPROPERTY('catalog_name', 'ItemCount')  
GO  
```  
  
##  <a name="HowToForcePopulation"></a> Aplicación del rellenado de los índices semánticos  
 Puede aplicar el rellenado de los índices de texto completo y de los índices semánticos usando las cláusulas START/STOP/PAUSE o RESUME POPULATION con la misma sintaxis y el mismo comportamiento descritos para los índices de texto completo. Para obtener más información, vea [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md) y [Rellenar índices de texto completo](../../relational-databases/search/populate-full-text-indexes.md).  
  
 Dado que la indización semántica depende de la indización de texto completo, los índices semánticos solo se rellenan cuando lo hacen los índices de texto completo.  
  
 **Ejemplo: iniciar el rellenado completo de los índices de texto completo y semántico**  
  
 En el siguiente ejemplo se inicia el rellenado completo de los índices de texto completo y los índices semánticos modificando un índice de texto completo existente en la tabla **Production.Document** de la base de datos de ejemplo AdventureWorks2012.  
  
```vb  
USE AdventureWorks2012  
GO  
  
ALTER FULLTEXT INDEX ON Production.Document  
    START FULL POPULATION  
GO  
```  
  
##  <a name="HowToDisableIndexing"></a> Deshabilitación o nueva habilitación de la indización semántica  
 Puede habilitar o deshabilitar la indización de texto completo o semántica usando la cláusula ENABLE/DISABLE con la misma sintaxis y el mismo comportamiento descritos para los índices de texto completo. Para obtener más información, vea [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md).  
  
 Cuando se deshabilita y se suspende la indización semántica, las consultas sobre datos semánticos siguen funcionando correctamente y devolviendo los datos indizados previamente. Este comportamiento no es coherente con el comportamiento de la búsqueda de texto completo.  
  
```sql  
-- To disable semantic indexing on a table  
USE database_name  
GO  
  
ALTER FULLTEXT INDEX ON table_name DISABLE  
GO  
  
-- To re-enable semantic indexing on a table  
USE database_name  
GO  
  
ALTER FULLTEXT INDEX ON table_name ENABLE  
GO  
```  
  
##  <a name="SemanticIndexing"></a> Acerca de las fases de la indización semántica  
 La búsqueda semántica indiza dos tipos de datos para cada columna en la que esté habilitada:  
  
1.  **Frases clave**  
  
2.  **Similitud de documentos**  
  
 La indización semántica se produce en dos fases, junto con la indización de texto completo:  
  
1.  **Fase 1**. El índice de palabras clave de texto completo y el índice semántico de frases clave se rellenan en paralelo a la vez. Los datos necesarios para indizar la similitud de documentos también se extrae en este momento.  
  
2.  **Fase 2**. Después se rellena el índice semántico de similitud de documentos. Este índice depende de los dos índices que se rellenaron en la fase anterior.  
  
##  <a name="BestPracticeUnderstand"></a>   
##  <a name="ProblemNotPopulated"></a> Problema: los índices semánticos no se rellenan  
### <a name="are-the-associated-full-text-indexes-populated"></a>¿Se rellenan los índices de texto completo asociados?  
 Dado que la indización semántica depende de la indización de texto completo, los índices semánticos solo se rellenan cuando lo hacen los índices de texto completo.  
  
### <a name="are-full-text-search-and-semantic-search-properly-installed-and-configured"></a>¿La búsqueda de texto completo y la búsqueda semántica están instaladas y configuradas correctamente?  
 Para obtener más información, vea [Instalar y configurar la búsqueda semántica](../../relational-databases/search/install-and-configure-semantic-search.md).  
  
### <a name="is-the-fdhost-service-not-available-or-is-there-another-condition-that-would-cause-full-text-indexing-to-fail"></a>¿El servicio FDHOST no está disponible o existe otra condición que provocaría un error de indización de texto completo?  
 Para obtener más información, vea [Solucionar problemas de indexación de texto completo](../../relational-databases/search/troubleshoot-full-text-indexing.md).  
  
  
