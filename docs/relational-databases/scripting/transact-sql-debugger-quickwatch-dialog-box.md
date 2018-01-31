---
title: "Inspección rápida (cuadro de diálogo) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- vs.debug.quickwatch
helpviewer_keywords:
- QuickWatch Dialog [Transact-SQL]
ms.assetid: d6bbb373-1452-41f2-bdc5-86ae689c3dc0
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: b3b655a3f433c0957b36dc639c3f1d7f309cd151
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/24/2018
---
# <a name="transact-sql-debugger---quickwatch-dialog-box"></a>Depurador de Transact-SQL: cuadro de diálogo Inspección rápida
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Utilice el cuadro de diálogo **Inspección rápida** para ver rápidamente el tipo de datos y el valor de una expresión de [!INCLUDE[tsql](../../includes/tsql-md.md)], como una variable o un parámetro, cuando esté depurando el código de [!INCLUDE[tsql](../../includes/tsql-md.md)]. Para inspeccionar varias expresiones, puede agregar también la expresión a una ventana **Inspección** .  
  
## <a name="task-list"></a>Lista de tareas  
 **Para tener acceso al cuadro de diálogo Inspección rápida**  
  
-   En el menú **Depurar** , haga clic en **Inspección rápida**.  
  
 **Para ver la información sobre una expresión**  
  
1.  En el cuadro de lista **Expresión** , escriba o seleccione la expresión que desea. Se admiten las expresiones [!INCLUDE[tsql](../../includes/tsql-md.md)] siguientes:  
  
    -   Variables.  
  
    -   Parámetros.  
  
    -   Funciones del sistema cuyo nombre empieza con @@.  
  
    -   Expresiones generadas mediante la aplicación de operadores a una o más variables, parámetros o funciones del sistema, como @IntegerCounter + 1 o FirstName + LastName.  
  
    -   Instrucciones Transact-SQL que devuelven un valor único, como SELECT CharacterCol FROM MyTable WHERE PrimaryKey = 1.  
  
2.  Haga clic en **Actualizar**.  
  
 **Para agregar una expresión de Inspección rápida a la ventana Inspección**  
  
-   Haga clic en **Agregar inspección**.  
  
 **Para cambiar el valor de una expresión de Inspección rápida**  
  
-   Haga clic con el botón derecho en la expresión y, después, seleccione **Editar valor**.  
  
## <a name="options"></a>.  
 **Lista de expresiones**  
 Muestra la expresión seleccionada actualmente. La lista desplegable contiene un conjunto de expresiones que puede seleccionar para mostrarse. Las expresiones de la lista son las que están disponibles en el ámbito del marco de pila que está seleccionado actualmente en la ventana **Pila de llamadas** . Para mostrar una expresión diferente, escríbala o selecciónela en la lista. El depurador de [!INCLUDE[tsql](../../includes/tsql-md.md)] admite las expresiones siguientes: variables, parámetros y funciones de sistema cuyos nombres comienzan por @@.  
  
 **Cuadrícula Valor**  
 Muestra las propiedades de la expresión que se está inspeccionando.  
  
 **Nombre**  
 Expresión [!INCLUDE[tsql](../../includes/tsql-md.md)] que se va a observar.  
  
 **Value**  
 Muestra el valor que está asignado actualmente a la expresión. Se muestra un espacio en blanco cuando la expresión no tiene ningún valor en este momento.  
  
 Si la longitud de una expresión es mayor que el ancho de la columna **Valor** , una información sobre herramientas muestra el valor completo al mover el puntero sobre la celda **Valor** para esa expresión.  
  
 Un icono de lupa en una celda **Valor** indica que el visualizador del depurador de [!INCLUDE[tsql](../../includes/tsql-md.md)] está disponible. En la lista, puede especificar **Visualizador de texto**, **Visualizador XML**o **Visualizador HTML**. Para iniciar un visualizador del depurador, haga clic en el icono de lupa. El depurador de [!INCLUDE[tsql](../../includes/tsql-md.md)] abre un cuadro de diálogo que muestra los datos en un formato adecuado al tipo de datos.  
  
 **Tipo**  
 Muestra el tipo de datos de la expresión.  
  
## <a name="see-also"></a>Ver también  
 [Depurador de Transact-SQL](../../relational-databases/scripting/transact-sql-debugger.md)   
 [Ver información del depurador de Transact-SQL](../../relational-databases/scripting/transact-sql-debugger-information.md)   
 [Ventana de inspección](../../relational-databases/scripting/transact-sql-debugger-watch-window.md)   
 [Ventana de locales](../../relational-databases/scripting/transact-sql-debugger-locals-window.md)   
 [Ventana de pila de llamadas](../../relational-databases/scripting/transact-sql-debugger-call-stack-window.md)   
 [Expresiones &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
  
  
