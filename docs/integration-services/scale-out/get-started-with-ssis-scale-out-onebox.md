---
title: "Empezar a trabajar con una escala SSIS en un único equipo | Documentos de Microsoft"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 7175c63be4c0e15e50f2020f75d283ac0e3dfdbf
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="get-started-with-integration-services-ssis-scale-out-on-a-single-computer"></a>Empezar a trabajar con Integration Services (SSIS) horizontalmente en un único equipo
Esta sección proporciona las instrucciones de configuración de horizontalmente Integration Services en un entorno en un equipo con la configuración predeterminada.

## <a name="1-install-sql-server-features"></a>1. Instalar las características de SQL Server
En el Asistente para la instalación de SQL Server, seleccione Servicios de motor de base de datos, Integration Services, escala Out Master y escala Out trabajo en el **selección de características** página.

![Característica seleccione Onebox 1](media/feature-select-onebox1.PNG)

![Característica seleccione Onebox 2](media/feature-select-onebox2.PNG)

En el **configuración del servidor** página, simplemente haga clic en "Siguiente" para usar cuentas de servicio predeterminadas y tipos de inicio.

En el **configuración del motor de base de datos** página, seleccione "**modo mixto**"y haga clic en"**Agregar usuario actual**" botón. 

![Configuración del motor](media/engine-config.PNG)

Una el **escala Out configuración de Integration Services - nodo Master** y **escala Out configuración de Integration Services - nodo de trabajo** páginas, simplemente haga clic en "Siguiente" para aplicar la configuración predeterminada del puerto y certificados.

Finalizar el Asistente para instalación de SQL Server.

## <a name="2-install-sql-server-management-studio"></a>2. Instalar SQL Server Management Studio

[Descargar](../../ssms/download-sql-server-management-studio-ssms.md) SQL Server Management Studio e instalarlo.

## <a name="3-enable-scale-out"></a>3. Habilitar el escalado horizontal
Abra SSMS y conéctese a la instancia local de Sql Server.
Haga clic en **catálogos de Integration Services** en el Explorador de objetos y seleccione **crear catálogo**.

En el **crear catálogo** cuadro de diálogo, **habilita este servidor como SSIS escalada master** está activada de forma predeterminada. Basta con crear el catálogo como de costumbre. 

## <a name="4-enable-scale-out-worker"></a>4. Habilitar el escalado horizontal de trabajo
En SSMS, haga clic en **SSISDB** y seleccione **administrar horizontalmente...** . 
![Administrar el escalado horizontal](media/manage-scale-out.PNG)

Se abrirá la escala fuera Administrador de Integration Services. Puede administrar horizontalmente con él. Para obtener más información, consulte [escala a Administrador de servicios de integración](integration-services-ssis-scale-out-manager.md).

Para habilitar el trabajo de salida de escala, pase a **director trabajador** y seleccione el trabajo que desea habilitar. El trabajador originalmente está deshabilitado. Haga clic en **habilitar trabajo** para habilitarla.

## <a name="5-run-packages-in-scale-out"></a>5. Ejecutar paquetes en el escalado horizontal
Ahora, está listo para ejecutar paquetes SSIS en horizontalmente. Vea [ejecutar paquetes de Integration Services (SSIS) escalar horizontalmente](run-packages-in-integration-services-ssis-scale-out.md).


Para agregar más trabajadores horizontalmente, vea [agregar una escala Out trabajo con escala Out Manager](add-scale-out-worker.md).
