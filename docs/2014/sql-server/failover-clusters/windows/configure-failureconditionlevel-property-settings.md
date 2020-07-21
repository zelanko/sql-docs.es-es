---
title: Configurar los valores de la propiedad FailureConditionLevel | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 513dd179-9a46-46da-9fdd-7632cf6d0816
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8924b864d7cc8be078b370e3182713114f54ff6c
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85062521"
---
# <a name="configure-failureconditionlevel-property-settings"></a>Configurar los valores de la propiedad FailureConditionLevel
  Utilice la propiedad FailureConditionLevel para establecer las condiciones para que la instancia de clúster de conmutación por error AlwaysOn (FCI) conmute por error o se reinicie. Los cambios en esta propiedad se aplican inmediatamente sin tener que reiniciar el servicio de Clúster de conmutación por error de Windows Server (WSFC) o el recurso FCI.  
  
-   **Antes de empezar:**  [Valores de propiedad FailureConditionLevel](#Restrictions), [Seguridad](#Security)  
  
-   **Para configurar la propiedad FailureConditionLevel mediante**  [PowerShell](#PowerShellProcedure), [Administrador de clústeres de conmutación por error](#WSFC), [Transact-SQL](#TsqlProcedure).  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="failureconditionlevel-property-settings"></a><a name="Restrictions"></a> Valores de propiedad FailureConditionLevel  
 Las condiciones de error se establecen en una escala creciente. Para los niveles 1 a 5, cada nivel incluye todas las condiciones de los niveles anteriores además de sus propias condiciones. Esto significa que con cada nivel, hay mayor probabilidad de que se produzca una conmutación por error o un reinicio.  Para obtener más información, vea la sección "Determinar los errores" del tema [Failover Policy for Failover Cluster Instances](failover-policy-for-failover-cluster-instances.md) .  
  
###  <a name="security"></a><a name="Security"></a> Seguridad  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permisos  
 Se necesitan los permisos ALTER SETTINGS y VIEW SERVER STATE.  
  
##  <a name="using-powershell"></a><a name="PowerShellProcedure"></a> Usar PowerShell  
  
### <a name="to-configure-failureconditionlevel-settings"></a>Para configurar los valores de FailureConditionLevel  
  
1.  Inicie Windows PowerShell con derechos elevados mediante **Ejecutar como administrador**.  
  
2.  Importe el módulo `FailoverClusters` para habilitar los cmdlets de clúster.  
  
3.  Use el `Get-ClusterResource` cmdlet para buscar el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] recurso y, después, use el `Set-ClusterParameter` cmdlet para establecer la propiedad **FailureConditionLevel** para una instancia de clúster de conmutación por error.  
  
> [!TIP]  
>  Cada vez que abre una nueva ventana de PowerShell, necesita importar el módulo `FailoverClusters`.  

 En el ejemplo siguiente se cambia el valor de FailureConditionLevel en el recurso " [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] " de`SQL Server (INST1)`para la conmutación por error o el reinicio en caso de que se produzcan errores críticos en el servidor.  
  
```powershell  
Import-Module FailoverClusters  
  
$fci = "SQL Server (INST1)"  
Get-ClusterResource $fci | Set-ClusterParameter FailureConditionLevel 3
```  
  
### <a name="related-content-powershell"></a>Contenido relacionado (PowerShell)  
  
-   [Clustering and High-Availability (Clústeres y alta disponibilidad)](https://techcommunity.microsoft.com/t5/failover-clustering/bg-p/FailoverClustering) (blog del equipo de Agrupacion de clústeres de conmutación por error y equilibrio de carga de red)  
  
-   [Introducción a Windows PowerShell en un clúster de conmutación por error](https://technet.microsoft.com/library/ee619762\(WS.10\).aspx)  
  
-   [Comandos de recursos de clúster y cmdlets equivalentes de Windows PowerShell](https://msdn.microsoft.com/library/ee619744.aspx#BKMK_resource)  
  
##  <a name="using-the-failover-cluster-manager-snap-in"></a><a name="WSFC"></a> Usar el complemento Administrador de clústeres de conmutación por error  

### <a name="to-configure-failureconditionlevel-property-settings"></a>Para configurar los valores de la propiedad FailureConditionLevel
  
1.  Abra el complemento Administrador de clústeres de conmutación por error.  
  
2.  Expanda **Servicios y aplicaciones** y seleccione la FCI.  
  
3.  Haga clic con el botón derecho en el **recurso de SQL Server** en **Otros recursos**y seleccione **Propiedades** en el menú. Se abrirá el cuadro de diálogo **Propiedades** del recurso de SQL Server.  
  
4.  Seleccione la pestaña **Propiedades** , escriba el valor deseado para la propiedad **FaliureConditionLevel** y, a continuación, haga clic en **Aceptar** para aplicar el cambio.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usar Transact-SQL  

### <a name="to-configure-failureconditionlevel-property-settings"></a>Para configurar los valores de la propiedad FailureConditionLevel
  
 Con la instrucción [ALTER Server Configuration](/sql/t-sql/statements/alter-server-configuration-transact-sql) [!INCLUDE[tsql](../../../includes/tsql-md.md)] , puede especificar el valor de la propiedad FailureConditionLevel.  
  
###  <a name="example-transact-sql"></a><a name="TsqlExample"></a> Ejemplo (Transact-SQL)  
 En el ejemplo siguiente se establece la propiedad FailureConditionLevel en 0, lo que indica que no se desencadenará automáticamente una conmutación por error o un reinicio si se produce algún error.  
  
```sql
ALTER SERVER CONFIGURATION SET FAILOVER CLUSTER PROPERTY FailureConditionLevel = 0;  
```  
  
## <a name="see-also"></a>Consulte también  
 [sp_server_diagnostics &#40;&#41;de Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql)   
 [Directiva de conmutación por error para instancias de clúster de conmutación por error](failover-policy-for-failover-cluster-instances.md)  
