---
title: 'SQL a C: binario ? Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to c types [ODBC], binary
- binary data type [ODBC]
- data conversions from SQL to C types [ODBC], binary
- binary data transfers [ODBC]
ms.assetid: 8c519072-ae4c-4d32-9d4e-775e3d3d6389
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 70b0ce72f650e61b83ec99b0727752612d18da52
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298833"
---
# <a name="sql-to-c-binary"></a>SQL a C: Binary
Los identificadores para los tipos de datos ODBC SQL binarios son:  
  
 SQL_BINARY  
  
 SQL_VARBINARY  
  
 SQL_LONGVARBINARY  
  
 En la tabla siguiente se muestran los tipos de datos ODBC C a los que se pueden convertir datos SQL binarios. Para obtener una explicación de las columnas y los términos de la tabla, vea [Convertir datos de SQL a tipos](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)de datos C .  
  
|Identificador de tipo C|Prueba|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|(Longitud de bytes de los datos) \* 2 < *BufferLength*<br /><br /> (Longitud de bytes de los datos) \* 2 >- *BufferLength*|data<br /><br /> Datos truncados|Longitud de los datos en bytes<br /><br /> Longitud de los datos en bytes|N/D<br /><br /> 01004|  
|SQL_C_WCHAR|(Longitud de caracteres de datos) \* 2 < *BufferLength*<br /><br /> (Longitud de caracteres de datos) \* 2 >- *BufferLength*|data<br /><br /> Datos truncados|Longitud de los datos en caracteres<br /><br /> Longitud de los datos en caracteres|N/D<br /><br /> 01004|  
|SQL_C_BINARY|Longitud de bytes de los datos <- *BufferLength*<br /><br /> Longitud de bytes de los datos > *BufferLength*|data<br /><br /> Datos truncados|Longitud de los datos en bytes<br /><br /> Longitud de los datos en bytes|N/D<br /><br /> 01004|  
  
 Cuando los datos SQL binarios se convierten en datos de caracteres C, cada byte (8 bits) de datos de origen se representa como dos caracteres ASCII. Estos caracteres son la representación de caracteres ASCII del número en su forma hexadecimal. Por ejemplo, un binario 00000001 se convierte en "01" y un binario 11111111 se convierte en "FF".  
  
 El controlador siempre convierte bytes individuales en pares de dígitos hexadecimales y termina la cadena de caracteres con un byte nulo. Por este culpa, si *BufferLength* es par y es menor que la longitud de los datos convertidos, no se utiliza el último byte del **TargetValuePtr* búfer. (Los datos convertidos requieren un número par de bytes, el bit siguiente al último es un byte nulo y no se puede utilizar el último byte.)  
  
> [!NOTE]  
>  Se desaconseja a los desarrolladores de aplicaciones enlazar datos SQL binarios a un tipo de datos de carácter C. Esta conversión suele ser ineficiente y lenta.
