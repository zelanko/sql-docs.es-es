---
title: "Configurar SCOM para supervisar el sistema de la plataforma de análisis"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4dba9b50-1447-45fc-b219-b9fc99d47d8d
caps.latest.revision: "10"
ms.openlocfilehash: f9c8a778afad89abea9ad4fd092fefb15844a5ae
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="configure-scom-to-monitor-analytics-platform-system"></a>Configurar SCOM para supervisar el sistema de la plataforma de análisis
Siga estos pasos para configurar los módulos de administración de System Center Operations Manager (SCOM) para el sistema de la plataforma de análisis. Los módulos de administración necesarias para supervisar el sistema de la plataforma de análisis de SCOM.  
  
## <a name="BeforeBegin"></a>Antes de comenzar  
**Requisitos previos**  
  
System Center Operations Manager 2007 R2 debe estar instalado y ejecutándose.  
  
Los módulos de administración deben estar instalados y configurados. Vea [instalar los módulos de administración de SCOM &#40; Sistema de la plataforma de análisis &#41; ](install-the-scom-management-packs.md) y [importar el módulo de administración de SCOM para PDW &#40; Sistema de la plataforma de análisis &#41; ](import-the-scom-management-pack-for-pdw.md).  
  
## <a name="ConfigureRunAsProfile"></a>Configurar perfil de ejecución en System Center  
Para configurar System Center tendrá que realice los siguientes pasos:  
  
-   Crear cuenta de ejecución para la **APS monitor** usuario de dominio y asígnelo a la **Microsoft APS monitor cuenta.**  
  
-   Crear cuenta de ejecución para la **monitoring_user** usuario APS y asígnelo a la **cuenta de acción de puntos de acceso de Microsoft**.  
  
Estas son instrucciones detalladas sobre cómo hacerlo:  
  
1.  Crear el **APS monitor** cuenta de ejecución con **Windows** cuenta tipo para el **APS monitor** usuario de dominio.  
  
    1.  Navegue hasta la **administración** panel, el botón secundario en **configuración de ejecución** -> **cuentas** y seleccione **crear cuenta de ejecución...**  
  
        ![ConfigureScomCreateRunAsAccount](./media/configure-scom-to-monitor-analytics-platform-system/ConfigureScomCreateRunAsAccount.png "ConfigureScomCreateRunAsAccount")  
  
    2.  El **ejecutar como asistente para crear cuentas** se abrirá el cuadro de diálogo. En el **Introducción** página haga clic en **siguiente**.  
  
    3.  En el **propiedades generales** página, seleccione **Windows** de **tipo de cuenta de ejecución** y especifique "Monitor de APS" como el **nombre para mostrar**.  
  
        ![CreateRunAsAccountWizardGeneralProperties](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardGeneralProperties.png "CreateRunAsAccountWizardGeneralProperties")  
  
    4.  En el **credenciales** página proporcionar credenciales de usuario de dominio de "Monitor de puntos de acceso".  
  
        ![CreateRunAsAccountWizardCredentials](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardCredentials.png "CreateRunAsAccountWizardCredentials")  
  
    5.  En el **distribución seguridad** página, seleccione **menos seguro** y haga clic en el **crear** para terminar.  
  
        ![CreateRunAsAccountWizardDistributionSecurity](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardDistributionSecurity.png "CreateRunAsAccountWizardDistributionSecurity")  
  
        1.  Si opta por utilizar la **más seguro** opción tendrá que especificar manualmente los equipos para que las credenciales que se va a distribuir. Para ello, después de crear la cuenta de ejecución, haga doble clic en él y seleccione **propiedades**.  
  
        2.  Navegue hasta la **distribución** ficha y **agregar** deseado equipos.  
  
            ![RunAsAccountProperties](./media/configure-scom-to-monitor-analytics-platform-system/RunAsAccountProperties.png "RunAsAccountProperties")  
  
2.  Establecer el **Microsoft APS monitor cuenta** para usar **APS monitor** cuenta de ejecución.  
  
    1.  Vaya a **administración** -> **configuración de ejecución** -> **perfiles**.  
  
        ![AdministrationRunAsConfigurationProfiles](./media/configure-scom-to-monitor-analytics-platform-system/AdministrationRunAsConfigurationProfiles.png "AdministrationRunAsConfigurationProfiles")  
  
    2.  Haga clic con el botón secundario en **Microsoft APS monitor cuenta** en la lista y seleccione **propiedades**.  
  
        ![MicrosoftApsWatcherAccountProperties](./media/configure-scom-to-monitor-analytics-platform-system/MicrosoftApsWatcherAccountProperties.png "MicrosoftApsWatcherAccountProperties")  
  
    3.  El **Ejecutar Asistente para perfiles de** se abrirá el cuadro de diálogo. Omitir la **Introducción** página haciendo clic en **siguiente**.  
  
    4.  En el **propiedades generales** página haga clic en **siguiente**.  
  
    5.  En el **cuentas de ejecución** haz clic en el **agregar...** botón y seleccione creado previamente **APS monitor** cuenta de ejecución.  
  
        ![RunAsProfileWizardAdd](./media/configure-scom-to-monitor-analytics-platform-system/RunAsProfileWizardAdd.png "RunAsProfileWizardAdd")  
  
    6.  Haga clic en **guardar** para finalizar la asignación de perfil.  
  
3.  Espere a que termine la detección de dispositivos de APS.  
  
    1.  Navegue hasta la **supervisión** panel y abra el **SQL Server Appliance** -> **Microsoft Analytics Platform System**  ->   **Dispositivos** vista de estado.  
  
        ![SqlServerApplianceMicrosoftApsAppliances](./media/configure-scom-to-monitor-analytics-platform-system/SqlServerApplianceMicrosoftApsAppliances.png "SqlServerApplianceMicrosoftApsAppliances")  
  
    2.  Espere a que el dispositivo aparece en la lista. El nombre del dispositivo debe ser igual a la especificada en el registro.  
  
    Una vez completada la detección debería ver todos los dispositivos enumerados pero no se supervisarán. Para la supervisión de trabajo siga los pasos siguientes.  
  
    > [!NOTE]  
    > Los siguientes pasos pueden realizarse en paralelo mientras se está esperando a que termine la detección de dispositivo inicial.  
  
4.  Cree otra nueva cuenta de ejecución para consultar puntos de acceso para la recuperación de datos de estado.  
  
    1.  Empezar a crear una nueva cuenta de ejecución tal como se describe en el paso 1.  
  
    2.  En el **propiedades generales** página, seleccione **la autenticación básica** tipo de cuenta.  
  
        ![CreateRunAsAccountWizardGeneralProperties2](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardGeneralProperties2.png "CreateRunAsAccountWizardGeneralProperties2")  
  
    3.  En el **credenciales** página alimentación unas credenciales válidas para tener acceso a estado de mantenimiento APS DMV.  
  
        ![CreateRunAsAccountWizardCredentials2](./media/configure-scom-to-monitor-analytics-platform-system/CreateRunAsAccountWizardCredentials2.png "CreateRunAsAccountWizardCredentials2")  
  
5.  Configurar la **cuenta de acción de puntos de acceso de Microsoft** para usar la cuenta de ejecución recién creada para la instancia APS.  
  
    1.  Navegue hasta la **cuenta de acción de puntos de acceso de Microsoft** propiedades tal como se describe en el paso 2.  
  
    2.  En el **cuentas de ejecución** página haga clic en **agregar...** y seleccione la cuenta de ejecución recién creada.  
  
        ![RunAsProfileWizardAdd2](./media/configure-scom-to-monitor-analytics-platform-system/RunAsProfileWizardAdd2.png "RunAsProfileWizardAdd2")  
  
## <a name="next-step"></a>Paso siguiente  
Ahora que ha configurado los módulos de administración, está listo para empezar a supervisar el dispositivo. Para obtener más información, vea [supervisar el dispositivo mediante el uso de System Center Operations Manager &#40; Sistema de la plataforma de análisis &#41; ](monitor-the-appliance-by-using-system-center-operations-manager.md).  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
