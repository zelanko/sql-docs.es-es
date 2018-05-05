---
title: Tipos de datos de archivo de texto | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], data types
- ODBC desktop database drivers [ODBC], text file driver
- desktop database drivers [ODBC], text file driver
- text file data types [ODBC]
- Jet-based ODBC drivers [ODBC], text file driver
ms.assetid: e113112e-ae42-469e-8e4b-a365a10d9071
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 14b808ff5d2cdc22afa050e2c7e0b760532b880d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="text-file-data-types"></a>Tipos de datos de archivo de texto
En la tabla siguiente se muestra cómo se asignan los tipos de datos de texto a tipos de datos SQL de ODBC. Tenga en cuenta que no todos los tipos de datos SQL de ODBC son compatibles con el controlador de ODBC texto.  
  
|Tipo de datos de texto|Tipo de datos de ODBC|  
|--------------------|--------------------|  
|CHAR|SQL_VARCHAR|  
|DATETIME|SQL_TIMESTAMP|  
|FLOAT|SQL_DOUBLE|  
|INTEGER|SQL_INTEGER|  
|LONGCHAR|SQL_LONGVARCHAR|  
  
> [!NOTE]  
>  **SQLGetTypeInfo** devuelve tipos de datos ODBC. Todas las conversiones en el apéndice D de la *referencia del programador de ODBC* son compatibles con los tipos de datos SQL que aparecen en la tabla anterior.  
  
 La siguiente tabla muestra las limitaciones en los tipos de datos de texto.  
  
|Tipo de datos|Description|  
|---------------|-----------------|  
|CHAR|Creación de una columna CHAR de cero o sin especificar longitud realmente devuelve una columna de tipo bit 255.<br /><br /> En archivos delimitados, una columna CHAR puede no tener o delimitadores de comillas al principio y al final; en los archivos de longitud fija, no se utilizan comillas dobles como delimitadores.|  
|DATETIME|MM-DD-AA (por ejemplo, 01-17-92)<br /><br /> MMM-DD-AA (por ejemplo, enero-17-92)<br /><br /> DD-MMM-aa (por ejemplo, 17-Ene-92)<br /><br /> AAAA-MM-DD (por ejemplo, 1992-01-17)<br /><br /> AAAA-MMM-DD (por ejemplo, 17 de enero de 1992)<br /><br /> No se permiten los separadores de fecha mixto dentro de una tabla.<br /><br /> El ISAM de texto da formato a un campo de fecha y hora en el formato de Estados Unidos o Europeo, dependiendo de la configuración internacional en el Panel de Control de Windows.|  
|FLOAT|El ancho máximo incluye el inicio de sesión y el separador decimal. En Schema.ini, el ancho se indica como se indica a continuación:<br /><br /> 14.083 es FLOAT 6 de ancho<br /><br /> -14.083 es FLOAT 7 de ancho<br /><br /> +14.083 es FLOAT 7 de ancho<br /><br /> 14083. es FLOAT ancho 6<br /><br /> ODBC siempre devuelve 8 para las columnas de tipo FLOAT.<br /><br /> Columnas de tipo FLOAT también pueden estar en notación científica, por ejemplo:<br /><br /> -3.04E + 2 es Float 8 de ancho<br /><br /> 25E4 es Float 4 de ancho<br /><br /> **Tenga en cuenta** notación científica y Decimal no se pueden combinar en una columna.<br /><br /> Valores NULL se representan mediante una cadena rellenada en blanco en los archivos de longitud fija y se omiten en archivos delimitados.<br /><br /> Datos float pueden estar rellena con espacios en blanco a la izquierda.|  
|INTEGER|Los valores válidos para las columnas de enteros son 32767 para -32.766.<br /><br /> En Schema.ini, el ancho se indica como se indica a continuación:<br /><br /> 14083 es 5 de ancho de entero<br /><br /> 0 es 1 de ancho de entero<br /><br /> ODBC siempre devuelve 4 para las columnas de enteros.<br /><br /> El ancho máximo incluye un inicio de sesión. El ancho máximo de una columna de enteros es 11, aunque el ancho puede ser mayor debido a los espacios en blanco que se permiten en tablas de formato fijo.|  
|LONGCHAR|Limita la teórico en el ancho de una columna LONGCHAR en la vista una longitud fija o tabla delimitado es 65500K. El ISAM de texto es más probable proporcionar compatibilidad con confiable hasta aproximadamente 32 K.|  
  
 Para conocer más limitaciones en los tipos de datos pueden encontrarse en [limitaciones del tipo de datos](../../odbc/microsoft/data-type-limitations.md).
