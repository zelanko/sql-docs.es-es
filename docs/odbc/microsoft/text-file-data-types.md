---
title: Tipos de datos de archivos de texto ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7864dc81eaa3dd37f3d0053b2329c8842e445c8d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302663"
---
# <a name="text-file-data-types"></a>Tipos de datos de archivo de texto
En la tabla siguiente se muestra cómo se asignan los tipos de datos de texto a los tipos de datos SQL ODBC. Tenga en cuenta que no todos los tipos de datos SQL ODBC son compatibles con el controlador de texto ODBC.  
  
|Tipo de datos de texto|Tipo de datos de ODBC|  
|--------------------|--------------------|  
|CHAR|SQL_VARCHAR|  
|DATETIME|SQL_TIMESTAMP|  
|FLOAT|SQL_DOUBLE|  
|INTEGER|SQL_INTEGER|  
|LONGCHAR|SQL_LONGVARCHAR|  
  
> [!NOTE]  
>  **SQLGetTypeInfo** devuelve tipos de datos ODBC. Todas las conversiones en el Apéndice D de la *Referencia del programador ODBC* son compatibles con los tipos de datos SQL enumerados en la tabla anterior.  
  
 En la tabla siguiente se muestran las limitaciones de los tipos de datos Text.  
  
|Tipo de datos|Descripción|  
|---------------|-----------------|  
|CHAR|La creación de una columna CHAR de longitud cero o no especificada devuelve realmente una columna de 255 bits.<br /><br /> En archivos delimitados, una columna CHAR puede o no tener delimitadores de comillas dobles al principio y al final; en los archivos de longitud fija, las comillas dobles no se utilizan como delimitadores.|  
|DATETIME|MM-DD-AA (por ejemplo, 01-17-92)<br /><br /> MMM-DD-YY (por ejemplo, Ene-17-92)<br /><br /> DD-MMM-YY (por ejemplo, 17-enero-92)<br /><br /> AAAA-MM-DD (por ejemplo, 1992-01-17)<br /><br /> AAAA-MMM-DD (por ejemplo, 1992-enero-17)<br /><br /> No se permiten separadores de fecha mixtos dentro de una tabla.<br /><br /> El texto ISAM da formato a un campo DATETIME en el formato de Estados Unidos o europeo, dependiendo de la configuración internacional en el Panel de control de Windows.|  
|FLOAT|El ancho máximo incluye el signo y el punto decimal. En Schema.ini, el ancho se indica de la siguiente manera:<br /><br /> 14.083 es FLOAT Ancho 6<br /><br /> -14.083 es FLOAT Ancho 7<br /><br /> +14.083 es FLOAT Ancho 7<br /><br /> 14083. es FLOAT Ancho 6<br /><br /> ODBC siempre devuelve 8 para las columnas FLOAT.<br /><br /> Las columnas FLOAT también pueden estar en notación científica, por ejemplo:<br /><br /> -3.04E+2 es Ancho de Flotador 8<br /><br /> 25E4 es Ancho Flotador 4<br /><br /> **Nota** La notación decimal y científica no se puede mezclar en una columna.<br /><br /> Los valores NULL se representan mediante una cadena rellenaen en blanco en archivos de longitud fija y se omiten en archivos delimitados.<br /><br /> Los datos flotantes se pueden acolchar con espacios en blanco iniciales.|  
|INTEGER|Los valores válidos para las columnas INTEGER son 32767 a -32766.<br /><br /> En Schema.ini, el ancho se indica de la siguiente manera:<br /><br /> 14083 es INTEGER Ancho 5<br /><br /> 0 es INTEGER Ancho 1<br /><br /> ODBC siempre devuelve 4 para las columnas INTEGER.<br /><br /> El ancho máximo incluye un signo. El ancho máximo de una columna INTEGER es 11, aunque el ancho puede ser mayor debido a los espacios en blanco que se permiten en las tablas de formato fijo.|  
|LONGCHAR|El límite teórico en el ancho de una columna LONGCHAR en una tabla de longitud fija o delimitada es 65500K. El TEXTO ISAM es más propenso a proporcionar soporte confiable hasta aproximadamente 32K.|  
  
 Puede encontrar más limitaciones en los tipos de datos en [Limitaciones](../../odbc/microsoft/data-type-limitations.md)de tipos de datos .
