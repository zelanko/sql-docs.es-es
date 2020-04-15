---
title: Conexión con SQLBrowseConnect Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to driver [ODBC], SQLBrowseConnect
- SQLBrowseConnect function [ODBC], connecting
- connecting to data source [ODBC], SQLBrowseConnect
ms.assetid: 6c2e9f76-b766-48df-b109-246bb05ae45d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e4d738d394bb3c507f6aa08f736016b51ac4fefb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294665"
---
# <a name="connecting-with-sqlbrowseconnect"></a>Conectar con SQLBrowseConnect
**SQLBrowseConnect**, como **SQLDriverConnect**, utiliza una cadena de conexión. Sin embargo, mediante **SQLBrowseConnect**, una aplicación puede construir una cadena de conexión completa en tiempo de ejecución. Esto permite a la aplicación hacer dos cosas:  
  
-   Cree sus propios cuadros de diálogo para solicitar esta información, conservando así el control sobre su "aspecto".  
  
-   Buscar en el sistema los orígenes de datos que un controlador determinado puede utilizar, posiblemente en varios pasos. Por ejemplo, el usuario podría buscar primero en la red los servidores y, después de elegir un servidor, buscar en el servidor las bases de datos accesibles para el controlador.  
  
 La aplicación llama a **SQLBrowseConnect** y pasa una cadena de conexión, conocida como la cadena de conexión de solicitud de *exploración,* que especifica un controlador o origen de datos. El controlador devuelve una cadena de conexión, conocida como cadena de conexión de resultados de *exploración,* que contiene palabras clave, valores posibles (si la palabra clave acepta un conjunto discreto de valores) y nombres fáciles de usar. La aplicación crea un cuadro de diálogo con los nombres fáciles de usar y solicita al usuario valores. A continuación, crea una nueva cadena de conexión de solicitud de exploración a partir de estos valores y devuelve esto al controlador con otra llamada a **SQLBrowseConnect**.  
  
 Dado que las cadenas de conexión se pasan de un lado a otro, el controlador puede proporcionar varios niveles de exploración devolviendo una nueva cadena de conexión cuando la aplicación devuelve la antigua. Por ejemplo, la primera vez que una aplicación llama a **SQLBrowseConnect**, el controlador puede devolver palabras clave para solicitar al usuario un nombre de servidor. Cuando la aplicación devuelve el nombre del servidor, el controlador puede devolver palabras clave para solicitar al usuario una base de datos. El proceso de exploración se completaría después de que la aplicación devolviera el nombre de la base de datos.  
  
 Cada vez que **SQLBrowseConnect** devuelve una nueva cadena de conexión de resultados de exploración, devuelve SQL_NEED_DATA como su código de retorno. Esto indica a la aplicación que el proceso de conexión no está completo. Hasta que **SQLBrowseConnect** devuelve SQL_SUCCESS, la conexión está en un estado Need Data y no se puede usar para otros fines, como establecer un atributo de conexión. La aplicación puede finalizar el proceso de exploración de la conexión llamando a **SQLDisconnect**.  
  
 Esta sección contiene el tema siguiente.  
  
-   [Ejemplo de exploración de SQL Server](../../../odbc/reference/develop-app/sql-server-browsing-example.md)
