---
title: Simulando instrucciones Update y DELETE posicionadas | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301996"
---
# <a name="simulating-positioned-update-and-delete-statements"></a>Simulación de actualización por posición y las instrucciones Delete
Si el origen de datos no admite instrucciones Update y DELETE posicionadas, el controlador puede simularlas. Por ejemplo, la biblioteca de cursores ODBC simula las instrucciones Update y DELETE posicionadas. La estrategia general para simular instrucciones Update y DELETE posicionadas es convertir las instrucciones posicionadas en las que se buscan. Esto se hace reemplazando la cláusula **WHERE CURRENT of** por una cláusula **Where** de búsqueda que identifica la fila actual.  
  
 Por ejemplo, dado que la columna CustID identifica de forma única cada fila de la tabla Customers, la instrucción Delete posicionada  
  
```  
DELETE FROM Customers WHERE CURRENT OF CustCursor  
```  
  
 se puede convertir en  
  
```  
DELETE FROM Customers WHERE (CustID = ?)  
```  
  
 El controlador puede usar uno de los siguientes *identificadores de fila* en la cláusula **Where** :  
  
-   Columnas cuyos valores sirven para identificar de forma única cada fila de la tabla. Por ejemplo, al llamar a **SQLSpecialColumns** con SQL_BEST_ROWID se devuelve la columna óptima o el conjunto de columnas que sirven para este propósito.  
  
-   Pseudo columnas, proporcionadas por algunos orígenes de datos, con el fin de identificar de forma única cada fila. También se pueden recuperar llamando a **SQLSpecialColumns**.  
  
-   Índice único, si está disponible.  
  
-   Todas las columnas del conjunto de resultados.  
  
 Exactamente qué columnas debe usar un controlador en la cláusula **Where** que crea depende del controlador. En algunos orígenes de datos, la determinación de un identificador de fila puede ser costosa. Sin embargo, es más rápido ejecutar y garantiza que una instrucción simulada actualiza o elimina como máximo una fila. En función de las capacidades del DBMS subyacente, el uso de un identificador de fila puede ser caro de configurar. Sin embargo, es más rápido ejecutar y garantiza que una instrucción simulada actualizará o eliminará una sola fila. La opción de usar todas las columnas del conjunto de resultados suele ser mucho más fácil de configurar. Sin embargo, es más lento ejecutar y, si las columnas no identifican de forma única una fila, pueden provocar que las filas se actualicen o eliminen involuntariamente, especialmente cuando la lista de selección para el conjunto de resultados no contenga todas las columnas que existen en la tabla subyacente.  
  
 En función de las estrategias anteriores que admita el controlador, una aplicación puede elegir qué estrategia desea que use el controlador con el atributo de instrucción SQL_ATTR_SIMULATE_CURSOR. Aunque puede parecer extraño que una aplicación se arriesga a la actualización o eliminación accidental de una fila, la aplicación puede eliminar este riesgo asegurándose de que las columnas del conjunto de resultados identifican de forma única cada fila del conjunto de resultados. Esto evita que el controlador tenga que hacerlo.  
  
 Si el controlador elige usar un identificador de fila, intercepta la instrucción **Select for update** que crea el conjunto de resultados. Si las columnas de la lista de selección no identifican de forma eficaz una fila, el controlador agrega las columnas necesarias al final de la lista de selección. Algunos orígenes de datos tienen una única columna que siempre identifica de forma única una fila, como la columna ROWID en Oracle. Si este tipo de columna está disponible, el controlador lo utiliza. De lo contrario, el controlador llama a **SQLSpecialColumns** para cada tabla de la cláusula **from** para recuperar una lista de las columnas que identifican de forma única cada fila. Una restricción común que se obtiene de esta técnica es que se produce un error en la simulación de cursor si hay más de una tabla en la cláusula **from** .  
  
 Independientemente de cómo el controlador identifique las filas, normalmente elimina la cláusula **for update OF de** la instrucción **Select for update** antes de enviarla al origen de datos. La cláusula **for Update of** solo se usa con las instrucciones Update y DELETE posicionadas. Los orígenes de datos que no admiten las instrucciones Update y DELETE posicionadas no lo admiten normalmente.  
  
 Cuando la aplicación envía una instrucción UPDATE o DELETE posicionada para su ejecución, el controlador reemplaza la cláusula **WHERE CURRENT of** por una cláusula **Where** que contiene el identificador de fila. Los valores de estas columnas se recuperan de una caché mantenida por el controlador para cada columna que utiliza en la cláusula **Where** . Una vez que el controlador ha reemplazado la cláusula **Where** , envía la instrucción al origen de datos para su ejecución.  
  
 Por ejemplo, supongamos que la aplicación envía la instrucción siguiente para crear un conjunto de resultados:  
  
```  
SELECT Name, Address, Phone FROM Customers FOR UPDATE OF Phone, Address  
```  
  
 Si la aplicación ha establecido SQL_ATTR_SIMULATE_CURSOR para solicitar una garantía de unicidad y si el origen de datos no proporciona una pseudocolumna que siempre identifique de forma única una fila, el controlador llama a **SQLSpecialColumns** para la tabla Customers, detecta que CustID es la clave para la tabla Customers y lo agrega a la lista de selección, y elimina la cláusula **for Update of** :  
  
```  
SELECT Name, Address, Phone, CustID FROM Customers  
```  
  
 Si la aplicación no ha solicitado una garantía de unicidad, el controlador solo quita la cláusula **for Update of** :  
  
```  
SELECT Name, Address, Phone FROM Customers  
```  
  
 Supongamos que la aplicación se desplaza por el conjunto de resultados y envía la siguiente instrucción de actualización posicionada para su ejecución, donde Cust es el nombre del cursor sobre el conjunto de resultados:  
  
```  
UPDATE Customers SET Address = ?, Phone = ? WHERE CURRENT OF Cust  
```  
  
 Si la aplicación no ha solicitado una garantía de unicidad, el controlador reemplaza la cláusula **Where** y enlaza el parámetro CustID a la variable en su caché:  
  
```  
UPDATE Customers SET Address = ?, Phone = ? WHERE (CustID = ?)  
```  
  
 Si la aplicación no ha solicitado una garantía de unicidad, el controlador reemplaza la cláusula **Where** y enlaza los parámetros de nombre, dirección y teléfono de esta cláusula con las variables de su caché:  
  
```  
UPDATE Customers SET Address = ?, Phone = ?  
   WHERE (Name = ?) AND (Address = ?) AND (Phone = ?)  
```
