---
title: Tipos de datos de Paradox | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], Paradox driver
- desktop database drivers [ODBC], Paradox driver
- Paradox data types [ODBC]
- Jet-based ODBC drivers [ODBC], Paradox driver
- data types [ODBC], Paradox driver
- Paradox driver [ODBC], data types
ms.assetid: 0c9e5d21-9321-49f8-a055-69459e1c9c85
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9099d9a84fb79132249c74d1d24cc240bcf8aae0
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="paradox-data-types"></a>Tipos de datos de Paradox
El controlador ODBC Paradox asigna tipos de datos de Paradox a tipos de datos SQL de ODBC. En la tabla siguiente se enumera todos los tipos de datos de Paradox y muestra que se asignan a los tipos de datos de ODBC SQL.  
  
|Tipo de datos de Paradox|Tipo de datos de ODBC|  
|-----------------------|--------------------|  
|ALFANUMÉRICO|SQL_VARCHAR|  
|AUTOINCREMENT [1]|SQL_INTEGER|  
|BCD [1]|SQL_DOUBLE|  
|BYTES [1]|SQL_BINARY|  
|DATE|SQL_DATE|  
|IMAGEN DE [2]|SQL_LONGVARBINARY|  
|LÓGICA [1]|SQL_BIT|  
|LARGA [1]|SQL_INTEGER|  
|MEMORANDO [2]|SQL_LONGVARCHAR|  
|MONEY [1]|SQL_DOUBLE|  
|NUMBER|SQL_DOUBLE|  
|CORTO|SQL_SMALLINT|  
|TIEMPO [1]|SQL_TIMESTAMP|  
|MARCA DE TIEMPO [1]|SQL_TIMESTAMP|  
  
 [1] válido únicamente para versiones de Paradox 5. *x*.  
  
 [2] válido sólo para versiones de Paradox 4. *x* y 5. *x*.  
  
> [!NOTE]  
>  **SQLGetTypeInfo** devuelve tipos de datos de SQL de ODBC. Todas las conversiones en el apéndice D de la *referencia del programador de ODBC* son compatibles con los tipos de datos SQL de ODBC enumerados anteriormente en este tema.  
  
 La siguiente tabla muestra las limitaciones en los tipos de datos de Paradox.  
  
|Tipo de datos|Description|  
|---------------|-----------------|  
|ALFANUMÉRICO|Crear una columna ALFANUMÉRICA de cero o sin especificar longitud realmente devuelve una columna de 255 bytes.|  
|BYTES|Si inserta NULL en una columna binaria con el controlador de Paradox5, se cambia a 0.|  
|LONG|El valor negativo máximo admitido por el controlador de Paradox para el tipo de datos de tipo Long en 5 Paradox. *x* no es -2 ^ 31 (-2147483648), ya que debe ser desde largo se asigna a los datos ODBC escriba SQL_INTEGER. El valor negativo máximo admitido largos es realmente -2 ^ 31 + 1 (-2147483647).|  
|timestamp|Cuando un valor se inserta en una columna de marca de tiempo con el controlador de Paradox y que posteriormente se recupera de la columna, el valor recuperado puede diferir del valor insertado por tanto como 1 segundo a causa del redondeo.|  
  
 Para conocer más limitaciones en los tipos de datos pueden encontrarse en [limitaciones del tipo de datos](../../odbc/microsoft/data-type-limitations.md).

