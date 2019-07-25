---
title: Inspección rápida (cuadro de diálogo) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- vs.debug.quickwatch
helpviewer_keywords:
- QuickWatch Dialog [Transact-SQL]
ms.assetid: d6bbb373-1452-41f2-bdc5-86ae689c3dc0
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0cffe35d5d46b76ef049538710961898d1832b7d
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2019
ms.locfileid: "68253330"
---
# <a name="transact-sql-debugger---quickwatch-dialog-box"></a>Depurador de Transact-SQL: cuadro de diálogo Inspección rápida
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  Utilice el cuadro de diálogo **Inspección rápida** para ver rápidamente el tipo de datos y el valor de una expresión de [!INCLUDE[tsql](../../includes/tsql-md.md)] , como una variable o un parámetro, cuando esté depurando el código de [!INCLUDE[tsql](../../includes/tsql-md.md)] . Para inspeccionar varias expresiones, puede agregar también la expresión a una ventana **Inspección** .  
  
## <a name="task-list"></a>Lista de tareas  
 **Para tener acceso al cuadro de diálogo Inspección rápida**  
  
-   En el menú **Depurar** , haga clic en **Inspección rápida**.  
  
 **Para ver la información sobre una expresión**  
  
1.  En el cuadro de lista **Expresión** , escriba o seleccione la expresión que desea. Se admiten las expresiones [!INCLUDE[tsql](../../includes/tsql-md.md)] siguientes:  
  
    -   Variables.  
  
    -   Parámetros.  
  
    -   Funciones del sistema cuyo nombre empieza con @@.  
  
    -   Expresiones generadas mediante la aplicación de operadores a una o más variables, parámetros o funciones del sistema, como @IntegerCounter + 1 o FirstName + LastName.  
  
    -   Instrucciones de Transact-SQL que devuelven un valor único, como: SELECT CharacterCol FROM MyTable WHERE PrimaryKey = 1.  
  
2.  Haga clic en **Actualizar**.  
  
 **Para agregar una expresión de Inspección rápida a la ventana Inspección**  
  
-   Haga clic en **Agregar inspección**.  
  
 **Para cambiar el valor de una expresión de Inspección rápida**  
  
-   Haga clic con el botón derecho en la expresión y, después, seleccione **Editar valor**.  
  
## <a name="options"></a>Opciones  
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
  
## <a name="see-also"></a>Consulte también  
 [Depurador de Transact-SQL](../../relational-databases/scripting/transact-sql-debugger.md)   
 [Ver información del depurador de Transact-SQL](../../relational-databases/scripting/transact-sql-debugger-information.md)   
 [Ventana de inspección](../../relational-databases/scripting/transact-sql-debugger-watch-window.md)   
 [Ventana de locales](../../relational-databases/scripting/transact-sql-debugger-locals-window.md)   
 [Ventana de pila de llamadas](../../relational-databases/scripting/transact-sql-debugger-call-stack-window.md)   
 [Expresiones &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
  
  
