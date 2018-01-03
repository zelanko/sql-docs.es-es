---
title: Controla | Documentos de Microsoft
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
- handles [ODBC]
- driver handles [ODBC]
- driver manager [ODBC], handles
- handles [ODBC], about handles
ms.assetid: f663101e-a4cc-402b-b9d7-84d5e975be71
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1c1198607b5a664b14fe6da31c9ebdc4f82bdb8e
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="handles"></a>Asas
Los identificadores son valores opacos y de 32 bits que identifican un elemento determinado; en ODBC, este elemento puede ser un entorno, la conexión, la instrucción o el descriptor. Cuando la aplicación llama **SQLAllocHandle**, el Administrador de controladores o controlador crea un nuevo elemento del tipo especificado y devuelve su identificador de la aplicación. La aplicación más tarde, usa el identificador para identificar dicho elemento al llamar a funciones ODBC. El Administrador de controladores y el controlador utilizan el identificador para buscar información sobre el elemento.  
  
 Por ejemplo, el código siguiente utiliza dos identificadores de instrucciones (*hstmtOrder* y *hstmtLine*) para identificar las instrucciones en el que se va a crear conjuntos de resultados de ventas pedidos y ventas de pedido de números de línea. Más adelante se utiliza estos identificadores para identificar qué resultado se establece para capturar los datos de.  
  
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
  
 Los identificadores son significativos únicamente para el componente ODBC que se usaron para crearlas; es decir, solo el Administrador de controladores puede interpretar los identificadores del Administrador de controladores y solo un controlador puede interpretar sus propios identificadores.  
  
 Por ejemplo, suponga que el controlador en el ejemplo anterior asigna una estructura para almacenar información sobre una instrucción y devuelve el puntero a esta estructura como el identificador de instrucción. Cuando la aplicación llama **SQLPrepare**, pasa una instrucción SQL y el identificador de la instrucción que se utiliza para números de línea de pedido de ventas. El controlador envía la instrucción SQL al origen de datos, que lo prepara y devuelve un identificador de plan de acceso. El controlador utiliza el identificador para buscar la estructura en la que se va a almacenar este identificador.  
  
 Posteriormente, cuando la aplicación llama a **SQLExecute** para generar el conjunto de resultados de números de línea para un determinado pedido de venta, pasa el mismo identificador. El controlador utiliza el identificador para recuperar el identificador del plan de acceso de la estructura. El identificador envía al origen de datos para indicar el plan que desee ejecutar.  
  
 ODBC tiene dos niveles de identificadores: identificadores de administrador de controladores e identificadores de controlador. La aplicación utiliza identificadores de administrador de controladores al llamar a funciones ODBC porque llama a estas funciones en el Administrador de controladores. El Administrador de controladores usa este identificador para buscar el identificador de controlador correspondiente y usa el identificador de controlador cuando se llama a la función en el controlador. Para obtener un ejemplo de cómo se usan los controladores y los identificadores del Administrador de controladores, consulte [rol del Administrador de controladores en el proceso de conexión](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md).  
  
 Que hay dos niveles de identificadores es un artefacto de la arquitectura ODBC; en la mayoría de los casos, no es relevante para la aplicación o el controlador. Aunque por lo general, no hay ninguna razón para hacerlo, es posible que la aplicación para determinar los identificadores de controlador mediante una llamada a **SQLGetInfo**.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Identificadores de entorno](../../../odbc/reference/develop-app/environment-handles.md)  
  
-   [Identificadores de conexión](../../../odbc/reference/develop-app/connection-handles.md)  
  
-   [Identificadores de instrucciones](../../../odbc/reference/develop-app/statement-handles.md)  
  
-   [Identificadores de descriptor](../../../odbc/reference/develop-app/descriptor-handles.md)  
  
-   [Transiciones de estado](../../../odbc/reference/develop-app/state-transitions.md)
