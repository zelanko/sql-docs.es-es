---
description: 'Lección 3-1: Copiar el conjunto de implementación'
title: 'Paso 1: Copiar el conjunto de implementación | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: b6ef1e56-d278-4a24-afd3-68d8e0595cbb
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c8f3f026833037c66581ffa95e2e1a736b07091c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88390321"
---
# <a name="lesson-3-1---copying-the-deployment-bundle"></a>Lección 3-1: Copiar el conjunto de implementación

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


En esta tarea, copiará el paquete de implementación en el equipo de destino.  
  
La forma más fácil de copiar el paquete de implementación en el equipo de destino es crear primero un recurso compartido público en dicho equipo, asignar una unidad al recurso compartido público y, a continuación, copiar el paquete de implementación en el recurso compartido. Si no sabe cómo crear y configurar carpetas públicas o asignar unidades, vea la documentación de Windows.  
  
### <a name="to-copy-the-deployment-bundle"></a>Para copiar el paquete de implementación  
  
1.  Busque el paquete de implementación en el equipo.  
  
    Si ha usado la ubicación predeterminada, el paquete de implementación está en la carpeta Bin\Deployment dentro de la carpeta Deployment Tutorial.  
  
2.  Haga clic con el botón derecho en la carpeta Deployment y luego en **Copiar**.  
  
3.  Busque el recurso compartido público en el que desea copiar la carpeta en el equipo de destino y haga clic en **Pegar**.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
[Paso 2: Ejecución del Asistente para la instalación de paquetes](../integration-services/lesson-3-2-running-the-package-installation-wizard.md)  
  
  
  
