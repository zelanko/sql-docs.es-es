---
title: Conectar con SQLBrowseConnect | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- connecting to driver [ODBC], SQLBrowseConnect
- SQLBrowseConnect function [ODBC], connecting
- connecting to data source [ODBC], SQLBrowseConnect
ms.assetid: 6c2e9f76-b766-48df-b109-246bb05ae45d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f6382b0a02963395008dd02c962c10479aa5f29d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="connecting-with-sqlbrowseconnect"></a>Conectar con SQLBrowseConnect
**SQLBrowseConnect**, como **SQLDriverConnect**, usa una cadena de conexión. Sin embargo, mediante el uso de **SQLBrowseConnect**, una aplicación puede construir una cadena de conexión completa en tiempo de ejecución. Esto permite a la aplicación hacer dos cosas:  
  
-   Crear sus propios cuadros de diálogo para solicitar esta información, reteniendo así el control sobre su "apariencia y funcionamiento."  
  
-   Buscar en el sistema los orígenes de datos que un controlador determinado puede utilizar, posiblemente en varios pasos. Por ejemplo, el usuario podría buscar primero en la red los servidores y, después de elegir un servidor, buscar en el servidor las bases de datos accesibles para el controlador.  
  
 La aplicación llama **SQLBrowseConnect** y pasa una cadena de conexión, que se conoce como el *examinar cadena de conexión de la solicitud,* que especifica un controlador u origen de datos. El controlador devuelve una cadena de conexión, que se conoce como el *examinar cadena de conexión de resultados,* que contiene palabras clave, los valores posibles (si la palabra clave acepta un conjunto discreto de valores) y nombres descriptivos. La aplicación genera un cuadro de diálogo con los nombres descriptivos y solicita al usuario para los valores. Compila una nueva cadena de conexión de solicitud de exploración de estos valores, a continuación y lo devuelve al controlador con otra llamada a **SQLBrowseConnect**.  
  
 Dado que las cadenas de conexión se pasan y hacia atrás, el controlador puede proporcionar varios niveles de exploración devolviendo una nueva cadena de conexión cuando la aplicación devuelve el antiguo. Por ejemplo, la primera vez que una aplicación llama **SQLBrowseConnect**, el controlador podría devolver palabras clave para pedir al usuario un nombre de servidor. Cuando la aplicación devuelve el nombre del servidor, el controlador podría devolver palabras clave para solicitar al usuario para una base de datos. El proceso de exploración estaría completado después de la aplicación devuelve el nombre de la base de datos.  
  
 Cada vez que **SQLBrowseConnect** devuelve una nueva cadena de conexión de resultados de exploración, devuelve SQL_NEED_DATA como su código de retorno. Esto indica que la aplicación que el proceso de conexión no está completado. Hasta que **SQLBrowseConnect** devuelve SQL_SUCCESS, la conexión está en un estado de datos necesario y no puede usarse para otros fines, como para establecer un atributo de conexión. La aplicación puede finalizar la conexión exploración proceso mediante una llamada a **SQLDisconnect**.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Ejemplo de exploración de SQL Server](../../../odbc/reference/develop-app/sql-server-browsing-example.md)
