---
title: Simulación de las declaraciones de actualización y eliminación posicionadas de la aplicación de la aplicación de la aplicación de la aplicación de la aplicación de la aplicación de Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- positioned deletes [ODBC]
- data updates [ODBC], positioned update or delete
- row identifiers [ODBC]
- positioned updates [ODBC]
- updating data [ODBC], positioned update or delete
ms.assetid: b24ed59f-f25b-4646-a135-5f3596abc1a4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e1eb498a99180d145147e67c8955eeb7a0027024
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301996"
---
# <a name="simulating-positioned-update-and-delete-statements"></a>Simulación de actualización por posición y las instrucciones Delete
Si el origen de datos no admite instrucciones de actualización y eliminación posicionadas, el controlador puede simularlas. Por ejemplo, la biblioteca de cursores ODBC simula instrucciones de actualización y eliminación posicionadas. La estrategia general para simular instrucciones de actualización y eliminación posicionadas consiste en convertir instrucciones posicionadas en las buscadas. Esto se hace reemplazando la cláusula **WHERE CURRENT OF** por una cláusula **WHERE** buscada que identifica la fila actual.  
  
 Por ejemplo, dado que la columna CustID identifica de forma única cada fila de la tabla Customers, la instrucción delete posicionada  
  
```  
DELETE FROM Customers WHERE CURRENT OF CustCursor  
```  
  
 podría convertirse a  
  
```  
DELETE FROM Customers WHERE (CustID = ?)  
```  
  
 El controlador puede utilizar uno de los siguientes *identificadores* de fila en la cláusula **WHERE:**  
  
-   Columnas cuyos valores sirven para identificar de forma única cada fila de la tabla. Por ejemplo, llamar a **SQLSpecialColumns** con SQL_BEST_ROWID devuelve la columna o conjunto óptimo de columnas que sirven a este propósito.  
  
-   Pseudocolumnas, proporcionadas por algunos orígenes de datos, con el fin de identificar de forma única cada fila. También se pueden recuperar llamando a **SQLSpecialColumns**.  
  
-   Un índice único, si está disponible.  
  
-   Todas las columnas del conjunto de resultados.  
  
 Exactamente qué columnas debe usar un controlador en la cláusula **WHERE** que construye depende del controlador. En algunos orígenes de datos, determinar un identificador de fila puede ser costoso. Sin embargo, es más rápido ejecutar y garantiza que una instrucción simulada se actualiza o elimina como máximo una fila. Dependiendo de las capacidades del DBMS subyacente, el uso de un identificador de fila puede ser costoso de configurar. Sin embargo, es más rápido ejecutar y garantiza que una instrucción simulada actualizará o eliminará solo una fila. La opción de usar todas las columnas del conjunto de resultados suele ser mucho más fácil de configurar. Sin embargo, es más lento ejecutar y, si las columnas no identifican de forma exclusiva una fila, puede provocar que las filas se actualicen o eliminen involuntariamente, especialmente cuando la lista de selección para el conjunto de resultados no contiene todas las columnas que existen en la tabla subyacente.  
  
 Dependiendo de cuál de las estrategias anteriores admite el controlador, una aplicación puede elegir qué estrategia desea que utilice el controlador con el atributo de instrucción SQL_ATTR_SIMULATE_CURSOR. Aunque puede parecer extraño que una aplicación corra el riesgo de actualizar o eliminar involuntariamente una fila, la aplicación puede quitar este riesgo asegurándose de que las columnas del conjunto de resultados identifican de forma única cada fila del conjunto de resultados. Esto ahorra al conductor el esfuerzo de tener que hacer esto.  
  
 Si el controlador decide usar un identificador de fila, intercepta la instrucción **SELECT FOR UPDATE** que crea el conjunto de resultados. Si las columnas de la lista de selección no identifican eficazmente una fila, el controlador agrega las columnas necesarias al final de la lista de selección. Algunos orígenes de datos tienen una sola columna que siempre identifica de forma única una fila, como la columna ROWID en Oracle; si una columna de este tipo está disponible, el controlador utiliza esto. De lo contrario, el controlador llama a **SQLSpecialColumns** para cada tabla de la cláusula **FROM** para recuperar una lista de las columnas que identifican de forma única cada fila. Una restricción común que resulta de esta técnica es que se produce un error en la simulación de cursor si hay más de una tabla en la cláusula **FROM.**  
  
 Independientemente de cómo identifique el controlador de filas, normalmente quita la cláusula **FOR UPDATE OF** de la instrucción SELECT FOR **UPDATE** antes de enviarla al origen de datos. La cláusula **FOR UPDATE OF** solo se utiliza con instrucciones de actualización y eliminación posicionadas. Los orígenes de datos que no admiten instrucciones de actualización y eliminación posicionadas generalmente no lo admiten.  
  
 Cuando la aplicación envía una instrucción de actualización o eliminación posicionada para su ejecución, el controlador reemplaza la cláusula **WHERE CURRENT OF** por una cláusula **WHERE** que contiene el identificador de fila. Los valores de estas columnas se recuperan de una memoria caché mantenida por el controlador para cada columna que utiliza en la cláusula **WHERE.** Después de que el controlador ha reemplazado la cláusula **WHERE,** envía la instrucción al origen de datos para su ejecución.  
  
 Por ejemplo, supongamos que la aplicación envía la siguiente instrucción para crear un conjunto de resultados:  
  
```  
SELECT Name, Address, Phone FROM Customers FOR UPDATE OF Phone, Address  
```  
  
 Si la aplicación ha establecido SQL_ATTR_SIMULATE_CURSOR para solicitar una garantía de unicidad y si el origen de datos no proporciona una pseudocolumna que siempre identifica de forma única una fila, el controlador llama a **SQLSpecialColumns** para la tabla Customers, descubre que CustID es la clave de la tabla Customers y la agrega a la lista de selección y elimina la cláusula **FOR UPDATE OF:**  
  
```  
SELECT Name, Address, Phone, CustID FROM Customers  
```  
  
 Si la aplicación no ha solicitado una garantía de unicidad, el conductor sólo elimina la cláusula **FOR UPDATE OF:**  
  
```  
SELECT Name, Address, Phone FROM Customers  
```  
  
 Supongamos que la aplicación se desplaza por el conjunto de resultados y envía la siguiente instrucción de actualización posicionada para su ejecución, donde Cust es el nombre del cursor sobre el conjunto de resultados:  
  
```  
UPDATE Customers SET Address = ?, Phone = ? WHERE CURRENT OF Cust  
```  
  
 Si la aplicación no ha solicitado una garantía de unicidad, el controlador reemplaza la cláusula **WHERE** y enlaza el parámetro CustID a la variable en su caché:  
  
```  
UPDATE Customers SET Address = ?, Phone = ? WHERE (CustID = ?)  
```  
  
 Si la aplicación no ha solicitado una garantía de unicidad, el controlador reemplaza la cláusula **WHERE** y enlaza los parámetros Name, Address y Phone de esta cláusula a las variables de su caché:  
  
```  
UPDATE Customers SET Address = ?, Phone = ?  
   WHERE (Name = ?) AND (Address = ?) AND (Phone = ?)  
```
