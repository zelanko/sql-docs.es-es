---
title: Quitar un agente de escucha del grupo de disponibilidad (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.availabilitygroup.removeaglistener.default.f1
helpviewer_keywords:
- Availability Groups [SQL Server], listeners
ms.assetid: fd9bba9a-d29f-4c23-8ecd-aaa049ed5f1b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1490e7b5165cb3d977747d1b47b1f364f4975f97
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68014318"
---
# <a name="remove-an-availability-group-listener-sql-server"></a>Quitar un agente de escucha del grupo de disponibilidad (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  En este tema se describe cómo se quita un agente de escucha de un grupo de disponibilidad AlwaysOn usando [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]o PowerShell en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
  
##  <a name="Prerequisites"></a> Requisitos previos  
  
-   Debe estar conectado a la instancia del servidor que hospeda la réplica principal.  
  
##  <a name="Recommendations"></a> Recomendaciones  
 Antes de eliminar un agente de escucha del grupo de disponibilidad, se recomienda asegurarse de que no se está utilizando ninguna aplicación.  
 
  
##  <a name="Permissions"></a> Permisos  
 Se requiere el permiso ALTER AVAILABILITY GROUP en el grupo de disponibilidad, el permiso CONTROL AVAILABILITY GROUP, el permiso ALTER ANY AVAILABILITY GROUP o el permiso CONTROL SERVER.  
  
##  <a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
 **Para quitar un agente de escucha del grupo de disponibilidad**  
  
1.  En el Explorador de objetos, conéctese a la instancia del servidor que hospeda la réplica principal y haga clic en el nombre del servidor para expandir el árbol.  
  
2.  Expanda los nodos **Alta disponibilidad de AlwaysOn** y **Grupos de disponibilidad** .  
  
3.  Expanda el nodo del grupo de disponibilidad y expanda el nodo **Agentes de escucha de grupos de disponibilidad** .  
  
4.  Haga clic con el botón derecho en el agente de escucha que quiere quitar y seleccione el comando **Eliminar** .  
  
5.  Se abrirá el cuadro de diálogo de **Quitar agente de escucha del grupo de disponibilidad** . Para obtener más información, vea [Quitar agente de escucha del grupo de disponibilidad](#AgListenerPropertiesDialog), más adelante en este tema.  
  
###  <a name="AgListenerPropertiesDialog"></a> Quitar agente de escucha del grupo de disponibilidad (cuadro de diálogo)  
 **Nombre**  
 Nombre del agente de escucha que se va a quitar.  
  
 **Resultado**  
 Muestra un vínculo, **Correcto** o **Error**, en el que se puede hacer clic para obtener más información.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 **Para quitar un agente de escucha del grupo de disponibilidad**  
  
1.  Conéctese a la instancia del servidor que hospeda la réplica principal.  
  
2.  Use la instrucción [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md) del siguiente modo:  
  
     ALTER AVAILABILITY GROUP *nombre_de_grupo* REMOVE LISTENER **"** _nombre_de_dns_ **"**  
  
     donde *nombre_grupo* es el nombre del grupo de disponibilidad y *nombre_DNS* es el nombre DNS del agente de escucha de grupo de disponibilidad.  
  
     En el ejemplo siguiente se elimina el agente de escucha del grupo de disponibilidad `AccountsAG` . El nombre DNS es AccountsAG_Listener.  
  
    ```  
    ALTER AVAILABILITY GROUP AccountsAG REMOVE LISTENER 'AccountsAG_Listener';  
    ```  
  
##  <a name="PowerShellProcedure"></a> Usar PowerShell  
 **Para quitar un agente de escucha del grupo de disponibilidad**  
  
1.  Establezca el valor predeterminado (**cd**) en la instancia del servidor que hospeda la réplica principal.  
  
2.  Use el cmdlet integrado **Remove-Item** para quitar un agente de escucha. Por ejemplo, el comando siguiente quita un agente de escucha denominado `MyListener` del grupo de disponibilidad `MyAg`.  
  
    ```  
    Remove-Item `   
    SQLSERVER:\Sql\PrimaryServer\InstanceName\AvailabilityGroups\MyAg\AGListeners\MyListener  
    ```  
  
    > [!NOTE]  
    >  Para ver la sintaxis de un cmdlet, use el cmdlet **Get-Help** en el entorno de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell. Para más información, consulte [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md).  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Crear o configurar un agente de escucha de grupo de disponibilidad &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [Ver las propiedades del agente de escucha de grupo de disponibilidad &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-group-listener-properties-sql-server.md)  
  
## <a name="see-also"></a>Consulte también  
 [Información general de los grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Agentes de escucha de grupo de disponibilidad, conectividad de cliente y conmutación por error de una aplicación &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)  
  
  
