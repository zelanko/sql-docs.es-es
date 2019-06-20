---
title: Asignación de SQL-DMO a SMO | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
ms.assetid: 590f5396-98d5-485e-9b41-728c6ed7cb9d
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2a6273032f88807291bfc7024f1abcdbd1440073
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62780685"
---
# <a name="sql-dmo-mapping-to-smo"></a>Asignación de SQL-DMO a SMO
  SQL Distributed Management Objects (SQL-DMO) ya no se incluyen en [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], las aplicaciones SQL-DMO se deberían convertir para utilizar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects (SMO). El modelo de objetos de SMO es similar a SQL-DMO, de modo que la mayor parte de los objetos de SQL-DMO se asignan a un objeto con el mismo nombre en SMO. Sin embargo, algunos objetos de SQL-DMO se cambiaron o se quitaron en la transición a SMO. En esta tabla se enumera la acción recomendada para los objetos de SQL-DMO que no se convirtieron directamente en SMO.  
  
|Objeto SQL-DMO|Acción en SMO|  
|---------------------|-------------------|  
|Objeto View2|Trasladado al espacio de nombres <xref:Microsoft.SqlServer.Management.Smo.Agent>.|  
|Objeto AlertSystem|Trasladado al espacio de nombres <xref:Microsoft.SqlServer.Management.Smo.Agent>.|  
|Objeto Application|Quitado.|  
|Objetos Backup y Backup2|Objetos <xref:Microsoft.SqlServer.Management.Smo.Backup> y <xref:Microsoft.SqlServer.Management.Smo.BackupRestoreBase>.|  
|Objeto BackupDevice|Objetos <xref:Microsoft.SqlServer.Management.Smo.BackupDevice>.|  
|Objetos BulkCopy y BulkCopy2|Quitado y reemplazado por el objeto <xref:Microsoft.SqlServer.Management.Smo.Transfer>.|  
|Objeto Category|Trasladado al espacio de nombres <xref:Microsoft.SqlServer.Management.Smo.Agent>. Reemplazar por los objetos <xref:Microsoft.SqlServer.Management.Smo.Agent.AlertCategory>, <xref:Microsoft.SqlServer.Management.Smo.Agent.OperatorCategory>, <xref:Microsoft.SqlServer.Management.Smo.Agent.JobCategory>.|  
|Objeto Check|Objecto <xref:Microsoft.SqlServer.Management.Smo.Check>|  
|Objetos Column y Column2|<xref:Microsoft.SqlServer.Management.Smo.Column> objeto.|  
|Objeto Configuration|Objetos <xref:Microsoft.SqlServer.Management.Smo.Configuration> y <xref:Microsoft.SqlServer.Management.Smo.ConfigurationBase>.|  
|Objeto ConfigValue|<xref:Microsoft.SqlServer.Management.Smo.ConfigProperty> objeto.|  
|Objetos Database y Database2|<xref:Microsoft.SqlServer.Management.Smo.Database> objeto.|  
|Objetos DatabaseRole y DatabaseRole2|<xref:Microsoft.SqlServer.Management.Smo.DatabaseRole> objeto.|  
|Objeto DBFile|<xref:Microsoft.SqlServer.Management.Smo.DataFile> objeto.|  
|Objetos DBOption y DBOption2|Trasladado al objeto <xref:Microsoft.SqlServer.Management.Smo.DatabaseOptions>.|  
|Objetos Default y Default2|<xref:Microsoft.SqlServer.Management.Smo.Default> objeto.|  
|Objetos DistributionArticle y DistributionArticle2|Mover a <xref:Microsoft.SqlServer.Replication> espacio de nombres.|  
|Objetos DistributionDatabase y DistributionDatabase2|Mover a <xref:Microsoft.SqlServer.Replication> espacio de nombres.|  
|Objetos DistributionPublication y DistributionPublication2|Mover a <xref:Microsoft.SqlServer.Replication> espacio de nombres.|  
|Objetos DistributionSubscription y DistributionSubscription2|Mover a <xref:Microsoft.SqlServer.Replication> espacio de nombres.|  
|Objetos Distributor y Distributor2|Mover a la <xref:Microsoft.SqlServer.Replication> espacio de nombres.|  
|Objeto DRIDefault|Mover a <xref:Microsoft.SqlServer.Management.Smo.ScriptingOptions> objeto.|  
|Objetos FileGroup y FileGroup2|<xref:Microsoft.SqlServer.Management.Smo.FileGroup> objeto.|  
|Objetos FullTextCatalog y FullTextCatalog2|Objetos <xref:Microsoft.SqlServer.Management.Smo.FullTextCatalog> y <xref:Microsoft.SqlServer.Management.Smo.FullTextIndex>.|  
|Objetos Index e Index2|Objecto <xref:Microsoft.SqlServer.Management.Smo.Index>|  
|Objeto IntegratedSecurity|Funcionalidad trasladada al objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> del espacio de nombres <xref:Microsoft.SqlServer.Management.Common>.|  
|Objeto Job|<xref:Microsoft.SqlServer.Management.Smo.Agent.Job> objeto. Mover a <xref:Microsoft.SqlServer.Management.Smo.Agent> espacio de nombres.|  
|Objeto JobFilter|<xref:Microsoft.SqlServer.Management.Smo.Agent.JobFilter> objeto. Mover a <xref:Microsoft.SqlServer.Management.Smo.Agent> espacio de nombres.|  
|Objeto JobHistoryFilter|<xref:Microsoft.SqlServer.Management.Smo.Agent.JobHistoryFilter> objeto. Mover a <xref:Microsoft.SqlServer.Management.Smo.Agent> espacio de nombres.|  
|Objeto JobSchedule|<xref:Microsoft.SqlServer.Management.Smo.Agent.JobSchedule> objeto. Mover a <xref:Microsoft.SqlServer.Management.Smo.Agent> espacio de nombres.|  
|Objetos JobServer y JobServer2|<xref:Microsoft.SqlServer.Management.Smo.Agent.JobServer> objeto. Mover a <xref:Microsoft.SqlServer.Management.Smo.Agent> espacio de nombres.|  
|Objeto JobStep|<xref:Microsoft.SqlServer.Management.Smo.Agent.JobStep> objeto. Mover a <xref:Microsoft.SqlServer.Management.Smo.Agent> espacio de nombres.|  
|Objeto Key|Objetos <xref:Microsoft.SqlServer.Management.Smo.ForeignKey> y <xref:Microsoft.SqlServer.Management.Smo.Index>.|  
|Objetos LinkedServer y LinkedServer2|<xref:Microsoft.SqlServer.Management.Smo.LinkedServer> objeto.|  
|Objeto LinkedServerLogin|<xref:Microsoft.SqlServer.Management.Smo.LinkedServerLogin> objeto.|  
|Objeto LogFile|<xref:Microsoft.SqlServer.Management.Smo.LogFile> objeto.|  
|Objetos Login y Login2|<xref:Microsoft.SqlServer.Management.Smo.Login> objeto.|  
|Objetos MergeArticle y MergeArticle2|<xref:Microsoft.SqlServer.Replication.MergeArticle> objeto. Mover a <xref:Microsoft.SqlServer.Replication> espacio de nombres.|  
|Objeto MergeDynamicSnapshotJob|Mover a <xref:Microsoft.SqlServer.Replication> espacio de nombres.|  
|Objetos MergePublication y MergePublication2|<xref:Microsoft.SqlServer.Replication.MergePublication> objeto. Mover a <xref:Microsoft.SqlServer.Replication> espacio de nombres.|  
|Objetos MergePullSubscription y MergePullSubscription2|<xref:Microsoft.SqlServer.Replication.MergePullSubscription> objeto. Mover a <xref:Microsoft.SqlServer.Replication> espacio de nombres.|  
|Objeto MergeSubscription|<xref:Microsoft.SqlServer.Replication.MergeSubscription> objeto. Mover a <xref:Microsoft.SqlServer.Replication> espacio de nombres.|  
|Objeto MergeSubsetFilter|Mover a `N:Microsoft.SqlServer.Replication` espacio de nombres.|  
|Objeto NameList|Quitado. Funcionalidad alternativa del objeto <xref:Microsoft.SqlServer.Management.Smo.Scripter>.|  
|Objeto Operator|Mover a <xref:Microsoft.SqlServer.Management.Smo.Agent> espacio de nombres.|  
|Objetos Permission y Permission2|Objetos <xref:Microsoft.SqlServer.Management.Smo.ServerPermission>, <xref:Microsoft.SqlServer.Management.Smo.DatabasePermission>, <xref:Microsoft.SqlServer.Management.Smo.ApplicationRole> y <xref:Microsoft.SqlServer.Management.Smo.ObjectPermission>.|  
|Objeto Property|`Property` objeto.|  
|Objetos Publisher y Publisher2|<xref:Microsoft.SqlServer.Replication.ReplicationServer> objeto. Mover a <xref:Microsoft.SqlServer.Replication> espacio de nombres.|  
|Objetos QueryResults y QueryResults2|Reemplazado por el objeto de sistema <xref:System.Data.DataTable> o <xref:System.Data.DataSet>.|  
|Objeto RegisteredServer|Mover a <xref:Microsoft.SqlServer.Replication> espacio de nombres.|  
|Objeto RegisteredSubscriber|Mover a <xref:Microsoft.SqlServer.Replication> espacio de nombres.|  
|Objetos Registry y Registry2|Quitado.|  
|Objeto RemoteLogin|<xref:Microsoft.SqlServer.Management.Common.ServerConnection> objeto. Trasladado al espacio de nombres Common.|  
|Objetos RemoteServer y RemoteServer2|<xref:Microsoft.SqlServer.Management.Common.ServerConnection> objeto. Mover a <xref:Microsoft.SqlServer.Management.Common> espacio de nombres.|  
|Objeto Replication|Mover a <xref:Microsoft.SqlServer.Replication> espacio de nombres.|  
|Objetos ReplicationDatabase y ReplicationDatabase2|<xref:Microsoft.SqlServer.Replication.ReplicationDatabase> objeto. Mover a <xref:Microsoft.SqlServer.Replication> espacio de nombres.|  
|Objeto ReplicationSecurity|<xref:Microsoft.SqlServer.Management.Common.ServerConnection> objeto. Mover a <xref:Microsoft.SqlServer.Management.Common> espacio de nombres.|  
|Objetos ReplicationStoredProcedure y ReplicationStoredProcedure2|<xref:Microsoft.SqlServer.Replication.ReplicationStoredProcedure> objeto. Mover a <xref:Microsoft.SqlServer.Replication> espacio de nombres.|  
|Objetos ReplicationTable y ReplicationTable2|<xref:Microsoft.SqlServer.Replication.ReplicationTable> objeto. Mover a <xref:Microsoft.SqlServer.Replication> espacio de nombres.|  
|Objetos Restore y Restore2|Objetos <xref:Microsoft.SqlServer.Management.Smo.Restore> y <xref:Microsoft.SqlServer.Management.Smo.BackupRestoreBase>.|  
|Objetos Rule y Rule2|Objecto <xref:Microsoft.SqlServer.Management.Smo.Rule>|  
|Objeto Schedule|Mover a <xref:Microsoft.SqlServer.Replication> espacio de nombres.|  
|Objeto ServerGroup|Quitado.|  
|Objeto ServerRole|<xref:Microsoft.SqlServer.Management.Smo.ServerRole> objeto.|  
|Objeto SQLObjectList|<xref:Microsoft.SqlServer.Management.Smo.SqlSmoObject> matriz.|  
|Objetos SQLServer y SQLServer2|<xref:Microsoft.SqlServer.Management.Smo.Server> objeto.|  
|Objetos StoredProcedure y StoredProcedure2|<xref:Microsoft.SqlServer.Management.Smo.StoredProcedure> y <xref:Microsoft.SqlServer.Management.Smo.StoredProcedureParameter> objetos|  
|Objetos Subscriber y Subscriber2|Mover a <xref:Microsoft.SqlServer.Replication> espacio de nombres.|  
|Objetos SystemDatatype y SystemDataType2|<xref:Microsoft.SqlServer.Management.Smo.DataType> objeto.|  
|Objetos Table y Table2|<xref:Microsoft.SqlServer.Management.Smo.Table> objeto.|  
|Objeto TargetServer|Mover a <xref:Microsoft.SqlServer.Management.Smo.Agent> espacio de nombres.|  
|Objeto TargetServerGroup|Mover a <xref:Microsoft.SqlServer.Management.Smo.Agent> espacio de nombres.|  
|Objeto TransactionLog|Funcionalidad trasladada al objeto <xref:Microsoft.SqlServer.Management.Smo.Database>.|  
|Objetos TransArticle y TransArticle2|<xref:Microsoft.SqlServer.Replication.TransArticle> objeto. Mover a <xref:Microsoft.SqlServer.Replication> espacio de nombres.|  
|Método Transfer y objeto Transfer2|<xref:Microsoft.SqlServer.Management.Smo.Transfer> objeto.|  
|Objeto TransPublication y TransPublication2|<xref:Microsoft.SqlServer.Replication.TransPublication> objeto. Mover a <xref:Microsoft.SqlServer.Replication> espacio de nombres.|  
|Objetos TransPullSubscription y TransPullSubscription2|<xref:Microsoft.SqlServer.Replication.TransPullSubscription> objeto. Mover a <xref:Microsoft.SqlServer.Replication> espacio de nombres.|  
|Objeto Trigger y Trigger2|<xref:Microsoft.SqlServer.Management.Smo.Trigger> objeto.|  
|Objetos User y User2|<xref:Microsoft.SqlServer.Management.Smo.User> objeto.|  
|Objetos UserDefinedDatatype y UserDefinedDataType2|<xref:Microsoft.SqlServer.Management.Smo.UserDefinedType> objeto.|  
|Objeto UserDefinedFunction|Objetos <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction> y <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunctionParameter>.|  
|Objetos View y View2|<xref:Microsoft.SqlServer.Management.Smo.View> objeto.|  
  
## <a name="see-also"></a>Vea también  
 [Guía de programación para objetos de administración de SQL Server &#40;SMO&#41;](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)  
  
  
