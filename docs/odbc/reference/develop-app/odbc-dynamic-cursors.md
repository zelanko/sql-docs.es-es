---
description: Cursores dinámicos de ODBC
title: Cursores dinámicos de ODBC | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 19ae15a211329e07fdab13a5b6ff40e210e97cb5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429197"
---
# <a name="odbc-dynamic-cursors"></a>Cursores dinámicos de ODBC
Un cursor dinámico es simplemente eso: Dynamic. Puede detectar cualquier cambio realizado en la pertenencia, el orden y los valores del conjunto de resultados después de abrir el cursor. Por ejemplo, suponga que un cursor dinámico captura dos filas y después otra aplicación actualiza una de esas filas y elimina la otra. Si el cursor dinámico intenta volver a capturar esas filas, no encontrará la fila eliminada, pero devolverá los nuevos valores de la fila actualizada.  
  
 Los cursores dinámicos detectan todas las actualizaciones, eliminaciones e inserciones, las suyas propias y las realizadas por otros usuarios. (Esto está sujeto al nivel de aislamiento de la transacción, según lo establecido por el atributo de conexión SQL_ATTR_TXN_ISOLATION). La matriz de estado de fila especificada por el atributo de instrucción SQL_ATTR_ROW_STATUS_PTR refleja estos cambios y puede contener SQL_ROW_SUCCESS, SQL_ROW_SUCCESS_WITH_INFO, SQL_ROW_ERROR, SQL_ROW_UPDATED y SQL_ROW_ADDED. No puede devolver SQL_ROW_DELETED porque un cursor dinámico no devuelve filas eliminadas fuera del conjunto de filas y, por tanto, ya no reconoce la existencia de la fila eliminada en el conjunto de resultados o su elemento correspondiente en la matriz de estado de fila. SQL_ROW_ADDED solo se devuelve cuando una fila se actualiza mediante una llamada a **SQLSetPos**, no cuando se actualiza mediante otro cursor.  
  
 Una manera de implementar cursores dinámicos en la base de datos es mediante la creación de un índice selectivo que define la pertenencia y el orden del conjunto de resultados. Dado que el índice se actualiza cuando otros usuarios realizan cambios, un cursor basado en dicho índice es sensible a todos los cambios. La selección adicional en el conjunto de resultados definido por este índice es posible mediante el procesamiento a lo largo del índice.  
  
 Los cursores dinámicos se pueden simular requiriendo que el conjunto de resultados se ordene por una clave única. Con este tipo de restricción, las capturas se realizan ejecutando una instrucción **Select** cada vez que el cursor captura filas. Por ejemplo, supongamos que el conjunto de resultados se define con esta instrucción:  
  
```  
SELECT * FROM Customers ORDER BY Name, CustID  
```  
  
 Para capturar el siguiente conjunto de filas de este conjunto de resultados, el cursor simulado establece los parámetros de la siguiente instrucción **Select** en los valores de la última fila del conjunto de filas actual y, a continuación, lo ejecuta:  
  
```  
SELECT * FROM Customers WHERE (Name > ?) AND (CustID > ?)  
   ORDER BY Name, CustID  
```  
  
 Esta instrucción crea un segundo conjunto de resultados, el primer conjunto de filas de que es el siguiente conjunto de filas del conjunto de resultados original; en este caso, el conjunto de filas de la tabla customers. El cursor devuelve este conjunto de filas a la aplicación.  
  
 Es interesante tener en cuenta que un cursor dinámico implementado de esta manera crea realmente muchos conjuntos de resultados, lo que permite detectar los cambios en el conjunto de resultados original. La aplicación nunca aprende la existencia de estos conjuntos de resultados auxiliares; simplemente aparece como si el cursor pudiera detectar cambios en el conjunto de resultados original.
