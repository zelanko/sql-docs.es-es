---
title: Puntos de interrupción de Transact-SQL | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Transact-SQL debugger, breakpoints
ms.assetid: c234430f-bd94-4d0d-9e74-2bf11681fa50
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a2b5e9d6e47a71f8bc65d71e0fb6364e352e8045
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2019
ms.locfileid: "68263231"
---
# <a name="transact-sql-breakpoints"></a>Utilizar puntos de interrupción de Transact-SQL
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  Los puntos de interrupción especifican que el depurador de [!INCLUDE[tsql](../../includes/tsql-md.md)] pausa la ejecución en una instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] específica, puede ver el estado de los elementos de código en ese momento.  
  
## <a name="breakpoints"></a>Puntos de interrupción  
 Al ejecutar el depurador de [!INCLUDE[tsql](../../includes/tsql-md.md)] , puede alternar un punto de interrupción en instrucciones concretas. Cuando la ejecución llegue a una instrucción con un punto de interrupción, el depurador pausa la ejecución para que se pueda ver información de depuración, como los valores presentes en variables y parámetros.  
  
 Puede administrar los puntos de interrupción individualmente en la ventana del editor, o colectivamente mediante la ventana de **Puntos de interrupción** . Puede modificar los puntos de interrupción para especificar elementos como las condiciones particulares en las que la acción debe pausar, o las acciones que deben realizarse si ejecuta el punto de interrupción.  
  
## <a name="breakpoint-tasks"></a>Tareas de punto de interrupción  
  
|Descripción de la tarea|Tema|  
|----------------------|-----------|  
|Describe cómo especificar la instrucción de [!INCLUDE[tsql](../../includes/tsql-md.md)] en la que desea que el depurador en pause.|[Alternar un punto de interrupción](../../relational-databases/scripting/toggle-a-breakpoint.md)|  
|Describe cómo desactivar temporalmente un punto de interrupción y reactivarlo posteriormente. También se describe cómo eliminar un punto de interrupción.|[Habilitar, deshabilitar y eliminar puntos de interrupción](../../relational-databases/scripting/enable-disable-and-delete-breakpoints.md)|  
|Describe cómo especificar una condición, que define si el punto de interrupción interrumpe basándose en la evaluación de una expresión de Transact SQL especificada.|[Especificar una condición de punto de interrupción](../../relational-databases/scripting/specify-a-breakpoint-condition.md)|  
|Describe como especificar un número de llamadas, que causa que un punto de interrupción se interrumpa solo cuando la instrucción que lo contiene se ha ejecutado un número de veces especificado.|[Especificar un número de llamadas](../../relational-databases/scripting/specify-a-hit-count.md)|  
|Describe cómo especificar un filtro, que hace que un punto de interrupción interrumpa únicamente en procesos o subprocesos especificados.|[Especificar un filtro del punto de interrupción](../../relational-databases/scripting/specify-a-breakpoint-filter.md)|  
|Describe cómo especificar una acción **Cuándo se llama** , una operación personalizada que se realiza cuando se ejecuta la instrucción de punto de interrupción. Un ejemplo de lo anterior sería imprimir un mensaje.|[Especificar una acción del punto de interrupción](../../relational-databases/scripting/specify-a-breakpoint-action.md)|  
|Describe cómo editar la ubicación de un punto de interrupción.|[Modificar la ubicación de un punto de interrupción](../../relational-databases/scripting/edit-a-breakpoint-location.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Ver información del depurador de Transact-SQL](../../relational-databases/scripting/transact-sql-debugger-information.md)  
  
  
