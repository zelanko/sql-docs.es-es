---
title: Los cursores dinámicos de ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], dynamic
- dynamic cursors [ODBC]
ms.assetid: de709fd3-9eb2-44e1-a2f0-786e2b9602a6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 64215cff750e39dc78ad1a695bbe553d900f4120
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52541871"
---
# <a name="odbc-dynamic-cursors"></a>Cursores dinámicos de ODBC
Un cursor dinámico es justamente eso: dinámica. Puede detectar los cambios realizados en la pertenencia, el orden y los valores del conjunto una vez abierto el cursor de resultados. Por ejemplo, suponga que un cursor dinámico obtiene dos filas y otra aplicación, a continuación, actualiza una de esas filas y elimina la otra. Si el cursor dinámico, a continuación, intenta volver a obtener esas filas, no encontrará la fila eliminada pero devolverá los nuevos valores de la fila actualizada.  
  
 Los cursores dinámicos detectan todas las actualizaciones, eliminaciones e inserciones, tanto sus propios y los realizados por otros usuarios. (Esto está sujeto al aislamiento de nivel de la transacción, según lo establecido por el atributo de conexión SQL_ATTR_TXN_ISOLATION.) La matriz de Estados de fila especificada por el atributo de instrucción SQL_ATTR_ROW_STATUS_PTR refleja estos cambios y puede contener SQL_ROW_SUCCESS, SQL_ROW_SUCCESS_WITH_INFO, SQL_ROW_ERROR, SQL_ROW_UPDATED y SQL_ROW_ADDED. No se devolverá SQL_ROW_DELETED porque un cursor dinámico no devuelve las filas eliminadas fuera del conjunto de filas y, por tanto, ya no reconoce la existencia de la fila eliminada en el conjunto de resultados o su elemento correspondiente en la matriz de Estados de fila. SQL_ROW_ADDED solo se devuelve cuando se actualiza una fila mediante una llamada a **SQLSetPos**, no cuando se actualiza mediante otro cursor.  
  
 Una manera de implementar los cursores dinámicos de la base de datos está creando un índice selectivo que define la pertenencia y ordenación del resultado establecida. Dado que el índice se actualiza cuando otros usuarios realizan cambios, un cursor basado en ese índice es sensible a todos los cambios. Selección adicional en el conjunto de resultados definido por este índice es posible mediante el procesamiento a lo largo del índice.  
  
 Los cursores dinámicos se pueden simular exigiendo el resultado se ordenen por una clave única. Con estas restricciones, se realizan búsquedas mediante la ejecución de un **seleccione** cada vez que el cursor recupera las filas de la instrucción. Por ejemplo, supongamos que se define el conjunto de resultados mediante esta instrucción:  
  
```  
SELECT * FROM Customers ORDER BY Name, CustID  
```  
  
 Para capturar el siguiente conjunto de filas en este conjunto de resultados, el cursor simulado establece los parámetros en la siguiente **seleccione** instrucción a los valores de la última fila del conjunto de filas actual y, a continuación, se ejecuta:  
  
```  
SELECT * FROM Customers WHERE (Name > ?) AND (CustID > ?)  
   ORDER BY Name, CustID  
```  
  
 Esta instrucción crea un segundo conjunto de resultados, el primer conjunto de filas de los cuales es el siguiente conjunto de filas en el conjunto de resultados original - en este caso, el conjunto de filas en la tabla Customers. El cursor devuelve este conjunto de filas a la aplicación.  
  
 Es interesante tener en cuenta que un cursor dinámico implementado de esta manera realmente crea muchos conjuntos de resultados, que le permite detectar los cambios realizados en el conjunto de resultados original. La aplicación nunca se entera de la existencia de estos conjuntos de resultados auxiliar; simplemente aparece como si el cursor es capaz de detectar los cambios realizados en el conjunto de resultados original.
