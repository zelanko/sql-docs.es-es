---
title: Argumentos de identificador | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- identifier arguments [ODBC]
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], identifier
ms.assetid: b9de003f-cb49-4dec-b528-14a5b8ff12bd
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1d483c50928d93ecd64419726eb77ae162f221f5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="identifier-arguments"></a>Argumentos de identificador
Si se definen una cadena dentro de un argumento de identificador, el controlador quita iniciales y finales de los espacios en blanco y literalmente trata la cadena entre comillas. Si la cadena no está entre comillas, el controlador quita subconjuntos y espacios en blanco finales a la cadena a mayúsculas. Si se establece un argumento de identificador a un puntero null devuelve SQL_ERROR y SQLSTATE HY009 (uso no válido del puntero null), a menos que el argumento es un nombre de catálogo y no se admiten los catálogos.  
  
 Si el atributo de instrucción SQL_ATTR_METADATA_ID está establecido en SQL_TRUE, estos argumentos se tratan como argumentos de identificador. En este caso, el carácter de subrayado (_) y el signo de porcentaje (%) se tratará como el carácter real, no como un carácter de patrón de búsqueda. Estos argumentos se tratan como un argumento normal o un argumento pattern, dependiendo del argumento, si este atributo se establece en SQL_FALSE.  
  
 Aunque los identificadores que contienen caracteres especiales deben ir entre comillas en instrucciones SQL, debe no ir entre comillas cuando se pasan como argumentos de función de catálogo, porque se pasa a funciones de catálogo de caracteres de comillas se interpretan literalmente. Por ejemplo, suponga que el identificador de carácter de comillas (que es específico del controlador y se devuelven a través de **SQLGetInfo**) es un signo de comillas dobles ("). La primera llamada a **SQLTables** devuelve un conjunto que contiene información acerca de la tabla de cuentas por pagar, mientras que la segunda llamada devuelve información acerca de la tabla "Cuentas por pagar", que es probable que no lo que se pretendía de resultados.  
  
```  
SQLTables(hstmt1, NULL, 0, NULL, 0, "Accounts Payable", SQL_NTS, NULL, 0);  
SQLTables(hstmt2, NULL, 0, NULL, 0, "\"Accounts Payable\"", SQL_NTS, NULL, 0);  
```  
  
 Los identificadores entre comillas se usan para distinguir un nombre de columna true desde una pseudocolumna del mismo nombre, como ROWID en Oracle. Si se pasa un argumento de una función de catálogo "ROWID", la función funcionará con la pseudocolumna ROWID si existe. Si no existe la pseudocolumna, la función funcionará con la columna "ROWID". Si ROWID se pasa un argumento de entrada de una función de catálogo, la función funcionará con la columna ROWID.  
  
 Para obtener más información acerca de los identificadores entre comillas, vea [identificadores entrecomillados](../../../odbc/reference/develop-app/quoted-identifiers.md).
