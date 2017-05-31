---
title: Configurar los valores de la propiedad HealthCheckTimeout | Microsoft Docs
ms.custom: 
ms.date: 03/09/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3bbeb979-e6fc-4184-ad6e-cca62108de74
caps.latest.revision: 31
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: fe45e057f3e8a9a4cd105cad16ef773c2aed0928
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="configure-healthchecktimeout-property-settings"></a>Configurar los valores de la propiedad HealthCheckTimeout
  El valor HealthCheckTimeout se emplea para especificar el tiempo, en milisegundos, que la DLL de recursos de SQL Server debe esperar la información devuelta por el procedimiento almacenado [sp_server_diagnostics](../../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md) antes de notificar a la instancia de clúster de conmutación por error (FCI) AlwaysOn que no ha recibido respuesta. Los cambios que se realizan en la configuración del tiempo de espera son vigentes de forma inmediata y no requieren reiniciar el recurso de SQL Server.  
  
-   **Before you begin:**  [Limitations and Restrictions](#Limits), [Security](#Security)  
  
-   **To Configure the HeathCheckTimeout setting, using:**  [PowerShell](#PowerShellProcedure), [Failover Cluster Manager](#WSFC), [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Limits"></a> Limitaciones y restricciones  
 El valor predeterminado para esta propiedad es 30 000 milisegundos (30 segundos). El valor mínimo es 15.000 milisegundos (15 segundos).  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Se necesitan los permisos ALTER SETTINGS y VIEW SERVER STATE.  
  
##  <a name="PowerShellProcedure"></a> Usar PowerShell  
  
##### <a name="to-configure-healthchecktimeout-settings"></a>Para configurar los valores de HealthCheckTimeout  
  
1.  Inicie Windows PowerShell con derechos elevados mediante **Ejecutar como administrador**.  
  
2.  Importe el módulo **FailoverClusters** para habilitar los cmdlets de clúster.  
  
3.  Use el cmdlet **Get-ClusterResource** para encontrar el recurso [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Después, use el cmdlet **Set-ClusterParameter** a fin de establecer la propiedad **HealthCheckTimeout** para la instancia de clúster de conmutación por error.  
  
> [!TIP]  
>  Cada vez que abre una nueva ventana de PowerShell, tiene que importar el módulo **FailoverClusters** .  
  
### <a name="example-powershell"></a>Ejemplo (PowerShell)  
 En el ejemplo siguiente se cambia el valor de HealthCheckTimeout en el recurso de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] "`SQL Server (INST1)`" a 60000 milisegundos.  
  
```powershell  
Import-Module FailoverClusters  
  
$fci = "SQL Server (INST1)"  
Get-ClusterResource $fci | Set-ClusterParameter HealthCheckTimeout 60000  
  
```  
  
### <a name="related-content-powershell"></a>Contenido relacionado (PowerShell)  
  
-   [Clustering and High-Availability (Clústeres y alta disponibilidad)](http://blogs.msdn.com/b/clustering/archive/2009/05/23/9636665.aspx) (blog del equipo de Agrupacion de clústeres de conmutación por error y equilibrio de carga de red)  
  
-   [Introducción a Windows PowerShell en un clúster de conmutación por error](http://technet.microsoft.com/library/ee619762\(WS.10\).aspx)  
  
-   [Comandos de recursos de clúster y cmdlets equivalentes de Windows PowerShell](http://msdn.microsoft.com/library/ee619744.aspx#BKMK_resource)  
  
##  <a name="WSFC"></a> Usar el complemento Administrador de clústeres de conmutación por error  
 **Para configurar el valor de HealthCheckTimeout**  
  
1.  Abra el complemento Administrador de clústeres de conmutación por error.  
  
2.  Expanda **Servicios y aplicaciones** y seleccione la FCI.  
  
3.  Haga clic con el botón derecho en el **recurso de SQL Server** en **Otros recursos** y seleccione **Propiedades** en el menú contextual. Se abrirá el cuadro de diálogo **Propiedades** del recurso de SQL Server.  
  
4.  Seleccione la pestaña **Propiedades** , escriba el valor deseado para la propiedad **HealthCheckTimeout** y, a continuación, haga clic en **Aceptar** para aplicar el cambio.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 Con la instrucción [ALTER SERVER CONFIGURATION](../../../t-sql/statements/alter-server-configuration-transact-sql.md)[!INCLUDE[tsql](../../../includes/tsql-md.md)] , puede especificar el valor de propiedad HealthCheckTimeOut.  
  
###  <a name="TsqlExample"></a> Ejemplo (Transact-SQL)  
 En el ejemplo siguiente se establece la opción HealthCheckTimeout en 15.000 milisegundos (15 segundos).  
  
```  
ALTER SERVER CONFIGURATION   
SET FAILOVER CLUSTER PROPERTY HealthCheckTimeout = 15000;  
```  
  
## <a name="see-also"></a>Vea también  
 [Directiva de conmutación por error para instancias de clústeres de conmutación por error](../../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md)  
  
  

