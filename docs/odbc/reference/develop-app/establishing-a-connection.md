---
title: Establecimiento de una conexión ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], connection functions
- SQLBrowseConnect function [ODBC], establishing a connection
- functions [ODBC], data source or driver connections
- connecting to data source [ODBC], functions
- connecting to driver [ODBC], functions
- connection functions [ODBC]
- SQLConnect function [ODBC], establishing a connection
- SQLDriverConnect function [ODBC], making a connection
- ODBC drivers [ODBC], connection functions
ms.assetid: 8e3c717e-35e3-47ef-b5d3-3a96eeb7b869
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6f71190a8a2ca1dd8af0d28adb5531540fb1b57e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298705"
---
# <a name="establishing-a-connection"></a>Establecer una conexión
Después de asignar identificadores de entorno y conexión y establecer los atributos de conexión, la aplicación está lista para conectarse al origen de datos o al controlador. Hay tres funciones diferentes que la aplicación puede usar para hacer esto: **SQLConnect** (nivel de conformidad de la interfaz principal), **SQLDriverConnect** (núcleo) y **SQLBrowseConnect** (nivel 1). Cada uno de los tres está diseñado para ser utilizado en un escenario diferente. Antes de conectarse, la aplicación puede determinar cuál de estas funciones se admite con la palabra clave **ConnectFunctions** devuelta por **SQLDrivers**.  
  
> [!NOTE]  
>  Algunos controladores limitan el número de conexiones activas que admiten. Una aplicación llama a **SQLGetInfo** con la opción SQL_MAX_DRIVER_CONNECTIONS para determinar cuántas conexiones activas admite un controlador determinado.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Origen de datos predeterminado](../../../odbc/reference/develop-app/default-data-source.md)  
  
-   [Conexión con SQLConnect](../../../odbc/reference/develop-app/connecting-with-sqlconnect.md)  
  
-   [Cadenas de conexión](../../../odbc/reference/develop-app/connection-strings.md)  
  
-   [Conexión con SQLDriverConnect](../../../odbc/reference/develop-app/connecting-with-sqldriverconnect.md)  
  
-   [Conectar con SQLBrowseConnect](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md)
