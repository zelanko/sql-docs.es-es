---
title: Manijas de la casa de la página Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- handles [ODBC]
- driver handles [ODBC]
- driver manager [ODBC], handles
- handles [ODBC], about handles
ms.assetid: f663101e-a4cc-402b-b9d7-84d5e975be71
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 713c2a71ec195b75d682b97239413e98d07b5861
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300215"
---
# <a name="handles"></a>Asas
Los controladores son valores opacos de 32 bits que identifican un elemento determinado; en ODBC, este elemento puede ser un entorno, conexión, instrucción o descriptor. Cuando la aplicación llama a **SQLAllocHandle**, el Administrador de controladores o el controlador crea un nuevo elemento del tipo especificado y devuelve su identificador a la aplicación. La aplicación más adelante usa el identificador para identificar ese elemento al llamar a funciones ODBC. El Administrador de controladores y el controlador usan el identificador para buscar información sobre el elemento.  
  
 Por ejemplo, el código siguiente utiliza dos identificadores de instrucción (*hstmtOrder* y *hstmtLine*) para identificar las instrucciones en las que se crean conjuntos de resultados de pedidos de ventas y números de línea de pedido de ventas. Más adelante usa estos identificadores para identificar el conjunto de resultados del que se va a capturar datos.  
  
```  
SQLHSTMT      hstmtOrder, hstmtLine; // Statement handles.  
SQLUINTEGER   OrderID;  
SQLINTEGER    OrderIDInd = 0;  
SQLRETURN     rc;  
  
// Prepare the statement that retrieves line number information.  
SQLPrepare(hstmtLine, "SELECT * FROM Lines WHERE OrderID = ?", SQL_NTS);  
  
// Bind OrderID to the parameter in the preceding statement.  
SQLBindParameter(hstmtLine, 1, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 5, 0,  
               &OrderID, 0, &OrderIDInd);  
  
// Bind the result sets for the Order table and the Lines table. Bind  
// OrderID to the OrderID column in the Orders table. When each row is  
// fetched, OrderID will contain the current order ID, which will then be  
// passed as a parameter to the statement tofetch line number  
// information. Code not shown.  
  
// Create a result set of sales orders.  
SQLExecDirect(hstmtOrder, "SELECT * FROM Orders", SQL_NTS);  
  
// Fetch and display the sales order data. Code to check if rc equals  
// SQL_ERROR or SQL_SUCCESS_WITH_INFO not shown.  
while ((rc = SQLFetch(hstmtOrder)) != SQL_NO_DATA) {  
   // Display the sales order data. Code not shown.  
  
   // Create a result set of line numbers for the current sales order.  
   SQLExecute(hstmtLine);  
  
   // Fetch and display the sales order line number data. Code to check  
   // if rc equals SQL_ERROR or SQL_SUCCESS_WITH_INFO not shown.  
   while ((rc = SQLFetch(hstmtLine)) != SQL_NO_DATA) {  
      // Display the sales order line number data. Code not shown.  
   }  
  
   // Close the sales order line number result set.  
   SQLCloseCursor(hstmtLine);  
}  
  
// Close the sales order result set.  
SQLCloseCursor(hstmtOrder);  
```  
  
 Los controladores son significativos solo para el componente ODBC que los creó; es decir, solo el Administrador de controladores puede interpretar los identificadores del Administrador de controladores y solo un controlador puede interpretar sus propios identificadores.  
  
 Por ejemplo, supongamos que el controlador del ejemplo anterior asigna una estructura para almacenar información sobre una instrucción y devuelve el puntero a esta estructura como identificador de instrucción. Cuando la aplicación llama a **SQLPrepare**, pasa una instrucción SQL y el identificador de la instrucción utilizada para los números de línea de pedido de ventas. El controlador envía la instrucción SQL al origen de datos, que la prepara y devuelve un identificador de plan de acceso. El controlador utiliza el identificador para buscar la estructura en la que se almacenará este identificador.  
  
 Más adelante, cuando la aplicación llama a **SQLExecute** para generar el conjunto de resultados de números de línea para un pedido de ventas determinado, pasa el mismo identificador. El controlador utiliza el identificador para recuperar el identificador del plan de acceso de la estructura. Envía el identificador al origen de datos para indicarle qué planea ejecutar.  
  
 ODBC tiene dos niveles de identificadores: identificadores del Administrador de controladores y identificadores de controlador. La aplicación usa identificadores del Administrador de controladores al llamar a funciones ODBC porque llama a esas funciones en el Administrador de controladores. El Administrador de controladores utiliza este identificador para buscar el identificador de controlador correspondiente y usa el identificador de controlador al llamar a la función en el controlador. Para obtener un ejemplo de cómo se usan los identificadores de controlador y Administrador de controladores, vea Rol del Administrador de [controladores en el proceso](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md)de conexión .  
  
 Que hay dos niveles de identificadores es un artefacto de la arquitectura ODBC; en la mayoría de los casos, no es relevante para la aplicación o el controlador. Aunque normalmente no hay ninguna razón para hacerlo, es posible que la aplicación determine los identificadores de controlador mediante una llamada a **SQLGetInfo**.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Identificadores de entorno](../../../odbc/reference/develop-app/environment-handles.md)  
  
-   [Identificadores de conexión](../../../odbc/reference/develop-app/connection-handles.md)  
  
-   [Identificadores de instrucciones](../../../odbc/reference/develop-app/statement-handles.md)  
  
-   [Identificadores de descriptor](../../../odbc/reference/develop-app/descriptor-handles.md)  
  
-   [Transiciones de estado](../../../odbc/reference/develop-app/state-transitions.md)
