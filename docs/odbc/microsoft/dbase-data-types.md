---
title: Tipos de datos de dBASE | Documentos de Microsoft
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
- Jet-based ODBC drivers [ODBC], DBasedriver
- desktop database drivers [ODBC], DBasedriver
- DBase driver [ODBC], data types
- data types [ODBC], DBase driver
- dbase data types [ODBC]
- ODBC desktop database drivers [ODBC], DBasedriver
ms.assetid: a0e31e6b-d02b-4ee2-9b37-5baf6a11c0a6
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 49fb588f5793eb3ee2fce7417632301794a65a22
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="dbase-data-types"></a>Tipos de datos de dBASE
En la tabla siguiente se muestra cómo se asignan los tipos de datos de dBASE a tipos de datos SQL de ODBC. Tenga en cuenta que no todos los tipos de datos SQL de ODBC son compatibles.  
  
|tipo de datos de dBASE|Tipo de datos de ODBC|  
|---------------------|--------------------|  
|CHAR|SQL_VARCHAR|  
|DATE|SQL_DATE|  
|FLOAT [1]|SQL_DOUBLE|  
|LÓGICO|SQL_BIT|  
|MEMORANDO|SQL_LONGVARCHAR|  
|NUMÉRICO (BCD)|SQL_DOUBLE|  
|OLEOBJECT [1]|SQL_LONGBINARY|  
  
 [1] válido sólo para dBASE versión 5. *x*  
  
 Precisión en dBASE III permite números con hacia arriba los exponentes de dos dígitos y, en números de dBASE IV con hasta los exponentes de tres dígitos. Dado que los números se almacenan como texto, se convierten a números. Si el número que se va a convertir no cabe en un campo, pueden producirse resultados inexplicadas.  
  
 Aunque dBASE permite una precisión y una escala que especificarse con un tipo de datos numérico, no se admite por el controlador ODBC dBASE. El controlador ODBC dBASE siempre devuelve una precisión de 15 y una escala de 0 para un tipo de datos NUMÉRICOS.  
  
 Una columna creada con el tipo de datos numéricos con las asignaciones de controlador ODBC dBASE al tipo de datos SQL_DOUBLE ODBC. Por lo tanto los datos de esta columna están sujeto a redondeo. Este comportamiento no es igual a medida que los datos NUMÉRICOS escribe en dBASE (tipo N), que es Binary Coded Decimal (BCD).  
  
> [!NOTE]  
>  **SQLGetTypeInfo** devuelve tipos de datos de SQL de ODBC. Todas las conversiones en el apéndice D de la *referencia del programador de ODBC* son compatibles con los tipos de datos SQL de ODBC enumerados anteriormente en este tema.  
  
 En la tabla siguiente muestra las limitaciones en dBASE tipos de datos.  
  
|Tipo de datos|Description|  
|---------------|-----------------|  
|CHAR|Creación de una columna CHAR de cero o sin especificar longitud realmente devuelve una columna 254 bytes.|  
|Datos cifrados|El controlador dBASE no admite tablas dBASE cifrados.|  
|LÓGICO|El controlador de dBASE no puede crear un índice en una columna lógica.|  
|MEMORANDO|La longitud máxima de una columna de memorando es 65.500 bytes.|  
  
 Para conocer más limitaciones en los tipos de datos pueden encontrarse en [limitaciones del tipo de datos](../../odbc/microsoft/data-type-limitations.md).

