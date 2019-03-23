---
title: Usar una expresión en una restricción de precedencia | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- precedence constraints [Integration Services], adding expressions
- expressions [Integration Services], adding
ms.assetid: 601038bb-3b17-42ac-b09d-5b3a82fb6564
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0b2491a03e0d0121f3aa3b31f354f71b36088e5d
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2019
ms.locfileid: "58375382"
---
# <a name="use-an-expression-in-a-precedence-constraint"></a>Usar una expresión en una restricción de precedencia
  Este procedimiento describe cómo agregar una expresión a una restricción de precedencia mediante el cuadro de diálogo **Editor de restricciones de precedencia** . Antes de poder agregar una expresión a una restricción de precedencia, el paquete debe incluir por lo menos dos ejecutables, ya sean tareas o contenedores, y deben estar conectados por una restricción de precedencia.  
  
### <a name="to-add-an-expression-to-a-precedence-constraint"></a>Para agregar una expresión a una restricción de precedencia  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  Haga clic en la pestaña **Flujo de control** .  
  
4.  En la superficie de diseño de la pestaña **Flujo de control** , haga doble clic en la restricción de precedencia. Se abre el **Editor de restricciones de precedencia** .  
  
5.  Seleccione **Expresión**, **Expresión y restricción**, o **Expresión o restricción** en la lista **Operación de evaluación** .  
  
6.  Escriba una expresión o haga clic en el cuadro **Expresión** o inicie el Generador de expresiones para crear una expresión.  
  
7.  Para validar la sintaxis de expresión, haga clic en **Probar**.  
  
8.  Para guardar el paquete actualizado, haga clic en **Guardar los elementos seleccionados**, en el menú **Archivo**.  
  
## <a name="see-also"></a>Vea también  
 [Restricciones de precedencia](control-flow/precedence-constraints.md)   
 [Conectar tareas y contenedores mediante una restricción de precedencia predeterminada](../../2014/integration-services/connect-tasks-and-containers-by-using-a-default-precedence-constraint.md)   
 [Establecer el valor de una restricción de precedencia mediante el menú contextual](../../2014/integration-services/set-the-value-of-a-precedence-constraint-by-using-the-shortcut-menu.md)   
 [Establecer las propiedades de una restricción de precedencia](../../2014/integration-services/set-the-properties-of-a-precedence-constraint.md)   
 [Expresiones de Integration Services &#40;SSIS&#41;](expressions/integration-services-ssis-expressions.md)  
  
  
