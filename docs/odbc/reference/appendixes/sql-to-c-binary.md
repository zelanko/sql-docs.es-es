---
title: 'SQL a C: binario | Microsoft Docs'
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 16112ca3b66e0218efd54d3bf385e04cb654e3e4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47622593"
---
# <a name="sql-to-c-binary"></a>SQL a C: binario
Los identificadores de los tipos de datos SQL de ODBC binarios son:  
  
 SQL_BINARY  
  
 SQL_VARBINARY  
  
 SQL_LONGVARBINARY  
  
 La siguiente tabla muestra los tipos de datos a la que se pueden convertir los datos binarios de SQL de la C de ODBC. Para obtener una explicación de las columnas y los términos de la tabla, vea [convertir datos de SQL a tipos de datos C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  
  
|Identificador de tipo de C|Prueba|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|(Longitud de bytes de datos) \* 2 < *BufferLength*<br /><br /> (Longitud de bytes de datos) \* 2 > = *BufferLength*|data<br /><br /> Datos truncados|Longitud de datos en bytes<br /><br /> Longitud de datos en bytes|n/d<br /><br /> 01004|  
|SQL_C_WCHAR|(Caracteres de longitud de datos) \* 2 < *BufferLength*<br /><br /> (Caracteres de longitud de datos) \* 2 > = *BufferLength*|data<br /><br /> Datos truncados|Longitud de datos de caracteres<br /><br /> Longitud de datos de caracteres|n/d<br /><br /> 01004|  
|SQL_C_BINARY|Longitud de bytes de datos < = *BufferLength*<br /><br /> Longitud de bytes de datos > *BufferLength*|data<br /><br /> Datos truncados|Longitud de datos en bytes<br /><br /> Longitud de datos en bytes|n/d<br /><br /> 01004|  
  
 Cuando los datos binarios de SQL se convierten en datos de caracteres de C, cada byte (8 bits) de datos de origen se representa como dos caracteres ASCII. Estos caracteres son la representación de carácter ASCII del número en formato hexadecimal. Por ejemplo, un 00000001 binario se convierte en "01" y un binario 11111111 se convierte en "FF".  
  
 El controlador siempre convierte los bytes individuales a pares de dígitos hexadecimales y finaliza la cadena de caracteres con un byte nulo. Por este motivo, si *BufferLength* incluso y es menor que la longitud de los datos convertidos, el último byte de la **TargetValuePtr* no se usa el búfer. (Los datos convertidos requieren un número par de bytes, el byte siguiente al último es un byte null y no se puede usar el último byte).  
  
> [!NOTE]  
>  Se desaconseja datos binarios de SQL de enlace a un tipo de datos de carácter C a los desarrolladores de aplicaciones. Esta conversión suele ser ineficaz y lento.
