---
title: Avanzar paso a paso por el código Transact-SQL | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Transact-SQL debugger, debugging code
- Transact-SQL debugger, step over
- Transact-SQL debugger, step out
- Transact-SQL debugger, step into
ms.assetid: e09079b8-c4c9-42b4-821b-4ce81a98a086
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e79a92bc1756003341cbb9e0581ade42a2bcee8b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66090007"
---
# <a name="step-through-transact-sql-code"></a>Avanzar paso a paso por el código Transact-SQL
  El depurador de [!INCLUDE[tsql](../../includes/tsql-md.md)] permite controlar las instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] que se ejecutan en una ventana del Editor de consultas de [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Puede detener el depurador en instrucciones individuales y, a continuación, ver el estado de los elementos de código en ese punto.  
  
## <a name="breakpoints"></a>Puntos de interrupción  
 Un punto de interrupción indica al depurador que detenga la ejecución en una instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] específica. Para obtener más información sobre los puntos de interrupción, vea Utilizar puntos de interrupción de Transact-SQL.  
  
## <a name="controlling-statement-execution"></a>Controlar la ejecución de instrucciones  
 En el depurador de [!INCLUDE[tsql](../../includes/tsql-md.md)] , puede especificar las siguientes opciones para su ejecución desde la instrucción actual del código [!INCLUDE[tsql](../../includes/tsql-md.md)] :  
  
-   Ejecutar un proceso hasta el siguiente punto de interrupción.  
  
-   Ir a la siguiente instrucción.  
  
     Si la siguiente instrucción invoca un procedimiento almacenado, función o desencadenador de [!INCLUDE[tsql](../../includes/tsql-md.md)] , el depurador muestra una nueva ventana del Editor de consultas que contiene el código del módulo. La ventana está en el modo de depuración y la ejecución se detiene en la primera instrucción del módulo. Después puede desplazarse por el código del módulo, por ejemplo, estableciendo puntos de interrupción o recorriendo el código.  
  
-   Paso a paso por la siguiente instrucción.  
  
     Se ejecuta la siguiente instrucción. Sin embargo, si la instrucción invoca un procedimiento almacenado, una función o un desencadenador, el código del módulo se ejecuta hasta que termine y los resultados se devuelven al código de llamada. Si está seguro de que no hay errores en un procedimiento almacenado, puede omitirlo. La ejecución se detiene en la instrucción que sigue a la llamada al procedimiento almacenado, a la función o al desencadenador.  
  
-   Salir de un procedimiento almacenado, función o desencadenador.  
  
     La ejecución se detiene en la instrucción que sigue a la llamada al procedimiento almacenado, a la función o al desencadenador.  
  
-   Ejecutar el proceso desde la ubicación actual hasta la ubicación actual del puntero e ignorar todos los puntos de interrupción.  
  
 La tabla siguiente muestra las distintas formas en las que puede controlar la ejecución de las instrucciones del depurador de [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
|Acción|Procedimiento|  
|------------|---------------|  
|Ejecutar todas las instrucciones desde la instrucción actual hasta el siguiente punto de interrupción|En el **depurar** menú, haga clic en **continuar**.<br /><br /> En el **depurar** barra de herramientas, haga clic en el **continuar** botón.|  
|Ir a la siguiente instrucción o módulo|En el **depurar** menú, haga clic en **paso a paso**.<br /><br /> En el **depurar** barra de herramientas, haga clic en el **paso a paso** botón.<br /><br /> Presione F11.|  
|Paso a paso por la siguiente instrucción o módulo|En el **depurar** menú, haga clic en **paso a paso por**.<br /><br /> En el **depurar** barra de herramientas, haga clic en el **saltar** botón.<br /><br /> Presione F10.|  
|Salir de un módulo|En el **depurar** menú, haga clic en **paso a paso fuera**.<br /><br /> En el **depurar** barra de herramientas, haga clic en el **paso a paso fuera** botón.<br /><br /> Presione MAYÚS+F11.|  
|Ejecutar un proceso hasta la ubicación del cursor actual|Haga clic con el botón derecho en la ventana del Editor de consultas y, después, haga clic en **Ejecutar hasta el cursor**.<br /><br /> Presione CTRL+F10.|  
  
## <a name="see-also"></a>Vea también  
 [Ver información del depurador de Transact-SQL](transact-sql-debugger-information.md)  
  
  
