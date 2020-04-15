---
title: Argumentos de identificador ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- identifier arguments [ODBC]
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], identifier
ms.assetid: b9de003f-cb49-4dec-b528-14a5b8ff12bd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6831eab30daebe37baecebe3ed7053537d7de8f8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300165"
---
# <a name="identifier-arguments"></a>Argumentos de identificador
Si se cita una cadena en un argumento de identificador, el controlador quita los espacios en blanco iniciales y finales y trata literalmente la cadena entre comillas. Si la cadena no se cita, el controlador quita los espacios en blanco finales y dobla la cadena a mayúsculas. Establecer un argumento de identificador en un puntero nulo devuelve SQL_ERROR y SQLSTATE HY009 (uso no válido del puntero nulo), a menos que el argumento sea un nombre de catálogo y no se admitan catálogos.  
  
 Estos argumentos se tratan como argumentos de identificador si el atributo de instrucción SQL_ATTR_METADATA_ID se establece en SQL_TRUE. En este caso, el carácter de subrayado (_) y el signo de porcentaje (%) se tratará como el carácter real, no como un carácter de patrón de búsqueda. Estos argumentos se tratan como un argumento normal o un argumento de patrón, dependiendo del argumento, si este atributo se establece en SQL_FALSE.  
  
 Aunque los identificadores que contienen caracteres especiales deben entrecomillar se citan en instrucciones SQL, no se deben entrecomitar cuando se pasan como argumentos de función de catálogo, porque los caracteres de comillas pasados a las funciones de catálogo se interpretan literalmente. Por ejemplo, supongamos que el carácter de comillas de identificador (que es específico del controlador y se devuelve a través de **SQLGetInfo**) es una comilla doble ("). La primera llamada a **SQLTables** devuelve un conjunto de resultados que contiene información sobre la tabla Proveedores, mientras que la segunda llamada devuelve información sobre la tabla "Cuentas por pagar", que probablemente no es lo previsto.  
  
```  
SQLTables(hstmt1, NULL, 0, NULL, 0, "Accounts Payable", SQL_NTS, NULL, 0);  
SQLTables(hstmt2, NULL, 0, NULL, 0, "\"Accounts Payable\"", SQL_NTS, NULL, 0);  
```  
  
 Los identificadores entre comillas se utilizan para distinguir un nombre de columna verdadero de una pseudocolumna del mismo nombre, como ROWID en Oracle. Si se pasa "ROWID" en un argumento de una función de catálogo, la función funcionará con la pseudocolumna ROWID si existe. Si la pseudocolumna no existe, la función funcionará con la columna "ROWID". Si rowID se pasa en un argumento de una función de catálogo, la función funcionará con la columna ROWID.  
  
 Para obtener más información acerca de los identificadores entre comillas, vea [Identificadores entre comillas](../../../odbc/reference/develop-app/quoted-identifiers.md).
