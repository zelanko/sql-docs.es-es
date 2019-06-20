---
title: Argumentos de identificador | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 156dfaf5c6a6a4ec06a0c96b5f726383cba32ba6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62447554"
---
# <a name="identifier-arguments"></a>Argumentos de identificador
Si una cadena en un argumento de identificador está entre comillas, el controlador quita iniciales y finales de los espacios en blanco y literalmente trata la cadena entre comillas. Si la cadena no está entre comillas, el controlador quita subconjuntos y espacios en blanco finales a la cadena a mayúsculas. Al establecer un argumento de identificador a un puntero null devuelve SQL_ERROR y SQLSTATE HY009 (uso no válido del puntero null), a menos que el argumento es un nombre de catálogo y no se admiten los catálogos.  
  
 Si el atributo de instrucción de SQL_ATTR_METADATA_ID está establecido en SQL_TRUE, estos argumentos se tratan como argumentos de identificador. En este caso, el carácter de subrayado (_) y el porcentaje de sesión (%) se tratará como el carácter real, no como un carácter de patrón de búsqueda. Estos argumentos se tratan como un argumento normal o un argumento de patrón, dependiendo del argumento, si este atributo se establece en SQL_FALSE.  
  
 Aunque los identificadores que contienen caracteres especiales se deben escribir entre comillas en instrucciones SQL, deba no ir entre comillas cuando se pasan como argumentos de función de catálogo, porque los caracteres de comillas pasados a funciones de catálogo se interpretan literalmente. Por ejemplo, suponga que el identificador de carácter de comilla (que es específico del controlador y se devuelven a través de **SQLGetInfo**) es un signo de comillas doble ("). La primera llamada a **SQLTables** devuelve un conjunto que contiene información acerca de la tabla de cuentas por pagar, mientras que la segunda llamada devuelve información acerca de la tabla "Cuentas por pagar", que es probablemente no lo que se pretendía de resultados.  
  
```  
SQLTables(hstmt1, NULL, 0, NULL, 0, "Accounts Payable", SQL_NTS, NULL, 0);  
SQLTables(hstmt2, NULL, 0, NULL, 0, "\"Accounts Payable\"", SQL_NTS, NULL, 0);  
```  
  
 Los identificadores entre comillas se usan para distinguir un nombre de columna true desde una pseudocolumna del mismo nombre, como ROWID en Oracle. Si se pasa un argumento de una función de catálogo "ROWID", la función funcionará con la pseudocolumna ROWID si existe. Si no existe la pseudocolumna, la función funcionará con la columna "ROWID". Si se pasa un argumento de una función de catálogo ROWID, la función funcionará con la columna ROWID.  
  
 Para obtener más información acerca de los identificadores entre comillas, vea [identificadores entre comillas](../../../odbc/reference/develop-app/quoted-identifiers.md).
