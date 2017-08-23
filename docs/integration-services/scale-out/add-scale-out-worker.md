---
title: Agregar un SSIS escalada trabajo con escalado horizontal Manager | Documentos de Microsoft
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
ms.openlocfilehash: b769236330941a107865a0b133961bce5bf6b85b
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="add-a-scale-out-worker-with-scale-out-manager"></a>Agregar un trabajo de ampliación con escalado horizontal Manager

Escala a Administrador de servicios de integración evita en gran medida la complejidad para agregar escala Out trabajo a su entorno existente horizontalmente. 

Los pasos siguientes le permiten agregar un trabajador escala fuera de su topología de ampliación en horizontal:

## <a name="1-install-scale-out-worker"></a>1. Instalar el escalado horizontal de trabajo
En el Asistente para la instalación de SQL Server, seleccione Integration Services y escala Out trabajo en el **selección de características** página. 
![Selección de características: Worker](media/feature-select-worker.PNG)

En el **escala Out configuración de Integration Services - nodo de trabajo** página, puede hacer simplemente clic en "Siguiente" para omitir la configuración aquí y utilizar **escala Out Manager** para efectuar la configuración después de la instalación.

Finalizar al Asistente para la instalación.

## <a name="2-open-firewall-on-scale-out-master-computer"></a>2. Abra firewall en el equipo de escala Out Master
Abrir el puerto especificado durante la instalación de escala Out Master (8391, de forma predeterminada) y el puerto de SQL Server (1433, de forma predeterminada), con Firewall de Windows en el equipo de escala Out Master.

## <a name="3-add-scale-out-worker-with-scale-out-manager"></a>3. Agregar escalada trabajo con escalado horizontal Manager
Ejecute SQL Server Management Studio como administrador y conéctese a la instancia de SQL Server de escala Out Master.

Haga clic en **SSISDB** en el Explorador de objetos y seleccione **administrar horizontalmente...** . 

![Administrar el escalado horizontal](media/manage-scale-out.PNG)

En el texto extraído seguridad **escala Out Manager**, cambie a **trabajo Manager**. Haga clic en "+" botón y siga las instrucciones del cuadro de diálogo de trabajo conectarse. Para obtener más información, consulte [escala Out Manager](integration-services-ssis-scale-out-manager.md).

