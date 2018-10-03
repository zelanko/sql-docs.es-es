---
title: Parámetros de la instrucción | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b366ddd7a665112e6b40b814b13037a517d623a5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47648873"
---
# <a name="statement-parameters"></a>Parámetros de la instrucción
Un *parámetro* es una variable en una instrucción SQL. Por ejemplo, suponga que una tabla de piezas tiene las columnas PartID, descripción y precio. Para agregar un elemento sin parámetros requeriría la construcción de una instrucción SQL, como:  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (2100, 'Drive shaft', 50.00)  
```  
  
 Aunque esta instrucción inserta un nuevo pedido, no es una buena solución para una aplicación de entrada de pedidos porque los valores que se va a insertar no pueden ser codificados de forma rígida en la aplicación. Una alternativa es crear la instrucción SQL en tiempo de ejecución utilizando los valores que para se va a insertar. Esto tampoco es una buena solución, dada la complejidad de las instrucciones de creación en tiempo de ejecución. La mejor solución consiste en reemplazar los elementos de la **valores** cláusula con signos de interrogación (?), o *marcadores de parámetros*:  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 Los marcadores de parámetros se enlazan a variables de aplicación. Para agregar una nueva fila, la aplicación tiene solo establecer los valores de las variables y ejecute la instrucción. Después, el controlador recupera los valores actuales de las variables y los envía al origen de datos. Si la instrucción se ejecutará varias veces, la aplicación puede realizar el proceso aún más eficaz al preparar la instrucción.  
  
 La instrucción muestra podría ser codificados de forma rígida en una aplicación de entrada de pedidos para insertar una fila nueva. Sin embargo, los marcadores de parámetros no están limitados a aplicaciones verticales. Para cualquier aplicación, estos facilitan la dificultad de crear instrucciones SQL en tiempo de ejecución, ya que evita las conversiones a y de texto. Por ejemplo, solo se muestra el Id. de parte es más probable es que almacena en la aplicación como un entero. Si la instrucción SQL se construye sin marcadores de parámetros, la aplicación debe convertir el Id. de la parte a texto y el origen de datos debe convertir a un entero. Mediante el uso de un marcador de parámetro, la aplicación puede enviar el Id. de parte del controlador como un entero, que normalmente puede enviarlo al origen de datos como un entero. Esto ahorra dos conversiones. Para los valores de datos grandes, esto es muy importante, porque las formas de texto de estos valores con frecuencia superan la longitud permitida de una instrucción SQL.  
  
 Los parámetros solo son válidos en ciertos lugares en las instrucciones SQL. Por ejemplo, no se permiten en la lista de selección (la lista de columnas que va a devolver un **seleccione** instrucción), ni se pueden utilizar como ambos operandos de un operador binario como el signo igual (=), porque sería imposible determinar el tipo de parámetro. Por lo general, los parámetros son válidos únicamente en las instrucciones de lenguaje de manipulación de datos (DML) y no en las instrucciones de lenguaje de definición de datos (DDL). Para obtener más información, consulte [marcadores de parámetros](../../../odbc/reference/appendixes/parameter-markers.md) en Apéndice C: SQL gramática.  
  
 Puede usarse cuando la instrucción SQL invoca un procedimiento, parámetros con nombre. Parámetros con nombre se identifican por sus nombres, no por su posición en la instrucción SQL. Se puede enlazar mediante una llamada a **SQLBindParameter**, pero el parámetro identificado por el campo SQL_DESC_NAME de la IPD (descriptor de parámetro de implementación), no por la *ParameterNumber* argumento de **SQLBindParameter**. También pueden estar enlazadas mediante una llamada a **SQLSetDescField** o **SQLSetDescRec**. Para obtener más información acerca de los parámetros con nombre, vea [enlazar parámetros por nombre (parámetros con nombre)](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md), más adelante en esta sección. Para obtener más información acerca de los descriptores, consulte [descriptores](../../../odbc/reference/develop-app/descriptors.md).  
  
 Esta sección contiene los temas siguientes.  
  
-   [Enlazar parámetros](../../../odbc/reference/develop-app/binding-parameters-odbc.md)  
  
-   [Establecer valores de parámetro](../../../odbc/reference/develop-app/setting-parameter-values.md)  
  
-   [Enviar datos de tipo Long](../../../odbc/reference/develop-app/sending-long-data.md)  
  
-   [Recuperar parámetros de salida mediante SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)  
  
-   [Parámetros de procedimiento](../../../odbc/reference/develop-app/procedure-parameters.md)  
  
-   [Matrices de valores de parámetro](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)
