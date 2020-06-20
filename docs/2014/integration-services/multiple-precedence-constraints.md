---
title: Varias restricciones de precedencia | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- multiple precedence constraints
- precedence executables [Integration Services]
- precedence constraints [Integration Services], multiple
- constrained executables [Integration Services]
ms.assetid: 71c53ead-3d19-4bc1-aafd-e5b32595b420
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 61939b09b4a4365c09089df2b52026e96f9427ee
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84965155"
---
# <a name="multiple-precedence-constraints"></a>Varias restricciones de precedencia
  Una restricción de precedencia conecta dos ejecutables: dos tareas, dos contenedores o uno de cada. Se conocen como el ejecutable de precedencia y el ejecutable restringido. Un ejecutable restringido puede tener varias restricciones de precedencia. Para obtener más información, vea [Restricciones de precedencia](control-flow/precedence-constraints.md).  
  
 El ensamblaje de escenarios de restricciones complejas mediante la agrupación de restricciones le permite implementar un flujo de control complejo en paquetes. Por ejemplo, en la siguiente ilustración, la tarea D se vincula a la tarea A mediante una restricción `Success`, la tarea D se vincula a la tarea B mediante una restricción `Failure`, y la tarea D se vincula a la tarea C mediante una restricción `Success`. Las restricciones de precedencia entre la tarea D y la tarea A, entre la tarea D y la tarea B, y entre la tarea D y la tarea C participan en una relación lógica *and* . Por lo tanto, para que la tarea D se ejecute, la tarea A se debe ejecutar correctamente, la tarea B debe sufrir un error en su ejecución, y la tarea C se debe ejecutar correctamente.  
  
 ![Tareas vinculadas por las restricciones de precedencia](media/precedenceconstraints.gif "Tareas vinculadas por las restricciones de precedencia")  
  
## <a name="logicaland-property"></a>Propiedad LogicalAnd  
 Si una tarea o contenedor tiene varias restricciones, la propiedad `LogicalAnd` especifica si se evalúa una restricción de precedencia individualmente o en conjunto con otras restricciones.  
  
 Puede establecer la `LogicalAnd` propiedad mediante el **Editor de restricciones de precedencia** en [!INCLUDE[ssIS](../includes/ssis-md.md)] el diseñador o en el ventana Propiedades que [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] proporciona.  
  
## <a name="related-tasks"></a>Related Tasks  
 [Establecer las propiedades de una restricción de precedencia](../../2014/integration-services/set-the-properties-of-a-precedence-constraint.md)  
  
  
