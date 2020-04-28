---
title: Habilitar y deshabilitar Grupos de disponibilidad AlwaysOn (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], server instance
- Availability Groups [SQL Server], deploying
- Availability Groups [SQL Server], disabling
- Availability Groups [SQL Server], enabling
ms.assetid: 7c326958-5ae9-4761-9c57-905972276a8f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a441595fa07c86ff1cdbeac4e67e3a6ca0361f80
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "72782978"
---
# <a name="enable-and-disable-alwayson-availability-groups-sql-server"></a>Habilitar y deshabilitar grupos de disponibilidad de AlwaysOn (SQL Server)
  Habilitar [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] es un requisito previo para que una instancia de servidor use grupos de disponibilidad. Para poder crear y configurar un grupo de disponibilidad, la característica de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] se debe haber habilitado en la cada instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que hospedará una réplica de disponibilidad para uno o varios grupos de disponibilidad.  
  
> [!IMPORTANT]  
>  Si elimina y vuelve a crear un clúster de WSFC, debe deshabilitar y volver a habilitar la característica de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] en cada instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que hospedaba una réplica de disponibilidad en el clúster de WSFC original.  
  
-   **Antes de empezar:**  
  
     [Requisitos previos](#Prerequisites)  
  
     [Seguridad](#Security)  
  
-   **Cómo:**  
  
    -   [Determinar si los grupos de disponibilidad de AlwaysOn están habilitados](#IsEnabled)  
  
    -   [Habilitar los grupos de disponibilidad de AlwaysOn](#EnableAOAG)  
  
    -   [Deshabilitar los grupos de disponibilidad de AlwaysOn](#DisableAOAG)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="prerequisites-for-enabling-alwayson-availability-groups"></a><a name="Prerequisites"></a>Requisitos previos para habilitar Grupos de disponibilidad AlwaysOn  
  
-   La instancia de servidor debe residir en un nodo de clústeres de conmutación por error de Windows Server (WSFC).  
  
-   La instancia del servidor debe ejecutar una edición de SQL Server que admita [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]. Para obtener más información, vea [características compatibles con las ediciones de SQL Server 2014](../../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
-   Habilite los grupos de disponibilidad de AlwaysOn solo en una instancia del servidor cada vez. Después de habilitar los grupos de disponibilidad de AlwaysOn, espere hasta que se haya reiniciado el servicio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] antes de seguir con otra instancia del servidor.  
  
 Para obtener información sobre los requisitos previos adicionales para crear y configurar grupos de disponibilidad, vea [requisitos previos, restricciones y recomendaciones para obtener Grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md).  
  
###  <a name="security"></a><a name="Security"></a> Seguridad  
 Mientras los grupos de disponibilidad de AlwaysOn están habilitados en una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], la instancia del servidor tiene control total del clúster de WSFC.  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permisos  
 Requiere la pertenencia al grupo **Administrador** en el equipo local y control total del clúster de WSFC. Cuando habilite AlwaysOn mediante PowerShell, abra la ventana del símbolo del sistema mediante la opción **Ejecutar como administrador** .  
  
 Requiere permisos para crear y administrar objetos de Active Directory.  
  
##  <a name="determine-whether-alwayson-availability-groups-is-enabled"></a><a name="IsEnabled"></a>Determinar si Grupos de disponibilidad AlwaysOn está habilitado  
  
-   [SQL Server Management Studio](#SSMS1Procedure)  
  
-   [Transact-SQL](#Tsql1Procedure)  
  
-   [PowerShell](#PowerShell1Procedure)  
  
###  <a name="using-sql-server-management-studio"></a><a name="SSMS1Procedure"></a> Uso de SQL Server Management Studio  
 **Para determinar si los grupos de disponibilidad de AlwaysOn están habilitados**  
  
1.  En el Explorador de objetos, haga clic con el botón derecho en la instancia del servidor y haga clic en **Propiedades**.  
  
2.  En el cuadro de diálogo **Propiedades del servidor** , haga clic en la página **General** . La propiedad **Habilitado para HADR** muestra uno de los valores siguientes:  
  
    -   **True**si los grupos de disponibilidad de AlwaysOn están habilitados  
  
    -   **False**si los grupos de disponibilidad de AlwaysOn están deshabilitados.  
  
###  <a name="using-transact-sql"></a><a name="Tsql1Procedure"></a> Usar Transact-SQL  
 **Para determinar si los grupos de disponibilidad de AlwaysOn están habilitados**  
  
1.  Use la siguiente instrucción [SERVERPROPERTY](/sql/t-sql/functions/serverproperty-transact-sql) :  
  
    ```sql
    SELECT SERVERPROPERTY ('IsHadrEnabled');  
    ```  
  
     El valor de la propiedad del servidor `IsHadrEnabled` indica si una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] está habilitada para los grupos de disponibilidad de AlwaysOn, de la manera siguiente:  
  
    -   Si `IsHadrEnabled` = 1, los grupos de disponibilidad de AlwaysOn están habilitados.  
  
    -   Si `IsHadrEnabled` = 0, los grupos de disponibilidad de AlwaysOn están deshabilitados.  
  
    > [!NOTE]  
    >  Para obtener más información acerca `IsHadrEnabled` de la propiedad de servidor, vea [SERVERPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/serverproperty-transact-sql).  
  
###  <a name="using-powershell"></a><a name="PowerShell1Procedure"></a> Usar PowerShell  
 **Para determinar si los grupos de disponibilidad de AlwaysOn están habilitados**  
  
1.  Establezca el valor`cd`predeterminado () en la instancia del servidor `\SQL\NODE1\DEFAULT`(por ejemplo,) en la que [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] desea determinar si está habilitado.  
  
2.  Escriba el siguiente comando `Get-Item` de PowerShell:  
  
    ```powershell
    Get-Item . | Select IsHadrEnabled  
    ```  
  
    > [!NOTE]  
    >  Para ver la sintaxis de un cmdlet, use el cmdlet `Get-Help` en el entorno de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell. Para más información, consulte [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md).  
  
 **Para configurar y usar el proveedor de SQL Server PowerShell**  
  
-   [Proveedor de SQL Server PowerShell Provider](../../../powershell/sql-server-powershell-provider.md)  
  
##  <a name="enable-alwayson-availability-groups"></a><a name="EnableAOAG"></a>Habilitar Grupos de disponibilidad AlwaysOn  
 **Para habilitar AlwaysOn, mediante:**  
  
-   [Administrador de configuración de SQL Server](#SQLCM2Procedure)  
  
-   [PowerShell](#PScmd2Procedure)  
  
###  <a name="using-sql-server-configuration-manager"></a><a name="SQLCM2Procedure"></a> Usar el Administrador de configuración de SQL Server  
 **Para habilitar los grupos de disponibilidad de AlwaysOn**  
  
1.  Conéctese al nodo de clúster de conmutación por error de Windows Server (WSFC) que hospeda la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] donde desea habilitar los grupos de disponibilidad de AlwaysOn.  
  
2.  En el menú **Inicio** , seleccione **Todos los programas**, [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)], **Herramientas de configuración**y haga clic en **Administrador de configuración de SQL Server**.  
  
3.  En **Administrador de configuración de SQL Server**, haga clic en **servicios de SQL Server**, haga clic con el botón secundario en SQL Server (** < *`instance name`*>)**, donde ** < *`instance name`* ** es el nombre de una instancia del servidor local para la que desea habilitar grupos de disponibilidad AlwaysOn y, a continuación, haga clic en **propiedades.**  
  
4.  Seleccione la pestaña **alta disponibilidad de AlwaysOn** .  
  
5.  Compruebe que el campo **Nombre del clúster de conmutación por error de Windows** contiene el nombre del clúster de conmutación por error local. Si este campo está en blanco, esta instancia del servidor no admite actualmente [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]. Puede ser que el equipo local no sea un nodo de clúster, que se haya cerrado el clúster de WSFC o que esta edición de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] que no admita [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)].  
  
6.  Active la casilla **habilitar grupos de disponibilidad AlwaysOn** y haga clic en **Aceptar**.  
  
     [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] guarda el cambio. A continuación, debe reiniciarse manualmente el servicio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Esto le permite elegir una hora de reinicio que sea la mejor para sus requisitos empresariales. Al reiniciar el servicio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], AlwaysOn estará habilitado y la propiedad del servidor `IsHadrEnabled` se establecerá en 1.  
  
###  <a name="using-sql-server-powershell"></a><a name="PScmd2Procedure"></a> Usar SQL Server PowerShell  
 **Para habilitar AlwaysOn**  
  
1.  Cambie el directorio (`cd`) a una instancia del servidor que desee habilitar para los grupos de disponibilidad de AlwaysOn.  
  
2.  Use el cmdlet `Enable-SqlAlwaysOn` para habilitar los grupos de disponibilidad de AlwaysOn.  
  
     Para ver la sintaxis de un cmdlet, use el cmdlet `Get-Help` en el entorno de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell. Para más información, consulte [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md).  
  
    > [!NOTE]  
    >  Para obtener información sobre cómo controlar si el `Enable-SqlAlwaysOn` cmdlet reinicia el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] servicio, vea ¿ [Cuándo reinicia un cmdlet el servicio SQL Server?](#WhenCmdletRestartsSQL)más adelante en este tema.  
  
 **Para configurar y usar el proveedor de SQL Server PowerShell**  
  
-   [Proveedor de SQL Server PowerShell Provider](../../../powershell/sql-server-powershell-provider.md)  
  
####  <a name="example-enable-sqlalwayson"></a><a name="ExmplEnable-SqlHadrServic"></a>Ejemplo: enable-SqlAlwaysOn  
 El siguiente comando de PowerShell [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] habilita en una instancia de SQL Server (*instancia*de*equipo*\\).  
  
```powershell
Enable-SqlAlwaysOn -Path SQLSERVER:\SQL\Computer\Instance  
```  
  
##  <a name="disable-alwayson-availability-groups"></a><a name="DisableAOAG"></a>Deshabilitar Grupos de disponibilidad AlwaysOn  
  
-   **Antes de deshabilitar AlwaysOn:**  
  
     [Recomendaciones](#Recommendations)  
  
-   **Para deshabilitar AlwaysOn, mediante:**  
  
    -   [Administrador de configuración de SQL Server](#SQLCM3Procedure)  
  
    -   [PowerShell](#PScmd3Procedure)  
  
-   **Seguimiento:**  [Después de deshabilitar AlwaysOn](#FollowUp)  
  
> [!IMPORTANT]  
>  Deshabilite AlwaysOn solamente en una instancia del servidor cada vez. Después de deshabilitar los grupos de disponibilidad de AlwaysOn, espere hasta que se haya reiniciado el servicio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] antes de seguir con otra instancia del servidor.  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> Recomendaciones  
 Antes de deshabilitar AlwaysOn en una instancia de servidor, se recomienda realizar lo siguiente:  
  
1.  Si la instancia de servidor hospeda actualmente la réplica principal de un grupo de disponibilidad que desea conservar, se recomienda realizar una conmutación por error manual del grupo de disponibilidad a una réplica secundaria sincronizada, si es posible. Para obtener más información, vea [Realizar una conmutación por error manual planeada de un grupo de disponibilidad &#40;SQL Server&#41;](perform-a-planned-manual-failover-of-an-availability-group-sql-server.md).  
  
2.  Quite todas las réplicas secundarias locales. Para obtener más información, vea [Quitar una réplica secundaria de un grupo de disponibilidad &#40;SQL Server&#41;](remove-a-secondary-replica-from-an-availability-group-sql-server.md).  
  
###  <a name="using-sql-server-configuration-manager"></a><a name="SQLCM3Procedure"></a> Usar el Administrador de configuración de SQL Server  
 **Para deshabilitar AlwaysOn**  
  
1.  Conéctese al nodo de clúster de conmutación por error de Windows Server (WSFC) que hospeda la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] donde desea deshabilitar los grupos de disponibilidad de AlwaysOn.  
  
2.  En el menú **Inicio** , seleccione **todos los programas**, seleccione [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)], **herramientas de configuración**y haga clic en **Administrador de configuración de SQL Server**.  
  
3.  En **Administrador de configuración de SQL Server**, haga clic en **servicios de SQL Server**, haga clic con el botón secundario en SQL Server (** < *`instance name`*>)**, donde ** < *`instance name`* ** es el nombre de una instancia del servidor local para la que desea deshabilitar grupos de disponibilidad AlwaysOn y, a continuación, haga clic en **propiedades**.  
  
4.  En la pestaña**Alta disponibilidad de AlwaysOn**, desactive la casilla **Habilitar los grupos de disponibilidad de AlwaysOn** y haga clic en **Aceptar**.  
  
     [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] guarda los cambios y reinicie el servicio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Cuando se reinicia el servicio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], AlwaysOn estará deshabilitado y la propiedad del servidor `IsHadrEnabled` se establecerá en 0 para indicar que los grupos de disponibilidad de AlwaysOn están deshabilitados.  
  
5.  Se recomienda leer la información de [Seguimiento: Después de deshabilitar AlwaysOn](#FollowUp), más adelante en este tema.  
  
###  <a name="using-sql-server-powershell"></a><a name="PScmd3Procedure"></a> Usar SQL Server PowerShell  
 **Para deshabilitar AlwaysOn**  
  
1.  Cambie el directorio`cd`() a una instancia de servidor habilitada actualmente que desee deshabilitar para grupos de disponibilidad AlwaysOn.  
  
2.  Use el cmdlet `Disable-SqlAlwaysOn` para habilitar los grupos de disponibilidad de AlwaysOn.  
  
     Por ejemplo, el comando siguiente deshabilita grupos de disponibilidad AlwaysOn en una instancia de SQL Server (*Computer*\\*instancia*de equipo).  Este comando requiere reiniciar la instancia y le pedirá que confirme este reinicio.  
  
    ```powershell
    Disable-SqlAlwaysOn -Path SQLSERVER:\SQL\Computer\Instance  
    ```  
  
    > [!IMPORTANT]  
    >  Para obtener información sobre cómo controlar si el `Disable-SqlAlwaysOn` cmdlet reinicia el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] servicio, vea ¿ [Cuándo reinicia un cmdlet el servicio SQL Server?](#WhenCmdletRestartsSQL)más adelante en este tema.  
  
     Para ver la sintaxis de un cmdlet, use el cmdlet `Get-Help` en el entorno de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell. Para más información, consulte [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md).  
  
 **Para configurar y usar el proveedor de SQL Server PowerShell**  
  
-   [Proveedor de SQL Server PowerShell Provider](../../../powershell/sql-server-powershell-provider.md)  
  
###  <a name="follow-up-after-disabling-alwayson"></a><a name="FollowUp"></a>Seguimiento: después de deshabilitar AlwaysOn  
 Después de deshabilitar grupos de disponibilidad de AlwaysOn, se debe reiniciar la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . El Administrador de configuración de SQL reinicia la instancia de servidor automáticamente. Sin embargo, si utilizó el cmdlet `Disable-SqlAlwaysOn`, deberá reiniciar la instancia de servidor manualmente. Para más información, consulte [sqlservr Application](../../../tools/sqlservr-application.md).  
  
 En la instancia del servidor reiniciada:  
  
-   Las bases de datos de disponibilidad no se inician en el arranque de SQL Server, por lo que están inaccesibles.  
  
-   La única instrucción [!INCLUDE[tsql](../../../includes/tsql-md.md)] compatible con AlwaysOn es [DROP AVAILABILITY GROUP](/sql/t-sql/statements/drop-availability-group-transact-sql). Las opciones CREATE AVAILABILITY GROUP, ALTER AVAILABILITY GROUP y SET HADR de ALTER DATABASE no se admiten.  
  
-   Los metadatos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y los datos de configuración de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] en WSFC no se ven afectados al deshabilitar los grupos de disponibilidad de AlwaysOn.  
  
 Si deshabilita de forma permanente grupos de disponibilidad de AlwaysOn en cada instancia de servidor que hospeda una réplica de disponibilidad para uno o varios grupos de disponibilidad, se recomienda completar los pasos siguientes:  
  
1.  Si no quitó las réplicas de disponibilidad locales antes de deshabilitar AlwaysOn, elimine (quite) cada grupo de disponibilidad para el que la instancia de servidor hospeda una réplica de disponibilidad. Para obtener información sobre cómo eliminar un grupo de disponibilidad, vea [Quitar un grupo de disponibilidad &#40;SQL Server&#41;](remove-an-availability-group-sql-server.md).  
  
2.  Para quitar los metadatos que quedan atrás, elimine (quite) cada grupo de disponibilidad afectado en una instancia de servidor que forme parte del clúster de WSFC original.  
  
3.  Cualquier base de datos principal continúa estando accesible para todas las conexiones, pero se detiene la sincronización de datos entre las bases de datos primaria y secundaria.  
  
4.  Las bases de datos secundarias entran en el estado RESTORING. Puede eliminarlas o restaurarlas mediante RESTORE WITH RECOVERY. Sin embargo, las bases de datos restauradas ya no participarán en la sincronización de datos del grupo de disponibilidad.  
  
##  <a name="when-does-a-cmdlet-restart-the-sql-server-service"></a><a name="WhenCmdletRestartsSQL"></a>¿Cuándo reinicia un cmdlet el servicio SQL Server?  
 En una instancia del servidor que se esté ejecutando actualmente, el uso de `Enable-SqlAlwaysOn` o `Disable-SqlAlwaysOn` para cambiar el valor actual de AlwaysOn podría provocar que se reinicie el servicio SQL Server. El comportamiento de reinicio depende de las condiciones siguientes:  
  
|Parámetro -NoServiceRestart especificado|Parámetro -Force especificado|¿Se ha reiniciado el servicio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ?|  
|--------------------------------------------|---------------------------------|---------------------------------------------------------|  
|No|No|De forma predeterminada. Pero el cmdlet indica lo siguiente:<br /><br /> **Para completar esta acción, debemos reiniciar el servicio de SQL Server para la instancia de servidor ' <instance_name> '. ¿Desea continuar?**<br /><br /> **[Y] Sí  [N] No  [S] Suspender  [?] Ayuda (el valor predeterminado es "Y"):**<br /><br /> Si especifica **N** o **S**, el servicio no se reinicia.|  
|No|Sí|El servicio se reinicia.|  
|Sí|No|El servicio no se reinicia.|  
|Sí|Sí|El servicio no se reinicia.|  
  
## <a name="see-also"></a>Consulte también  
 [Información general de Grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [SERVERPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/serverproperty-transact-sql)  
