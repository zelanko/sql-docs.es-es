---
title: "Configurar puntos de comprobaci&#243;n para reiniciar un paquete con error | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "puntos de comprobación [Integration Services]"
  - "reiniciar paquetes"
  - "iniciar paquetes"
ms.assetid: 9afffa5a-d803-4653-8afc-386453fc163f
caps.latest.revision: 25
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 25
---
# Configurar puntos de comprobaci&#243;n para reiniciar un paquete con error
  Los paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] se configuran para que se reinicien desde un punto de error, en lugar de volver a ejecutar todo el paquete, estableciendo las propiedades que afectan a los puntos de comprobación.  
  
### Para configurar un paquete de modo que se reinicie  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contiene el paquete que desea configurar.  
  
2.  En el **Explorador de soluciones**, haga doble clic en el paquete para abrirlo.  
  
3.  Haga clic en la pestaña **Flujo de control** .  
  
4.  Haga clic con el botón derecho en cualquier parte del fondo de la superficie de diseño de flujo de control y haga clic en **Propiedades**.  
  
5.  Establezca la propiedad SaveCheckpoints en **True**.  
  
6.  Escriba el nombre del archivo de punto de comprobación en la propiedad CheckpointFileName.  
  
7.  Establezca la propiedad CheckpointUsage en uno de estos dos valores:  
  
    -   Seleccione **Always** para reiniciar siempre el paquete desde el punto de comprobación.  
  
        > [!IMPORTANT]  
        >  Si el archivo de punto de comprobación no está disponible se produce un error.  
  
    -   Seleccione **IfExists** para reiniciar el paquete solo si está disponible el archivo de punto de comprobación.  
  
8.  Configure las tareas y contenedores desde los cuales puede reiniciarse el paquete.  
  
    -   Haga clic con el botón derecho en una tarea o contenedor y haga clic en **Propiedades**.  
  
    -   Establezca la propiedad FailPackageOnFailure en **True** para cada tarea y contenedor seleccionados.  
  
## Vea también  
 [Reiniciar paquetes de usando puntos de comprobación](../../integration-services/packages/restart-packages-by-using-checkpoints.md)  
  
  