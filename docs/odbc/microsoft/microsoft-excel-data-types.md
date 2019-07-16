---
title: Tipos de datos de Microsoft Excel | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], Excel driver
- Excel data types [ODBC]
- Jet-based ODBC drivers [ODBC], Excel driver
- desktop database drivers [ODBC], Excel driver
- ODBC desktop database drivers [ODBC], Excel driver
- Excel driver [ODBC], data types
ms.assetid: 7b44c8e5-0bc3-4912-8a5d-56f4d5562fe6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5a8385c8efb1ab7dcee651e5acb52062292a0bcc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68045018"
---
# <a name="microsoft-excel-data-types"></a>Tipos de datos de Microsoft Excel
En la tabla siguiente se muestra cómo se asignan los tipos de datos del controlador de Microsoft Excel para los tipos de datos SQL de ODBC. El controlador de Microsoft Excel asigna a estos tipos de datos a columnas de tablas de Microsoft Excel basadas en los datos en la columna.  
  
|Tipo de datos de Microsoft Excel|Tipo de datos de ODBC|  
|-------------------------------|--------------------|  
|Moneda|SQL_NUMERIC|  
|DATETIME|SQL_TIMESTAMP|  
|LÓGICO|SQL_BIT|  
|NUMBER|SQL_DOUBLE|  
|TEXT|SQL_VARCHAR|  
  
> [!NOTE]  
>  **SQLGetTypeInfo** devuelve tipos de datos de SQL de ODBC. Todas las conversiones en el apéndice D de la *referencia del programador de ODBC* son compatibles con los tipos de datos SQL de ODBC enumerados anteriormente en este tema.  
  
 La siguiente tabla muestra las limitaciones en los tipos de datos de Microsoft Excel.  
  
|Tipo de datos|Descripción|  
|---------------|-----------------|  
|Datos cifrados|El controlador de Microsoft Excel no puede leer los datos cifrados.|  
|Cadenas de error|El controlador de Microsoft Excel no puede devolver una cadena de caracteres para los valores de error de Microsoft Excel (#N/A!, #VALUE!, #REF!, #DIV/0!, #NUM!, #NAME? y #NULL!), pero devuelve un valor NULL en su lugar.|  
|LÓGICO|Se devuelve el valor de una columna lógico en un búfer SQL_C_CHAR como 0 o 1.|  
|NUMBER|Si se crea una columna de enteros, se pueden escribir los números que son demasiado grandes para el tipo de datos entero, y se pueden insertar datos que contienen valores no enteros, con lo que se puede convertir la columna en SQL_DOUBLE.|  
|TEXT|Cuando las filas de una columna contienen más de un tipo de datos de Microsoft Excel, el controlador ODBC de Microsoft Excel asigna al tipo de datos SQL_VARCHAR a la columna. Hay una excepción a esto: si la columna contiene sólo dos o tres de los tipos de datos datetime (fecha, hora y fecha y hora), el controlador ODBC de Microsoft Excel asigna el tipo de datos SQL_TIMESTAMP a la columna.<br /><br /> Creación de una columna de texto de cero o sin especificar longitud devuelve realmente una columna de 255 bytes.<br /><br /> Un literal de cadena de caracteres puede contener cualquier carácter ANSI (de 1 a 255 decimal). Usar dos consecutivos comillas (") para representar una comilla simple (').<br /><br /> Insertar un valor NULL en una columna con un tipo de datos distinto SQL_VARCHAR hará que el tipo de datos de la columna para cambiar a SQL_VARCHAR.|  
  
 Para conocer más limitaciones en los tipos de datos pueden encontrarse en [limitaciones del tipo de datos](../../odbc/microsoft/data-type-limitations.md).
