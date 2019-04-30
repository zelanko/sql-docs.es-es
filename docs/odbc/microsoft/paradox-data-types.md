---
title: Tipos de datos de Paradox | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], Paradox driver
- desktop database drivers [ODBC], Paradox driver
- Paradox data types [ODBC]
- Jet-based ODBC drivers [ODBC], Paradox driver
- data types [ODBC], Paradox driver
- Paradox driver [ODBC], data types
ms.assetid: 0c9e5d21-9321-49f8-a055-69459e1c9c85
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8e2f3b1e63578af7c0b42f00113fbb9e87cb8003
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63208410"
---
# <a name="paradox-data-types"></a>Tipos de datos de Paradox
El controlador ODBC Paradox asigna tipos de datos de Paradox a tipos de datos SQL de ODBC. En la tabla siguiente se enumera todos los tipos de datos de Paradox y muestra el SQL de ODBC se asignan a los tipos de datos.  
  
|Tipo de datos de Paradox|Tipo de datos de ODBC|  
|-----------------------|--------------------|  
|ALFANUMÉRICO|SQL_VARCHAR|  
|[1] DE INCREMENTO AUTOMÁTICO|SQL_INTEGER|  
|BCD[1]|SQL_DOUBLE|  
|BYTES [1]|SQL_BINARY|  
|DATE|SQL_DATE|  
|IMAGEN DE [2]|SQL_LONGVARBINARY|  
|LOGICAL[1]|SQL_BIT|  
|LONG[1]|SQL_INTEGER|  
|MEMO[2]|SQL_LONGVARCHAR|  
|MONEY [1]|SQL_DOUBLE|  
|NUMBER|SQL_DOUBLE|  
|CORTO|SQL_SMALLINT|  
|TIEMPO [1]|SQL_TIMESTAMP|  
|MARCA DE TIEMPO [1]|SQL_TIMESTAMP|  
  
 [1] válido solo para las versiones de Paradox 5. *x*.  
  
 [2] válido solo para las versiones de Paradox 4. *x* y 5. *x*.  
  
> [!NOTE]  
>  **SQLGetTypeInfo** devuelve tipos de datos de SQL de ODBC. Todas las conversiones en el apéndice D de la *referencia del programador de ODBC* son compatibles con los tipos de datos SQL de ODBC enumerados anteriormente en este tema.  
  
 La siguiente tabla muestra las limitaciones en los tipos de datos de Paradox.  
  
|Tipo de datos|Descripción|  
|---------------|-----------------|  
|ALFANUMÉRICO|Creación de una columna ALFANUMÉRICA de cero o sin especificar longitud devuelve realmente una columna de 255 bytes.|  
|BYTES|Si inserta NULL en una columna binaria con el controlador Paradox5, se cambia a 0.|  
|LONG|El valor negativo máximo admitido por el controlador de Paradox para el tipo de datos Long en 5 Paradox. *x* no es -2 ^ 31 (-2147483648), como debería ser desde largo se asigna a los datos ODBC escriba SQL_INTEGER. El valor negativo máximo admitido durante mucho tiempo es realmente -2 ^ 31 + 1 (-2147483647).|  
|timestamp|Cuando un valor se inserta en una columna de marca de tiempo por el controlador de Paradox y luego posteriormente recuperado de la columna, el valor recuperado puede diferir el valor insertado por tanto como 1 segundo a causa del redondeo.|  
  
 Para conocer más limitaciones en los tipos de datos pueden encontrarse en [limitaciones del tipo de datos](../../odbc/microsoft/data-type-limitations.md).
