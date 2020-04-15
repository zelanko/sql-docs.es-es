---
title: Parámetros de la declaración ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- statement parameters [ODBC]
ms.assetid: 58d5b166-2578-4699-a560-1f1e6d86c49a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 02327ff4bb6a1ac3ac57fbf7d3c6b09b70c11534
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306826"
---
# <a name="statement-parameters"></a>Parámetros de la instrucción
Un *parámetro* es una variable en una instrucción SQL. Por ejemplo, supongamos que una tabla Parts tiene columnas denominadas PartID, Description y Price. Para agregar una pieza sin parámetros sería necesario construir una instrucción SQL como:  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (2100, 'Drive shaft', 50.00)  
```  
  
 Aunque esta instrucción inserta un nuevo orden, no es una buena solución para una aplicación de entrada de pedidos porque los valores que se van a insertar no se pueden codificar de forma rígida en la aplicación. Una alternativa es construir la instrucción SQL en tiempo de ejecución, utilizando los valores que se van a insertar. Tampoco es una buena solución, debido a la complejidad de la construcción de instrucciones en tiempo de ejecución. La mejor solución es reemplazar los elementos de la cláusula **VALUES** por signos de interrogación (?), o marcadores de *parámetros:*  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 Los marcadores de parámetros se enlazan a variables de aplicación. Para agregar una nueva fila, la aplicación solo tiene que establecer los valores de las variables y ejecutar la instrucción. Después, el controlador recupera los valores actuales de las variables y los envía al origen de datos. Si la instrucción se ejecutará varias veces, la aplicación puede hacer que el proceso sea aún más eficaz preparando la instrucción.  
  
 La instrucción que se muestra puede estar codificada de forma rígida en una aplicación de entrada de pedido para insertar una nueva fila. Sin embargo, los marcadores de parámetros no se limitan a aplicaciones verticales. Para cualquier aplicación, alivian la dificultad de construir instrucciones SQL en tiempo de ejecución evitando conversiones hacia y desde texto. Por ejemplo, lo más probable es que el ID de pieza que se muestra se almacene en la aplicación como un entero. Si la instrucción SQL se construye sin marcadores de parámetro, la aplicación debe convertir el identificador de pieza en texto y el origen de datos debe convertirlo de nuevo en un entero. Mediante el uso de un marcador de parámetro, la aplicación puede enviar el identificador de pieza al controlador como un entero, que normalmente puede enviarlo al origen de datos como un entero. Esto ahorra dos conversiones. Para los valores de datos largos, esto es muy importante, porque las formas de texto de estos valores superan con frecuencia la longitud permitida de una instrucción SQL.  
  
 Los parámetros solo son válidos en determinados lugares de instrucciones SQL. Por ejemplo, no se permiten en la lista de selección (la lista de columnas que se va a devolver mediante una instrucción **SELECT),** ni se permiten como ambos operandos de un operador binario, como el signo igual ( ) porque sería imposible determinar el tipo de parámetro. Por lo general, los parámetros solo son válidos en instrucciones de lenguaje de manipulación de datos (DML) y no en instrucciones de lenguaje de definición de datos (DDL). Para obtener más información, consulte Marcadores de [parámetros](../../../odbc/reference/appendixes/parameter-markers.md) en el Apéndice C: Gramática SQL.  
  
 Cuando la instrucción SQL invoca un procedimiento, se pueden utilizar parámetros con nombre. Los parámetros con nombre se identifican por sus nombres, no por su posición en la instrucción SQL. Se pueden enlazar mediante una llamada a **SQLBindParameter**, pero el parámetro se identifica mediante el campo SQL_DESC_NAME de la IPD (descriptor de parámetro de implementación), no mediante el *ParameterNumber* argumento de **SQLBindParameter**. También se pueden enlazar llamando a **SQLSetDescField** o **SQLSetDescRec**. Para obtener más información acerca de los parámetros con nombre, vea parámetros de [enlace por nombre (parámetros con nombre)](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md), más adelante en esta sección. Para obtener más información acerca de los descriptores, consulte [Descriptores](../../../odbc/reference/develop-app/descriptors.md).  
  
 Esta sección contiene los temas siguientes.  
  
-   [Enlazar parámetros](../../../odbc/reference/develop-app/binding-parameters-odbc.md)  
  
-   [Establecer valores de parámetro](../../../odbc/reference/develop-app/setting-parameter-values.md)  
  
-   [Enviar datos de tipo Long](../../../odbc/reference/develop-app/sending-long-data.md)  
  
-   [Recuperación de parámetros de salida por SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)  
  
-   [Parámetros de procedimiento](../../../odbc/reference/develop-app/procedure-parameters.md)  
  
-   [Matrices de valores de parámetro](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)
