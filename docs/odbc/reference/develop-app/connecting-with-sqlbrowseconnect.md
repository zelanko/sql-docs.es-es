---
description: Conectar con SQLBrowseConnect
title: Conectar con SQLBrowseConnect | Microsoft Docs
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
ms.openlocfilehash: d7ad54276f54155c68fbdbe984642dda4300a7c1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424827"
---
# <a name="connecting-with-sqlbrowseconnect"></a>Conectar con SQLBrowseConnect
**SQLBrowseConnect**, como **SQLDriverConnect**, utiliza una cadena de conexión. Sin embargo, mediante **SQLBrowseConnect**, una aplicación puede crear una cadena de conexión completa en tiempo de ejecución. Esto permite a la aplicación hacer dos cosas:  
  
-   Cree sus propios cuadros de diálogo para solicitar esta información, conservando así el control sobre su "aspecto y funcionamiento".  
  
-   Buscar en el sistema los orígenes de datos que un controlador determinado puede utilizar, posiblemente en varios pasos. Por ejemplo, el usuario podría buscar primero en la red los servidores y, después de elegir un servidor, buscar en el servidor las bases de datos accesibles para el controlador.  
  
 La aplicación llama a **SQLBrowseConnect** y pasa una cadena de conexión, conocida como la cadena de conexión de la *solicitud de exploración,* que especifica un controlador o un origen de datos. El controlador devuelve una cadena de conexión, conocida como la cadena de conexión del resultado de la *exploración,* que contiene palabras clave, valores posibles (si la palabra clave acepta un conjunto discreto de valores) y nombres descriptivos. La aplicación crea un cuadro de diálogo con los nombres descriptivos y solicita al usuario los valores. A continuación, crea una nueva cadena de conexión de solicitud de búsqueda a partir de estos valores y lo devuelve al controlador con otra llamada a **SQLBrowseConnect**.  
  
 Dado que las cadenas de conexión se pasan atrás y adelante, el controlador puede proporcionar varios niveles de exploración mediante la devolución de una nueva cadena de conexión cuando la aplicación devuelve la antigua. Por ejemplo, la primera vez que una aplicación llama a **SQLBrowseConnect**, el controlador podría devolver palabras clave para solicitar al usuario un nombre de servidor. Cuando la aplicación devuelve el nombre del servidor, el controlador podría devolver palabras clave para preguntar al usuario sobre una base de datos. El proceso de exploración se completará después de que la aplicación devuelva el nombre de la base de datos.  
  
 Cada vez que **SQLBrowseConnect** devuelve una nueva cadena de conexión de resultado de búsqueda, devuelve SQL_NEED_DATA como su código de retorno. Esto indica a la aplicación que el proceso de conexión no se ha completado. Hasta **SQLBrowseConnect** devuelve SQL_SUCCESS, la conexión se encuentra en un estado de datos necesario y no se puede usar para otros propósitos, como para establecer un atributo de conexión. La aplicación puede finalizar el proceso de exploración de conexión mediante una llamada a **SQLDisconnect**.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Ejemplo de exploración de SQL Server](../../../odbc/reference/develop-app/sql-server-browsing-example.md)
