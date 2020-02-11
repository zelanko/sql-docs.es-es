---
title: Ejecución preparada ODBC | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2107ca1eeecc6fad24311c5bce629784ae4ceff0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68023283"
---
# <a name="prepared-execution-odbc"></a>Ejecución preparada ODBC
La ejecución preparada es una manera eficaz de ejecutar una instrucción más de una vez. La instrucción se compila primero o está *preparada* en un plan de acceso. Después, el plan de acceso se ejecuta una o más veces más adelante. Para obtener más información sobre los planes de acceso, vea [procesar una instrucción SQL](../../../odbc/reference/processing-a-sql-statement.md).  
  
 La ejecución preparada suele usarse en aplicaciones verticales y personalizadas para ejecutar repetidamente la misma instrucción SQL parametrizada. Por ejemplo, el código siguiente prepara una instrucción para actualizar los precios de distintas partes. A continuación, ejecuta la instrucción varias veces con distintos valores de parámetro cada vez.  
  
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
  
 La ejecución preparada es más rápida que la ejecución directa para las instrucciones ejecutadas más de una vez, principalmente porque la instrucción se compila una sola vez; las instrucciones ejecutadas directamente se compilan cada vez que se ejecutan. La ejecución preparada también puede proporcionar una reducción en el tráfico de red porque el controlador puede enviar un identificador de plan de acceso al origen de datos cada vez que se ejecuta la instrucción, en lugar de una instrucción SQL completa, si el origen de datos admite identificadores de plan de acceso.  
  
 La aplicación puede recuperar los metadatos del conjunto de resultados después de preparar la instrucción y antes de que se ejecute. Sin embargo, la devolución de metadatos para las instrucciones preparadas y sin ejecutar es costosa para algunos controladores y se debe evitar mediante aplicaciones interoperables si es posible. Para obtener más información, consulte [metadatos del conjunto de resultados](../../../odbc/reference/develop-app/result-set-metadata.md).  
  
 La ejecución preparada no se debe utilizar para las instrucciones que se ejecutan una sola vez. Para estas instrucciones, es ligeramente más lenta que la ejecución directa porque requiere una llamada a una función ODBC adicional.  
  
> [!IMPORTANT]  
>  La confirmación o reversión de una transacción, ya sea mediante una llamada explícita a **SQLEndTran** o al trabajar en el modo de confirmación automática, hace que algunos orígenes de datos eliminen los planes de acceso de todas las instrucciones de una conexión. Para obtener más información, vea las opciones SQL_CURSOR_COMMIT_BEHAVIOR y SQL_CURSOR_ROLLBACK_BEHAVIOR en la descripción de la función [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) .  
  
 Para preparar y ejecutar una instrucción, la aplicación:  
  
1.  Llama a **SQLPrepare** y le pasa una cadena que contiene la instrucción SQL.  
  
2.  Establece los valores de los parámetros. Los parámetros se pueden establecer antes o después de preparar la instrucción. Para obtener más información, vea [parámetros de instrucción](../../../odbc/reference/develop-app/statement-parameters.md), más adelante en esta sección.  
  
3.  Llama a **SQLExecute** y realiza cualquier procesamiento adicional que sea necesario, como la recuperación de datos.  
  
4.  Repite los pasos 2 y 3 según sea necesario.  
  
5.  Cuando se llama a **SQLPrepare** , el controlador:  
  
    -   Modifica la instrucción SQL para utilizar la gramática de SQL del origen de datos sin analizar la instrucción. Esto incluye reemplazar las secuencias de escape descritas en [secuencias de escape en ODBC](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md). La aplicación puede recuperar el formulario modificado de una instrucción SQL mediante una llamada a **SQLNativeSql**. Las secuencias de escape no se reemplazan si se establece el atributo de instrucción SQL_ATTR_NOSCAN.  
  
    -   Envía la instrucción al origen de datos para su preparación.  
  
    -   Almacena el identificador del plan de acceso devuelto para su ejecución posterior (si la preparación se realizó correctamente) o devuelve errores (si se produjo un error en la preparación). Los errores incluyen errores sintácticos como SQLSTATE 42000 (error de sintaxis o infracción de acceso) y errores semánticos como SQLSTATE 42S02 (tabla base o vista no encontrada).  
  
        > [!NOTE]  
        >  Algunos controladores no devuelven errores en este momento, sino que los devuelven cuando se ejecuta la instrucción o cuando se llama a las funciones de catálogo. Por lo tanto, es posible que **SQLPrepare** parezca que se ha realizado correctamente cuando se ha producido un error.  
  
6.  Cuando se llama a **SQLExecute** , el controlador:  
  
    -   Recupera los valores de parámetro actuales y los convierte según sea necesario. Para obtener más información, vea [parámetros de instrucción](../../../odbc/reference/develop-app/statement-parameters.md), más adelante en esta sección.  
  
    -   Envía el identificador del plan de acceso y los valores de parámetro convertidos al origen de datos.  
  
    -   Devuelve cualquier error. Suelen ser errores en tiempo de ejecución como SQLSTATE 24000 (estado de cursor no válido). Sin embargo, algunos controladores devuelven errores sintácticos y semánticos en este momento.  
  
 Si el origen de datos no admite la preparación de instrucciones, el controlador debe emularlo en la medida de lo posible. Por ejemplo, el controlador podría no hacer nada cuando se llama a **SQLPrepare** y, a continuación, realizar la ejecución directa de la instrucción cuando se llama a **SQLExecute** .  
  
 Si el origen de datos admite la comprobación de sintaxis sin ejecución, el controlador podría enviar la instrucción para comprobar cuándo se llama a **SQLPrepare** y enviar la instrucción para su ejecución cuando se llama a **SQLExecute** .  
  
 Si el controlador no puede emular la preparación de instrucciones, almacena la instrucción cuando se llama a **SQLPrepare** y la envía para su ejecución cuando se llama a **SQLExecute** .  
  
 Dado que la preparación de la instrucción emulada no es perfecta, **SQLExecute** puede devolver los errores devueltos normalmente por **SQLPrepare**.
