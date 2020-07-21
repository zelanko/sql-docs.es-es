---
title: Controladores | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300215"
---
# <a name="handles"></a>Asas
Los identificadores son valores de 32 bits opacos que identifican un elemento determinado; en ODBC, este elemento puede ser un entorno, una conexión, una instrucción o un descriptor. Cuando la aplicación llama a **SQLAllocHandle**, el administrador de controladores o el controlador crea un nuevo elemento del tipo especificado y devuelve su identificador a la aplicación. Posteriormente, la aplicación usa el identificador para identificar ese elemento al llamar a funciones de ODBC. El administrador de controladores y el controlador usan el identificador para buscar información sobre el elemento.  
  
 Por ejemplo, el código siguiente utiliza dos identificadores de instrucciones (*hstmtOrder* y *hstmtLine*) para identificar las instrucciones en las que se van a crear conjuntos de resultados de pedidos de ventas y números de línea de pedidos de ventas. Más adelante usa estos identificadores para identificar el conjunto de resultados del que se van a capturar datos.  
  
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
  
 Los identificadores solo son significativos para el componente ODBC que los creó. es decir, solo el administrador de controladores puede interpretar los identificadores del administrador de controladores y solo un controlador puede interpretar sus propios identificadores.  
  
 Por ejemplo, supongamos que el controlador del ejemplo anterior asigna una estructura para almacenar información sobre una instrucción y devuelve el puntero a esta estructura como identificador de instrucción. Cuando la aplicación llama a **SQLPrepare**, pasa una instrucción SQL y el identificador de la instrucción que se usa para los números de línea del pedido de ventas. El controlador envía la instrucción SQL al origen de datos, que lo prepara y devuelve un identificador de plan de acceso. El controlador utiliza el identificador para encontrar la estructura en la que se va a almacenar este identificador.  
  
 Más adelante, cuando la aplicación llama a **SQLExecute** para generar el conjunto de resultados de los números de línea de un pedido de ventas determinado, pasa el mismo identificador. El controlador utiliza el identificador para recuperar el identificador del plan de acceso de la estructura. Envía el identificador al origen de datos para indicarle el plan que se va a ejecutar.  
  
 ODBC tiene dos niveles de identificadores: Controladores de administrador de controladores y controladores de controladores. La aplicación utiliza identificadores del administrador de controladores al llamar a funciones de ODBC porque llama a esas funciones en el administrador de controladores. El administrador de controladores usa este identificador para buscar el controlador de controlador correspondiente y usa el identificador de controlador al llamar a la función en el controlador. Para ver un ejemplo de cómo se usan los controladores del controlador y del administrador de controladores, consulte [el rol del administrador de controladores en el proceso de conexión](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md).  
  
 Hay dos niveles de identificadores que son un artefacto de la arquitectura ODBC; en la mayoría de los casos, no es relevante para la aplicación o el controlador. Aunque no suele haber ninguna razón para hacerlo, es posible que la aplicación determine los identificadores de controlador mediante una llamada a **SQLGetInfo**.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Identificadores de entorno](../../../odbc/reference/develop-app/environment-handles.md)  
  
-   [Identificadores de conexión](../../../odbc/reference/develop-app/connection-handles.md)  
  
-   [Identificadores de instrucciones](../../../odbc/reference/develop-app/statement-handles.md)  
  
-   [Identificadores de descriptor](../../../odbc/reference/develop-app/descriptor-handles.md)  
  
-   [Transiciones de estado](../../../odbc/reference/develop-app/state-transitions.md)
