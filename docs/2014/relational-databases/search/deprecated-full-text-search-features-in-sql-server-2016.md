---
title: Características de búsqueda de texto completo en SQL Server 2014 en desuso | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- deprecated features [full-text search]
- full-text search [SQL Server], deprecated features
- full-text queries [SQL Server], proximity
ms.assetid: ab0d799c-ba79-4459-837b-c4862730dafd
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 1a49d7db68fe32d9794e89db66020d7f90555508
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/22/2019
ms.locfileid: "66011397"
---
# <a name="deprecated-full-text-search-features-in-sql-server-2014"></a>Características de la búsqueda de texto completo desusadas en SQL Server 2014
  En este tema se describen las características de búsqueda de texto completo desusadas que todavía están disponibles en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Está previsto quitar estas características en una futura versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Las características en desuso no se deben usar en nuevas aplicaciones.  
  
 Puede supervisar el uso de características en desuso utilizando el contador de rendimiento del objeto **SQL Server:Deprecated Features** (SQL Server:Características en desuso) y eventos de seguimiento. Para obtener más información, vea [Usar objetos de SQL Server](../performance-monitor/use-sql-server-objects.md).  
  
## <a name="features-not-supported-in-the-next-version-of-sql-server"></a>Características no admitidas en la siguiente versión de SQL Server  
 Las características de búsqueda de texto completo siguientes no se admitirán en la siguiente versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Característica desusada|Sustituta|Nombre de característica|Id. de la característica|  
|------------------------|-----------------|------------------|----------------|  
|Propiedad FULLTEXTCATALOGPROPERTY: LogSize|Ninguno.|FULLTEXTCATALOGPROPERTY **('LogSize')**|211|  
|Propiedad FULLTEXTSERVICEPROPERTY:<br /><br /> ConnectTimeout<br /><br /> DataTimeout|Ninguno.|FULLTEXTSERVICEPROPERTY **('ConnectTimeout')**<br /><br /> FULLTEXTSERVICEPROPERTY **('DataTimeout'**)|210<br /><br /> 209|  
|sp_fulltext_catalog|CREATE FULL CATALOG<br /><br /> ALTER FULLTEXT CATALOG<br /><br /> DROP FULLTEXT CATALOG|sp_fulltext_catalog|84|  
|sp_fulltext_column<br /><br /> sp_fulltext_database<br /><br /> sp_fulltext_table|CREATE FULL INDEX<br /><br /> ALTER FULLTEXT INDEX<br /><br /> DROP FULLTEXT INDEX|sp_fulltext_column<br /><br /> sp_fulltext_database<br /><br /> sp_fulltext_table|86<br /><br /> 87<br /><br /> 85|  
|sp_help_fulltext_catalogs<br /><br /> sp_help_fulltext_catalog_components<br /><br /> sp_help_fulltext_catalogs_cursor<br /><br /> sp_help_fulltext_columns<br /><br /> sp_help_fulltext_columns_cursor<br /><br /> sp_help_fulltext_tables<br /><br /> sp_help_fulltext_tables_cursor|sys.fulltext_catalogs<br /><br /> sys.fulltext_index_columns<br /><br /> sys.fulltext_indexes|sp_help_fulltext_catalogs<br /><br /> sp_help_fulltext_catalog_components<br /><br /> sp_help_fulltext_catalogs_cursor<br /><br /> sp_help_fulltext_columns<br /><br /> sp_help_fulltext_columns_cursor<br /><br /> sp_help_fulltext_table<br /><br /> sp_help_fulltext_tables_cursor|88<br /><br /> 203<br /><br /> 90<br /><br /> 92<br /><br /> 93<br /><br /> 91<br /><br /> 89|  
|sp_fulltext_service action values: clean_up, connect_timeout y data_timeout devuelven cero|None|sp_fulltext_service @action=clean_up<br /><br /> sp_fulltext_service @action=connect_timeout<br /><br /> sp_fulltext_service @action=data_timeout|116<br /><br /> 117<br /><br /> 118|  
|Columnas sys.dm_fts_active_catalogs:<br /><br /> is_paused<br /><br /> previous_status<br /><br /> previous_status_description<br /><br /> row_count_in_thousands<br /><br /> status<br /><br /> status_description<br /><br /> worker_count|Ninguno.|dm_fts_active_catalogs.is_paused<br /><br /> dm_fts_active_catalogs.previous_status<br /><br /> dm_fts_active_catalogs.previous_status_description<br /><br /> dm_fts_active_catalogs.row_count_in_thousands<br /><br /> dm_fts_active_catalogs.status<br /><br /> dm_fts_active_catalogs.status_description<br /><br /> dm_fts_active_catalogs.worker_count|218<br /><br /> 221<br /><br /> 222<br /><br /> 224<br /><br /> 219<br /><br /> 220<br /><br /> 223|  
|Columna sys.dm_fts_memory_buffers:<br /><br /> row_count|Ninguno.|dm_fts_memory_buffers.row_count|225|  
|Columnas sys.fulltext_catalogs:<br /><br /> path<br /><br /> data_space_id<br /><br /> Columnas file_id|Ninguno.|fulltext_catalogs.path<br /><br /> fulltext_catalogs.data_space_id<br /><br /> fulltext_catalogs.file_id|215<br /><br /> 216<br /><br /> 217|  
  
## <a name="features-not-supported-in-a-future-version-of-sql-server"></a>Características no admitidas en una versión futura de SQL Server  
 Las características de búsqueda de texto completo se admiten en la siguiente versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], pero se quitarán en una versión posterior. No se ha determinado la versión específica de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 El valor en **Nombre de característica** aparece en los eventos de seguimiento como el nombre de objeto (ObjectName) y, en los contadores de rendimiento y en sys.dm_os_performance_counters, como el nombre de instancia. El valor de **Id. de la característica** aparece en los eventos de seguimiento como el identificador de objeto (ObjectId).  
  
|Característica desusada|Sustituta|Nombre de característica|Id. de la característica|  
|------------------------|-----------------|------------------|----------------|  
|Operador NEAR genérico de CONTAINS y CONTAINSTABLE:<br /><br /> {<simple_term> &#124; <prefix_term>}<br /><br /> {<br /><br /> { { NEAR &#124; ~ }    {<simple_term> &#124; <prefix_term>} } [...*n*]<br /><br /> }|El operador NEAR personalizado:<br /><br /> NEAR(<br /><br /> {   {<simple_term> &#124; <prefix_term>} [ ,...*n* ]<br /><br /> &#124; ( {<simple_term> &#124; <prefix_term>} [,...*n*] )<br /><br /> [,\<distance> [,\<order>] ]<br /><br /> }<br /><br /> )<br /><br /> \<distance> ::= {*integer* &#124; **MAX**}<br /><br /> \<order> ::= {TRUE &#124; **FALSE**}|FULLTEXT_OLD_NEAR_SYNTAX|247|  
|Opción CREATE FULLTEXT CATALOG:<br /><br /> IN PATH '*rootpath*'<br /><br /> ON FILEGROUP *filegroup*|Ninguno.|CREATE FULLTEXT CATLOG IN PATH<br /><br /> Ninguno.*|237<br /><br /> Ninguno.<sup>*</sup>|  
|Propiedad DATABASEPROPERTYEX: IsFullTextEnabled|Ninguno.|DATABASEPROPERTYEX **('IsFullTextEnabled')**|202|  
|sp_detach_db option:<br /><br /> [ @keepfulltextindexfile = ] '*KeepFulltextIndexFile*'|Ninguno.|sp_detach_db @keepfulltextindexfile|226|  
|Valores de acción sp_fulltext_service: resource_usage no tiene ninguna función.|None|sp_fulltext_service @action=resource_usage|200|  
  
 \*El objeto **SQL Server:Deprecated Features** no supervisa las apariciones de CREATE FULLTEXT CATLOG ON FILEGROUP *filegroup*.  
  
## <a name="see-also"></a>Vea también  
 [SQL Server, objeto características en desuso](../performance-monitor/sql-server-deprecated-features-object.md)   
 [Cambios sustanciales en búsqueda de texto completo](../../database-engine/breaking-changes-to-full-text-search.md)   
 [Características desusadas del motor de base de datos de SQL Server 2014](../../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)  
  
  
