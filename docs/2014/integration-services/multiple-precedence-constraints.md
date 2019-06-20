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
manager: craigg
ms.openlocfilehash: c0b75b96f30d2fe7f104e8f59aa03d7de6202e6a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66057412"
---
# <a name="multiple-precedence-constraints"></a>Varias restricciones de precedencia
  Una restricción de precedencia conecta dos ejecutables: dos tareas, dos contenedores o uno de cada. Se conocen como el ejecutable de precedencia y el ejecutable restringido. Un ejecutable restringido puede tener varias restricciones de precedencia. Para más información, consulte [Precedence Constraints](control-flow/precedence-constraints.md).  
  
 El ensamblaje de escenarios de restricciones complejas mediante la agrupación de restricciones le permite implementar un flujo de control complejo en paquetes. Por ejemplo, en la siguiente ilustración, la tarea D se vincula a la tarea A mediante una restricción `Success`, la tarea D se vincula a la tarea B mediante una restricción `Failure`, y la tarea D se vincula a la tarea C mediante una restricción `Success`. Las restricciones de precedencia entre la tarea D y la tarea A, entre la tarea D y la tarea B, y entre la tarea D y la tarea C participan en una relación lógica *and* . Por lo tanto, para que la tarea D se ejecute, la tarea A se debe ejecutar correctamente, la tarea B debe sufrir un error en su ejecución, y la tarea C se debe ejecutar correctamente.  
  
 ![Tareas vinculadas por las restricciones de precedencia](media/precedenceconstraints.gif "Tasks linked by precedence constraints")  
  
## <a name="logicaland-property"></a>Propiedad LogicalAnd  
 Si una tarea o contenedor tiene varias restricciones, la propiedad `LogicalAnd` especifica si se evalúa una restricción de precedencia individualmente o en conjunto con otras restricciones.  
  
 Puede establecer el `LogicalAnd` propiedad utilizando el **Editor de restricciones de precedencia** en [!INCLUDE[ssIS](../includes/ssis-md.md)] diseñador, o en la ventana Propiedades que [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] proporciona.  
  
## <a name="related-tasks"></a>Related Tasks  
 [Establecer las propiedades de una restricción de precedencia](../../2014/integration-services/set-the-properties-of-a-precedence-constraint.md)  
  
  
