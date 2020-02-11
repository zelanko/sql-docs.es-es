---
title: Enlazar parámetros por nombre (parámetros con nombre) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3fdd8d00bd6af5479079e66c1ca42f249e033d29
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68107641"
---
# <a name="binding-parameters-by-name-named-parameters"></a>Enlazar parámetros por nombre (parámetros con nombre)
Algunos DBMS permiten a una aplicación especificar los parámetros de un procedimiento almacenado por nombre en lugar de por posición en la llamada al procedimiento. Estos parámetros se denominan *parámetros con nombre*. ODBC admite el uso de parámetros con nombre. En ODBC, los parámetros con nombre solo se usan en las llamadas a procedimientos almacenados y no se pueden usar en otras instrucciones SQL.  
  
 El controlador comprueba el valor del campo de SQL_DESC_UNNAMED de IPD para determinar si se usan parámetros con nombre. Si SQL_DESC_UNNAMED no se establece en SQL_UNNAMED, el controlador usa el nombre en el campo SQL_DESC_NAME de IPD para identificar el parámetro. Para enlazar el parámetro, una aplicación puede llamar a **SQLBindParameter** para especificar la información de parámetros y, a continuación, puede llamar a **SQLSetDescField** para establecer el campo de SQL_DESC_NAME de IPD. Cuando se utilizan parámetros con nombre, el orden del parámetro en la llamada al procedimiento no es importante y se omite el número de registro del parámetro.  
  
 La diferencia entre los parámetros sin nombre y los parámetros con nombre está en la relación entre el número de registro del descriptor y el número de parámetro del procedimiento. Cuando se usan parámetros sin nombre, el primer marcador de parámetros se relaciona con el primer registro del descriptor de parámetros, que a su vez está relacionado con el primer parámetro (en el orden de creación) de la llamada a procedimiento. Cuando se utilizan parámetros con nombre, el primer marcador de parámetro sigue relacionado con el primer registro del descriptor de parámetros, pero ya no existe la relación entre el número de registro del descriptor y el número de parámetro del procedimiento. Los parámetros con nombre no usan la asignación del número de registro del descriptor en la posición del parámetro de procedimiento; en su lugar, el nombre del registro del descriptor se asigna al nombre del parámetro del procedimiento.  
  
> [!NOTE]  
>  Si está habilitado el rellenado automático de IPD, el controlador rellenará el descriptor de tal forma que el orden de los registros del descriptor coincida con el orden de los parámetros de la definición del procedimiento, incluso si se usan parámetros con nombre.  
  
 Si se usa un parámetro con nombre, todos los parámetros deben ser parámetros con nombre. Si algún parámetro no es un parámetro con nombre, ninguno de los parámetros de la entidad de certificación debe ser parámetros con nombre. Si hubiera una combinación de parámetros con nombre y parámetros sin nombre, el comportamiento sería dependiente del controlador.  
  
 Como ejemplo de parámetros con nombre, supongamos que se ha definido un SQL Server procedimiento almacenado como se indica a continuación:  
  
```  
CREATE PROCEDURE test @title_id int = 1, @quote char(30) AS <blah>  
```  
  
 En este procedimiento, el primer parámetro, @title_id, tiene un valor predeterminado de 1. Una aplicación puede utilizar el siguiente código para invocar este procedimiento, de modo que solo especifique un parámetro dinámico. Este parámetro es un parámetro con nombre denominado "\@quote".  
  
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
