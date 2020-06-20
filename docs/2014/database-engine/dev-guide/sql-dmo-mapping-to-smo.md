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
ms.openlocfilehash: 147c75384fa65a103c3d17c731add99ecec79b63
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84933376"
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
|Objetos Column y Column2|Objeto <xref:Microsoft.SqlServer.Management.Smo.Column>.|  
|Objeto Configuration|Objetos <xref:Microsoft.SqlServer.Management.Smo.Configuration> y <xref:Microsoft.SqlServer.Management.Smo.ConfigurationBase>.|  
|Objeto ConfigValue|Objeto <xref:Microsoft.SqlServer.Management.Smo.ConfigProperty>.|  
|Objetos Database y Database2|Objeto <xref:Microsoft.SqlServer.Management.Smo.Database>.|  
|Objetos DatabaseRole y DatabaseRole2|Objeto <xref:Microsoft.SqlServer.Management.Smo.DatabaseRole>.|  
|Objeto DBFile|Objeto <xref:Microsoft.SqlServer.Management.Smo.DataFile>.|  
|Objetos DBOption y DBOption2|Trasladado al objeto <xref:Microsoft.SqlServer.Management.Smo.DatabaseOptions>.|  
|Objetos Default y Default2|Objeto <xref:Microsoft.SqlServer.Management.Smo.Default>.|  
|Objetos DistributionArticle y DistributionArticle2|Se mueve al <xref:Microsoft.SqlServer.Replication> espacio de nombres.|  
|Objetos DistributionDatabase y DistributionDatabase2|Se mueve al <xref:Microsoft.SqlServer.Replication> espacio de nombres.|  
|Objetos DistributionPublication y DistributionPublication2|Se mueve al <xref:Microsoft.SqlServer.Replication> espacio de nombres.|  
|Objetos DistributionSubscription y DistributionSubscription2|Se mueve al <xref:Microsoft.SqlServer.Replication> espacio de nombres.|  
|Objetos Distributor y Distributor2|Se ha pasado al <xref:Microsoft.SqlServer.Replication> espacio de nombres.|  
|Objeto DRIDefault|Se ha pasado al <xref:Microsoft.SqlServer.Management.Smo.ScriptingOptions> objeto.|  
|Objetos FileGroup y FileGroup2|Objeto <xref:Microsoft.SqlServer.Management.Smo.FileGroup>.|  
|Objetos FullTextCatalog y FullTextCatalog2|Objetos <xref:Microsoft.SqlServer.Management.Smo.FullTextCatalog> y <xref:Microsoft.SqlServer.Management.Smo.FullTextIndex>.|  
|Objetos Index e Index2|Objecto <xref:Microsoft.SqlServer.Management.Smo.Index>|  
|Objeto IntegratedSecurity|Funcionalidad trasladada al objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> del espacio de nombres <xref:Microsoft.SqlServer.Management.Common>.|  
|Objeto Job|Objeto <xref:Microsoft.SqlServer.Management.Smo.Agent.Job>. Se mueve al <xref:Microsoft.SqlServer.Management.Smo.Agent> espacio de nombres.|  
|Objeto JobFilter|Objeto <xref:Microsoft.SqlServer.Management.Smo.Agent.JobFilter>. Se mueve al <xref:Microsoft.SqlServer.Management.Smo.Agent> espacio de nombres.|  
|Objeto JobHistoryFilter|Objeto <xref:Microsoft.SqlServer.Management.Smo.Agent.JobHistoryFilter>. Se mueve al <xref:Microsoft.SqlServer.Management.Smo.Agent> espacio de nombres.|  
|Objeto JobSchedule|Objeto <xref:Microsoft.SqlServer.Management.Smo.Agent.JobSchedule>. Se mueve al <xref:Microsoft.SqlServer.Management.Smo.Agent> espacio de nombres.|  
|Objetos JobServer y JobServer2|Objeto <xref:Microsoft.SqlServer.Management.Smo.Agent.JobServer>. Se mueve al <xref:Microsoft.SqlServer.Management.Smo.Agent> espacio de nombres.|  
|Objeto JobStep|Objeto <xref:Microsoft.SqlServer.Management.Smo.Agent.JobStep>. Se mueve al <xref:Microsoft.SqlServer.Management.Smo.Agent> espacio de nombres.|  
|Objeto Key|Objetos <xref:Microsoft.SqlServer.Management.Smo.ForeignKey> y <xref:Microsoft.SqlServer.Management.Smo.Index>.|  
|Objetos LinkedServer y LinkedServer2|Objeto <xref:Microsoft.SqlServer.Management.Smo.LinkedServer>.|  
|Objeto LinkedServerLogin|Objeto <xref:Microsoft.SqlServer.Management.Smo.LinkedServerLogin>.|  
|Objeto LogFile|Objeto <xref:Microsoft.SqlServer.Management.Smo.LogFile>.|  
|Objetos Login y Login2|Objeto <xref:Microsoft.SqlServer.Management.Smo.Login>.|  
|Objetos MergeArticle y MergeArticle2|Objeto <xref:Microsoft.SqlServer.Replication.MergeArticle>. Se mueve al <xref:Microsoft.SqlServer.Replication> espacio de nombres.|  
|Objeto MergeDynamicSnapshotJob|Se mueve al <xref:Microsoft.SqlServer.Replication> espacio de nombres.|  
|Objetos MergePublication y MergePublication2|Objeto <xref:Microsoft.SqlServer.Replication.MergePublication>. Se mueve al <xref:Microsoft.SqlServer.Replication> espacio de nombres.|  
|Objetos MergePullSubscription y MergePullSubscription2|Objeto <xref:Microsoft.SqlServer.Replication.MergePullSubscription>. Se mueve al <xref:Microsoft.SqlServer.Replication> espacio de nombres.|  
|Objeto MergeSubscription|Objeto <xref:Microsoft.SqlServer.Replication.MergeSubscription>. Se mueve al <xref:Microsoft.SqlServer.Replication> espacio de nombres.|  
|Objeto MergeSubsetFilter|Se mueve al `N:Microsoft.SqlServer.Replication` espacio de nombres.|  
|Objeto NameList|Quitado. Funcionalidad alternativa del objeto <xref:Microsoft.SqlServer.Management.Smo.Scripter>.|  
|Objeto Operator|Se mueve al <xref:Microsoft.SqlServer.Management.Smo.Agent> espacio de nombres.|  
|Objetos Permission y Permission2|Objetos <xref:Microsoft.SqlServer.Management.Smo.ServerPermission>, <xref:Microsoft.SqlServer.Management.Smo.DatabasePermission>, <xref:Microsoft.SqlServer.Management.Smo.ApplicationRole> y <xref:Microsoft.SqlServer.Management.Smo.ObjectPermission>.|  
|Objeto Property|Objeto `Property`.|  
|Objetos Publisher y Publisher2|Objeto <xref:Microsoft.SqlServer.Replication.ReplicationServer>. Se mueve al <xref:Microsoft.SqlServer.Replication> espacio de nombres.|  
|Objetos QueryResults y QueryResults2|Reemplazado por el objeto de sistema <xref:System.Data.DataTable> o <xref:System.Data.DataSet>.|  
|Objeto RegisteredServer|Se mueve al <xref:Microsoft.SqlServer.Replication> espacio de nombres.|  
|Objeto RegisteredSubscriber|Se mueve al <xref:Microsoft.SqlServer.Replication> espacio de nombres.|  
|Objetos Registry y Registry2|Quitado.|  
|Objeto RemoteLogin|Objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection>. Trasladado al espacio de nombres Common.|  
|Objetos RemoteServer y RemoteServer2|Objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection>. Se mueve al <xref:Microsoft.SqlServer.Management.Common> espacio de nombres.|  
|Objeto Replication|Se mueve al <xref:Microsoft.SqlServer.Replication> espacio de nombres.|  
|Objetos ReplicationDatabase y ReplicationDatabase2|Objeto <xref:Microsoft.SqlServer.Replication.ReplicationDatabase>. Se mueve al <xref:Microsoft.SqlServer.Replication> espacio de nombres.|  
|Objeto ReplicationSecurity|Objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection>. Se mueve al <xref:Microsoft.SqlServer.Management.Common> espacio de nombres.|  
|Objetos ReplicationStoredProcedure y ReplicationStoredProcedure2|Objeto <xref:Microsoft.SqlServer.Replication.ReplicationStoredProcedure>. Se mueve al <xref:Microsoft.SqlServer.Replication> espacio de nombres.|  
|Objetos ReplicationTable y ReplicationTable2|Objeto <xref:Microsoft.SqlServer.Replication.ReplicationTable>. Se mueve al <xref:Microsoft.SqlServer.Replication> espacio de nombres.|  
|Objetos Restore y Restore2|Objetos <xref:Microsoft.SqlServer.Management.Smo.Restore> y <xref:Microsoft.SqlServer.Management.Smo.BackupRestoreBase>.|  
|Objetos Rule y Rule2|Objecto <xref:Microsoft.SqlServer.Management.Smo.Rule>|  
|Objeto Schedule|Se mueve al <xref:Microsoft.SqlServer.Replication> espacio de nombres.|  
|Objeto ServerGroup|Quitado.|  
|Objeto ServerRole|Objeto <xref:Microsoft.SqlServer.Management.Smo.ServerRole>.|  
|Objeto SQLObjectList|Matriz de tipo<xref:Microsoft.SqlServer.Management.Smo.SqlSmoObject> .|  
|Objetos SQLServer y SQLServer2|Objeto <xref:Microsoft.SqlServer.Management.Smo.Server>.|  
|Objetos StoredProcedure y StoredProcedure2|<xref:Microsoft.SqlServer.Management.Smo.StoredProcedure><xref:Microsoft.SqlServer.Management.Smo.StoredProcedureParameter>objetos y|  
|Objetos Subscriber y Subscriber2|Se mueve al <xref:Microsoft.SqlServer.Replication> espacio de nombres.|  
|Objetos SystemDatatype y SystemDataType2|Objeto <xref:Microsoft.SqlServer.Management.Smo.DataType>.|  
|Objetos Table y Table2|Objeto <xref:Microsoft.SqlServer.Management.Smo.Table>.|  
|Objeto TargetServer|Se mueve al <xref:Microsoft.SqlServer.Management.Smo.Agent> espacio de nombres.|  
|Objeto TargetServerGroup|Se mueve al <xref:Microsoft.SqlServer.Management.Smo.Agent> espacio de nombres.|  
|Objeto TransactionLog|Funcionalidad trasladada al objeto <xref:Microsoft.SqlServer.Management.Smo.Database>.|  
|Objetos TransArticle y TransArticle2|Objeto <xref:Microsoft.SqlServer.Replication.TransArticle>. Se mueve al <xref:Microsoft.SqlServer.Replication> espacio de nombres.|  
|Método Transfer y objeto Transfer2|Objeto <xref:Microsoft.SqlServer.Management.Smo.Transfer>.|  
|Objeto TransPublication y TransPublication2|Objeto <xref:Microsoft.SqlServer.Replication.TransPublication>. Se mueve al <xref:Microsoft.SqlServer.Replication> espacio de nombres.|  
|Objetos TransPullSubscription y TransPullSubscription2|Objeto <xref:Microsoft.SqlServer.Replication.TransPullSubscription>. Se mueve al <xref:Microsoft.SqlServer.Replication> espacio de nombres.|  
|Objeto Trigger y Trigger2|Objeto <xref:Microsoft.SqlServer.Management.Smo.Trigger>.|  
|Objetos User y User2|Objeto <xref:Microsoft.SqlServer.Management.Smo.User>.|  
|Objetos UserDefinedDatatype y UserDefinedDataType2|Objeto <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType>.|  
|Objeto UserDefinedFunction|Objetos <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction> y <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunctionParameter>.|  
|Objetos View y View2|Objeto <xref:Microsoft.SqlServer.Management.Smo.View>.|  
  
## <a name="see-also"></a>Consulte también  
 [Guía de programación para objetos de administración de SQL Server &#40;SMO&#41;](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)  
  
  
