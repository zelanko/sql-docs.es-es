---
title: Las cadenas de conexión | Documentos de Microsoft
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
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e5b88b1056d8b645614a7f17fd6edf81eb804f16
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="connection-strings"></a>Cadenas de conexión
Una cadena de conexión contiene información utilizada para establecer una conexión. Una cadena de conexión completa contiene toda la información necesaria para establecer una conexión. La cadena de conexión es una serie de pares de palabra clave/valor separados por punto y coma. (Para obtener la sintaxis completa de una cadena de conexión, consulte el [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) descripción de la función.) La cadena de conexión es utilizada por:  
  
-   **SQLDriverConnect**, que completa la cadena de conexión a la interacción con el usuario.  
  
-   **SQLBrowseConnect**, que completa la cadena de conexión de forma iterativa con el origen de datos.  
  
 **SQLConnect** no usa una cadena de conexión; mediante **SQLConnect** es análogo a conectarse con una cadena de conexión con exactamente tres pares de palabra clave/valor (para el nombre del origen de datos y, opcionalmente, el usuario ID y la contraseña) .
