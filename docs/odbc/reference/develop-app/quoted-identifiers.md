---
title: Identificadores entrecomillados | Documentos de Microsoft
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
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], quoted identifiers
- quoted identifiers [ODBC]
ms.assetid: 729ba55f-743b-4a04-8c39-ac0a9914211d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e74c39ad73357e50c1040e8a90029c0bf65f7b6e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32911530"
---
# <a name="quoted-identifiers"></a>Identificadores entre comillas
En una instrucción SQL, los identificadores que contienen caracteres especiales o palabras clave de la coincidencia deben incluirse entre *caracteres de comillas de identificador*; identificadores dentro de estos caracteres se denominan *identificadoresentrecomillados*(también conocido como *identificadores delimitados* en SQL-92). Por ejemplo, el identificador de cuentas por pagar se definen en la siguiente **seleccione** instrucción:  
  
```  
SELECT * FROM "Accounts Payable"  
```  
  
 La razón para entrecomillar los identificadores es que analizar la instrucción. Por ejemplo, si las cuentas por pagar no se entrecomilló en la instrucción anterior, el analizador se había dos tablas, las cuentas y por pagar, se supone y devolver un error de sintaxis que no estaban separados por punto y coma. El identificador de oferta caracteres son específicos del controlador y se recuperan con la opción SQL_IDENTIFIER_QUOTE_CHAR en **SQLGetInfo**. Las listas de caracteres especiales y de las palabras clave se recuperan con las opciones SQL_SPECIAL_CHARACTERS y SQL_KEYWORDS en **SQLGetInfo**.  
  
 Para que sea segura, aplicaciones interoperables a menudo entrecomillar todos los identificadores excepto los de las pseudocolumnas, por ejemplo, la columna ROWID en Oracle. **SQLSpecialColumns** devuelve una lista de las pseudocolumnas. Además, si hay restricciones específicas de la aplicación en donde pueden aparecer los caracteres especiales en un nombre de objeto, es mejor para aplicaciones interoperables para que no use caracteres especiales en las posiciones.
