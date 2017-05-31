---
title: "Configurar los valores de NodeWeight de cuórum de clúster | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Availability Groups [SQL Server], WSFC clusters
- quorum [SQL Server], AlwaysOn and WSFC quorum
ms.assetid: cb3fd9a6-39a2-4e9c-9157-619bf3db9951
caps.latest.revision: 15
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 2c43965a7e6b0021bb4bcf2d6fdca14e66cafa18
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="configure-cluster-quorum-nodeweight-settings"></a>Configurar los valores de NodeWeight de quórum de clúster
  En este tema se describe cómo configurar los valores de NodeWeight para un nodo miembro en un clúster de clústeres de conmutación por error de Windows Server (WSFC). La configuración de NodeWeight durante el voto de quórum para admitir los escenarios de recuperación de desastres y de múltiples subredes para las instancias de clúster de conmutación por error de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] y [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
-   **Before you start:**  [Prerequisites](#Prerequisites), [Security](#Security)  
  
-   **To view quorum NodeWeight settings using:** [Using Powershell](#PowerShellProcedure), [Using Cluster.exe](#CommandPromptProcedure)  
  
-   [Contenido relacionado](#RelatedContent)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Prerequisites"></a> Requisitos previos  
 Esta característica solo se admite en [!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] o versiones posteriores.  
  
> [!IMPORTANT]  
>  Para usar la configuración de NodeWeight, se debe aplicar la siguiente revisión a todos los servidores del clúster de WSFC:  
>   
>  [KB2494036](http://support.microsoft.com/kb/2494036): hay disponible una revisión para permitir configurar un nodo de clúster que no tiene votos de quórum en [!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] y en [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)]  
  
> [!TIP]  
>  Si esta revisión no está instalada, los ejemplos de este tema devolverán valores vacíos o NULL para NodeWeight.  
  
###  <a name="Security"></a> Seguridad  
 El usuario debe ser una cuenta de dominio que sea miembro del grupo Administradores en cada nodo del clúster de WSFC.  
  
##  <a name="PowerShellProcedure"></a> Usar PowerShell  
  
##### <a name="to-configure-nodeweight-settings"></a>Para configurar las opciones de NodeWeight  
  
1.  Inicie Windows PowerShell con derechos elevados mediante **Ejecutar como administrador**.  
  
2.  Importe el módulo `FailoverClusters` para habilitar los commandlets de clúster.  
  
3.  Use el objeto `Get-ClusterNode` para establecer la propiedad `NodeWeight` para cada nodo del clúster.  
  
4.  Enviar las propiedades de nodo de clúster en un formato legible.  
  
### <a name="example-powershell"></a>Ejemplo (PowerShell)  
 En el siguiente ejemplo se cambia la configuración de NodeWeight para quitar el voto de cuórum del nodo “Always OnSrv1” y, después, se envía la configuración para todos los nodos del clúster.  
  
```powershell  
Import-Module FailoverClusters  
  
$node = “Always OnSrv1”  
(Get-ClusterNode $node).NodeWeight = 0  
  
$cluster = (Get-ClusterNode $node).Cluster  
$nodes = Get-ClusterNode -Cluster $cluster  
  
$nodes | Format-Table -property NodeName, State, NodeWeight  
```  
  
##  <a name="CommandPromptProcedure"></a> Usar Cluster.exe  
  
> [!NOTE]  
>  La utilidad cluster.exe se ha desusado en la versión de [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)] .  Use PowerShell con clústeres de conmutación por error para el desarrollo futuro.  La utilidad cluster.exe se quitará en la siguiente versión de Windows Server. Para obtener más información, vea [Asignar comandos de Cluster.exe a cmdlets de Windows PowerShell para clústeres de conmutación por error](http://technet.microsoft.com/library/ee619744\(WS.10\).aspx).  
  
##### <a name="to-configure-nodeweight-settings"></a>Para configurar las opciones de NodeWeight  
  
1.  Inicie un símbolo del sistema con privilegios elevados mediante **Ejecutar como administrador**.  
  
2.  Use **cluster.exe** para establecer los valores de `NodeWeight` .  
  
### <a name="example-clusterexe"></a>Ejemplo (Cluster.exe)  
 En el siguiente ejemplo se cambia el valor de NodeWeight para quitar el voto de cuórum del nodo “Always OnSrv1” en el clúster “Cluster001”.  
  
```ms-dos  
cluster.exe Cluster001 node Always OnSrv1 /prop NodeWeight=0  
```  
  
##  <a name="RelatedContent"></a> Contenido relacionado  
  
-   [Ver eventos y registros para un clúster de conmutación por error](http://technet.microsoft.com/library/cc772342\(WS.10\).aspx)  
  
-   [Cmdlet de clúster de conmutación por error Get-ClusterLog](http://technet.microsoft.com/library/ee461045.aspx)  
  
## <a name="see-also"></a>Vea también  
 [Configuración de los votos y modos de cuórum WSFC &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/wsfc-quorum-modes-and-voting-configuration-sql-server.md)   
 [Ver la configuración de NodeWeight de quórum de clúster](../../../sql-server/failover-clusters/windows/view-cluster-quorum-nodeweight-settings.md)   
 [Cmdlets de clúster de conmutación por error en Windows PowerShell enumerados por tarea](http://technet.microsoft.com/library/ee619761\(WS.10\).aspx)  
  
  
