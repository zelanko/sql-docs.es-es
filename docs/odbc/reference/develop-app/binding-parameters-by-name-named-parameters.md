---
title: "Enlazar parámetros por nombre (parámetros con nombre) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- named parameters [ODBC]
- binding parameters by name [ODBC]
ms.assetid: e2c3da5a-6c10-4dd5-acf9-e951eea71a6b
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a9548f671ce082d41423c1f85eb543c55b6194a2
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="binding-parameters-by-name-named-parameters"></a>Enlazar parámetros por nombre (parámetros con nombre)
Ciertos DBMS permiten que una aplicación especificar los parámetros a un procedimiento almacenado por su nombre en lugar de por posición en la llamada a procedimiento. Estos parámetros se denominan *parámetros con nombre*. ODBC admite el uso de parámetros con nombre. En ODBC, los parámetros con nombre solo se usan en llamadas a procedimientos almacenados y no se puede usar en otras instrucciones SQL.  
  
 El controlador comprueba el valor del campo SQL_DESC_UNNAMED de la IPD para determinar si denominado se usan parámetros. Si no se establece SQL_DESC_UNNAMED en SQL_UNNAMED, el controlador utiliza el nombre del campo SQL_DESC_NAME de la IPD para identificar el parámetro. Para enlazar el parámetro, una aplicación puede llamar a **SQLBindParameter** para especificar la información de parámetros y, a continuación, puede llamar a **SQLSetDescField** para establecer el campo SQL_DESC_NAME de la IPD. Cuando se utilizan parámetros con nombre, el orden del parámetro en la llamada a procedimiento no es importante y se omite el número de registro del parámetro.  
  
 La diferencia entre los parámetros sin nombre y parámetros con nombre está en la relación entre el número de registro del descriptor y el número de parámetro en el procedimiento. Cuando se utilizan parámetros sin nombre, el primer marcador de parámetro está relacionado con el primer registro en el descriptor de parámetro, que a su vez está relacionado con el primer parámetro (en orden de creación) en la llamada a procedimiento. Cuando se utilizan parámetros con nombre, el primer marcador de parámetro todavía está relacionado con el primer registro del descriptor de parámetro, pero la relación entre el número de registro del descriptor y el número de parámetro en el procedimiento ya no existe. Parámetros con nombre no utilizan la asignación del número de registros de descriptor para la posición de parámetro de procedimiento; en su lugar, el nombre de registro del descriptor se asigna al nombre del parámetro de procedimiento.  
  
> [!NOTE]  
>  Si está habilitado el rellenado automático de la IPD, el controlador llenará el descriptor de forma que el orden de los registros de descriptor coincidirá con el orden de los parámetros en la definición del procedimiento, incluso si se utilizan parámetros con nombre.  
  
 Si se utiliza un parámetro con nombre, todos los parámetros deben ser parámetros con nombre. Si cualquier parámetro no es un parámetro con nombre, a continuación, ninguna de la entidad de certificación de parámetros se parámetros con nombre. Si hubiera una combinación de parámetros con nombre y parámetros sin nombre, el comportamiento sería dependiente del controlador.  
  
 Como ejemplo de parámetros con nombre, suponga que un procedimiento almacenado se ha definido como se indica a continuación de SQL Server:  
  
```  
CREATE PROCEDURE test @title_id int = 1, @quote char(30) AS <blah>  
```  
  
 En este procedimiento, el primer parámetro, @title_id, tiene un valor predeterminado de 1. Una aplicación puede utilizar el siguiente código para invocar este procedimiento de forma que especifica solo un parámetro dinámico. Este parámetro es un parámetro con nombre con el nombre "@quote".  
  
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
