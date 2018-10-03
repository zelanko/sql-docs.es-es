---
title: Configurar los puntos de comprobación para reiniciar un paquete con error | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- checkpoints [Integration Services]
- restarting packages
- starting packages
ms.assetid: 9afffa5a-d803-4653-8afc-386453fc163f
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 9204220c7ea32c59f75785ad0b50fa050a47840f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48123405"
---
# <a name="configure-checkpoints-for-restarting-a-failed-package"></a>Configurar puntos de comprobación para reiniciar un paquete con error
  Los paquetes de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] se configuran para que se reinicien desde un punto de error, en lugar de volver a ejecutar todo el paquete, estableciendo las propiedades que afectan a los puntos de comprobación.  
  
### <a name="to-configure-a-package-to-restart"></a>Para configurar un paquete de modo que se reinicie  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contiene el paquete que desea configurar.  
  
2.  En el **Explorador de soluciones**, haga doble clic en el paquete para abrirlo.  
  
3.  Haga clic en la pestaña **Flujo de control** .  
  
4.  Haga clic con el botón derecho en cualquier parte del fondo de la superficie de diseño de flujo de control y haga clic en **Propiedades**.  
  
5.  Establezca la propiedad SaveCheckpoints en `True`.  
  
6.  Escriba el nombre del archivo de punto de comprobación en la propiedad CheckpointFileName.  
  
7.  Establezca la propiedad CheckpointUsage en uno de estos dos valores:  
  
    -   Seleccione `Always` para reiniciar siempre el paquete desde el punto de comprobación.  
  
        > [!IMPORTANT]  
        >  Si el archivo de punto de comprobación no está disponible se produce un error.  
  
    -   Seleccione `IfExists` para reiniciar el paquete solo si el archivo de punto de comprobación está disponible.  
  
8.  Configure las tareas y contenedores desde los cuales puede reiniciarse el paquete.  
  
    -   Haga clic con el botón derecho en una tarea o contenedor y haga clic en **Propiedades**.  
  
    -   Establezca la propiedad FailPackageOnFailure en `True` para cada tarea y contenedor seleccionados.  
  
## <a name="see-also"></a>Vea también  
 [Reiniciar paquetes mediante el uso de puntos de comprobación](packages/restart-packages-by-using-checkpoints.md)  
  
  
