---
title: Puntos de interrupción de Transact-SQL | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Transact-SQL debugger, breakpoints
ms.assetid: c234430f-bd94-4d0d-9e74-2bf11681fa50
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 06342291cc73951043c14c6f29539eaf9f1be689
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48119485"
---
# <a name="transact-sql-breakpoints"></a>Utilizar puntos de interrupción de Transact-SQL
  Los puntos de interrupción especifican que el depurador de [!INCLUDE[tsql](../../includes/tsql-md.md)] pausa la ejecución en una instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] específica, puede ver el estado de los elementos de código en ese momento.  
  
## <a name="breakpoints"></a>Puntos de interrupción  
 Al ejecutar el depurador de [!INCLUDE[tsql](../../includes/tsql-md.md)] , puede alternar un punto de interrupción en instrucciones concretas. Cuando la ejecución llegue a una instrucción con un punto de interrupción, el depurador pausa la ejecución para que se pueda ver información de depuración, como los valores presentes en variables y parámetros.  
  
 Puede administrar los puntos de interrupción individualmente en la ventana del editor, o colectivamente mediante la ventana de **Puntos de interrupción** . Puede modificar los puntos de interrupción para especificar elementos como las condiciones particulares en las que la acción debe pausar, o las acciones que deben realizarse si ejecuta el punto de interrupción.  
  
## <a name="breakpoint-tasks"></a>Tareas de punto de interrupción  
  
|Descripción de la tarea|Tema|  
|----------------------|-----------|  
|Describe cómo especificar la instrucción de [!INCLUDE[tsql](../../includes/tsql-md.md)] en la que desea que el depurador en pause.|[Alternar un punto de interrupción](../spatial/point.md)|  
|Describe cómo desactivar temporalmente un punto de interrupción y reactivarlo posteriormente. También se describe cómo eliminar un punto de interrupción.|[Habilitar, deshabilitar y eliminar puntos de interrupción](enable-disable-and-delete-breakpoints.md)|  
|Describe cómo especificar una condición, que define si el punto de interrupción interrumpe basándose en la evaluación de una expresión de Transact SQL especificada.|[Especificar una condición de punto de interrupción](specify-a-breakpoint-condition.md)|  
|Describe como especificar un número de llamadas, que causa que un punto de interrupción se interrumpa solo cuando la instrucción que lo contiene se ha ejecutado un número de veces especificado.|[Especificar un número de llamadas](specify-a-hit-count.md)|  
|Describe cómo especificar un filtro, que hace que un punto de interrupción interrumpa únicamente en procesos o subprocesos especificados.|[Especificar un filtro del punto de interrupción](specify-a-breakpoint-filter.md)|  
|Describe cómo especificar una acción **Cuándo se llama** , una operación personalizada que se realiza cuando se ejecuta la instrucción de punto de interrupción. Un ejemplo de lo anterior sería imprimir un mensaje.|[Especificar una acción del punto de interrupción](specify-a-breakpoint-action.md)|  
|Describe cómo editar la ubicación de un punto de interrupción.|[Modificar la ubicación de un punto de interrupción](edit-a-breakpoint-location.md)|  
  
## <a name="see-also"></a>Vea también  
 [Ver información del depurador de Transact-SQL](transact-sql-debugger-information.md)  
  
  
