---
title: Ejecución preparada ODBC Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- prepared execution [ODBC]
- SQL statements [ODBC], prepared execution
- SQL statements [ODBC], executing
ms.assetid: f08c8a98-31ee-48b2-9dbf-6f31c2166dbb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 147ca85b21296575ff55afbe66ab286cc4824fae
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282315"
---
# <a name="prepared-execution-odbc"></a>Ejecución preparada ODBC
La ejecución preparada es una forma eficaz de ejecutar una instrucción más de una vez. La instrucción se compila o *prepara* primero en un plan de acceso. A continuación, el plan de acceso se ejecuta una o más veces más adelante. Para obtener más información acerca de los planes de acceso, vea [Procesamiento de una instrucción SQL](../../../odbc/reference/processing-a-sql-statement.md).  
  
 Las aplicaciones verticales y personalizadas suelen utilizar la ejecución preparada para ejecutar repetidamente la misma instrucción SQL parametrizada. Por ejemplo, el código siguiente prepara una instrucción para actualizar los precios de diferentes partes. A continuación, ejecuta la instrucción varias veces con diferentes valores de parámetro cada vez.  
  
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
  
 La ejecución preparada es más rápida que la ejecución directa para las instrucciones ejecutadas más de una vez, principalmente porque la instrucción se compila solo una vez; las instrucciones ejecutadas directamente se compilan cada vez que se ejecutan. La ejecución preparada también puede proporcionar una reducción en el tráfico de red porque el controlador puede enviar un identificador de plan de acceso al origen de datos cada vez que se ejecuta la instrucción, en lugar de una instrucción SQL completa, si el origen de datos admite identificadores de plan de acceso.  
  
 La aplicación puede recuperar los metadatos del conjunto de resultados después de preparar la instrucción y antes de que se ejecute. Sin embargo, devolver metadatos para instrucciones preparadas y no ejecutadas es costoso para algunos controladores y debe evitarse mediante aplicaciones interoperables si es posible. Para obtener más información, consulte Metadatos del conjunto de [resultados](../../../odbc/reference/develop-app/result-set-metadata.md).  
  
 La ejecución preparada no se debe utilizar para las instrucciones que se ejecutan una sola vez. Para estas instrucciones, es ligeramente más lento que la ejecución directa porque requiere una llamada de función ODBC adicional.  
  
> [!IMPORTANT]  
>  La confirmación o reversión de una transacción, ya sea llamando explícitamente a **SQLEndTran** o trabajando en modo de confirmación automática, hace que algunos orígenes de datos eliminen los planes de acceso para todas las instrucciones de una conexión. Para obtener más información, vea las opciones SQL_CURSOR_COMMIT_BEHAVIOR y SQL_CURSOR_ROLLBACK_BEHAVIOR en la descripción de la función [SQLGetInfo.](../../../odbc/reference/syntax/sqlgetinfo-function.md)  
  
 Para preparar y ejecutar una instrucción, la aplicación:  
  
1.  Llama a **SQLPrepare** y le pasa una cadena que contiene la instrucción SQL.  
  
2.  Establece los valores de cualquier parámetro. En realidad, los parámetros se pueden establecer antes o después de preparar la instrucción. Para obtener más información, consulte Parámetros de [instrucción](../../../odbc/reference/develop-app/statement-parameters.md), más adelante en esta sección.  
  
3.  Llama a **SQLExecute** y realiza cualquier procesamiento adicional que sea necesario, como la obtención de datos.  
  
4.  Repite los pasos 2 y 3 según sea necesario.  
  
5.  Cuando se llama a **SQLPrepare,** el controlador:  
  
    -   Modifica la instrucción SQL para usar la gramática SQL del origen de datos sin analizar la instrucción. Esto incluye la sustitución de las secuencias de escape descritas en [Secuencias](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)de escape en ODBC . La aplicación puede recuperar la forma modificada de una instrucción SQL llamando a **SQLNativeSql**. Las secuencias de escape no se reemplazan si se establece el atributo de instrucción SQL_ATTR_NOSCAN.  
  
    -   Envía la instrucción al origen de datos para su preparación.  
  
    -   Almacena el identificador del plan de acceso devuelto para su ejecución posterior (si la preparación se realizó correctamente) o devuelve los errores (si se produjo un error en la preparación). Los errores incluyen errores sintácticos como SQLSTATE 42000 (error de sintaxis o infracción de acceso) y errores semánticos como SQLSTATE 42S02 (tabla base o vista no encontrada).  
  
        > [!NOTE]  
        >  Algunos controladores no devuelven errores en este punto, sino que los devuelven cuando se ejecuta la instrucción o cuando se llama a funciones de catálogo. Por lo tanto, **SQLPrepare** puede parecer que se ha realizado correctamente cuando, de hecho, ha fallado.  
  
6.  Cuando se llama a **SQLExecute,** el controlador:  
  
    -   Recupera los valores de parámetro actuales y los convierte según sea necesario. Para obtener más información, consulte Parámetros de [instrucción](../../../odbc/reference/develop-app/statement-parameters.md), más adelante en esta sección.  
  
    -   Envía el identificador del plan de acceso y los valores de parámetro convertidos al origen de datos.  
  
    -   Devuelve los errores. Por lo general, se trata de errores en tiempo de ejecución, como SQLSTATE 24000 (estado de cursor no válido). Sin embargo, algunos controladores devuelven errores sintácticos y semánticos en este punto.  
  
 Si el origen de datos no admite la preparación de instrucciones, el controlador debe emularlo en la medida de lo posible. Por ejemplo, el controlador podría no hacer nada cuando **SQLPrepare** se llama y, a continuación, realizar la ejecución directa de la instrucción cuando **SQLExecute** se llama.  
  
 Si el origen de datos admite la comprobación de sintaxis sin ejecución, el controlador puede enviar la instrucción para comprobar cuándo **sqlPrepare** se llama y enviar la instrucción para su ejecución cuando **SQLExecute** se llama.  
  
 Si el controlador no puede emular la preparación de instrucciones, almacena la instrucción cuando **SQLPrepare** se llama y la envía para su ejecución cuando **SQLExecute** se llama.  
  
 Dado que la preparación de instrucciones emuladas no es perfecta, **SQLExecute** puede devolver los errores devueltos normalmente por **SQLPrepare**.
