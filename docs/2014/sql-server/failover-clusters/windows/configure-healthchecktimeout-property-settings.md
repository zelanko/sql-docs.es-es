---
title: Configurar los valores de la propiedad HealthCheckTimeout | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 3bbeb979-e6fc-4184-ad6e-cca62108de74
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4106de497a43404cb44606259d53beb1ed8f5a58
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "72797451"
---
# <a name="configure-healthchecktimeout-property-settings"></a>Configurar los valores de la propiedad HealthCheckTimeout
  El valor HealthCheckTimeout se emplea para especificar el tiempo, en milisegundos, que la DLL de recursos de SQL Server debe esperar la información devuelta por el procedimiento almacenado [sp_server_diagnostics](/sql/relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql) antes de notificar a la instancia de clúster de conmutación por error (FCI) AlwaysOn que no ha recibido respuesta. Los cambios que se realizan en la configuración del tiempo de espera son vigentes de forma inmediata y no requieren reiniciar el recurso de SQL Server.  
  
-   **Antes de empezar:**  [limitaciones y restricciones](#Limits), [seguridad](#Security)  
  
-   **Para configurar el valor HeathCheckTimeout, mediante:**  [PowerShell](#PowerShellProcedure), [Administrador de clústeres de conmutación por error](#WSFC), [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Limits"></a> Limitaciones y restricciones  
 El valor predeterminado para esta propiedad es 60.000 milisegundos (60 segundos). El valor mínimo es 15.000 milisegundos (15 segundos).  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Se necesitan los permisos ALTER SETTINGS y VIEW SERVER STATE.  
  
##  <a name="PowerShellProcedure"></a> Usar PowerShell  
  
### <a name="to-configure-healthchecktimeout-settings"></a>Para configurar los valores de HealthCheckTimeout  
  
1.  Inicie Windows PowerShell con derechos elevados mediante **Ejecutar como administrador**.  
  
2.  Importe el módulo `FailoverClusters` para habilitar los cmdlets de clúster.  
  
3.  Use el `Get-ClusterResource` cmdlet para buscar el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] recurso y, después `Set-ClusterParameter` , use el cmdlet para establecer la propiedad **HealthCheckTimeout** para la instancia de clúster de conmutación por error.  
  
> [!TIP]  
>  Cada vez que abre una nueva ventana de PowerShell, necesita importar el módulo `FailoverClusters`.  

 En el ejemplo siguiente se cambia el valor de HealthCheckTimeout en el recurso de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] "`SQL Server (INST1)`" a 60000 milisegundos.  
  
```powershell  
Import-Module FailoverClusters  
  
$fci = "SQL Server (INST1)"  
Get-ClusterResource $fci | Set-ClusterParameter HealthCheckTimeout 60000  
```  
  
### <a name="related-content-powershell"></a>Contenido relacionado (PowerShell)  
  
-   [Agrupación en clústeres y alta disponibilidad](https://blogs.msdn.com/b/clustering/archive/2009/05/23/9636665.aspx) (blog del equipo de clústeres de conmutación por error y equilibrio de carga de red)  
  
-   [Introducción con Windows PowerShell en un clúster de conmutación por error](https://technet.microsoft.com/library/ee619762\(WS.10\).aspx)  
  
-   [Comandos de recursos de clúster y cmdlets de Windows PowerShell equivalentes](https://msdn.microsoft.com/library/ee619744.aspx#BKMK_resource)  
  
##  <a name="WSFC"></a>Usar el complemento Administrador de clústeres de conmutación por error  
 **Para configurar el valor de HealthCheckTimeout**  
  
1.  Abra el complemento Administrador de clústeres de conmutación por error.  
  
2.  Expanda **Servicios y aplicaciones** y seleccione la FCI.  
  
3.  Haga clic con el botón derecho en el **recurso de SQL Server** en **Otros recursos** y seleccione **Propiedades** en el menú contextual. Se abrirá el cuadro de diálogo **Propiedades** del recurso de SQL Server.  
  
4.  Seleccione la pestaña **Propiedades** , escriba el valor deseado para la propiedad **HealthCheckTimeout** y, a continuación, haga clic en **Aceptar** para aplicar el cambio.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 Con la instrucción [ALTER Server Configuration](/sql/t-sql/statements/alter-server-configuration-transact-sql) [!INCLUDE[tsql](../../../includes/tsql-md.md)] , puede especificar el valor de la propiedad HealthCheckTimeOut.  
  
###  <a name="TsqlExample"></a> Ejemplo (Transact-SQL)  
 En el ejemplo siguiente se establece la opción HealthCheckTimeout en 15.000 milisegundos (15 segundos).  
  
```sql
ALTER SERVER CONFIGURATION   
SET FAILOVER CLUSTER PROPERTY HealthCheckTimeout = 15000;  
```  
  
## <a name="see-also"></a>Consulte también  
 [Directiva de conmutación por error para instancias de clúster de conmutación por error](failover-policy-for-failover-cluster-instances.md)  
