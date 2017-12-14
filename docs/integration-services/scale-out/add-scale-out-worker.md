---
title: Agregar un trabajo de escalabilidad horizontal de SSIS con el administrador de escalabilidad horizontal | Microsoft Docs
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
ms.openlocfilehash: ef11448d03bd188aaea425225312af9f681f530c
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="add-a-scale-out-worker-with-scale-out-manager"></a>Agregar un trabajo de escalabilidad horizontal con el administrador de escalabilidad horizontal

El administrador de escalabilidad horizontal de Integration Services evita en gran medida la complejidad de agregar un trabajo de escalabilidad horizontal al entorno existente de escalabilidad horizontal. 

Los pasos siguientes le permiten agregar un trabajo de escalabilidad horizontal a su topología de escalabilidad horizontal:

## <a name="1-install-scale-out-worker"></a>1. Instalar el trabajo de escalabilidad horizontal
En el Asistente para la instalación de SQL Server, seleccione Integration Services y Trabajo de escalabilidad horizontal en la página **Selección de características**. 
![Selección de características: Worker](media/feature-select-worker.PNG)

En la página **Configuración de escalabilidad horizontal de Integration Services: nodo de trabajo**, puede simplemente hacer clic en "Siguiente" para omitir la configuración aquí y utilizar el **Administrador de escalabilidad horizontal** para efectuar la configuración después de la instalación.

Finalice el asistente para la instalación.

## <a name="2-open-firewall-on-scale-out-master-computer"></a>2. Abrir el firewall en el equipo de patrón de escalabilidad horizontal
Abra el puerto especificado durante la instalación del patrón de escalabilidad horizontal (8391, de manera predeterminada) y el puerto de SQL Server (1433, de manera predeterminada) usando Firewall de Windows en el equipo que ejecuta el patrón de escalabilidad horizontal.

## <a name="3-add-scale-out-worker-with-scale-out-manager"></a>3. Agregar un trabajo de escalabilidad horizontal con el administrador de escalabilidad horizontal
Ejecute SQL Server Management Studio como administrador y conéctese a la instancia de SQL Server del patrón de escalabilidad horizontal.

Haga clic con el botón derecho en **SSISDB** en el Explorador de objetos y seleccione **Administrar escalabilidad horizontal...**. 

![Administrar escalabilidad horizontal](media/manage-scale-out.PNG)

En el **Administrador de escalabilidad horizontal** que aparece, cambie a **Administrador del trabajo**. Haga clic en el botón "+" y siga las instrucciones del cuadro de diálogo Connect Worker (Conectar trabajo). Para obtener más detalles, vea [Scale Out Manager](integration-services-ssis-scale-out-manager.md) (Administrador de escalabilidad horizontal).
