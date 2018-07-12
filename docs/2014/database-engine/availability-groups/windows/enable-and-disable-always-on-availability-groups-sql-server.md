---
title: Habilitar y deshabilitar grupos de disponibilidad AlwaysOn (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], server instance
- Availability Groups [SQL Server], deploying
- Availability Groups [SQL Server], disabling
- Availability Groups [SQL Server], enabling
ms.assetid: 7c326958-5ae9-4761-9c57-905972276a8f
caps.latest.revision: 58
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8cfcbdb8e61941a651539bd545b5067a1df5b63a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37185362"
---
# <a name="enable-and-disable-alwayson-availability-groups-sql-server"></a>Habilitar y deshabilitar grupos de disponibilidad de AlwaysOn (SQL Server)
  Habilitar [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] es un requisito previo para que una instancia de servidor use grupos de disponibilidad. Para poder crear y configurar un grupo de disponibilidad, la característica de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] se debe haber habilitado en la cada instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que hospedará una réplica de disponibilidad para uno o varios grupos de disponibilidad.  
  
> [!IMPORTANT]  
>  Si elimina y vuelve a crear un clúster de WSFC, debe deshabilitar y volver a habilitar la característica de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] en cada instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que hospedaba una réplica de disponibilidad en el clúster de WSFC original.  
  
-   **Antes de empezar:**  
  
     [Requisitos previos](#Prerequisites)  
  
     [Seguridad](#Security)  
  
-   **Procedimiento:**  
  
    -   [Determinar que si los grupos de disponibilidad AlwaysOn está habilitado](#IsEnabled)  
  
    -   [Habilitar a los grupos de disponibilidad AlwaysOn](#EnableAOAG)  
  
    -   [Deshabilitar a los grupos de disponibilidad AlwaysOn](#DisableAOAG)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Prerequisites"></a> Requisitos previos para habilitar grupos de disponibilidad AlwaysOn  
  
-   La instancia de servidor debe residir en un nodo de clústeres de conmutación por error de Windows Server (WSFC).  
  
-   La instancia del servidor debe ejecutar una edición de SQL Server que admita [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]. Para obtener más información, vea [Features Supported by the Editions of SQL Server 2014](../../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
-   Habilite los grupos de disponibilidad de AlwaysOn solo en una instancia del servidor cada vez. Después de habilitar los grupos de disponibilidad AlwaysOn, espere hasta que el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ha reiniciado el servicio antes de continuar con otra instancia del servidor.  
  
 Para obtener información acerca de los requisitos previos adicionales para crear y configurar grupos de disponibilidad, consulte [requisitos previos, restricciones y recomendaciones para grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md).  
  
###  <a name="Security"></a> Seguridad  
 Mientras los grupos de disponibilidad AlwaysOn están habilitados en una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], la instancia del servidor tiene control total en el clúster de WSFC.  
  
####  <a name="Permissions"></a> Permissions  
 Requiere la pertenencia al grupo **Administrador** en el equipo local y control total del clúster de WSFC. Cuando habilite AlwaysOn mediante PowerShell, abra la ventana del símbolo del sistema mediante la opción **Ejecutar como administrador** .  
  
 Requiere permisos para crear y administrar objetos de Active Directory.  
  
##  <a name="IsEnabled"></a> Determinar que si los grupos de disponibilidad AlwaysOn está habilitado  
  
-   [SQL Server Management Studio](#SSMS1Procedure)  
  
-   [Transact-SQL](#Tsql1Procedure)  
  
-   [PowerShell](#PowerShell1Procedure)  
  
###  <a name="SSMS1Procedure"></a> Usar SQL Server Management Studio  
 **Para determinar si están habilitados los grupos de disponibilidad AlwaysOn**  
  
1.  En el Explorador de objetos, haga clic con el botón derecho en la instancia del servidor y haga clic en **Propiedades**.  
  
2.  En el cuadro de diálogo **Propiedades del servidor** , haga clic en la página **General** . La propiedad **Habilitado para HADR** muestra uno de los valores siguientes:  
  
    -   **True**si los grupos de disponibilidad de AlwaysOn están habilitados  
  
    -   **False**si los grupos de disponibilidad de AlwaysOn están deshabilitados.  
  
###  <a name="Tsql1Procedure"></a> Usar Transact-SQL  
 **Para determinar si están habilitados los grupos de disponibilidad AlwaysOn**  
  
1.  Use la siguiente instrucción [SERVERPROPERTY](/sql/t-sql/functions/serverproperty-transact-sql) :  
  
    ```  
    SELECT SERVERPROPERTY ('IsHadrEnabled');  
    ```  
  
     El valor de la propiedad del servidor `IsHadrEnabled` indica si una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] está habilitada para los grupos de disponibilidad de AlwaysOn, de la manera siguiente:  
  
    -   Si `IsHadrEnabled` = 1, grupos de disponibilidad AlwaysOn están habilitados.  
  
    -   Si `IsHadrEnabled` = 0, grupos de disponibilidad AlwaysOn están deshabilitados.  
  
    > [!NOTE]  
    >  Para obtener más información sobre la `IsHadrEnabled` propiedad del servidor, consulte [SERVERPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/serverproperty-transact-sql).  
  
###  <a name="PowerShell1Procedure"></a> Usar PowerShell  
 **Para determinar si están habilitados los grupos de disponibilidad AlwaysOn**  
  
1.  Establezca como predeterminada (`cd`) la instancia del servidor en la que desea determinar si [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] está habilitada.  
  
2.  Escriba el siguiente comando `Get-Item` de PowerShell:  
  
    ```  
    PS SQLSERVER:\SQL\NODE1\DEFAULT> get-item . | select IsHadrEnabled  
    ```  
  
    > [!NOTE]  
    >  Para ver la sintaxis de un cmdlet, use el `Get-Help` cmdlet en el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] entorno de PowerShell. Para más información, consulte [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md).  
  
 **Para configurar y usar el proveedor de SQL Server PowerShell**  
  
-   [Proveedor de SQL Server PowerShell Provider](../../../powershell/sql-server-powershell-provider.md)  
  
##  <a name="EnableAOAG"></a> Habilitar los grupos de disponibilidad de AlwaysOn  
 **Para habilitar AlwaysOn, mediante:**  
  
-   [Administrador de configuración de SQL Server](#SQLCM2Procedure)  
  
-   [PowerShell](#PScmd2Procedure)  
  
###  <a name="SQLCM2Procedure"></a> Usar el Administrador de configuración de SQL Server  
 **Para habilitar a grupos de disponibilidad AlwaysOn**  
  
1.  Conéctese al nodo de clústeres de conmutación por error de servidor de Windows (WSFC) que hospeda el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instancia donde desea habilitar los grupos de disponibilidad AlwaysOn.  
  
2.  En el menú **Inicio** , seleccione **Todos los programas**, [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)], **Herramientas de configuración**y haga clic en **Administrador de configuración de SQL Server**.  
  
3.  En **Administrador de configuración de SQL Server**, haga clic en **Services de SQL Server**, haga clic en SQL Server (**<*`instance name`*>)**, donde **< *`instance name`* >** es el nombre de una instancia del servidor local para el que desea habilitar los grupos de disponibilidad AlwaysOn, y Haga clic en **propiedades.**  
  
4.  Seleccione la pestaña **Alta disponibilidad de AlwaysOn** .  
  
5.  Compruebe que el campo **Nombre del clúster de conmutación por error de Windows** contiene el nombre del clúster de conmutación por error local. Si este campo está en blanco, esta instancia del servidor no admite actualmente [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]. Puede ser que el equipo local no sea un nodo de clúster, que se haya cerrado el clúster de WSFC o que esta edición de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] que no admita [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)].  
  
6.  Active la casilla **Habilitar los grupos de disponibilidad de AlwaysOn** y haga clic en **Aceptar**.  
  
     [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] guarda el cambio. A continuación, debe reiniciarse manualmente el servicio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Esto le permite elegir una hora de reinicio que sea la mejor para sus requisitos empresariales. Cuando el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se haya reiniciado el servicio, AlwaysOn se habilitará y la `IsHadrEnabled` propiedad del servidor se establecerá en 1.  
  
###  <a name="PScmd2Procedure"></a> Usar SQL Server PowerShell  
 **Para habilitar AlwaysOn**  
  
1.  Cambie el directorio (`cd`) a una instancia del servidor que desee habilitar para los grupos de disponibilidad de AlwaysOn.  
  
2.  Use el `Enable-SqlAlwaysOn` cmdlet para habilitar grupos de disponibilidad AlwaysOn.  
  
     Para ver la sintaxis de un cmdlet, use el `Get-Help` cmdlet en el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] entorno de PowerShell. Para más información, consulte [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md).  
  
    > [!NOTE]  
    >  Para obtener información sobre cómo controlar si el `Enable-SqlAlwaysOn` cmdlet reinicia la [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de servicio, vea [cuándo reinicia un Cmdlet el servicio SQL Server?](#WhenCmdletRestartsSQL), más adelante en este tema.  
  
 **Para configurar y usar el proveedor de SQL Server PowerShell**  
  
-   [Proveedor de SQL Server PowerShell Provider](../../../powershell/sql-server-powershell-provider.md)  
  
####  <a name="ExmplEnable-SqlHadrServic"></a> Ejemplo: Enable-SqlAlwaysOn  
 El siguiente comando de PowerShell habilita [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] en una instancia de SQL Server (*Computer*\\*Instance*).  
  
```  
Enable-SqlAlwaysOn -Path SQLSERVER:\SQL\Computer\Instance  
```  
  
##  <a name="DisableAOAG"></a> Deshabilitar a los grupos de disponibilidad AlwaysOn  
  
-   **Antes de deshabilitar AlwaysOn:**  
  
     [Recomendaciones](#Recommendations)  
  
-   **Para deshabilitar AlwaysOn, mediante:**  
  
    -   [Administrador de configuración de SQL Server](#SQLCM3Procedure)  
  
    -   [PowerShell](#PScmd3Procedure)  
  
-   **Seguimiento:**  [Después de deshabilitar AlwaysOn](#FollowUp)  
  
> [!IMPORTANT]  
>  Deshabilite AlwaysOn solamente en una instancia del servidor cada vez. Después de deshabilitar los grupos de disponibilidad de AlwaysOn, espere hasta que se haya reiniciado el servicio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] antes de seguir con otra instancia del servidor.  
  
###  <a name="Recommendations"></a> Recomendaciones  
 Antes de deshabilitar AlwaysOn en una instancia de servidor, se recomienda realizar lo siguiente:  
  
1.  Si la instancia de servidor hospeda actualmente la réplica principal de un grupo de disponibilidad que desea conservar, se recomienda realizar una conmutación por error manual del grupo de disponibilidad a una réplica secundaria sincronizada, si es posible. Para obtener más información, vea [Realizar una conmutación por error manual planeada de un grupo de disponibilidad &#40;SQL Server&#41;](perform-a-planned-manual-failover-of-an-availability-group-sql-server.md).  
  
2.  Quite todas las réplicas secundarias locales. Para obtener más información, vea [Quitar una réplica secundaria de un grupo de disponibilidad &#40;SQL Server&#41;](remove-a-secondary-replica-from-an-availability-group-sql-server.md).  
  
###  <a name="SQLCM3Procedure"></a> Usar el Administrador de configuración de SQL Server  
 **Para deshabilitar AlwaysOn**  
  
1.  Conéctese al nodo de clúster de conmutación por error de Windows Server (WSFC) que hospeda la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] donde desea deshabilitar los grupos de disponibilidad de AlwaysOn.  
  
2.  En el menú **Inicio** , seleccione **Todos los programas**, [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)], **Herramientas de configuración**y haga clic en **Administrador de configuración de SQL Server**.  
  
3.  En **Administrador de configuración de SQL Server**, haga clic en **Services de SQL Server**, haga clic en SQL Server (**<*`instance name`*>)**, donde **< *`instance name`* >** es el nombre de una instancia del servidor local para el que desea deshabilitar los grupos de disponibilidad AlwaysOn, y Haga clic en **propiedades**.  
  
4.  En la pestaña**Alta disponibilidad de AlwaysOn**, desactive la casilla **Habilitar los grupos de disponibilidad de AlwaysOn** y haga clic en **Aceptar**.  
  
     [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] guarda los cambios y reinicie el servicio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Cuando se reinicia el servicio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], AlwaysOn estará deshabilitado y la propiedad del servidor `IsHadrEnabled` se establecerá en 0 para indicar que los grupos de disponibilidad de AlwaysOn están deshabilitados.  
  
5.  Se recomienda leer la información de [Seguimiento: Después de deshabilitar AlwaysOn](#FollowUp), más adelante en este tema.  
  
###  <a name="PScmd3Procedure"></a> Usar SQL Server PowerShell  
 **Para deshabilitar AlwaysOn**  
  
1.  Cambie el directorio (`cd`) a una instancia del servidor habilitada actualmente que desee deshabilitar para los grupos de disponibilidad de AlwaysOn.  
  
2.  Use el `Disable-SqlAlwaysOn` cmdlet para habilitar grupos de disponibilidad AlwaysOn.  
  
     Por ejemplo, el siguiente comando deshabilita los grupos de disponibilidad de AlwaysOn en una instancia de SQL Server (*Computer*\\*Instance*).  Este comando requiere reiniciar la instancia y le pedirá que confirme este reinicio.  
  
    ```  
    Disable-SqlAlwaysOn -Path SQLSERVER:\SQL\Computer\Instance  
    ```  
  
    > [!IMPORTANT]  
    >  Para obtener información sobre cómo controlar si el `Disable-SqlAlwaysOn` cmdlet reinicia la [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de servicio, vea [cuándo reinicia un Cmdlet el servicio SQL Server?](#WhenCmdletRestartsSQL), más adelante en este tema.  
  
     Para ver la sintaxis de un cmdlet, use el `Get-Help` cmdlet en el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] entorno de PowerShell. Para más información, consulte [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md).  
  
 **Para configurar y usar el proveedor de SQL Server PowerShell**  
  
-   [Proveedor de SQL Server PowerShell Provider](../../../powershell/sql-server-powershell-provider.md)  
  
###  <a name="FollowUp"></a> Seguimiento: Después de deshabilitar AlwaysOn  
 Después de deshabilitar los grupos de disponibilidad AlwaysOn, la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] debe reiniciarse. El Administrador de configuración de SQL reinicia la instancia de servidor automáticamente. Sin embargo, si utilizó el cmdlet `Disable-SqlAlwaysOn`, deberá reiniciar la instancia de servidor manualmente. Para más información, consulte [sqlservr Application](../../../tools/sqlservr-application.md).  
  
 En la instancia del servidor reiniciada:  
  
-   Las bases de datos de disponibilidad no se inician en el arranque de SQL Server, por lo que están inaccesibles.  
  
-   El único compatible con AlwaysOn [!INCLUDE[tsql](../../../includes/tsql-md.md)] instrucción es [DROP AVAILABILITY GROUP](/sql/t-sql/statements/drop-availability-group-transact-sql). Las opciones CREATE AVAILABILITY GROUP, ALTER AVAILABILITY GROUP y SET HADR de ALTER DATABASE no se admiten.  
  
-   Los metadatos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y los datos de configuración de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] en WSFC no se ven afectados al deshabilitar los grupos de disponibilidad de AlwaysOn.  
  
 Si deshabilita de forma permanente grupos de disponibilidad de AlwaysOn en cada instancia de servidor que hospeda una réplica de disponibilidad para uno o varios grupos de disponibilidad, se recomienda completar los pasos siguientes:  
  
1.  Si no quitó las réplicas de disponibilidad locales antes de deshabilitar AlwaysOn, elimine (quite) cada grupo de disponibilidad para el que la instancia de servidor hospeda una réplica de disponibilidad. Para obtener información sobre cómo eliminar un grupo de disponibilidad, vea [Quitar un grupo de disponibilidad &#40;SQL Server&#41;](remove-an-availability-group-sql-server.md).  
  
2.  Para quitar los metadatos que quedan atrás, elimine (quite) cada grupo de disponibilidad afectado en una instancia de servidor que forme parte del clúster de WSFC original.  
  
3.  Cualquier base de datos principal continúa estando accesible para todas las conexiones, pero se detiene la sincronización de datos entre las bases de datos primaria y secundaria.  
  
4.  Las bases de datos secundarias entran en el estado RESTORING. Puede eliminarlas o restaurarlas mediante RESTORE WITH RECOVERY. Sin embargo, las bases de datos restauradas ya no participarán en la sincronización de datos del grupo de disponibilidad.  
  
##  <a name="WhenCmdletRestartsSQL"></a> ¿Cuándo reinicia un cmdlet el servicio SQL Server?  
 En una instancia del servidor que se esté ejecutando actualmente, el uso de `Enable-SqlAlwaysOn` o `Disable-SqlAlwaysOn` para cambiar el valor actual de AlwaysOn podría provocar que se reinicie el servicio SQL Server. El comportamiento de reinicio depende de las condiciones siguientes:  
  
|Parámetro -NoServiceRestart especificado|Parámetro -Force especificado|¿Se ha reiniciado el servicio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ?|  
|--------------------------------------------|---------------------------------|---------------------------------------------------------|  
|no|no|De forma predeterminada. Pero el cmdlet indica lo siguiente:<br /><br /> **Para completar esta acción, debemos reiniciar el servicio SQL Server para la instancia del servidor '<nombre_instancia>'. ¿Desea continuar?**<br /><br /> **[Y] Sí  [N] No  [S] Suspender  [?] Ayuda (el valor predeterminado es "Y"):**<br /><br /> Si especifica **N** o **S**, el servicio no se reinicia.|  
|no|Sí|El servicio se reinicia.|  
|Sí|no|El servicio no se reinicia.|  
|Sí|Sí|El servicio no se reinicia.|  
  
## <a name="see-also"></a>Vea también  
 [Información general de grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [SERVERPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/serverproperty-transact-sql)  
  
  
