---
title: Simular coloca instrucciones Update y Delete | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6d98d40ae24c68f90a304edb0293febfe76fac2c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62445897"
---
# <a name="simulating-positioned-update-and-delete-statements"></a>Simulación de actualización por posición y las instrucciones Delete
Si el origen de datos no admite actualización posicionada e instrucciones delete, el controlador puede simular estos. Por ejemplo, la biblioteca de cursores ODBC simula actualización posicionada y eliminar las instrucciones. La estrategia general para simular instrucciones posicionada update y delete es convertir instrucciones posicionadas a que se busca. Para ello, reemplace el **WHERE CURRENT OF** cláusula con una búsqueda **donde** cláusula que identifica la fila actual.  
  
 Por ejemplo, porque la columna CustID identifica de forma única cada fila de la tabla Customers, la posición delete, instrucción  
  
```  
DELETE FROM Customers WHERE CURRENT OF CustCursor  
```  
  
 se pueden convertir en  
  
```  
DELETE FROM Customers WHERE (CustID = ?)  
```  
  
 El controlador puede usar uno de los siguientes *identificadores de fila* en el **donde** cláusula:  
  
-   Columnas cuyos valores sirven para identificar de forma única cada fila de la tabla. Por ejemplo, al llamar a **SQLSpecialColumns** con SQL_BEST_ROWID devuelve la columna óptima o el conjunto de columnas que sirven para este propósito.  
  
-   Pseudocolumnas, proporcionadas por algunos orígenes de datos, con el fin de identificar de forma exclusiva cada fila. También pueden ser recuperables mediante una llamada a **SQLSpecialColumns**.  
  
-   Un índice único, si está disponible.  
  
-   Todas las columnas del conjunto de resultados.  
  
 Exactamente qué columnas debe usar un controlador en el **donde** cláusula construye depende del controlador. En algunos datos de orígenes, determinar un identificador de fila pueden ser costosos. Sin embargo, es más rápido ejecutar y garantiza que una instrucción simulada actualiza o elimina una fila como máximo. Según las capacidades del DBMS subyacente, puede ser costoso configurar mediante un identificador de fila. Sin embargo, es más rápido ejecutar y garantiza que una instrucción simulada actualizará o eliminará una única fila. Es normalmente mucho más fácil configurar la opción de usar todas las columnas del conjunto de resultados. Sin embargo, es más lento ejecutar y, si las columnas no identificar inequívocamente una fila, puede dar lugar a las filas que se va a actualizar o eliminar de forma no intencionada, especialmente cuando se establece la lista de selección para el resultado no contiene todas las columnas que existen en la tabla subyacente.  
  
 Dependiendo de cuál de las estrategias anteriores el controlador admite, una aplicación puede decidir qué estrategia quiere que el controlador que se utilizará con el atributo de instrucción SQL_ATTR_SIMULATE_CURSOR. Aunque puede parecer extraño para una aplicación para que el riesgo de forma no intencionada, actualizar o eliminar una fila, la aplicación puede quitar este riesgo asegurándose de que las columnas del conjunto de resultados identifican de forma única cada fila del conjunto de resultados. Esto guarda al controlador en el esfuerzo de tener que hacerlo.  
  
 Si el controlador decide usar un identificador de fila, intercepta el **SELECT FOR UPDATE** instrucción que crea el conjunto de resultados. Si las columnas de la lista de selección no detectar de manera eficaz una fila, el controlador agrega las columnas necesarias al final de la lista de selección. Algunos orígenes de datos tienen una sola columna que identifica siempre de una fila, como la columna ROWID en Oracle; Si este tipo de columna está disponible, el controlador lo utiliza. En caso contrario, el controlador llama a **SQLSpecialColumns** para cada tabla en la **FROM** cláusula para recuperar una lista de las columnas que identifican de forma única cada fila. Una restricción común que se origina esta técnica es que se produce un error de simulación de cursor si no hay más de una tabla en la **FROM** cláusula.  
  
 Independientemente de cómo el controlador identifica las filas, normalmente elimina el **FOR UPDATE OF** cláusula desactivado el **SELECT FOR UPDATE** instrucción antes de enviarla al origen de datos. El **FOR UPDATE OF** cláusula se utiliza únicamente con actualización por posición y eliminar las instrucciones. Orígenes de datos que no admiten la actualización por posición y las instrucciones delete por lo general no lo admiten.  
  
 Cuando la aplicación envía una actualización por posición o la instrucción delete para su ejecución, el controlador reemplaza el **WHERE CURRENT OF** cláusula con una **donde** cláusula que contiene el identificador de fila. Los valores de estas columnas se recuperan desde una caché mantenida por el controlador para cada columna utiliza en el **donde** cláusula. Después de que el controlador ha reemplazado el **donde** cláusula, envía la instrucción para el origen de datos para su ejecución.  
  
 Por ejemplo, supongamos que la aplicación envía la instrucción siguiente para crear un conjunto de resultados:  
  
```  
SELECT Name, Address, Phone FROM Customers FOR UPDATE OF Phone, Address  
```  
  
 Si la aplicación ha establecido SQL_ATTR_SIMULATE_CURSOR para solicitar una garantía de exclusividad y si el origen de datos no proporciona una pseudocolumna que siempre se identifica una fila, el controlador llama a **SQLSpecialColumns** para el La tabla Customers, descubre que CustID es la clave para la tabla Customers y agrega a la lista de selección y elimina el **FOR UPDATE OF** cláusula:  
  
```  
SELECT Name, Address, Phone, CustID FROM Customers  
```  
  
 Si la aplicación no ha solicitado una garantía de exclusividad, el controlador se elimina solo el **FOR UPDATE OF** cláusula:  
  
```  
SELECT Name, Address, Phone FROM Customers  
```  
  
 Suponga que la aplicación se desplaza por el conjunto de resultados y envía la siguiente instrucción de actualización posicionada para su ejecución, donde Cust es el nombre del cursor sobre el conjunto de resultados:  
  
```  
UPDATE Customers SET Address = ?, Phone = ? WHERE CURRENT OF Cust  
```  
  
 Si la aplicación no ha solicitado una garantía de exclusividad, el controlador reemplaza el **donde** cláusula y enlaza el parámetro CustID a la variable en la memoria caché:  
  
```  
UPDATE Customers SET Address = ?, Phone = ? WHERE (CustID = ?)  
```  
  
 Si la aplicación no ha solicitado una garantía de exclusividad, el controlador reemplaza el **donde** cláusula y enlaza los parámetros de nombre, dirección y teléfono en esta cláusula para las variables en su memoria caché:  
  
```  
UPDATE Customers SET Address = ?, Phone = ?  
   WHERE (Name = ?) AND (Address = ?) AND (Phone = ?)  
```
