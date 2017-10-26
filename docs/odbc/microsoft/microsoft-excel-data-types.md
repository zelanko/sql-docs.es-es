---
title: Tipos de datos de Microsoft Excel | Documentos de Microsoft
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
- data types [ODBC], Excel driver
- Excel data types [ODBC]
- Jet-based ODBC drivers [ODBC], Excel driver
- desktop database drivers [ODBC], Excel driver
- ODBC desktop database drivers [ODBC], Excel driver
- Excel driver [ODBC], data types
ms.assetid: 7b44c8e5-0bc3-4912-8a5d-56f4d5562fe6
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: eeb2bc72ce34141eb3dbdca3f952dca0c476c2dd
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="microsoft-excel-data-types"></a>Tipos de datos de Microsoft Excel
En la tabla siguiente se muestra cómo se asignan los tipos de datos del controlador de Microsoft Excel a los tipos de datos SQL de ODBC. El controlador de Microsoft Excel asigna a estos tipos de datos a columnas de tablas de Microsoft Excel basadas en los datos de la columna.  
  
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
  
|Tipo de datos|Description|  
|---------------|-----------------|  
|Datos cifrados|El controlador de Microsoft Excel no puede leer los datos cifrados.|  
|Cadenas de error|El controlador de Microsoft Excel no puede devolver una cadena de caracteres para los valores de error de Microsoft Excel (# n /!, #VALUE!, #REF!, #DIV/0!, #NUM!, #NAME? y #NULL!), pero devuelve un valor NULL en su lugar.|  
|LÓGICO|El valor de una columna lógica se devuelve en un búfer SQL_C_CHAR como 0 o 1.|  
|NUMBER|Si se crea una columna de enteros, se pueden introducir números que son demasiado grandes para el tipo de datos entero y los datos que contienen valores no enteros se pueden insertar, con lo que se puede convertir la columna en SQL_DOUBLE.|  
|TEXT|Cuando las filas de una columna contienen más de un tipo de datos de Microsoft Excel, el controlador ODBC de Microsoft Excel asigna al tipo de datos SQL_VARCHAR a la columna. Hay una excepción a esto: si la columna contiene solo dos o tres de los tipos de datos de fecha y hora (fecha, hora y fecha y hora), el controlador ODBC de Microsoft Excel asigna el tipo de datos SQL_TIMESTAMP a la columna.<br /><br /> Creación de una columna de texto de cero o sin especificar longitud realmente devuelve una columna de 255 bytes.<br /><br /> Un literal de cadena de caracteres puede contener cualquier carácter ANSI (1-255 decimal). Utilice dos consecutivos comillas (") para representar una comilla simple (').<br /><br /> Insertar un valor NULL en una columna con un tipo de datos distinto SQL_VARCHAR hará que el tipo de datos de la columna que se va a cambiar a SQL_VARCHAR.|  
  
 Para conocer más limitaciones en los tipos de datos pueden encontrarse en [limitaciones del tipo de datos](../../odbc/microsoft/data-type-limitations.md).

