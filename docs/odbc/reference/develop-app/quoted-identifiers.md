---
title: Identificadores entre comillas | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], quoted identifiers
- quoted identifiers [ODBC]
ms.assetid: 729ba55f-743b-4a04-8c39-ac0a9914211d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b0a81237eddd4836394cc9797a79690ba4b49a35
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62861650"
---
# <a name="quoted-identifiers"></a>Identificadores entre comillas
En una instrucción SQL, los identificadores que contienen caracteres especiales o palabras clave de la coincidencia deben incluirse en *los caracteres de comillas identificador*; identificadores dentro de estos caracteres se conocen como *identificadoresentrecomillados*(también conocido como *identificadores delimitados* en SQL-92). Por ejemplo, el identificador de cuentas por pagar está entre comillas en la siguiente **seleccione** instrucción:  
  
```  
SELECT * FROM "Accounts Payable"  
```  
  
 Es el motivo de los identificadores de comillas que pueden analizar la instrucción. Por ejemplo, si cuentas por pagar no está entre comillas en la instrucción anterior, el analizador podría suponen había dos tablas, las cuentas y a pagar y devolver un error de sintaxis que no estaban separados por comas. El identificador de carácter de comilla son específicos del controlador y se recuperan con la opción SQL_IDENTIFIER_QUOTE_CHAR en **SQLGetInfo**. La lista de caracteres especiales y de palabras clave se recupera con las opciones SQL_SPECIAL_CHARACTERS y SQL_KEYWORDS **SQLGetInfo**.  
  
 Para estar seguros, aplicaciones interoperables suelen citar todos los identificadores, excepto los de las pseudocolumnas, como la columna ROWID en Oracle. **SQLSpecialColumns** devuelve una lista de las pseudocolumnas. Además, si hay restricciones específicas de la aplicación en donde pueden aparecer caracteres especiales en un nombre de objeto, es mejor para aplicaciones interoperables, no se debe utilizar caracteres especiales en las posiciones.
