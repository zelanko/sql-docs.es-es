---
title: Las cadenas de conexión | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], connection functions
- connecting to driver [ODBC], connection strings
- functions [ODBC], data source or driver connections
- connection strings [ODBC], about connection strings
- connecting to data source [ODBC], connection strings
- connecting to data source [ODBC], functions
- connecting to driver [ODBC], functions
- connection functions [ODBC]
- ODBC drivers [ODBC], connection functions
ms.assetid: 724c7b86-300a-4fa9-ad96-4afa0fdcb3e9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d7e52ec70e53608f1af48b4abcd2dd1edb4fc454
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63042589"
---
# <a name="connection-strings"></a>Cadenas de conexión
Una cadena de conexión contiene información utilizada para establecer una conexión. Una cadena de conexión completa contiene toda la información necesaria para establecer una conexión. La cadena de conexión es una serie de pares palabra clave-valor separados por punto y coma. (Para ver la sintaxis completa de una cadena de conexión, consulte el [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) descripción de la función.) Usa la cadena de conexión:  
  
-   **SQLDriverConnect**, lo que finaliza la cadena de conexión mediante la interacción con el usuario.  
  
-   **SQLBrowseConnect**, lo que finaliza la cadena de conexión de forma iterativa con el origen de datos.  
  
 **SQLConnect** no utiliza una cadena de conexión; el uso de **SQLConnect** es análoga a la conexión con una cadena de conexión exactamente tres pares palabra clave-valor (para el nombre del origen de datos y, opcionalmente, el usuario ID y contraseña) .
