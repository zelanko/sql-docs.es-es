---
title: Identificadores citados ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0c03fa8bbc059566288997b29c899056f26de252
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282008"
---
# <a name="quoted-identifiers"></a>Identificadores entre comillas
En una instrucción SQL, los identificadores que contengan caracteres especiales o palabras clave de coincidencia deben incluirse entre *caracteres de comillas*identificador; los identificadores incluidos en estos caracteres se conocen como *identificadores entrecomillas* (también conocidos como *identificadores delimitados* en SQL-92). Por ejemplo, el identificador Deproveedores se cotiza en el siguiente extracto **SELECT:**  
  
```  
SELECT * FROM "Accounts Payable"  
```  
  
 La razón para citar identificadores es hacer que la instrucción sea analizable. Por ejemplo, si Proveedores no se cotizaen en el extracto anterior, el analizador asumiría que había dos tablas, Cuentas y Proveedor, y devolvería un error de sintaxis que indica que no estaban separados por una coma. El carácter de comillas identificador es específico del controlador y se recupera con la opción SQL_IDENTIFIER_QUOTE_CHAR en **SQLGetInfo**. Las listas de caracteres especiales y de palabras clave se recuperan con las opciones SQL_SPECIAL_CHARACTERS y SQL_KEYWORDS de **SQLGetInfo**.  
  
 Para ser seguras, las aplicaciones interoperables a menudo citan todos los identificadores excepto los de pseudocolumnas, como la columna ROWID en Oracle. **SQLSpecialColumns** devuelve una lista de pseudocolumnas. Además, si hay restricciones específicas de la aplicación sobre dónde pueden aparecer caracteres especiales en un nombre de objeto, es mejor que las aplicaciones interoperables no utilicen caracteres especiales en esas posiciones.
