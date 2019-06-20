---
title: Tipos de datos de archivo de texto | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], data types
- ODBC desktop database drivers [ODBC], text file driver
- desktop database drivers [ODBC], text file driver
- text file data types [ODBC]
- Jet-based ODBC drivers [ODBC], text file driver
ms.assetid: e113112e-ae42-469e-8e4b-a365a10d9071
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 23416cb067507d821701e57255fdc6f81ee607c4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62633010"
---
# <a name="text-file-data-types"></a>Tipos de datos de archivo de texto
En la tabla siguiente se muestra cómo se asignan los tipos de datos de texto a los tipos de datos SQL de ODBC. Tenga en cuenta que no todos los tipos de datos SQL de ODBC son compatibles con el controlador ODBC texto.  
  
|Tipo de datos de texto|Tipo de datos de ODBC|  
|--------------------|--------------------|  
|CHAR|SQL_VARCHAR|  
|DATETIME|SQL_TIMESTAMP|  
|FLOAT|SQL_DOUBLE|  
|INTEGER|SQL_INTEGER|  
|LONGCHAR|SQL_LONGVARCHAR|  
  
> [!NOTE]  
>  **SQLGetTypeInfo** devuelve tipos de datos ODBC. Todas las conversiones en el apéndice D de la *referencia del programador de ODBC* son compatibles con los tipos de datos SQL de la tabla anterior.  
  
 La siguiente tabla muestra las limitaciones en los tipos de datos de texto.  
  
|Tipo de datos|Descripción|  
|---------------|-----------------|  
|CHAR|Creación de una columna CHAR de cero o sin especificar longitud devuelve realmente una columna de tipo bit de 255.<br /><br /> En los archivos delimitados, una columna CHAR puede o no tener delimitadores de comillas al principio y al final; en los archivos de longitud fija, no se utilizan comillas dobles como delimitadores.|  
|DATETIME|MM-DD-AA (por ejemplo, 01-17-92)<br /><br /> DD-MMM-YY (por ejemplo, Ene-17-92)<br /><br /> DD-MMM-YY (por ejemplo, 17-Ene-92)<br /><br /> AAAA-MM-DD (por ejemplo, 17-01-1992)<br /><br /> DD-MMM-aaaa (por ejemplo, Ene-1992-17)<br /><br /> No se permiten los separadores de fecha mixto dentro de una tabla.<br /><br /> El texto de ISAM da formato a un campo de fecha y hora en el formato de Estados Unidos o Europa, dependiendo de la configuración internacional en el Panel de Control de Windows.|  
|FLOAT|El ancho máximo incluye el inicio de sesión y el separador decimal. En Schema.ini, el ancho se indica como sigue:<br /><br /> 14.083 es FLOAT 6 de ancho<br /><br /> -14.083 es FLOAT 7 de ancho<br /><br /> +14.083 es FLOAT 7 de ancho<br /><br /> 14083. es FLOAT ancho 6<br /><br /> ODBC siempre devuelve 8 para las columnas de tipo FLOAT.<br /><br /> Columnas de tipo FLOAT también pueden estar en notación científica, por ejemplo:<br /><br /> -3.04E + 2 es Float de 8 de ancho<br /><br /> 25E4 es Float 4 de ancho<br /><br /> **Tenga en cuenta** notación científica y académica Decimal no se puede combinar en una columna.<br /><br /> Los valores NULL se representan mediante una cadena rellena en blanco en los archivos de longitud fija y se omiten en archivos delimitados.<br /><br /> Datos float pueden se rellenen con los espacios en blanco.|  
|INTEGER|Los valores válidos para las columnas de enteros son 32767 para -32.766.<br /><br /> En Schema.ini, el ancho se indica como sigue:<br /><br /> 14083 es entero 5 de ancho<br /><br /> 0 es el entero 1 de ancho<br /><br /> ODBC siempre devuelve 4 para las columnas de enteros.<br /><br /> El ancho máximo incluye un inicio de sesión. El ancho máximo de una columna de enteros es 11, aunque el ancho puede ser mayor debido a los espacios en blanco que se permiten en tablas de formato fijo.|  
|LONGCHAR|Limita el teórico en el ancho de una columna LONGCHAR ya sea una longitud fija o delimitado se 65500K. El ISAM de texto es más probable que proporcionan compatibilidad confiable hasta unos 32 K.|  
  
 Para conocer más limitaciones en los tipos de datos pueden encontrarse en [limitaciones del tipo de datos](../../odbc/microsoft/data-type-limitations.md).
