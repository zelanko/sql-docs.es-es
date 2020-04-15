---
title: Tipos de datos de dBASE ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 17b96ad0b6674a2d120ef46d9bfa221e8df6d140
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307696"
---
# <a name="dbase-data-types"></a>Tipos de datos de dBASE
En la tabla siguiente se muestra cómo se asignan los tipos de datos dBASE a tipos de datos SQL ODBC. Tenga en cuenta que no se admiten todos los tipos de datos SQL ODBC.  
  
|tipo de datos dBASE|Tipo de datos de ODBC|  
|---------------------|--------------------|  
|CHAR|SQL_VARCHAR|  
|DATE|SQL_DATE|  
|FLOTADOR[1]|SQL_DOUBLE|  
|Lógica|SQL_BIT|  
|memorándum|SQL_LONGVARCHAR|  
|NUMERICO (BCD)|SQL_DOUBLE|  
|OLEOBJECT[1]|SQL_LONGBINARY|  
  
 [1] Válido sólo para dBASE versión 5. *x*  
  
 La precisión en dBASE III permite números con exponentes de hasta dos dígitos y en números dBASE IV con exponentes de hasta tres dígitos. Dado que los números se almacenan como texto, se convierten en números. Si el número a convertir no cabe en un campo, pueden producirse resultados inexplicables.  
  
 Aunque dBASE permite especificar una precisión y una escala con un tipo de datos NUMERIC, no es compatible con el controlador ODBC dBASE. El controlador ODBC dBASE siempre devuelve una precisión de 15 y una escala de 0 para un tipo de datos NUMERIC.  
  
 Una columna creada con el tipo de datos numérico mediante el controlador dBASE ODBC se asigna al tipo de datos ODBC SQL_DOUBLE. Por lo tanto, los datos de esta columna están sujetos a redondeo. Este comportamiento no es el mismo que el del tipo de datos NUMERIC en dBASE (tipo N), que es Decimal codificado binario (BCD).  
  
> [!NOTE]  
>  **SQLGetTypeInfo** devuelve tipos de datos SQL ODBC. Todas las conversiones en el Apéndice D de la *referencia del programador ODBC* se admiten para los tipos de datos SQL ODBC enumerados anteriormente en este tema.  
  
 En la tabla siguiente se muestran las limitaciones de los tipos de datos dBASE.  
  
|Tipo de datos|Descripción|  
|---------------|-----------------|  
|CHAR|La creación de una columna CHAR de longitud cero o no especificada devuelve realmente una columna de 254 bytes.|  
|Datos cifrados|El controlador dBASE no admite tablas dBASE cifradas.|  
|Lógica|El controlador dBASE no puede crear un índice en una columna LOGICAL.|  
|memorándum|La longitud máxima de una columna MEMO es de 65.500 bytes.|  
  
 Puede encontrar más limitaciones en los tipos de datos en [Limitaciones](../../odbc/microsoft/data-type-limitations.md)de tipos de datos .
