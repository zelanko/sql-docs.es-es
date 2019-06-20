---
title: Configuración de SCOM para supervisar Analytics Platform System | Microsoft Docs
description: Siga estos pasos para configurar los módulos de administración de System Center Operations Manager (SCOM) para Analytics Platform System. Los módulos de administración necesarias para supervisar Analytics Platform System desde SCOM.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 2dae92263d7be76490a51ea7027f79ab5fcd6118
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62509800"
---
# <a name="configure-system-center-operations-manager-scom-to-monitor-analytics-platform-system"></a>Configurar System Center Operations Manager (SCOM) para supervisar Analytics Platform System
Siga estos pasos para configurar los módulos de administración de System Center Operations Manager (SCOM) para Analytics Platform System. Los módulos de administración necesarias para supervisar Analytics Platform System desde SCOM.  
  
## <a name="BeforeBegin"></a>Antes de empezar  
**Requisitos previos**  
  
System Center Operations Manager 2007 R2 debe estar instalado y ejecutándose.  
  
Los módulos de administración deben estar instalados y configurados. Consulte [instalar los módulos de administración de SCOM &#40;Analytics Platform System&#41; ](install-the-scom-management-packs.md) y [importar el módulo de administración de SCOM para PDW &#40;Analytics Platform System&#41;](import-the-scom-management-pack-for-pdw.md).  
  
## <a name="ConfigureRunAsProfile"></a>Configurar perfil de ejecución en System Center  
Para configurar System Center, tendrá que siga estos pasos:  
  
-   Crear cuenta de ejecución para el **APS Watcher** usuario de dominio y asignarlo a la **cuenta de Monitor de puntos de acceso de Microsoft.**  
  
-   Crear cuenta de ejecución para el **monitoring_user** usuario APS y asígnelo a la **cuenta de acción de APS Microsoft**.  
  
Estas son las instrucciones detalladas sobre cómo realizar las tareas:  
  
1.  Crear el **APS Watcher** cuenta de ejecución con **Windows** tipo para la cuenta el **APS Watcher** usuario de dominio.  
  
    1.  Navegue hasta la **administración** panel, el botón secundario en **configuración de ejecución** -> **cuentas** y seleccione **crear cuenta de ejecución...**  
  
        ![ConfigureScomCreateRunAsAccount](./media/configure-scom-to-monitor-analytics-platform-system/ConfigureScomCreateRunAsAccount.png "ConfigureScomCreateRunAsAccount")  
  
    2.  El **ejecutar como asistente para crear cuentas** se abrirá el cuadro de diálogo. En el **Introducción** página, haga clic en **siguiente**.  
  
    3.  En el **propiedades generales** página, seleccione **Windows** desde **el tipo de cuenta de ejecución** y especifique "Monitor de puntos de acceso" como el **nombre para mostrar**.  
  
        ![CreateRunAsAccountWizardGeneralProperties](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardGeneralProperties.png "CreateRunAsAccountWizardGeneralProperties")  
  
    4.  En el **credenciales** página, ![CreateRunAsAccountWizardCredentials](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardCredentials.png "CreateRunAsAccountWizardCredentials")  
  
    5.  En el **distribución seguridad** página, seleccione **menos seguro** y haga clic en el **crear** para terminar.  
  
        ![CreateRunAsAccountWizardDistributionSecurity](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardDistributionSecurity.png "CreateRunAsAccountWizardDistributionSecurity")  
  
        1.  Si decide usar el **más seguro** opción, tendrá que especificar manualmente los equipos a la que se distribuirán las credenciales. Para ello, después de crear la cuenta de ejecución, haga doble clic en él y seleccione **propiedades**.  
  
        2.  Navegue hasta la **distribución** pestaña y **agregar** deseado de los equipos.  
  
            ![RunAsAccountProperties](./media/configure-scom-to-monitor-analytics-platform-system/RunAsAccountProperties.png "RunAsAccountProperties")  
  
2.  Establecer el **Microsoft APS monitor cuenta** perfil para usar **APS Watcher** cuenta de ejecución.  
  
    1.  Vaya a **administración** -> **configuración de ejecución** -> **perfiles**.  
  
        ![AdministrationRunAsConfigurationProfiles](./media/configure-scom-to-monitor-analytics-platform-system/AdministrationRunAsConfigurationProfiles.png "AdministrationRunAsConfigurationProfiles")  
  
    2.  Haga clic con el botón derecho en **Microsoft APS monitor cuenta** en la lista y seleccione **propiedades**.  
  
        ![MicrosoftApsWatcherAccountProperties](./media/configure-scom-to-monitor-analytics-platform-system/MicrosoftApsWatcherAccountProperties.png "MicrosoftApsWatcherAccountProperties")  
  
    3.  El **Ejecutar Asistente para perfiles** se abrirá el cuadro de diálogo. Omitir la **Introducción** página haciendo clic en **siguiente**.  
  
    4.  En el **propiedades generales** página, haga clic en **siguiente**.  
  
    5.  En el **cuentas de ejecución** página, haga clic en el **agregar...**  botón y seleccione creado previamente **APS Watcher** cuenta de ejecución.  
  
        ![RunAsProfileWizardAdd](./media/configure-scom-to-monitor-analytics-platform-system/RunAsProfileWizardAdd.png "RunAsProfileWizardAdd")  
  
    6.  Haga clic en **guardar** para finalizar la asignación de perfiles.  
  
3.  Espere hasta que se completa la detección de dispositivos de APS.  
  
    1.  Navegue hasta la **supervisión** panel y abra el **SQL Server Appliance** -> **Microsoft Analytics Platform System**  ->   **Dispositivos** vista de estado.  
  
        ![SqlServerApplianceMicrosoftApsAppliances](./media/configure-scom-to-monitor-analytics-platform-system/SqlServerApplianceMicrosoftApsAppliances.png "SqlServerApplianceMicrosoftApsAppliances")  
  
    2.  Espere hasta que el dispositivo aparece en la lista. El nombre del dispositivo debe ser igual a uno especificados en el registro. Una vez finalizada la detección debería ver todos los dispositivos enumerados pero no supervisado. Para habilitar la supervisión, siga los pasos siguientes.  
  
    > [!NOTE]  
    > Los siguientes pasos pueden realizarse en paralelo mientras se está esperando la detección inicial del dispositivo Finalizar.  
  
4.  Cree otra nueva cuenta de ejecución para consultar puntos de acceso para la recuperación de datos de estado.  
  
    1.  Empezar a crear una nueva cuenta de ejecución tal como se describe en el paso 1.  
  
    2.  En el **propiedades generales** página, seleccione **autenticación básica** tipo de cuenta.  
  
        ![CreateRunAsAccountWizardGeneralProperties2](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardGeneralProperties2.png "CreateRunAsAccountWizardGeneralProperties2")  
  
    3.  En el **credenciales** página, proporcione credenciales válidas para tener acceso a estado de mantenimiento APS DMV.  
  
        ![CreateRunAsAccountWizardCredentials2](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardCredentials2.png "CreateRunAsAccountWizardCredentials2")  
  
5.  Configurar la **cuenta de acción de APS Microsoft** perfil para usar la cuenta de ejecución recién creada para la instancia APS.  
  
    1.  Navegue hasta la **cuenta de acción de APS Microsoft** propiedades tal como se describe en el paso 2.  
  
    2.  En el **cuentas de ejecución** página, haga clic en **agregar...**  y 
    3.  Seleccione la cuenta de ejecución recién creada.  
  
        ![RunAsProfileWizardAdd2](./media/configure-scom-to-monitor-analytics-platform-system/RunAsProfileWizardAdd2.png "RunAsProfileWizardAdd2")  
  
## <a name="next-step"></a>Paso siguiente  
Ahora que ha configurado los módulos de administración, está listo para empezar a supervisar el dispositivo. Para obtener más información, consulte [supervisar el dispositivo mediante el uso de System Center Operations Manager &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md).  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
