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
manager: craigg
ms.openlocfilehash: 68dfb8976312016ee7f2e42fc4fcdecb93fd28cf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63199374"
---
# <a name="binding-parameters-by-name-named-parameters"></a>Enlazar parámetros por nombre (parámetros con nombre)
Algunos de los DBMS permiten que una aplicación especificar los parámetros a un procedimiento almacenado por su nombre en lugar de por posición en la llamada a procedimiento. Estos parámetros se denominan *parámetros con nombre*. ODBC admite el uso de parámetros con nombre. En ODBC, los parámetros con nombre solo se usan en llamadas a procedimientos almacenados y no se puede usar en otras instrucciones SQL.  
  
 El controlador comprueba el valor del campo SQL_DESC_UNNAMED de la IPD para determinar si la llamada se usan parámetros. Si no se establece SQL_DESC_UNNAMED a SQL_UNNAMED, el controlador utiliza el nombre del campo SQL_DESC_NAME de la IPD para identificar el parámetro. Para enlazar el parámetro, una aplicación puede llamar a **SQLBindParameter** para especificar la información de parámetros y, a continuación, puede llamar a **SQLSetDescField** para establecer el campo SQL_DESC_NAME de la IPD. Cuando se utilizan parámetros con nombre, el orden del parámetro en la llamada a procedimiento no es importante y se omite el número de registro del parámetro.  
  
 Es la diferencia entre los parámetros sin nombre y parámetros con nombre en la relación entre el número de registro del descriptor y el número de parámetro en el procedimiento. Cuando se utilizan parámetros sin nombre, el primer marcador de parámetro está relacionado con el primer registro en el descriptor de parámetro, que a su vez está relacionado con el primer parámetro (en orden de creación) de la llamada a procedimiento. Cuando se utilizan parámetros con nombre, el primer marcador de parámetro todavía está relacionado con el primer registro del descriptor de parámetro, pero ya no existe la relación entre el número de registro del descriptor y el número de parámetro en el procedimiento. Parámetros con nombre no utilizan la asignación del número de registros de descriptor para la posición del parámetro de procedimiento; en su lugar, el nombre de registro del descriptor se asigna al nombre del parámetro de procedimiento.  
  
> [!NOTE]  
>  Si está habilitado el rellenado automático de la IPD, el controlador rellenará el descriptor de modo que el orden de los registros de descriptor coincidirá con el orden de los parámetros en la definición del procedimiento, incluso si se utilizan parámetros con nombre.  
  
 Si se utiliza un parámetro con nombre, todos los parámetros deben ser parámetros con nombre. Si cualquier parámetro no es un parámetro con nombre, a continuación, ninguno de la parámetros ca se parámetros con nombre. Si hubiera una combinación de parámetros con nombre y parámetros sin nombre, el comportamiento sería dependiente del controlador.  
  
 Un ejemplo de parámetros con nombre, supongamos que un servidor de SQL Server se ha definido el procedimiento almacenado como sigue:  
  
```  
CREATE PROCEDURE test @title_id int = 1, @quote char(30) AS <blah>  
```  
  
 En este procedimiento, el primer parámetro, @title_id, tiene un valor predeterminado de 1. Una aplicación puede utilizar el siguiente código para invocar este procedimiento, que especifica solo un parámetro dinámico. Este parámetro es un parámetro con nombre con el nombre "\@oferta".  
  
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
