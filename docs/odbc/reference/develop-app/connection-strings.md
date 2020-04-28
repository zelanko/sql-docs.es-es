---
title: Cadenas de conexión | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bbbb5b4672a8ea393380063887cfd77b3e910238
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299035"
---
# <a name="connection-strings"></a>Cadenas de conexión
Una cadena de conexión contiene información que se usa para establecer una conexión. Una cadena de conexión completa contiene toda la información necesaria para establecer una conexión. La cadena de conexión es una serie de pares de palabra clave y valor separados por punto y coma. (Para obtener la sintaxis completa de una cadena de conexión, consulte la descripción de la función [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) ). Utiliza la cadena de conexión:  
  
-   **SQLDriverConnect**, que completa la cadena de conexión mediante la interacción con el usuario.  
  
-   **SQLBrowseConnect**, que completa la cadena de conexión de forma iterativa con el origen de datos.  
  
 **SQLConnect** no utiliza una cadena de conexión; el uso de **SQLConnect** es análogo a la conexión mediante una cadena de conexión con exactamente tres pares de palabra clave y valor (para el nombre del origen de datos y, opcionalmente, el ID. de usuario y la contraseña).
