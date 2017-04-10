---
title: "Conectar componentes de un flujo de datos | Microsoft Docs"
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
  - "componentes [Integration Services], conexiones"
  - "conexiones [Integration Services], componentes de flujo de datos"
ms.assetid: 70616a58-8921-4218-85bf-f3e90c5a9dbf
caps.latest.revision: 41
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 40
---
# Conectar componentes de un flujo de datos
  Este procedimiento describe cómo conectar la salida de los componentes de un flujo de datos con otros componentes dentro del mismo flujo de datos.  
  
### Para conectar los componentes de un flujo de datos  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  Haga clic en la pestaña **Flujo de control** y luego haga doble clic en la tarea Flujo de datos que contiene el flujo de datos donde quiere conectar componentes.  
  
4.  En la superficie de diseño de la pestaña **Flujo de datos** , seleccione la transformación u origen que desea conectar.  
  
5.  Arrastre la flecha verde de salida de una transformación o un origen a una transformación o a un destino. Algunos componentes de flujo de datos tienen salidas de error que se pueden conectar de la misma manera.  
  
    > [!NOTE]  
    >  Algunos componentes de flujo de datos pueden tener varias salidas y cada una de ellas se puede conectar con una transformación o destino diferente.  
  
6.  Para guardar el paquete actualizado, haga clic en **Guardar los elementos seleccionados** , en el menú **Archivo** .  
  
## Vea también  
 [Agregar o eliminar un componente en un flujo de datos](../../integration-services/data-flow/add-or-delete-a-component-in-a-data-flow.md)   
 [Configurar una salida de error en un componente de flujo de datos](../../integration-services/troubleshooting/configure-an-error-output-in-a-data-flow-component.md)   
 [Flujo de datos](../../integration-services/data-flow/data-flow.md)  
  
  