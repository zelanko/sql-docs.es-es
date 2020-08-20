---
description: Identificadores entre comillas
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cd317e5d92618d8b458d6d28fa870c6945e136fd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465685"
---
# <a name="quoted-identifiers"></a>Identificadores entre comillas
En una instrucción SQL, los identificadores que contienen caracteres especiales o palabras clave de coincidencia deben ir entre *comillas de identificador*. los identificadores incluidos en dichos caracteres se conocen como *identificadores entre comillas* (también conocidos como *identificadores delimitados* en SQL-92). Por ejemplo, el identificador de cuentas por pagar se encuentra entre comillas en la siguiente instrucción **Select** :  
  
```  
SELECT * FROM "Accounts Payable"  
```  
  
 El motivo de los identificadores de Comillas es hacer que la instrucción sea analizable. Por ejemplo, si no se incluyó en la instrucción anterior cuentas por pagar, el analizador supondría que había dos tablas, cuentas y pagos, y devolvería un error de sintaxis que no se separó con una coma. El carácter de comilla de identificador es específico del controlador y se recupera con la opción SQL_IDENTIFIER_QUOTE_CHAR en **SQLGetInfo**. Las listas de caracteres especiales y de palabras clave se recuperan con las opciones SQL_SPECIAL_CHARACTERS y SQL_KEYWORDS de **SQLGetInfo**.  
  
 Para ser segura, las aplicaciones interoperables suelen citar todos los identificadores, excepto los de las pseudo-columnas, como la columna ROWID de Oracle. **SQLSpecialColumns** devuelve una lista de pseudo columnas. Además, si hay restricciones específicas de la aplicación en las que los caracteres especiales pueden aparecer en un nombre de objeto, es mejor para las aplicaciones interoperables no usar caracteres especiales en dichas posiciones.
