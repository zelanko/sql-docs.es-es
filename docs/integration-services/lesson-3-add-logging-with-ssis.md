---
description: 'Lección 3: Agregar registro con SSIS'
title: 'Lección 3: Agregar registro con SSIS | Microsoft Docs'
ms.custom: ''
ms.date: 01/04/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 64cd24cc-ba8e-4bd7-b10b-6b80d8b04af6
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 59065cf89a1b3f012e183eb062258bc20bbe6a1a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88422229"
---
# <a name="lesson-3-add-logging-with-ssis"></a>Lección 3: Adición de registro con SSIS

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]



[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] incluye características de registro que permiten supervisar y solucionar los problemas de ejecución de paquetes mediante el seguimiento de eventos de tarea y de contenedor. Las características de registro son flexibles. Puede habilitar el registro en el nivel de paquete, o bien en tareas individuales o contenedores dentro del paquete. Puede seleccionar qué eventos quiere registrar y crear varios registros para un único paquete.  
  
Los proveedores de registro crean los registros. Cada proveedor de registro puede escribir información de registro en distintos formatos y tipos de destino. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] proporciona los siguientes proveedores de registro:  
  
-   Archivo de texto  
  
-   [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]  
  
-   Registro de eventos de Windows  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
  
-   Archivo XML  
  
En esta lección, creará una copia del paquete que ha creado en [Lección 2: Adición de bucles con SSIS](../integration-services/lesson-2-adding-looping-with-ssis.md). Con este nuevo paquete, luego agregará y configurará el registro para supervisar eventos específicos durante la ejecución del paquete. Si no ha completado ninguna de las lecciones anteriores, también puede copiar el paquete de la lección 2 finalizada incluido en el tutorial.  

> [!NOTE]
> Si todavía no lo ha hecho, consulte los [requisitos previos de la lección 1](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md#prerequisites).

## <a name="lesson-tasks"></a>Tareas de la lección  
Esta lección contiene las siguientes tareas:  
  
-   [Paso 1: Copia del paquete de la lección 2](../integration-services/lesson-3-1-copying-the-lesson-2-package.md)  
  
-   [Paso 2: Adición y configuración del registro](../integration-services/lesson-3-2-adding-and-configuring-logging.md)  
  
-   [Paso 3: Prueba del paquete de la lección 3](../integration-services/lesson-3-3-testing-the-lesson-3-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>Iniciar la lección  
[Paso 1: Copia del paquete de la lección 2](../integration-services/lesson-3-1-copying-the-lesson-2-package.md)  
  
