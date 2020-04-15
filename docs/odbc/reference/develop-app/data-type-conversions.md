---
title: Conversiones de tipos de datos ( Data Type Conversions) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cd888fe32692494e2b0ceadc1ed872dd96e244a9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305217"
---
# <a name="data-type-conversions"></a>Conversiones de tipos de datos
Los datos se pueden convertir de un tipo a otro en una de cuatro veces: cuando los datos se transfieren de una variable de aplicación a otra (C a C), cuando los datos de una variable de aplicación se envían a un parámetro de instrucción (C a SQL), cuando los datos de una columna de conjunto de resultados se devuelven en una variable de aplicación (SQL a C) y cuando los datos se transfieren de una columna de origen de datos a otra (SQL a SQL).  
  
 Cualquier conversión que se produzca cuando los datos se transfieren de una variable de aplicación a otra está fuera del ámbito de este documento.  
  
 Cuando una aplicación enlaza una variable a una columna de conjunto de resultados o un parámetro de instrucción, la aplicación especifica implícitamente una conversión de tipo de datos en su elección del tipo de datos de la variable de aplicación. Por ejemplo, supongamos que una columna contiene datos enteros. Si la aplicación enlaza una variable entera a la columna, especifica que no se realiza ninguna conversión; si la aplicación enlaza una variable de carácter a la columna, especifica que los datos se conviertan de entero a carácter.  
  
 ODBC define cómo se convierten los datos entre cada tipo de datos SQL y C. Básicamente, ODBC admite todas las conversiones razonables, como carácter a entero y entero a flotante, y no admite conversiones mal definidas, como float to date. Los controladores son necesarios para admitir todas las conversiones para cada tipo de datos SQL que admiten. Para obtener una lista completa de conversiones entre tipos de datos SQL y C, vea Convertir datos de tipos de [datos SQL a C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) y Convertir datos de C a tipos de datos [SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) en Apéndice D: Tipos de datos.  
  
 ODBC también define una función escalar para convertir datos de un tipo de datos SQL a otro. El controlador asigna la función escalar **CONVERT** a la función escalar subyacente o a las funciones definidas para realizar conversiones en el origen de datos. Dado que esta función se asigna a funciones específicas de DBMS, ODBC no define cómo funcionan estas conversiones o qué conversiones se deben admitir. Una aplicación detecta qué conversiones admite un controlador y un origen de datos determinados a través de las opciones de SQL_CONVERT de **SQLGetInfo**. Para obtener más información acerca de la función escalar **CONVERT,** vea [Secuencias](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md) de escape en ODBC y Función de [conversión](../../../odbc/reference/appendixes/explicit-data-type-conversion-function.md)explícita de tipos de datos .
