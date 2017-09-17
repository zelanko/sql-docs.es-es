---
title: Conversiones de tipos de datos | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data types [ODBC], conversions
- SQL data types [ODBC], conversions
- converting data [ODBC]
- converting data types [ODBC]
- C data types [ODBC], conversions
ms.assetid: d311fe1c-d882-4136-9fa5-220a4121e04c
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2369b39ff415a5387205ce62811594fe08a9f324
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="data-type-conversions"></a>Conversiones de tipos de datos
Se pueden convertir datos de un tipo a otro en uno de los cuatro veces: cuando se transfieren datos de variable de una aplicación a otra (C y C), cuando se envían datos en una variable de aplicación con un parámetro de instrucción (C a SQL), cuando los datos en una columna de conjunto de resultados se devuelven en una variable de aplicación (SQL a C), y cuando se transfieren los datos de columna de origen de datos a otro (SQL con SQL).  
  
 Cualquier conversión que se produce cuando se transfieren datos de variable de una aplicación a otra está fuera del ámbito de este documento.  
  
 Cuando una aplicación enlaza una variable a un parámetro de instrucción o columna del conjunto de resultados, la aplicación especifica implícitamente una conversión de tipos de datos de su elección del tipo de datos de la variable de aplicación. Por ejemplo, suponga que una columna contiene datos enteros. Si la aplicación enlaza una variable de entero para la columna, especifica que no se realiza ninguna conversión; Si la aplicación enlaza una variable de caracteres a la columna, especifica que los datos se convierten de entero al carácter.  
  
 ODBC define cómo se convierten los datos entre cada tipo de datos SQL y C. Básicamente, ODBC admite todas las conversiones razonables, como carácter de entero y entero a float y no admite conversiones definido correctamente, por ejemplo, float hasta la fecha. Se requieren controladores para admitir todas las conversiones para cada tipo de datos SQL que admiten. Para obtener una lista completa de las conversiones entre tipos de datos SQL y C, consulte [convertir datos de SQL a tipos de datos C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) y [convertir datos de C a tipos de datos SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) en tipos de datos de apéndice D:.  
  
 ODBC también define una función escalar de convertir los datos de un tipo de datos SQL a otro. El **convertir** función escalar ha sido asignada por el controlador a la función escalar subyacente o funciones definidas para realizar conversiones en el origen de datos. Dado que esta función se asigna a funciones específicas del DBMS, ODBC no define cómo funcionan estas conversiones o qué conversiones deben ser compatibles. Una aplicación detecta qué conversiones son compatibles con un origen de datos y el controlador determinado a través de las opciones de SQL_CONVERT en **SQLGetInfo**. Para obtener más información sobre la **convertir** función escalar, consulte [secuencias de Escape de ODBC](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md) y [función de conversión de tipo de datos explícito](../../../odbc/reference/appendixes/explicit-data-type-conversion-function.md).
