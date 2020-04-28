---
title: Ver la configuración de NodeWeight de cuórum de clúster | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], WSFC clusters
- quorum [SQL Server], AlwaysOn and WSFC quorum
ms.assetid: b845e73a-bb01-4de2-aac2-8ac12abebc95
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 12d68b8494fee4400c0a8e9ec043f0972ba2de5c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "72783362"
---
# <a name="view-cluster-quorum-nodeweight-settings"></a>Ver la configuración de NodeWeight de quórum de clúster
  En este tema se describe cómo ver la configuración de NodeWeight para cada nodo miembro en un clúster de clústeres de conmutación por error de Windows Server (WSFC). La configuración de NodeWeight durante el voto de quórum para admitir los escenarios de recuperación de desastres y de múltiples subredes para las instancias de clúster de conmutación por error de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] y [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
-   **Antes de empezar:**  [Requisitos previos](#Prerequisites), [Seguridad](#Security)  
  
-   **Para ver la configuración de NodeWeight de quórum con:** [Uso de Transact-SQL](#TsqlProcedure), [Uso de Powershell](#PowerShellProcedure), [Uso de Cluster.exe](#CommandPromptProcedure)  
  
##  <a name="before-you-start"></a><a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> Requisitos previos  
 Esta característica solo se admite en [!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] o versiones posteriores.  
  
> [!IMPORTANT]  
>  Para usar la configuración de NodeWeight, se debe aplicar la siguiente revisión a todos los servidores del clúster de WSFC:  
>   
>  [KB2494036](https://support.microsoft.com/kb/2494036): hay disponible una revisión para permitir configurar un nodo de clúster que no tiene votos de quórum en [!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] y en [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)]  
  
> [!TIP]  
>  Si esta revisión no está instalada, los ejemplos de este tema devolverán valores vacíos o NULL para NodeWeight.  
  
###  <a name="security"></a><a name="Security"></a> Seguridad  
 El usuario debe ser una cuenta de dominio que sea miembro del grupo Administradores en cada nodo del clúster de WSFC.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usar Transact-SQL  
  
##### <a name="to-view-nodeweight-settings"></a>Para ver la configuración de NodeWeight  
  
1.  Conéctese a cualquier instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] del clúster.  
  
2.  Consulte la vista [sys].[dm_hadr_cluster_members].  
  
### <a name="example-transact-sql"></a>Ejemplo (Transact-SQL)  
 En el ejemplo siguiente se consulta una vista del sistema para devolver valores para todos los nodos del clúster de esa instancia.  
  
```sql  
SELECT  member_name, member_state_desc, number_of_quorum_votes  
 FROM   sys.dm_hadr_cluster_members;  
```  
  
##  <a name="using-powershell"></a><a name="PowerShellProcedure"></a> Usar PowerShell  
  
### <a name="to-view-nodeweight-settings"></a>Para ver la configuración de NodeWeight
  
1.  Inicie Windows PowerShell con derechos elevados mediante **Ejecutar como administrador**.  
  
2.  Importe el módulo `FailoverClusters` para habilitar los commandlets de clúster.  
  
3.  Use el objeto `Get-ClusterNode` para devolver una colección de objetos de nodo de clúster.  
  
4.  Enviar las propiedades de nodo de clúster en un formato legible.  
  
### <a name="example-powershell"></a>Ejemplo (PowerShell)  
 En el ejemplo siguiente se envían algunas de las propiedades de nodo para el clúster denominado "Cluster001".  
  
```powershell  
Import-Module FailoverClusters  
  
$cluster = "Cluster001"  
$nodes = Get-ClusterNode -Cluster $cluster  
  
$nodes | Format-Table -Property NodeName, State, NodeWeight  
```  
  
##  <a name="using-clusterexe"></a><a name="CommandPromptProcedure"></a> Usar Cluster.exe  
  
> [!NOTE]  
>  La utilidad cluster.exe se ha desusado en la versión de [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)] .  Use PowerShell con clústeres de conmutación por error para el desarrollo futuro.  La utilidad cluster.exe se quitará en la siguiente versión de Windows Server. Para obtener más información, vea [Asignar comandos de Cluster.exe a cmdlets de Windows PowerShell para clústeres de conmutación por error](https://technet.microsoft.com/library/ee619744\(WS.10\).aspx).  
  
##### <a name="to-view-nodeweight-settings"></a>Para ver la configuración de NodeWeight  
  
1.  Inicie un símbolo del sistema con privilegios elevados mediante **Ejecutar como administrador**.  
  
2.  Use **cluster.exe** para devolver el estado de nodo y los valores de NodeWeight  
  
### <a name="example-clusterexe"></a>Ejemplo (Cluster.exe)  
 En el ejemplo siguiente se envían algunas de las propiedades de nodo para el clúster denominado "Cluster001".  
  
```cmd
cluster.exe Cluster001 node /status /properties  
```  
  
## <a name="see-also"></a>Consulte también  
 [Configuración de los votos y modos de cuórum WSFC &#40;SQL Server&#41;](wsfc-quorum-modes-and-voting-configuration-sql-server.md)   
 [Configurar los valores de NodeWeight de quórum de clúster](configure-cluster-quorum-nodeweight-settings.md)   
 [sys.dm_hadr_cluster_members &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-members-transact-sql)   
 [Cmdlets de clúster de conmutación por error en Windows PowerShell enumerados por tarea](https://technet.microsoft.com/library/ee619761\(WS.10\).aspx)  
