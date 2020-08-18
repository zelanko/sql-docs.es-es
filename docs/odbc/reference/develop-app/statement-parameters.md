---
description: Parámetros de la instrucción
title: Parámetros de instrucción | Microsoft Docs
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
ms.openlocfilehash: 7400367d4b237d2d0e22c6363d1559eb89506d7d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482904"
---
# <a name="statement-parameters"></a>Parámetros de la instrucción
Un *parámetro* es una variable de una instrucción SQL. Por ejemplo, supongamos que una tabla de piezas tiene columnas denominadas el nombre del campo, la descripción y el precio. Para agregar un elemento sin parámetros, es necesario construir una instrucción SQL como:  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (2100, 'Drive shaft', 50.00)  
```  
  
 Aunque esta instrucción inserta un nuevo pedido, no es una buena solución para una aplicación de entrada de pedidos porque los valores que se van a insertar no se pueden codificar de forma rígida en la aplicación. Una alternativa consiste en construir la instrucción SQL en tiempo de ejecución, utilizando los valores que se van a insertar. Esto tampoco es una buena solución, debido a la complejidad de construir instrucciones en tiempo de ejecución. La mejor solución es reemplazar los elementos de la cláusula **Values** por signos de interrogación (?) o *marcadores de parámetros*:  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 Los marcadores de parámetros se enlazan a variables de aplicación. Para agregar una nueva fila, la aplicación solo tiene que establecer los valores de las variables y ejecutar la instrucción. Después, el controlador recupera los valores actuales de las variables y los envía al origen de datos. Si la instrucción se va a ejecutar varias veces, la aplicación puede hacer que el proceso sea aún más eficaz si prepara la instrucción.  
  
 La instrucción que se acaba de mostrar podría estar codificada de forma rígida en una aplicación de entrada de pedidos para insertar una nueva fila. Sin embargo, los marcadores de parámetros no se limitan a las aplicaciones verticales. Para cualquier aplicación, facilitan la dificultad de construir instrucciones SQL en tiempo de ejecución evitando las conversiones a y desde el texto. Por ejemplo, lo más probable es que el identificador de elemento que se muestra se almacene en la aplicación como un entero. Si la instrucción SQL se construye sin marcadores de parámetros, la aplicación debe convertir el ID. de elemento en texto y el origen de datos debe volver a convertirlo en un entero. Mediante el uso de un marcador de parámetro, la aplicación puede enviar el identificador de elemento al controlador como un entero, que normalmente puede enviarlo al origen de datos como un entero. Esto guarda dos conversiones. En el caso de los valores de datos largos, esto es muy importante, ya que las formas de texto de estos valores superan con frecuencia la longitud permitida de una instrucción SQL.  
  
 Los parámetros solo son válidos en determinados lugares en instrucciones SQL. Por ejemplo, no se permiten en la lista de selección (la lista de columnas que devolverá una instrucción **Select** ), ni se permiten como ambos operandos de un operador binario, como el signo igual (=), porque sería imposible determinar el tipo de parámetro. Normalmente, los parámetros solo son válidos en instrucciones de lenguaje de manipulación de datos (DML) y no en instrucciones de lenguaje de definición de datos (DDL). Para obtener más información, vea [marcadores de parámetros](../../../odbc/reference/appendixes/parameter-markers.md) en el Apéndice C: gramática de SQL.  
  
 Cuando la instrucción SQL invoca un procedimiento, se pueden usar parámetros con nombre. Los parámetros con nombre se identifican por sus nombres, no por su posición en la instrucción SQL. Se pueden enlazar mediante una llamada a **SQLBindParameter**, pero el parámetro se identifica mediante el campo SQL_DESC_NAME de IPD (descriptor de parámetros de implementación), no por el argumento *ParameterNumber* de **SQLBindParameter**. También se pueden enlazar llamando a **SQLSetDescField** o **SQLSetDescRec**. Para obtener más información sobre los parámetros con nombre, vea [enlazar parámetros por nombre (parámetros con nombre)](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md), más adelante en esta sección. Para obtener más información acerca de los descriptores, consulte [descriptores](../../../odbc/reference/develop-app/descriptors.md).  
  
 Esta sección contiene los temas siguientes.  
  
-   [Enlazar parámetros](../../../odbc/reference/develop-app/binding-parameters-odbc.md)  
  
-   [Establecer valores de parámetro](../../../odbc/reference/develop-app/setting-parameter-values.md)  
  
-   [Enviar datos de tipo Long](../../../odbc/reference/develop-app/sending-long-data.md)  
  
-   [Recuperación de parámetros de salida por SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)  
  
-   [Parámetros de procedimiento](../../../odbc/reference/develop-app/procedure-parameters.md)  
  
-   [Matrices de valores de parámetro](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)
