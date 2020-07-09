---
title: Características de búsqueda de texto completo en desuso en SQL Server 2016
ms.date: 08/19/2016
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- deprecated features [full-text search]
- full-text search [SQL Server], deprecated features
- full-text queries [SQL Server], proximity
ms.assetid: ab0d799c-ba79-4459-837b-c4862730dafd
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.custom: seo-lt-2019
ms.openlocfilehash: f74c1a7f5dbae4ce7d3fb1fe874cfb6ee170063e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85758053"
---
# <a name="deprecated-full-text-search-features-in-sql-server-2016"></a>Características de búsqueda de texto completo en desuso en SQL Server 2016
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  En este tema se describen las características de búsqueda de texto completo en desuso que todavía están disponibles en SQL Server. Está previsto quitar estas características en una versión futura. No use características en desuso en aplicaciones nuevas.  
  
Puede supervisar el uso de características en desuso mediante el contador de rendimiento del objeto **SQL Server:Deprecated Features** (SQL Server: características en desuso) y los eventos de seguimiento. Para obtener más información, vea [Usar objetos de SQL Server](../../relational-databases/performance-monitor/use-sql-server-objects.md).  
  
## <a name="features-no-longer-supported"></a>Características que ya no se admiten  

  
|Característica desusada|Sustituta|Nombre de característica|Id. de la característica|  
|------------------------|-----------------|------------------|----------------|  
|Propiedad FULLTEXTCATALOGPROPERTY: LogSize|Ninguno.|FULLTEXTCATALOGPROPERTY **('LogSize')**|211|  
|Propiedad FULLTEXTSERVICEPROPERTY:<br /><br /> ConnectTimeout<br /><br /> DataTimeout|Ninguno.|FULLTEXTSERVICEPROPERTY **('ConnectTimeout')**<br /><br /> FULLTEXTSERVICEPROPERTY **('DataTimeout'** )|210<br /><br /> 209|  
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
|Operador NEAR genérico de CONTAINS y CONTAINSTABLE:<br /><br /> {<simple_term> &#124; <prefix_term>}<br /><br /> {<br /><br /> { { NEAR &#124; ~ }    {<simple_term> &#124; <prefix_term>} } [...*n*]<br /><br /> }|El operador NEAR personalizado:<br /><br /> NEAR(<br /><br /> {   {<simple_term> &#124; <prefix_term>} [ ,...*n* ]<br /><br /> &#124; ( {<simple_term> &#124; <prefix_term>} [,...*n*] )<br /><br /> [,<distance> [,<order>] ]<br /><br /> }<br /><br /> )<br /><br /> <distance> ::= {*integer* &#124; **MAX**}<br /><br /> <order> ::= {TRUE &#124; **FALSE**}|FULLTEXT_OLD_NEAR_SYNTAX|247|  
|Opción CREATE FULLTEXT CATALOG:<br /><br /> IN PATH '*rootpath*'<br /><br /> ON FILEGROUP *filegroup*|Ninguno.|CREATE FULLTEXT CATLOG IN PATH<br /><br /> Ninguno.<sup>*</sup>|237<br /><br /> Ninguno.*|  
|Propiedad DATABASEPROPERTYEX: IsFullTextEnabled|Ninguno.|DATABASEPROPERTYEX **('IsFullTextEnabled')**|202|  
|sp_detach_db option:<br /><br /> [ @keepfulltextindexfile = ] '*KeepFulltextIndexFile*'|Ninguno.|sp_detach_db @keepfulltextindexfile|226|  
|Valores de acción sp_fulltext_service: resource_usage no tiene ninguna función.|None|sp_fulltext_service @action=resource_usage|200|  
  
 &#42;El objeto **SQL Server:Deprecated Features** no supervisa las repeticiones del *grupo de archivos* CREATE FULLTEXT CATLOG ON FILEGROUP.  
  
  
