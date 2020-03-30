---
title: Filtrar un seguimiento | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- filters [SQL Server], events
- events [SQL Server], filters
- filters [SQL Server]
- filters [SQL Server], traces
- traces [SQL Server], filters
ms.assetid: 019c10ab-68f6-4e40-a5e8-735b2e1270db
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 5e518050759aea98d249e93374a6335bddf30c75
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "72909487"
---
# <a name="filter-a-trace"></a>Filtrar un seguimiento
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Los filtros limitan los eventos que se recopilan en el seguimiento. Si no se establece un filtro, se devolverán todos los eventos de las clases de eventos seleccionadas en el resultado del seguimiento. Por ejemplo, si limita los nombres de usuarios de Windows de un seguimiento para usuarios específicos, los datos de la salida se limitarán solo a aquellos usuarios.  
  
 No es obligatorio establecer un filtro para un seguimiento. Sin embargo, un filtro minimiza la sobrecarga que comporta un seguimiento. Un filtro devuelve los datos relativos y, de este modo, facilita el análisis del rendimiento y las auditorías.  
  
 Para filtrar los datos de eventos capturados en un seguimiento, seleccione los criterios de los eventos de seguimiento que devuelven solo los datos relevantes del seguimiento. Por ejemplo, puede incluir o excluir la supervisión de la actividad de una aplicación específica en el seguimiento.  
  
> [!NOTE]  
>  Cuando el [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] crea seguimientos, filtra su propia actividad de manera predeterminada.  
  
 Como ejemplo adicional, si supervisa consultas para determinar los procesos por lotes que tardan más tiempo en ejecutarse, puede establecer los criterios de los eventos de seguimiento de modo que se supervisen solo los procesos por lotes que tarden más de 30 segundos en ejecutarse (un valor mínimo de CPU de 30.000 milisegundos).  
  
## <a name="filter-creation-guidelines"></a>Directrices para la creación de filtros  
 En general, se deben seguir los pasos que se indican a continuación para filtrar un seguimiento.  
  
1.  Identifique los eventos que desea incluir en el seguimiento.  
  
2.  Identifique los datos y las columnas de datos que contienen la información necesaria.  
  
3.  Identifique un subconjunto de los datos que necesita y defina filtros basándose en ese subconjunto de datos.  

 Por ejemplo, puede que solo le interesen los eventos que tardan más de un tiempo determinado. Puede crear un seguimiento que incluya los eventos en los que el valor de la columna de datos **Duration** supere los 300 milisegundos. El seguimiento no incluirá los eventos que finalicen en menos de 300 milisegundos.  
  
 Puede crear filtros mediante procedimientos almacenados de SQL Server Profiler o Transact-SQL.  
  
 **Para filtrar los eventos de una plantilla de seguimiento**  
  
 [Filtrar eventos en un seguimiento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-events-in-a-trace-sql-server-profiler.md)  
  
 [Establecer un filtro de seguimiento &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/set-a-trace-filter-transact-sql.md)  
  
 **Para modificar filtros**  
  
 [Modificar un filtro &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/modify-a-filter-sql-server-profiler.md)  
  
 La disponibilidad de filtros depende de la columna de datos. Algunas columnas de datos no se pueden filtrar. Las demás solo se pueden filtrar mediante determinados operadores relacionales, como se muestra en la siguiente tabla.  
  
|Operador relacional|Símbolo del operador|Descripción|  
|-------------------------|---------------------|-----------------|  
|Like|LIKE|Especifica que los datos del evento de seguimiento deben ser como el texto escrito. Acepta varios valores.|  
|No es como|No es como|Especifica que los datos del evento de seguimiento no deben ser como el texto escrito. Acepta varios valores.|  
|Equals|=|Especifica que los datos del evento de seguimiento deben ser iguales al valor escrito. Acepta varios valores.|  
|No es igual a|<>|Especifica que los datos del evento de seguimiento deben ser distintos del valor escrito. Acepta varios valores.|  
|Mayor que|>|Especifica que los datos del evento de seguimiento deben ser mayores que el valor escrito.|  
|Mayor o igual que|>=|Especifica que los datos del evento de seguimiento deben ser mayores o iguales que el valor escrito.|  
|Menor que|<|Especifica que los datos del evento de seguimiento deben ser menores que el valor escrito.|  
|Menor o igual que|<=|Especifica que los datos del evento de seguimiento deben ser menores o iguales que el valor escrito.|  
  
 En la siguiente tabla se muestran las columnas de datos filtrables y los operadores relacionales disponibles.  
  
|Columnas de datos|Operadores relacionales|  
|------------------|--------------------------|  
|**ApplicationName**|LIKE, NOT LIKE|  
|**BigintData1**|=, <>, >=, <=|  
|**BigintData2**|=, <>, >=, <=|  
|**BinaryData**|Utilice el [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para filtrar los eventos de esta columna de datos. Para obtener más información, vea [Filtrar seguimientos con SQL Server Profiler](../../tools/sql-server-profiler/filter-traces-with-sql-server-profiler.md).|  
|**ClientProcessID**|=, <>, >=, <=|  
|**ColumnPermissions**|=, <>, >=, <=|  
|**CPU**|=, <>, >=, <=|  
|**DatabaseID**|=, <>, >=, <=|  
|**DatabaseName**|LIKE, NOT LIKE|  
|**DBUserName**|LIKE, NOT LIKE|  
|**Duration**|=, <>, >=, \<=|  
|**EndTime**|>=, <=|  
|**Error**|=, <>, >=, <=|  
|**EventSubClass**|=, <>, >=, <=|  
|**FileName**|LIKE, NOT LIKE|  
|**GUID**|Utilice el [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para filtrar los eventos de esta columna de datos. Para obtener más información, vea [Filtrar seguimientos con SQL Server Profiler](../../tools/sql-server-profiler/filter-traces-with-sql-server-profiler.md).|  
|**Handle**|=, <>, >=, <=|  
|**HostName**|LIKE, NOT LIKE|  
|**IndexID**|=, <>, >=, <=|  
|**IntegerData**|=, <>, >=, <=|  
|**IntegerData2**|=, <>, >=, <=|  
|**IsSystem**|=, <>, >=, <=|  
|**LineNumber**|=, <>, >=, <=|  
|**LinkedServerName**|LIKE, NOT LIKE|  
|**LoginName**|LIKE, NOT LIKE|  
|**LoginSid**|Utilice el [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para filtrar los eventos de esta columna de datos. Para obtener más información, vea [Filtrar seguimientos con SQL Server Profiler](../../tools/sql-server-profiler/filter-traces-with-sql-server-profiler.md).|  
|**MethodName**|LIKE, NOT LIKE|  
|**Modo**|=, <>, >=, <=|  
|**NestLevel**|=, <>, >=, <=|  
|**NTDomainName**|LIKE, NOT LIKE|  
|**NTUserName**|LIKE, NOT LIKE|  
|**ObjectID**|=, <>, >=, <=|  
|**ObjectID2**|=, <>, >=, <=|  
|**ObjectName**|LIKE, NOT LIKE|  
|**ObjectType**|=, <>, >=, <=|  
|**Offset**|=, <>, >=, <=|  
|**OwnerID**|=, <>, >=, <=|  
|**OwnerName**|LIKE, NOT LIKE|  
|**ParentName**|LIKE, NOT LIKE|  
|**Permisos**|=, <>, >=, <=|  
|**ProviderName**|LIKE, NOT LIKE|  
|**Reads**|=, <>, >=, <=|  
|**IdSolicitud**|=, <>, >=, <=|  
|**RoleName**|LIKE, NOT LIKE|  
|**RowCounts**|=, <>, >=, <=|  
|**SessionLoginName**|LIKE, NOT LIKE|  
|**Gravedad**|=, <>, >=, <=|  
|**SourceDatabaseID**|=, <>, >=, <=|  
|**SPID**|=, <>, >=, \<=|  
|**SqlHandle**|Utilice el [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para filtrar los eventos de esta columna de datos. Para obtener más información, vea [Filtrar seguimientos con SQL Server Profiler](../../tools/sql-server-profiler/filter-traces-with-sql-server-profiler.md).|  
|**StartTime**|>=, <=|  
|**State**|=, <>, >=, <=|  
|**Success**|=, <>, >=, <=|  
|**TargetLoginName**|LIKE, NOT LIKE|  
|**TargetLoginSid**|Utilice el [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para filtrar los eventos de esta columna de datos. Para obtener más información, vea [Filtrar seguimientos con SQL Server Profiler](../../tools/sql-server-profiler/filter-traces-with-sql-server-profiler.md).|  
|**TargetUserName**|LIKE, NOT LIKE|  
|**TextData** *|LIKE, NOT LIKE|  
|**TransactionID**|=, <>, >=, <=|  
|**Tipo**|=, <>, >=, <=|  
|**Writes**|=, <>, >=, <=|  
|**XactSequence**|=, <>, >=, <=|  
  
 \* Si se realiza un seguimiento de los eventos con la utilidad **osql** o **sqlcmd** , agregue siempre **%** a los filtros de la columna **TextData** .  
  
 Como mecanismo de seguridad, Seguimiento de SQL omite automáticamente del seguimiento la información de los procedimientos almacenados relacionados con la seguridad que afecten a contraseñas. Este mecanismo de seguridad no es configurable y siempre está activo, lo que impide que los usuarios, que de otra manera tendrían los permisos para realizar el seguimiento de toda la actividad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], capturen contraseñas.  
  
 Se supervisan los siguientes procedimientos almacenados relativos a la seguridad, pero no se escribe ninguna salida en la columna de datos **TextData** :  
  
 [sp_addapprole &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addapprole-transact-sql.md)  
  
 [sp_adddistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)  
  
 [sp_adddistributiondb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md)  
  
 [sp_adddistributor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistributor-transact-sql.md)  
  
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)  
  
 [sp_addlinkedsrvlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)  
  
 [sp_addlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)  
  
 [sp_addmergepullsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)  
  
 [sp_addpullsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)  
  
 [sp_addremotelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addremotelogin-transact-sql.md)  
  
 [sp_addsubscriber &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscriber-transact-sql.md)  
  
 [sp_approlepassword &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-approlepassword-transact-sql.md)  
  
 [sp_changedistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql.md)  
  
 [sp_changesubscriber &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changesubscriber-transact-sql.md)  
  
 [sp_dsninfo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dsninfo-transact-sql.md)  
  
 [sp_helpsubscription_properties &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)  
  
 [sp_link_publication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md)  
  
 [sp_password &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-password-transact-sql.md)  
  
 [sp_setapprole &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-setapprole-transact-sql.md)  
  
  
