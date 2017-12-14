---
title: "Introducción a la escalabilidad horizontal de SSIS en un único equipo | Microsoft Docs"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: scale-out
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: "1"
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8514cd548b003a39bf198b83b6b80d775a55384b
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="get-started-with-integration-services-ssis-scale-out-on-a-single-computer"></a>Introducción a la escalabilidad horizontal de SSIS en un único equipo
En esta sección se proporcionan las instrucciones de configuración de escalabilidad horizontal de Integration Services en un entorno de un solo equipo con la configuración predeterminada.

## <a name="1-install-sql-server-features"></a>1. Instalar las características de SQL Server
En el Asistente para la instalación de SQL Server, seleccione Servicios de Motor de base de datos, Integration Services, patrón de escalabilidad horizontal y trabajo de escalabilidad horizontal en la página **Selección de características**.

![Selección de características en un equipo 1](media/feature-select-onebox1.PNG)

![Selección de características en un equipo 2](media/feature-select-onebox2.PNG)

En la página **Configuración del servidor**, simplemente haga clic en "Siguiente" para usar cuentas de servicio y tipos de inicio predeterminados.

En la página **Configuración del Motor de base de datos**, seleccione "**Modo mixto**" y haga clic en el botón "**Agregar usuario actual**". 

![Configuración del motor](media/engine-config.PNG)

En las páginas **Configuración de escalabilidad horizontal de Integration Services: nodo principal** y **Configuración de escalabilidad horizontal de Integration Services: nodo de trabajo**, simplemente haga clic en "Siguiente" para aplicar la configuración predeterminada del puerto y los certificados.

Finalice el Asistente para la instalación de SQL Server.

## <a name="2-install-sql-server-management-studio"></a>2. Instalar SQL Server Management Studio

[Descargue](../../ssms/download-sql-server-management-studio-ssms.md) SQL Server Management Studio e instálelo.

## <a name="3-enable-scale-out"></a>3. Habilitar la escalabilidad horizontal
Abra SSMS y conéctese a la instancia local de SQL Server.
Haga clic con el botón derecho en **Catálogos de Integration Services** en el Explorador de objetos y seleccione **Crear catálogo**.

En el cuadro de diálogo **Crear catálogo**, la opción **Habilitar este servidor como patrón de escalabilidad horizontal de SSIS** está activada de forma predeterminada. Cree el catálogo como de costumbre. 

## <a name="4-enable-scale-out-worker"></a>4. Habilitar el trabajo de escalabilidad horizontal
En SSMS, haga clic con el botón derecho en **SSISDB** y seleccione **Administrar escalabilidad horizontal...**. ![Administrar escalabilidad horizontal](media/manage-scale-out.PNG)

Se abrirá el Administrador de escalabilidad horizontal de Integration Services. Puede administrar la escalabilidad horizontal con él. Para obtener más información, consulte [Integration Services Scale Out Manager](integration-services-ssis-scale-out-manager.md) (Administrador de escalabilidad horizontal de Integration Services).

Para habilitar el trabajo de escalabilidad horizontal, pase al **Administrador del trabajo** y seleccione el trabajo que quiere habilitar. El trabajo está deshabilitado originalmente. Haga clic en **Habilitar trabajo** para habilitarlo.

## <a name="5-run-packages-in-scale-out"></a>5. Ejecutar paquetes en el escalado horizontal
Ahora, está listo para ejecutar paquetes SSIS en escalabilidad horizontal. Consulte [Run Packages in Integration Services (SSIS) Scale Out](run-packages-in-integration-services-ssis-scale-out.md) (Ejecutar paquetes en Escalabilidad horizontal de Integration Services [SSIS]).


Para agregar más trabajos de escalabilidad horizontal, vea [Agregar un trabajo de escalabilidad horizontal con el administrador de escalabilidad horizontal](add-scale-out-worker.md).
