---
title: Parámetros de enlace por nombre (parámetros con nombre) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- named parameters [ODBC]
- binding parameters by name [ODBC]
ms.assetid: e2c3da5a-6c10-4dd5-acf9-e951eea71a6b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a1e214f50488c4600ed39f76e91618cc5ce53de4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306376"
---
# <a name="binding-parameters-by-name-named-parameters"></a>Enlazar parámetros por nombre (parámetros con nombre)
Algunos DBMS permiten a una aplicación especificar los parámetros de un procedimiento almacenado por nombre en lugar de por posición en la llamada al procedimiento. Estos parámetros se denominan *parámetros con nombre.* ODBC admite el uso de parámetros con nombre. En ODBC, los parámetros con nombre solo se usan en llamadas a procedimientos almacenados y no se pueden usar en otras instrucciones SQL.  
  
 El controlador comprueba el valor del campo SQL_DESC_UNNAMED de la IPD para determinar si se utilizan parámetros con nombre. Si SQL_DESC_UNNAMED no está establecido en SQL_UNNAMED, el controlador utiliza el nombre en el campo SQL_DESC_NAME de la IPD para identificar el parámetro. Para enlazar el parámetro, una aplicación puede llamar a **SQLBindParameter** para especificar la información del parámetro y, a continuación, puede llamar a **SQLSetDescField** para establecer el SQL_DESC_NAME campo de la IPD. Cuando se utilizan parámetros con nombre, el orden del parámetro en la llamada a procedimiento no es importante y se omite el número de registro del parámetro.  
  
 La diferencia entre los parámetros sin nombre y los parámetros con nombre está en la relación entre el número de registro del descriptor y el número de parámetro en el procedimiento. Cuando se utilizan parámetros sin nombre, el primer marcador de parámetro está relacionado con el primer registro en el descriptor de parámetro, que a su vez está relacionado con el primer parámetro (en orden de creación) en la llamada al procedimiento. Cuando se utilizan parámetros con nombre, el primer marcador de parámetro sigue estando relacionado con el primer registro del descriptor de parámetro, pero la relación entre el número de registro del descriptor y el número de parámetro en el procedimiento ya no existe. Los parámetros con nombre no utilizan la asignación del número de registro descriptor a la posición del parámetro de procedimiento; en su lugar, el nombre del registro descriptor se asigna al nombre del parámetro de procedimiento.  
  
> [!NOTE]  
>  Si la población automática de la IPD está habilitada, el controlador rellenará el descriptor de modo que el orden de los registros descriptores coincida con el orden de los parámetros en la definición del procedimiento, incluso si se utilizan parámetros con nombre.  
  
 Si se utiliza un parámetro con nombre, todos los parámetros deben denominarse parámetros. Si cualquier parámetro no es un parámetro con nombre, ninguno de los parámetros ca se denominará parámetros. Si hubiera una mezcla de parámetros con nombre y parámetros sin nombre, el comportamiento dependería del controlador.  
  
 Como ejemplo de parámetros con nombre, supongamos que un procedimiento almacenado de SQL ServerSQL Server se ha definido de la siguiente manera:  
  
```  
CREATE PROCEDURE test @title_id int = 1, @quote char(30) AS <blah>  
```  
  
 En este procedimiento, el @title_idprimer parámetro, , tiene un valor predeterminado de 1. Una aplicación puede usar el código siguiente para invocar este procedimiento de modo que especifique solo un parámetro dinámico. Este parámetro es un parámetro\@con nombre con el nombre " quote".  
  
```  
// Prepare the procedure invocation statement.  
SQLPrepare(hstmt, "{call test(?)}", SQL_NTS);  
  
// Populate record 1 of ipd.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR,  
                  30, 0, szQuote, 0, &cbValue);  
  
// Get ipd handle and set the SQL_DESC_NAMED and SQL_DESC_UNNAMED fields  
// for record #1.  
SQLGetStmtAttr(hstmt, SQL_ATTR_IMP_PARAM_DESC, &hIpd, 0, 0);  
SQLSetDescField(hIpd, 1, SQL_DESC_NAME, "@quote", SQL_NTS);  
  
// Assuming that szQuote has been appropriately initialized,  
// execute.  
SQLExecute(hstmt);  
```
