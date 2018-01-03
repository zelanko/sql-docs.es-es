---
title: 'SQL a C: Binary | Documentos de Microsoft'
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- converting data from SQL to c types [ODBC], binary
- binary data type [ODBC]
- data conversions from SQL to C types [ODBC], binary
- binary data transfers [ODBC]
ms.assetid: 8c519072-ae4c-4d32-9d4e-775e3d3d6389
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 293c18d2206d1b034eadc532f8850c6599e904e1
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="sql-to-c-binary"></a>SQL a binario C:
Los identificadores para los tipos de datos SQL de ODBC binarios son:  
  
 SQL_BINARY  
  
 SQL_VARBINARY  
  
 SQL_LONGVARBINARY  
  
 La siguiente tabla muestra los tipos de datos a la que se pueden convertir datos binarios de SQL de la C de ODBC. Para obtener una explicación de las columnas y los términos de la tabla, vea [convertir datos de SQL a tipos de datos C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  
  
|Identificador de tipo de C|Prueba|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|(Longitud de bytes de datos) \* 2 < *BufferLength*<br /><br /> (Longitud de bytes de datos) \* 2 > = *BufferLength*|data<br /><br /> Datos truncados|Longitud de los datos en bytes<br /><br /> Longitud de los datos en bytes|n/d<br /><br /> 01004|  
|SQL_C_WCHAR|(Longitud de caracteres de datos) \* 2 < *BufferLength*<br /><br /> (Longitud de caracteres de datos) \* 2 > = *BufferLength*|data<br /><br /> Datos truncados|Longitud de datos de caracteres<br /><br /> Longitud de datos de caracteres|n/d<br /><br /> 01004|  
|SQL_C_BINARY|Longitud de bytes de datos < = *BufferLength*<br /><br /> Longitud de bytes de datos > *BufferLength*|data<br /><br /> Datos truncados|Longitud de los datos en bytes<br /><br /> Longitud de los datos en bytes|n/d<br /><br /> 01004|  
  
 Cuando los datos binarios de SQL se convierten en datos de caracteres C, cada byte (8 bits) de datos de origen se representa como dos caracteres ASCII. Estos caracteres son la representación de caracteres ASCII del número en su formato hexadecimal. Por ejemplo, un 00000001 binario se convierte en "01" y un binario 11111111 se convierte en "FF".  
  
 El controlador siempre convierte los bytes individuales en pares de dígitos hexadecimales y termina la cadena de caracteres con un byte nulo. Por este motivo, si *BufferLength* par y es menor que la longitud de los datos convertidos, el último byte de la **TargetValuePtr* no se utiliza el búfer. (Los datos convertidos requieren un número par de bytes, el byte siguiente al último es un byte nulo y no se puede usar el último byte).  
  
> [!NOTE]  
>  Se desaconseja datos binarios de SQL de enlace a un tipo de datos de carácter C a los desarrolladores de aplicaciones. Esta conversión suele ser ineficaz y lento.
