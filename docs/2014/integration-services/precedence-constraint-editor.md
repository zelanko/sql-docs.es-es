---
title: Editor de restricciones de precedencia | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.precedenceconstraint.f1
helpviewer_keywords:
- Precedence Constraint Editor dialog box
ms.assetid: b10d4330-6e35-4037-b309-ef56efcd60c5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7d2046882eeed6b04cd1b1c4035b89eccbddc4f6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66056685"
---
# <a name="precedence-constraint-editor"></a>Editor de restricciones de precedencia
  Utilice el cuadro de diálogo **Editor de restricciones de precedencia** para configurar restricciones de precedencia.  
  
## <a name="options"></a>Opciones  
 **Operación de evaluación**  
 Permite especificar la operación de evaluación que utiliza la restricción de precedencia. Las operaciones son: **Restricción**, **Expresión**, **Expresión y restricción**, y **Expresión o restricción**.  
  
 **Valor**  
 Permite especificar el valor de restricción: **Correcto**, **Error**o **Conclusión**.  
  
> [!NOTE]  
>  La línea de restricción de precedencia es verde para **Correcto**, resaltada para **Error**y azul para **Conclusión**.  
  
 **Expression**  
 Si usa las operaciones **Expresión**, **Expresión y restricción**o **Expresión o restricción**, escriba una expresión o inicie el Generador de expresiones para crear la expresión. La expresión debe evaluarse como un valor booleano.  
  
 **Muestre**  
 Permite validar la expresión.  
  
 **Y lógico**  
 Seleccione esta opción para indicar que varias restricciones de precedencia en el mismo archivo ejecutable deben evaluarse de forma conjunta. Todas las restricciones deben evaluarse como `True`.  
  
> [!NOTE]  
>  Este tipo de restricción de precedencia se muestra como una línea sólida verde, resaltada o azul.  
  
 **O lógico**  
 Seleccione esta opción para indicar que varias restricciones de precedencia en el mismo archivo ejecutable deben evaluarse de forma conjunta. Al menos una restricción debe evaluarse como `True`.  
  
> [!NOTE]  
>  Este tipo de restricción de precedencia se muestra como una línea de puntos verde, resaltada o azul.  
  
## <a name="see-also"></a>Consulte también  
 [Restricciones de precedencia](control-flow/precedence-constraints.md)   
 [Tareas de Integration Services](control-flow/integration-services-tasks.md)   
 [Contenedores de Integration Services](control-flow/integration-services-containers.md)   
 [Expresiones de Integration Services &#40;SSIS&#41;](expressions/integration-services-ssis-expressions.md)  
  
  
