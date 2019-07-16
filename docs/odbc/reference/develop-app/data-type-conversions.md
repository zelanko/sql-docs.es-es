---
title: Conversiones de tipos de datos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], conversions
- SQL data types [ODBC], conversions
- converting data [ODBC]
- converting data types [ODBC]
- C data types [ODBC], conversions
ms.assetid: d311fe1c-d882-4136-9fa5-220a4121e04c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 590bd488ae87e8e871837c3055a3225794850d00
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68077014"
---
# <a name="data-type-conversions"></a>Conversiones de tipos de datos
Se pueden convertir datos de un tipo a otro en uno de cuatro veces: cuando se transfieren datos de la variable de una aplicación a otra (C y C), cuando se envían datos de una variable de aplicación a un parámetro de instrucción (C a SQL), cuando los datos en una columna del conjunto de resultados se devuelven en una variable de aplicación (SQL a C) y cuando se transfieren los datos de columna de origen de datos de uno a otro (SQL para SQL).  
  
 Cualquier conversión que se produce cuando se transfieren datos de la variable de una aplicación a otro está fuera del ámbito de este documento.  
  
 Cuando una aplicación enlaza una variable con un parámetro de instrucción o la columna del conjunto de resultados, la aplicación especifica implícitamente una conversión de tipos de datos de su elección del tipo de datos de la variable de aplicación. Por ejemplo, suponga que una columna contiene datos enteros. Si la aplicación enlaza una variable de entero a la columna, especifica que se realiza ninguna conversión; Si la aplicación enlaza una variable de caracteres a la columna, especifica que los datos se convierten de entero al carácter.  
  
 ODBC define cómo se convierten los datos entre cada tipo de datos SQL y C. Básicamente, ODBC admite todas las conversiones razonables, como carácter de entero y entero a float y no admite conversiones bien definidas, como float hasta la fecha. Los controladores deben admitir todas las conversiones para cada tipo de datos SQL que admiten. Para obtener una lista completa de las conversiones entre tipos de datos SQL y C, consulte [convertir datos de SQL a tipos de datos C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) y [convertir datos de C a tipos de datos SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) en el apéndice D: Tipos de datos.  
  
 ODBC también define una función escalar para convertir los datos de un tipo de datos SQL a otro. El **convertir** función escalar está asignada por el controlador a la función escalar subyacente o funciones definidas para llevar a cabo las conversiones en el origen de datos. Dado que esta función se asigna a funciones específicas del DBMS, ODBC no define cómo funcionan estas conversiones o conversiones de qué deben ser compatibles. Una aplicación detecta qué conversiones son compatibles con un origen de datos y el controlador determinado a través de las opciones de SQL_CONVERT en **SQLGetInfo**. Para obtener más información sobre la **convertir** función escalar, vea [secuencias de Escape de ODBC](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md) y [función de conversión de tipo de datos explícita](../../../odbc/reference/appendixes/explicit-data-type-conversion-function.md).
