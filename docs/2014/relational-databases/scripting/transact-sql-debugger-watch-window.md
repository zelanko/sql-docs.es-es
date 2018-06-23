---
title: Inspección (ventana) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.debug.watch
helpviewer_keywords:
- Watch Window [Transact-SQL]
ms.assetid: 23f3baa4-14c2-4262-92f7-3f43fcfa0436
caps.latest.revision: 15
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 4c2cc64072bdf0d902499a162b7ac7c87629026d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36107846"
---
# <a name="watch-window"></a>Ventana de inspección
  La ventana **Inspección** muestra información sobre las expresiones que ha seleccionado. Puede haber hasta cuatro ventanas Inspección: **Inspección 1**, **Inspección 2, Inspección 3**e **Inspección 4**. Las expresiones se evalúan dentro del ámbito del marco de la pila de llamadas actual que está seleccionado en la ventana **Pila de llamadas** . Debe estar en modo de depuración para observar las variables y las expresiones.  
  
## <a name="task-list"></a>Lista de tareas  
 **Para tener acceso a las ventanas Inspección**  
  
-   En el menú **Depurar** , haga clic en **Ventanas**, luego en **Inspección**y, después, haga clic en **Inspección 1**, **Inspección 2, Inspección 3**o **Inspección 4**.  
  
 **Para cambiar el valor de una expresión**  
  
-   Haga clic con el botón derecho en la expresión y, después, seleccione **Editar valor**.  
  
## <a name="columns"></a>Columnas  
 **Nombre**  
 Son las expresiones que muestra el depurador de [!INCLUDE[tsql](../../includes/tsql-md.md)] . Se admiten las siguientes expresiones:  
  
-   Variables.  
  
-   Parámetros.  
  
-   Funciones del sistema cuyo nombre empieza con @@.  
  
-   Expresiones generadas mediante la aplicación de operadores a una o más variables, parámetros o funciones del sistema, como @IntegerCounter + 1 o FirstName + LastName.  
  
-   Instrucciones Transact-SQL que devuelven un valor único, como SELECT CharacterCol FROM MyTable WHERE PrimaryKey = 1.  
  
 **Value**  
 Muestra el valor que se devuelve después de que el depurador de [!INCLUDE[tsql](../../includes/tsql-md.md)] evalúe la expresión especificada en **Nombre**.  
  
 Si la longitud de una expresión es mayor que el ancho de la columna **Valor** , una información sobre herramientas muestra el valor completo al mover el puntero sobre la celda **Valor** para esa expresión.  
  
 Un icono de lupa en una celda **Valor** indica que el visualizador del depurador de [!INCLUDE[tsql](../../includes/tsql-md.md)] está disponible. En la lista, puede especificar **Visualizador de texto**, **Visualizador XML**o **Visualizador HTML**. Para iniciar un visualizador del depurador, haga clic en el icono de lupa. El depurador de [!INCLUDE[tsql](../../includes/tsql-md.md)] abre un diálogo que muestra los datos en un formato adecuado al tipo de datos.  
  
 **Tipo**  
 Muestra el tipo de datos de la expresión.  
  
## <a name="see-also"></a>Vea también  
 [Depurador de Transact-SQL](transact-sql-debugger.md)   
 [Ver información del depurador de Transact-SQL](transact-sql-debugger-information.md)   
 [Ventana de locales](transact-sql-debugger-locals-window.md)   
 [Ventana de pila de llamadas](transact-sql-debugger-call-stack-window.md)   
 [Cuadro de diálogo Inspección rápida](transact-sql-debugger-quickwatch-dialog-box.md)   
 [Expresiones &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/expressions-transact-sql)  
  
  
