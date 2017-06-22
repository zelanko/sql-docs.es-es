---
title: "Forzar el inicio de un clúster WSFC sin un quórum | Microsoft Docs"
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
ms.assetid: 4a121375-7424-4444-b876-baefa8fe9015
caps.latest.revision: 21
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 7cef5f82996bc541f55bc8ec6560edce2e0d9acf
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="force-a-wsfc-cluster-to-start-without-a-quorum"></a>Forzar el inicio de un clúster WSFC sin un quórum
  En este tema se describe cómo forzar que un nodo de clúster de los clústeres de conmutación por error de Windows Server (WSFC) se inicie sin un quórum.  Esto puede ser necesario en los escenarios de recuperación de desastres y de múltiples subredes para recuperar datos y reestablecer por completo la alta disponibilidad para las instancias de clúster de conmutación por error de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] y [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
-   **Antes de empezar:**  [Recomendaciones](#Recommendations), [Seguridad](#Security)  
  
-   **Para forzar un clúster se inicie sin un quórum mediante:**  [utilizando el Administrador de clústeres de conmutación por error](#FailoverClusterManagerProcedure), [mediante Powershell](#PowerShellProcedure), [usar Net.exe](#CommandPromptProcedure)  
  
-   **Seguimiento:**  [Seguimiento: Después de forzar que el clúster se inicie sin un quórum](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Recommendations"></a> Recomendaciones  
 Excepto donde se indique de forma explícita, los procedimientos de este tema deben funcionar si se ejecutan desde cualquier nodo del clúster de WSFC.  No obstante, se pueden obtener mejores resultados, y evitar programas de red, si se ejecutan estos pasos desde el nodo que se desea forzar para que se inicie sin un quórum.  
  
###  <a name="Security"></a> Seguridad  
 El usuario debe ser una cuenta de dominio que sea miembro del grupo Administradores en cada nodo del clúster de WSFC.  
  
##  <a name="FailoverClusterManagerProcedure"></a> Usar el Administrador de clústeres de conmutación por error  
  
##### <a name="to-force-a-cluster-to-start-without-a-quorum"></a>Para forzar que un clúster se inicie sin un quórum  
  
1.  Abra el Administrador de clústeres de conmutación por error y conéctese al nodo de clúster deseado para forzarlo en línea.  
  
2.  En el panel **Acciones** , haga clic en **Forzar inicio de clúster**y, a continuación, en **Sí, forzar el inicio del clúster**.  
  
3.  En el panel izquierda, en el árbol **Administrador de clústeres de conmutación por error** , haga clic en el nombre del clúster.  
  
4.  En el panel de resumen, configure que el valor de **Configuración de quórum** actual es:  **Advertencia: el clúster se está ejecutando en el estado ForceQuorum**.  
  
##  <a name="PowerShellProcedure"></a> Usar PowerShell  
  
##### <a name="to-force-a-cluster-to-start-without-a-quorum"></a>Para forzar que un clúster se inicie sin un quórum  
  
1.  Inicie Windows PowerShell con derechos elevados mediante **Ejecutar como administrador**.  
  
2.  Importe el módulo `FailoverClusters` para habilitar los commandlets de clúster.  
  
3.  Use `Stop-ClusterNode` para asegurarse de que el servicio de clúster está detenido.  
  
4.  Use `Start-ClusterNode` con `–FixQuorum` para forzar que se inicie el servicio de clúster.  
  
5.  Use `Get-ClusterNode` con `–Propery NodeWieght = 1` para establecer el valor que garantiza que el nodo es un miembro con derecho a voto del quórum.  
  
6.  Enviar las propiedades de nodo de clúster en un formato legible.  
  
### <a name="example-powershell"></a>Ejemplo (PowerShell)  
 En el siguiente ejemplo se fuerza al servicio de clúster del nodo AlwaysOnSrv02 a iniciarse sin un cuórum, se establece `NodeWeight = 1`y, luego, se enumera el estado de nodo de clúster a partir del nodo que se acaba de forzar.  
  
```powershell  
Import-Module FailoverClusters  
  
$node = "Always OnSrv02"  
Stop-ClusterNode –Name $node  
Start-ClusterNode –Name $node -FixQuorum  
  
(Get-ClusterNode $node).NodeWeight = 1  
  
$nodes = Get-ClusterNode -Cluster $node  
$nodes | Format-Table -property NodeName, State, NodeWeight  
  
```  
  
##  <a name="CommandPromptProcedure"></a> Usar Net.exe  
  
##### <a name="to-force-a-cluster-to-start-without-a-quorum"></a>Para forzar que un clúster se inicie sin un quórum  
  
1.  Use Escritorio remoto para conectarse al nodo de clúster deseado para forzarlo en línea.  
  
2.  Inicie un símbolo del sistema con privilegios elevados mediante **Ejecutar como administrador**.  
  
3.  Use **net.exe** para asegurarse de que el servicio de clúster local está detenido.  
  
4.  Use **net.exe** con `/forcequorum` para forzar que se inicie el servicio de clúster local.  
  
### <a name="example-netexe"></a>Ejemplo (Net.exe)  
 En el siguiente ejemplo se fuerza que un servicio de clúster de nodo se inicie sin un quórum, establece `NodeWeight = 1`y, a continuación, enumera el estado de nodo de clúster a partir del nodo que se acaba de forzar.  
  
```ms-dos  
net.exe stop clussvc  
net.exe start clussvc /forcequorum  
```  
  
##  <a name="FollowUp"></a> Seguimiento: Después de forzar que el clúster se inicie sin un quórum  
  
-   Debe evaluar y configurar de nuevo los valores de NodeWeight para construir correctamente un nuevo quórum antes de volver a poner otros nodos en línea. De lo contrario, el clúster puede volver a estar sin conexión.  
  
     Para obtener más información, vea [Configuración de los votos y modos de cuórum WSFC &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/wsfc-quorum-modes-and-voting-configuration-sql-server.md).  
  
-   Los procedimientos de este tema constituyen solo en paso para volver a poner en línea el clúster de WSFC si se produce un error de quórum no planificado.  Puede que también desee llevar a cabo pasos adicionales para impedir que otros nodos de clúster de WSFC interfieran en la nueva configuración de quórum.  
  
-   Otras características de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], creación de reflejo de la base de datos y trasvase de registros también pueden necesitar acciones posteriores para recuperar los datos y volver a establecer la alta disponibilidad por completo.  
  
     **Para obtener más información:**  
  
     [Realizar una conmutación por error manual forzada de un grupo de disponibilidad &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)  
  
     [Forzar el servicio en una sesión de creación de reflejo de la base de datos &#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/force-service-in-a-database-mirroring-session-transact-sql.md)  
  
     [Conmutar por error a una base de datos secundaria de trasvase de registros &#40;SQL Server&#41;](../../../database-engine/log-shipping/fail-over-to-a-log-shipping-secondary-sql-server.md)  
  
##  <a name="RelatedContent"></a> Contenido relacionado  
  
-   [Ver eventos y registros para un clúster de conmutación por error](http://technet.microsoft.com/en-us/library/cc772342\(WS.10\).aspx)  
  
-   [Cmdlet de clúster de conmutación por error Get-ClusterLog](http://technet.microsoft.com/library/ee461045.aspx)  
  
## <a name="see-also"></a>Vea también  
 [Recuperación ante desastres del clúster WSFC mediante cuórum forzado &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/wsfc-disaster-recovery-through-forced-quorum-sql-server.md)   
 [Configurar los valores de NodeWeight de quórum de clúster](../../../sql-server/failover-clusters/windows/configure-cluster-quorum-nodeweight-settings.md)   
 [Cmdlets de clúster de conmutación por error en Windows PowerShell enumerados por tarea](http://technet.microsoft.com/library/ee619761\(WS.10\).aspx)  
  
  
