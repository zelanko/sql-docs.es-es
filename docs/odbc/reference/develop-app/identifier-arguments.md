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
ms.openlocfilehash: 93cf744cf105762fb90a92049d6698e67a19d58c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68138998"
---
# <a name="identifier-arguments"></a>Argumentos de identificador
Si una cadena de un argumento de identificador está entre comillas, el controlador quita los espacios en blanco iniciales y finales y trata literalmente la cadena entre comillas. Si la cadena no está entre comillas, el controlador quita los espacios en blanco finales y dobla la cadena a mayúsculas. Si se establece un argumento de identificador en un puntero nulo, se devuelve SQL_ERROR y SQLSTATE HY009 (uso no válido de puntero nulo), a menos que el argumento sea un nombre de catálogo y no se admitan catálogos.  
  
 Estos argumentos se tratan como argumentos de identificador si el atributo de instrucción SQL_ATTR_METADATA_ID está establecido en SQL_TRUE. En este caso, el carácter de subrayado (_) y el signo de porcentaje (%) se tratará como el carácter real, no como un carácter de patrón de búsqueda. Estos argumentos se tratan como un argumento normal o un argumento de patrón, dependiendo del argumento, si este atributo se establece en SQL_FALSE.  
  
 Aunque los identificadores que contienen caracteres especiales deben ir entre comillas en las instrucciones SQL, no deben ir entre comillas cuando se pasan como argumentos de la función de catálogo, ya que los caracteres de Comillas pasadas a las funciones de catálogo se interpretan literalmente. Por ejemplo, supongamos que el carácter de comilla de identificador (que es específico del controlador y que se devuelve a través de **SQLGetInfo**) es una comilla doble ("). La primera llamada a **SQLTables** devuelve un conjunto de resultados que contiene información sobre la tabla Accounts Payable, mientras que la segunda llamada devuelve información acerca de la tabla "Accounts Payable", que probablemente no sea lo que se pretendía.  
  
```  
SQLTables(hstmt1, NULL, 0, NULL, 0, "Accounts Payable", SQL_NTS, NULL, 0);  
SQLTables(hstmt2, NULL, 0, NULL, 0, "\"Accounts Payable\"", SQL_NTS, NULL, 0);  
```  
  
 Los identificadores entre comillas se usan para distinguir un nombre de columna verdadero de una columna con el mismo nombre, como ROWID en Oracle. Si se pasa "ROWID" en un argumento de una función de catálogo, la función funcionará con la pseudocolumna ROWID si existe. Si la pseudocolumna no existe, la función funcionará con la columna "ROWID". Si se pasa ROWID en un argumento de una función de catálogo, la función funcionará con la columna ROWID.  
  
 Para obtener más información sobre los identificadores entre comillas, vea [identificadores entre comillas](../../../odbc/reference/develop-app/quoted-identifiers.md).
