---
title: Tipos de datos de Microsoft Excel ? Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283775"
---
# <a name="microsoft-excel-data-types"></a>Tipos de datos de Microsoft Excel
En la tabla siguiente se muestra cómo se asignan los tipos de datos del controlador de Microsoft Excel a los tipos de datos SQL ODBC. El controlador de Microsoft Excel asigna estos tipos de datos a columnas de tablas de Microsoft Excel en función de los datos de la columna.  
  
|Tipo de datos de Microsoft Excel|Tipo de datos de ODBC|  
|-------------------------------|--------------------|  
|Moneda|SQL_NUMERIC|  
|DATETIME|SQL_TIMESTAMP|  
|Lógica|SQL_BIT|  
|NUMBER|SQL_DOUBLE|  
|TEXT|SQL_VARCHAR|  
  
> [!NOTE]  
>  **SQLGetTypeInfo** devuelve tipos de datos SQL ODBC. Todas las conversiones en el Apéndice D de la *referencia del programador ODBC* se admiten para los tipos de datos SQL ODBC enumerados anteriormente en este tema.  
  
 En la tabla siguiente se muestran las limitaciones en los tipos de datos de Microsoft Excel.  
  
|Tipo de datos|Descripción|  
|---------------|-----------------|  
|Datos cifrados|El controlador de Microsoft Excel no puede leer datos cifrados.|  
|Cadenas de error|El controlador de Microsoft Excel no puede devolver una cadena de caracteres para los valores de error de Microsoft Excel (#N/A!, #VALUE!, #REF!, #DIV/0!, #NUM!, #NAME?, y #NULL!), pero devuelve un valor NULL en su lugar.|  
|Lógica|El valor de una columna LOGICAL se devuelve en un búfer de SQL_C_CHAR como 0 o 1.|  
|NUMBER|Si se crea una columna entera, se pueden introducir números demasiado grandes para el tipo de datos entero y se pueden insertar datos que contengan valores no enteros, con el resultado de que la columna se puede convertir en SQL_DOUBLE.|  
|TEXT|Cuando las filas de una columna contienen más de un tipo de datos de Microsoft Excel, el controlador ODBC de Microsoft Excel asigna el tipo de datos SQL_VARCHAR a la columna. Hay una excepción a esto: si la columna contiene solo dos o tres de los tipos de datos datetime (DATE, TIME y DATETIME), el controlador ODBC de Microsoft Excel asigna el tipo de datos SQL_TIMESTAMP a la columna.<br /><br /> La creación de una columna TEXT de longitud cero o no especificada devuelve realmente una columna de 255 bytes.<br /><br /> Un literal de cadena de caracteres puede contener cualquier carácter ANSI (1-255 decimal). Utilice dos comillas simples consecutivas (") para representar una comilla simple (').<br /><br /> Insertar un NULL en una columna con un tipo de datos distinto de SQL_VARCHAR hará que el tipo de datos de la columna cambie a SQL_VARCHAR.|  
  
 Puede encontrar más limitaciones en los tipos de datos en [Limitaciones](../../odbc/microsoft/data-type-limitations.md)de tipos de datos .
