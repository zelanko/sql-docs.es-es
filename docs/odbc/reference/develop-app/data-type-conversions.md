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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cd888fe32692494e2b0ceadc1ed872dd96e244a9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305217"
---
# <a name="data-type-conversions"></a>Conversiones de tipos de datos
Los datos se pueden convertir de un tipo a otro en cuatro veces: cuando los datos se transfieren de una variable de aplicación a otra (C a C), cuando los datos de una variable de aplicación se envían a un parámetro de instrucción (de C a SQL), cuando los datos de una columna de conjunto de resultados se devuelven en una variable de aplicación (SQL a C) y cuando se transfieren datos de una columna de origen de datos  
  
 Cualquier conversión que se produce cuando los datos se transfieren de una variable de aplicación a otra queda fuera del ámbito de este documento.  
  
 Cuando una aplicación enlaza una variable a un parámetro de instrucción o columna del conjunto de resultados, la aplicación especifica implícitamente una conversión de tipo de datos en su elección del tipo de datos de la variable de aplicación. Por ejemplo, supongamos que una columna contiene datos enteros. Si la aplicación enlaza una variable de entero a la columna, especifica que no se realizará ninguna conversión. Si la aplicación enlaza una variable de carácter a la columna, especifica que los datos se convertirán de entero a carácter.  
  
 ODBC define cómo se convierten los datos entre cada tipo de datos SQL y C. Básicamente, ODBC admite todas las conversiones razonables, como carácter a entero y entero a flotante, y no admite conversiones mal definidas, como Float hasta la fecha. Los controladores son necesarios para admitir todas las conversiones de cada tipo de datos de SQL que admiten. Para obtener una lista completa de las conversiones entre los tipos de datos de SQL y C, vea [convertir datos de SQL a tipos de datos de c](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) y [convertir datos de c en tipos de datos de SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) en el Apéndice D: tipos de datos.  
  
 ODBC también define una función escalar para convertir datos de un tipo de datos SQL a otro. El controlador asigna la **función escalar** a la función escalar subyacente o a las funciones definidas para realizar conversiones en el origen de datos. Dado que esta función está asignada a funciones específicas de DBMS, ODBC no define el funcionamiento de estas conversiones o las conversiones que se deben admitir. Una aplicación detecta qué conversiones son compatibles con un controlador y un origen de datos determinados a través de las opciones de SQL_CONVERT de **SQLGetInfo**. Para obtener más información acerca de la función escalar **Convert** , vea [secuencias de escape en ODBC](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md) y función de [conversión de tipos de datos explícita](../../../odbc/reference/appendixes/explicit-data-type-conversion-function.md).
