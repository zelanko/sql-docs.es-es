---
title: Pila de llamadas (ventana) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Call Stack Window [Transact-SQL]
ms.assetid: ddb0b19c-87cd-4883-bcb8-ec09ffb30369
author: markingmyname
ms.author: maghan
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0b8d2845aafb18a9121a5a44320bb361b62c23d0
ms.sourcegitcommit: c29150492383f48ef484fa02a483cde1cbc68aca
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/17/2019
ms.locfileid: "65821774"
---
# <a name="transact-sql-debugger---call-stack-window"></a>Depurador de Transact-SQL: ventana Pila de llamadas
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  La ventana **Pila de llamadas** muestra los módulos de la pila de llamadas y los tipos de datos y valores de los parámetros que se pasen a los módulos. [!INCLUDE[tsql](../../includes/tsql-md.md)] incluyen procedimientos almacenados, funciones y desencadenadores). Para mostrar la pila de llamadas, debe estar en modo de depuración.  
  
## <a name="task-list"></a>Lista de tareas  
 **Para tener acceso a la ventana Pila de llamadas**  
  
-   En el menú **Depurar** , haga clic en **Ventanas**y, a continuación, en **Pila de llamadas**.  
  
 **Para cambiar el marco de Pila de llamadas actual**  
  
 Puede utilizar cualquiera de los procedimientos siguientes para convertir un marco de pila en el marco actual:  
  
-   Haga clic con el botón derecho en el marco de pila y, después, haga clic en **Cambiar a marco**.  
  
-   Haga doble clic en el marco de pila.  
  
 **Para ver el origen de un marco distinto del marco actual**  
  
-   Haga clic con el botón derecho en el marco de pila y, después, haga clic en **Ir al código fuente**.  
  
## <a name="stack-frames"></a>Marcos de pila  
 Cada fila de la ventana **Pila de llamadas** se conoce como marco de pila y representa o bien una llamada de un archivo de script de [!INCLUDE[tsql](../../includes/tsql-md.md)] a un módulo o bien una llamada de un módulo a otro. El marco de pila inferior de la pantalla indica la línea de la ventana del Editor de consultas de [!INCLUDE[ssDE](../../includes/ssde-md.md)] que realizó la primera llamada en la pila. La fila superior indica la línea en la que el depurador pausó la ejecución y se identifica mediante una flecha amarilla en el margen izquierdo de la ventana. Cada fila intermedia indica el módulo y el número de línea del código fuente que llamó al marco de pila superior siguiente.  
  
 Todas las expresiones de las ventanas **Variables locales**, **Inspección**e **Inspección rápida** se evalúan según el marco de pila actual. La ventana del Editor de consultas muestra el código para el marco actual. De forma predeterminada, este marco es el marco superior de la pila, en el que el depurador de [!INCLUDE[tsql](../../includes/tsql-md.md)] detuvo la ejecución. Al cambiar el marco de pila actual a otro marco, las expresiones en las ventanas **Variables locales**, **Inspección**e **Inspección rápida** se vuelven a evaluar en el contexto del nuevo marco y el código fuente del nuevo marco se muestra en la ventana del Editor de consultas.  
  
## <a name="columns"></a>Columnas  
 **Nombre**  
 Muestra información sobre un módulo en la pila de llamadas.  
  
 En la fila inferior de la pila de llamadas, **Nombre** muestra la ventana de código fuente del Editor de consultas y el número de línea de la primera llamada en la pila. Para las otras filas, **Nombre** tiene el formato **módulo (instancia.baseDeDatos) (listaDeParámetros) númeroDeLínea**.  
  
 **módulo**  
 Es el nombre del procedimiento almacenado o función que llamó al marco siguiente.  
  
 **instancia.baseDeDatos**  
 Es la instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)] y la base de datos que contiene el módulo.  
  
 **listaDeParámetros**  
 Indica el tipo de datos, nombre y valor de cada parámetro que se pasa durante la llamada al módulo.  
  
 **LineNumber**  
 Para todas las filas excepto la fila superior, **númeroDeLínea** indica qué línea en el módulo llamó al marco. Para la fila superior, **númeroDeLínea** indica la línea en la que actualmente se centra el depurador.  
  
 **Lenguaje**  
 Muestra **Transact-SQL** para [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
## <a name="see-also"></a>Consulte también  
 [Depurador de Transact-SQL](../../relational-databases/scripting/transact-sql-debugger.md)   
 [Ver información del depurador de Transact-SQL](../../relational-databases/scripting/transact-sql-debugger-information.md)   
 [Avanzar paso a paso por el código Transact-SQL](../../relational-databases/scripting/step-through-transact-sql-code.md)  
