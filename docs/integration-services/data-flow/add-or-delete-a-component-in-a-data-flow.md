---
title: Agregar o eliminar un componente en un flujo de datos | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- adding components
- components [Integration Services], data flow
ms.assetid: d99124f9-0994-4f40-a48e-fdca6a4383e7
caps.latest.revision: 42
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: c3e47e4a5ae297202ba43679fba393421880a7ea
ms.openlocfilehash: 229fd23eb82ff7b6a1139bf1bd00554162cfc038
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="add-or-delete-a-component-in-a-data-flow"></a>Agregar o eliminar un componente en un flujo de datos
  Los componentes de flujo de datos son orígenes, destinos y transformaciones de un flujo de datos. Antes de poder agregar componentes a un flujo de datos, el flujo de control del paquete debe incluir una tarea Flujo de datos.  
  
 Los procedimientos siguientes describen cómo agregar o eliminar un componente en el flujo de datos de un paquete.  
  
### <a name="to-add-a-component-to-a-data-flow"></a>Para agregar un componente a un flujo de datos  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  Haga clic en la pestaña **Flujo de control** y, después, haga doble clic en la tarea Flujo de datos que contiene el flujo de datos al que quiere agregar un componente.  
  
4.  En el cuadro de herramientas, expanda **Orígenes de flujo de datos**, **Transformaciones de flujo de datos**o **Destinos de flujo de datos**, y luego arrastre un elemento de flujo de datos a la superficie de diseño de la pestaña **Flujo de datos** .  
  
5.  Para guardar el paquete actualizado, haga clic en **Guardar los elementos seleccionados** , en el menú **Archivo** .  
  
### <a name="to-delete-a-component-from-a-data-flow"></a>Para eliminar un componente de un flujo de datos  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  Haga clic en la pestaña **Flujo de control** y, después, haga doble clic en la tarea Flujo de datos que contiene el flujo de datos del que quiere eliminar un componente.  
  
4.  Haga clic con el botón derecho en el componente de flujo de datos y, después, haga clic en **Eliminar**.  
  
5.  Confirme la eliminación.  
  
6.  Para guardar el paquete actualizado, haga clic en **Guardar los elementos seleccionados** , en el menú **Archivo** .  
  
## <a name="see-also"></a>Vea también  
 [Conectar los componentes de un flujo de datos](../../integration-services/data-flow/connect-components-in-a-data-flow.md)   
 [Depurar el flujo de datos](../../integration-services/troubleshooting/debugging-data-flow.md)   
 [Flujo de datos](../../integration-services/data-flow/data-flow.md)  
  
  
