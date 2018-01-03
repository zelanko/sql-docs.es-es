---
title: "La ejecución de ODBC preparada | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- prepared execution [ODBC]
- SQL statements [ODBC], prepared execution
- SQL statements [ODBC], executing
ms.assetid: f08c8a98-31ee-48b2-9dbf-6f31c2166dbb
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6a4f91eb2e4e255007fef3f93504872f791499e7
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="prepared-execution-odbc"></a>Ejecución preparada ODBC
Ejecución preparada es una manera eficaz para ejecutar una instrucción varias veces. En primer lugar se compila la instrucción, o *preparado,* en un plan de acceso. El plan de acceso es, a continuación, ejecutan una o más veces en un momento posterior. Para obtener más información acerca de los planes de acceso, consulte [procesar una instrucción SQL](../../../odbc/reference/processing-a-sql-statement.md).  
  
 Las aplicaciones verticales y personalizadas suelen usar la ejecución preparada para ejecutar repetidamente la misma instrucción SQL parametrizada. Por ejemplo, en el código siguiente se prepara una instrucción para actualizar los precios de varias partes diferentes. A continuación, ejecuta la instrucción varias veces con distintos valores de parámetro cada vez.  
  
```  
SQLREAL       Price;  
SQLUINTEGER   PartID;  
SQLINTEGER    PartIDInd = 0, PriceInd = 0;  
  
// Prepare a statement to update salaries in the Employees table.  
SQLPrepare(hstmt, "UPDATE Parts SET Price = ? WHERE PartID = ?", SQL_NTS);  
  
// Bind Price to the parameter for the Price column and PartID to  
// the parameter for the PartID column.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_FLOAT, SQL_REAL, 7, 0,  
                  &Price, 0, &PriceInd);  
SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 10, 0,  
                  &PartID, 0, &PartIDInd);  
  
// Repeatedly execute the statement.  
while (GetPrice(&PartID, &Price)) {  
   SQLExecute(hstmt);  
}  
```  
  
 Ejecución preparada es más rápida que la ejecución directa de las instrucciones ejecutadas varias veces, principalmente porque la instrucción se compila una sola vez; las instrucciones ejecutadas directamente se compilan cada vez que se ejecutan. Ejecución preparada también puede proporcionar que una reducción del tráfico de red porque el controlador puede enviar un identificador de plan de acceso al origen de datos cada vez que la instrucción se ejecuta, en lugar de una instrucción SQL completa, si el acceso de admite el origen de datos previsto identificadores.  
  
 La aplicación puede recuperar los metadatos para el conjunto de resultados después de prepara la instrucción y antes de que se ejecute. Sin embargo, devolver los metadatos para preparar, instrucciones haber es costosas para algunos controladores y debe evitarse por aplicaciones interoperables si es posible. Para obtener más información, consulte [metadatos del conjunto de resultados](../../../odbc/reference/develop-app/result-set-metadata.md).  
  
 La ejecución preparada no se debe utilizar para las instrucciones que se ejecutan una sola vez. De dichas instrucciones es ligeramente más lenta que la ejecución directa porque requiere una llamada de función ODBC adicional.  
  
> [!IMPORTANT]  
>  Confirmar o revertir una transacción, ya sea llamando explícitamente a **SQLEndTran** o cuando se trabaja en modo de confirmación automática, hace que algunos orígenes de datos eliminar los planes de acceso para todas las instrucciones en una conexión. Para obtener más información, vea las opciones SQL_CURSOR_COMMIT_BEHAVIOR y SQL_CURSOR_ROLLBACK_BEHAVIOR en el [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) descripción de la función.  
  
 Para preparar y ejecutar una instrucción, la aplicación:  
  
1.  Llamadas **SQLPrepare** y le pasa una cadena que contiene la instrucción SQL.  
  
2.  Establece los valores de los parámetros. Parámetros pueden establecerse realmente antes o después de preparar la instrucción. Para obtener más información, consulte [parámetros de la instrucción](../../../odbc/reference/develop-app/statement-parameters.md), más adelante en esta sección.  
  
3.  Llamadas **SQLExecute** y realiza el procesamiento adicional que sea necesario, como la obtención de datos.  
  
4.  Repite los pasos 2 y 3 según sea necesario.  
  
5.  Cuando **SQLPrepare** se llama, el controlador:  
  
    -   Modifica la instrucción SQL para el uso de la gramática SQL del origen de datos sin analizar la instrucción. Esto incluye reemplazando las secuencias de escape que se describen en [secuencias de Escape de ODBC](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md). La aplicación puede recuperar el formulario modificado de una instrucción SQL mediante una llamada a **SQLNativeSql**. No se reemplazan las secuencias de escape si se establece el atributo de instrucción SQL_ATTR_NOSCAN.  
  
    -   La instrucción se envía al origen de datos para la preparación.  
  
    -   Almacena el identificador de plan de acceso devuelto para una ejecución posterior (si se realizó correctamente la preparación) o devuelve los errores (si la preparación de error). Los errores incluyen los errores sintácticos, como SQLSTATE 42000 (sintaxis o infracción de acceso) y errores semánticos como SQLSTATE 42S02 (con Base en tabla o vista no encontrado).  
  
        > [!NOTE]  
        >  Algunos controladores no devolver errores en este punto, pero en su lugar devolver cuando se ejecuta la instrucción o cuando se llaman a funciones de catálogo. Por lo tanto, **SQLPrepare** puede parecer que han sido correctos cuando en realidad se produce un error.  
  
6.  Cuando **SQLExecute** se llama, el controlador:  
  
    -   Recupera los valores de parámetro actuales y los convierte según sea necesario. Para obtener más información, consulte [parámetros de la instrucción](../../../odbc/reference/develop-app/statement-parameters.md), más adelante en esta sección.  
  
    -   Envía el identificador de plan de acceso y los valores de parámetro convertido al origen de datos.  
  
    -   Devuelve los errores. Se trata de errores en tiempo de ejecución por lo general, como SQLSTATE 24000 (estado de cursor no válido). Sin embargo, algunos controladores devuelven errores sintácticos y semánticos en este momento.  
  
 Si el origen de datos no admite la preparación de instrucciones, el controlador debe emular a la medida de lo posible. Por ejemplo, el controlador puede realizar nada cuando **SQLPrepare** se llama y, a continuación, realizar la ejecución directa de la instrucción cuando **SQLExecute** se llama.  
  
 Si el origen de datos es compatible con las comprobaciones de sintaxis sin ejecución, el controlador puede enviar la instrucción para comprobar cuándo **SQLPrepare** se llama y enviar la instrucción para la ejecución cuando **SQLExecute** es se llama.  
  
 Si el controlador no puede emular la preparación de instrucciones, almacena la instrucción cuando **SQLPrepare** se llama y lo envía para su ejecución cuando **SQLExecute** se llama.  
  
 Porque no es perfecta, preparación de instrucciones emulado **SQLExecute** puede devolver los errores devueltos normalmente por **SQLPrepare**.
