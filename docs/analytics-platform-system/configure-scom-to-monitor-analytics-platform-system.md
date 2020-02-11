---
title: Supervisión con SCOM
description: Siga estos pasos para configurar los módulos de administración de System Center Operations Manager (SCOM) para Analytics Platform System. Los módulos de administración son necesarios para supervisar Analytics Platform System desde SCOM.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 67029d235a1bc65b5ee0ab6f01f51dea42ebcc8b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401298"
---
# <a name="configure-system-center-operations-manager-scom-to-monitor-analytics-platform-system"></a>Configuración de System Center Operations Manager (SCOM) para supervisar el sistema de análisis de plataforma
Siga estos pasos para configurar los módulos de administración de System Center Operations Manager (SCOM) para Analytics Platform System. Los módulos de administración son necesarios para supervisar Analytics Platform System desde SCOM.  
  
## <a name="BeforeBegin"></a>Antes de empezar  
**Requisitos previos**  
  
System Center Operations Manager 2007 R2 debe estar instalado y en ejecución.  
  
Los módulos de administración deben estar instalados y configurados. Vea [instalar los módulos de administración de scom &#40;Analytics Platform system&#41;](install-the-scom-management-packs.md) e [importar el módulo de administración de scom para PDW &#40;analytics Platform System&#41;](import-the-scom-management-pack-for-pdw.md).  
  
## <a name="ConfigureRunAsProfile"></a>Configurar el perfil de ejecución en System Center  
Para configurar System Center, debe realizar los siguientes pasos:  
  
-   Cree una cuenta de ejecución para el usuario de dominio del **monitor APS** y asígnela a la **cuenta de Microsoft APS Watcher.**  
  
-   Cree una cuenta de ejecución para el usuario **monitoring_user** APS y asígnela a la **cuenta de acción de Microsoft APS**.  
  
Aquí encontrará instrucciones detalladas sobre cómo realizar las tareas:  
  
1.  Cree la cuenta de ejecución del **monitor APS** con el tipo de cuenta de **Windows** para el usuario del dominio del **monitor APS** .  
  
    1.  Vaya al panel **Administración** , haga clic con el botón derecho en**las cuentas** de **configuración** -> de ejecución y seleccione **crear cuenta de ejecución..** .  
  
        ![ConfigureScomCreateRunAsAccount](./media/configure-scom-to-monitor-analytics-platform-system/ConfigureScomCreateRunAsAccount.png "ConfigureScomCreateRunAsAccount")  
  
    2.  Se abrirá el cuadro de diálogo **Asistente para crear cuentas de ejecución** . En la página **Introducción**, haga clic en **Siguiente**.  
  
    3.  En la página **propiedades generales** , seleccione **Windows** en **tipo de cuenta de ejecución** y especifique "APS Watcher" como nombre para **Mostrar**.  
  
        ![CreateRunAsAccountWizardGeneralProperties](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardGeneralProperties.png "CreateRunAsAccountWizardGeneralProperties")  
  
    4.  En la página **credenciales** , ![CreateRunAsAccountWizardCredentials](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardCredentials.png "CreateRunAsAccountWizardCredentials")  
  
    5.  En la página **seguridad de distribución** , seleccione **menos seguro** y haga clic en el botón **crear** para finalizar.  
  
        ![CreateRunAsAccountWizardDistributionSecurity](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardDistributionSecurity.png "CreateRunAsAccountWizardDistributionSecurity")  
  
        1.  Si decide utilizar la opción **más segura** , debe especificar manualmente los equipos en los que se distribuirán las credenciales. Para ello, después de crear la cuenta de ejecución, haga clic con el botón derecho en ella y seleccione **propiedades**.  
  
        2.  Vaya a la pestaña **distribución** y **agregue** los equipos deseados.  
  
            ![RunAsAccountProperties](./media/configure-scom-to-monitor-analytics-platform-system/RunAsAccountProperties.png "RunAsAccountProperties")  
  
2.  Establezca el perfil de **cuenta del observador de Microsoft APS** para usar la cuenta de ejecución del **monitor APS** .  
  
    1.  Vaya a **Administración** -> **Ejecutar como perfiles de configuración** -> ****.  
  
        ![AdministrationRunAsConfigurationProfiles](./media/configure-scom-to-monitor-analytics-platform-system/AdministrationRunAsConfigurationProfiles.png "AdministrationRunAsConfigurationProfiles")  
  
    2.  Haga clic con el botón derecho en **cuenta de Microsoft APS Watcher** en la lista y seleccione **propiedades**.  
  
        ![MicrosoftApsWatcherAccountProperties](./media/configure-scom-to-monitor-analytics-platform-system/MicrosoftApsWatcherAccountProperties.png "MicrosoftApsWatcherAccountProperties")  
  
    3.  Se abrirá el cuadro de diálogo **Asistente para crear perfiles de ejecución** . Para omitir la página de **Introducción** , haga clic en **siguiente**.  
  
    4.  En la página **propiedades generales** , haga clic en **siguiente**.  
  
    5.  En la página **cuentas de ejecución** , haga clic en el botón **Agregar...** y seleccione la cuenta de ejecución del **monitor APS** creada anteriormente.  
  
        ![RunAsProfileWizardAdd](./media/configure-scom-to-monitor-analytics-platform-system/RunAsProfileWizardAdd.png "RunAsProfileWizardAdd")  
  
    6.  Haga clic en **Guardar** para finalizar la asignación de perfil.  
  
3.  Espere hasta que se complete la detección de dispositivos APS.  
  
    1.  Navegue hasta el panel **supervisión** y abra la vista**de estado de** la **aplicación** -> SQL Server**Microsoft Analytics Platform System** -> Appliances.  
  
        ![SqlServerApplianceMicrosoftApsAppliances](./media/configure-scom-to-monitor-analytics-platform-system/SqlServerApplianceMicrosoftApsAppliances.png "SqlServerApplianceMicrosoftApsAppliances")  
  
    2.  Espere hasta que el dispositivo aparezca en la lista. El nombre del dispositivo debe ser igual a uno especificado en el registro. Una vez finalizada la detección, debería ver todos los dispositivos enumerados pero no supervisados. Para habilitar la supervisión, siga los pasos siguientes.  
  
    > [!NOTE]  
    > Los pasos siguientes se pueden completar en paralelo mientras espera a que finalice la detección de la aplicación inicial.  
  
4.  Cree otra nueva cuenta de ejecución para consultar los AP para la recuperación de datos de mantenimiento.  
  
    1.  Empiece a crear una nueva cuenta de ejecución como se describe en el paso 1.  
  
    2.  En la página **propiedades generales** , seleccione tipo de cuenta **autenticación básica** .  
  
        ![CreateRunAsAccountWizardGeneralProperties2](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardGeneralProperties2.png "CreateRunAsAccountWizardGeneralProperties2")  
  
    3.  En la página **credenciales** , proporcione credenciales válidas para acceder a las DMV de estado de mantenimiento de APS.  
  
        ![CreateRunAsAccountWizardCredentials2](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardCredentials2.png "CreateRunAsAccountWizardCredentials2")  
  
5.  Configure el perfil de la **cuenta de acción de Microsoft APS** para usar la cuenta de ejecución recién creada para la instancia de APS.  
  
    1.  Vaya a las propiedades de la **cuenta de acción de Microsoft APS** como se describe en el paso 2.  
  
    2.  En la página **cuentas de ejecución** , haga clic en **Agregar...** y 
    3.  Seleccione la cuenta de ejecución que acaba de crear.  
  
        ![RunAsProfileWizardAdd2](./media/configure-scom-to-monitor-analytics-platform-system/RunAsProfileWizardAdd2.png "RunAsProfileWizardAdd2")  
  
## <a name="next-step"></a>siguiente paso  
Ahora que ha configurado los módulos de administración, está listo para empezar a supervisar el dispositivo. Para obtener más información, consulte [supervisión del dispositivo mediante el uso de System Center Operations Manager &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md).  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
