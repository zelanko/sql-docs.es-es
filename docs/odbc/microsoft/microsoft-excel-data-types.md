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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8574985e10e5aaa3ae5431af7ee1245643e20b60
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81283775"
---
# <a name="microsoft-excel-data-types"></a>Tipos de datos de Microsoft Excel
En la tabla siguiente se muestra cómo se asignan los tipos de datos del controlador de Microsoft Excel a los tipos de datos SQL de ODBC. El controlador de Microsoft Excel asigna estos tipos de datos a las columnas de las tablas de Microsoft Excel en función de los datos de la columna.  
  
|Tipo de datos de Microsoft Excel|Tipo de datos de ODBC|  
|-------------------------------|--------------------|  
|Moneda|SQL_NUMERIC|  
|DATETIME|SQL_TIMESTAMP|  
|OPERADOR|SQL_BIT|  
|NUMBER|SQL_DOUBLE|  
|TEXT|SQL_VARCHAR|  
  
> [!NOTE]  
>  **SQLGetTypeInfo** devuelve los tipos de datos SQL de ODBC. Todas las conversiones del Apéndice D de la *Referencia del programador de ODBC* son compatibles con los tipos de datos SQL de ODBC enumerados anteriormente en este tema.  
  
 En la tabla siguiente se muestran las limitaciones en los tipos de datos de Microsoft Excel.  
  
|Tipo de datos|Descripción|  
|---------------|-----------------|  
|Datos cifrados|El controlador de Microsoft Excel no puede leer datos cifrados.|  
|Cadenas de error|El controlador de Microsoft Excel no puede devolver una cadena de caracteres para los valores de error de Microsoft Excel (#N/A!, #VALUE!, #REF!, #DIV/0!, #NUM!, #NAME? y #NULL!), pero devuelve un valor NULL en su lugar.|  
|OPERADOR|El valor de una columna lógica se devuelve en un búfer de SQL_C_CHAR como 0 o 1.|  
|NUMBER|Si se crea una columna de enteros, se pueden escribir los números que son demasiado grandes para el tipo de datos entero y se pueden insertar datos que contienen valores no enteros, con lo que la columna se puede convertir en SQL_DOUBLE.|  
|TEXT|Cuando las filas de una columna contienen más de un tipo de datos de Microsoft Excel, el controlador ODBC de Microsoft Excel asigna el tipo de datos SQL_VARCHAR a la columna. Existe una excepción: Si la columna contiene solo dos o tres tipos de datos de fecha y hora (fecha, hora y fecha y hora), el controlador ODBC de Microsoft Excel asigna el tipo de datos SQL_TIMESTAMP a la columna.<br /><br /> Al crear una columna de texto de cero o una longitud no especificada, se devuelve realmente una columna de 255 bytes.<br /><br /> Un literal de cadena de caracteres puede contener cualquier carácter ANSI (1-255 decimal). Use dos comillas simples consecutivas (") para representar una comilla simple (').<br /><br /> Si se inserta un valor NULL en una columna con un tipo de datos distinto de SQL_VARCHAR, el tipo de datos de la columna cambiará a SQL_VARCHAR.|  
  
 Se pueden encontrar más limitaciones en los tipos de datos en limitaciones de tipos de [datos](../../odbc/microsoft/data-type-limitations.md).
