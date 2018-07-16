---
title: DDL de búsqueda semántica, funciones, procedimientos almacenados y vistas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: search
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- semantic search [SQL Server], database objects
ms.assetid: 182f395f-3168-48a4-b723-ef4403544f9f
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0632ec8d1222c1bdbda816052d5cfef7ff63ef16
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37208675"
---
# <a name="semantic-search-ddl-functions-stored-procedures-and-views"></a>DDL de búsqueda semántica, funciones, procedimientos almacenados y vistas
  Enumera las instrucciones Transact-SQL y los objetos de base de datos que admiten la búsqueda semántica estadística en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para obtener la lista de instrucciones y objetos de base de datos que admiten la búsqueda de texto completo, vea [DDL de búsqueda de texto completo, funciones, procedimientos almacenados y vistas](../views/views.md).  
  
##  <a name="ddl"></a> Instrucciones del lenguaje de definición de datos (DDL) de Transact-SQL  
  
|Objeto|Más información|  
|------------|----------------------|  
|[ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-index-transact-sql)|[Habilitar la búsqueda semántica en tablas y columnas](enable-semantic-search-on-tables-and-columns.md)|  
|[CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-index-transact-sql)|[Habilitar la búsqueda semántica en tablas y columnas](enable-semantic-search-on-tables-and-columns.md)|  
  
##  <a name="func"></a> Funciones del sistema  
  
|Objeto|Más información|  
|------------|----------------------|  
|[semantickeyphrasetable &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/semantickeyphrasetable-transact-sql)|[Buscar frases clave en documentos con la búsqueda semántica](find-key-phrases-in-documents-with-semantic-search.md)|  
|[semanticsimilaritydetailstable &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/semanticsimilaritydetailstable-transact-sql)|[Buscar documentos similares y relacionados con la búsqueda semántica](find-similar-and-related-documents-with-semantic-search.md)|  
|[semanticsimilaritytable &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/semanticsimilaritytable-transact-sql)|[Buscar documentos similares y relacionados con la búsqueda semántica](find-similar-and-related-documents-with-semantic-search.md)|  
  
##  <a name="meta"></a> Funciones de metadatos del sistema  
  
|Objeto|Más información|  
|------------|----------------------|  
|[COLUMNPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/columnproperty-transact-sql)|[Habilitar la búsqueda semántica en tablas y columnas](enable-semantic-search-on-tables-and-columns.md)|  
|[DATABASEPROPERTYEX &#40;Transact-SQL&#41;](/sql/t-sql/functions/databasepropertyex-transact-sql)|[Habilitar la búsqueda semántica en tablas y columnas](enable-semantic-search-on-tables-and-columns.md)|  
|[FULLTEXTCATALOGPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/fulltextcatalogproperty-transact-sql)|[Administrar y supervisar la búsqueda semántica](manage-and-monitor-semantic-search.md)|  
|[INDEXPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/indexproperty-transact-sql)|[Administrar y supervisar la búsqueda semántica](manage-and-monitor-semantic-search.md)|  
|[OBJECTPROPERTYEX &#40;Transact-SQL&#41;](/sql/t-sql/functions/objectproperty-transact-sql)|[Habilitar la búsqueda semántica en tablas y columnas](enable-semantic-search-on-tables-and-columns.md)|  
|[SERVERPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/serverproperty-transact-sql)|[Instalar y configurar la búsqueda semántica](install-and-configure-semantic-search.md)|  
  
##  <a name="sproc"></a> Procedimientos almacenados del sistema  
  
|Objeto|Más información|  
|------------|----------------------|  
|[sp_fulltext_semantic_register_language_statistics_db &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-fulltext-semantic-register-language-statistics-db-transact-sql)|[Instalar y configurar la búsqueda semántica](install-and-configure-semantic-search.md)|  
|[sp_fulltext_semantic_unregister_language_statistics_db &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-fulltext-semantic-unregister-language-statistics-db-transact-sql)|[Instalar y configurar la búsqueda semántica](install-and-configure-semantic-search.md)|  
  
##  <a name="cv"></a> Vistas del sistema: vistas de catálogo  
  
|Objeto|Más información|  
|------------|----------------------|  
|[sys.fulltext_index_columns &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql)|[Administrar y supervisar la búsqueda semántica](manage-and-monitor-semantic-search.md)|  
|[sys.fulltext_semantic_language_statistics_database &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-semantic-language-statistics-database-transact-sql)|[Instalar y configurar la búsqueda semántica](install-and-configure-semantic-search.md)|  
|[sys.fulltext_semantic_languages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-semantic-languages-transact-sql)|[Instalar y configurar la búsqueda semántica](install-and-configure-semantic-search.md)|  
  
##  <a name="dmv"></a> Vistas del sistema: vistas de administración dinámica  
  
|Objeto|Más información|  
|------------|----------------------|  
|[sys.dm_db_fts_index_physical_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-fts-index-physical-stats-transact-sql)|[Administrar y supervisar la búsqueda semántica](manage-and-monitor-semantic-search.md)|  
|[sys.dm_fts_index_population &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql)|[Administrar y supervisar la búsqueda semántica](manage-and-monitor-semantic-search.md)|  
|[sys.dm_fts_semantic_similarity_population &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-semantic-similarity-population-transact-sql)|[Administrar y supervisar la búsqueda semántica](manage-and-monitor-semantic-search.md)|  
  
## <a name="see-also"></a>Vea también  
 [Administrar y supervisar la búsqueda semántica](manage-and-monitor-semantic-search.md)  
  
  
