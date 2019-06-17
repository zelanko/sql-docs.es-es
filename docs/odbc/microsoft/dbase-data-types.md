---
title: Tipos de datos de dBASE | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], DBasedriver
- desktop database drivers [ODBC], DBasedriver
- DBase driver [ODBC], data types
- data types [ODBC], DBase driver
- dbase data types [ODBC]
- ODBC desktop database drivers [ODBC], DBasedriver
ms.assetid: a0e31e6b-d02b-4ee2-9b37-5baf6a11c0a6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fc4b4c7a5c1074a62bf0e84d265840109f65ea55
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63126318"
---
# <a name="dbase-data-types"></a>Tipos de datos de dBASE
En la tabla siguiente se muestra cómo se asignan los tipos de datos de dBASE a tipos de datos SQL de ODBC. Tenga en cuenta que no todos los tipos de datos SQL de ODBC son compatibles.  
  
|tipo de datos de dBASE|Tipo de datos de ODBC|  
|---------------------|--------------------|  
|CHAR|SQL_VARCHAR|  
|DATE|SQL_DATE|  
|FLOAT[1]|SQL_DOUBLE|  
|LÓGICO|SQL_BIT|  
|MEMORANDO|SQL_LONGVARCHAR|  
|NUMÉRICO (BCD)|SQL_DOUBLE|  
|OLEOBJECT[1]|SQL_LONGBINARY|  
  
 [1] válido sólo para dBASE versión 5. *x*  
  
 Precisión en dBASE III permite números con seguridad a los exponentes de dos dígitos y en los números de dBASE IV con hasta los exponentes de tres dígitos. Dado que los números se almacenan como texto, se convierten a números. Si el número que desea convertir no cabe en un campo, pueden producirse resultados inexplicables.  
  
 Aunque dBASE permite una precisión y una escala que especificarse con un tipo de datos numérico, no se admite el controlador de dBASE ODBC. El controlador ODBC dBASE siempre devuelve una precisión de 15 y una escala de 0 para un tipo de datos numérico.  
  
 Una columna creada con el tipo de datos numéricos mediante las asignaciones de controlador de dBASE ODBC para el tipo de datos SQL_DOUBLE ODBC. Por lo tanto los datos de esta columna están sujeto a redondeo. Este comportamiento no es igual a medida que los datos NUMÉRICOS escribe en dBASE (tipo N), que es Binary Coded Decimal (BCD).  
  
> [!NOTE]  
>  **SQLGetTypeInfo** devuelve tipos de datos de SQL de ODBC. Todas las conversiones en el apéndice D de la *referencia del programador de ODBC* son compatibles con los tipos de datos SQL de ODBC enumerados anteriormente en este tema.  
  
 En la tabla siguiente muestra las limitaciones en dBASE tipos de datos.  
  
|Tipo de datos|Descripción|  
|---------------|-----------------|  
|CHAR|Creación de una columna CHAR de cero o sin especificar longitud devuelve realmente una columna de bytes de 254.|  
|Datos cifrados|El controlador de dBASE no admite tablas de dBASE cifrados.|  
|LÓGICO|El controlador de dBASE no puede crear un índice en una columna lógica.|  
|MEMORANDO|La longitud máxima de una columna de memorando es 65.500 bytes.|  
  
 Para conocer más limitaciones en los tipos de datos pueden encontrarse en [limitaciones del tipo de datos](../../odbc/microsoft/data-type-limitations.md).
