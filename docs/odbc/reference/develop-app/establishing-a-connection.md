---
title: "Establecer una conexión | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data sources [ODBC], connection functions
- SQLBrowseConnect function [ODBC], establising a connection
- functions [ODBC], data source or driver connections
- connecting to data source [ODBC], functions
- connecting to driver [ODBC], functions
- connection functions [ODBC]
- SQLConnect function [ODBC], establising a connection
- SQLDriverConnect function [ODBC], making a connection
- ODBC drivers [ODBC], connection functions
ms.assetid: 8e3c717e-35e3-47ef-b5d3-3a96eeb7b869
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 43e7ab9f883df271f47b0ad55a931ce1a2d2c220
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="establishing-a-connection"></a>Establecer una conexión
Después de asignar identificadores de entorno y de conexión y establecer los atributos de conexión, la aplicación está preparada conectar con el origen de datos o el controlador. Hay tres funciones diferentes, la aplicación puede utilizar para hacer esto: **SQLConnect** (principales del nivel de conformidad de interfaz), **SQLDriverConnect** (principal), y **SQLBrowseConnect**(Nivel 1). Cada uno de los tres está diseñado para utilizarse en un escenario diferente. Antes de conectarse, la aplicación puede determinar cuál de estas funciones es compatible con la **ConnectFunctions** palabra clave devuelto por **SQLDrivers**.  
  
> [!NOTE]  
>  Algunos controladores de limitan el número de conexiones activas que admiten. Una aplicación llama **SQLGetInfo** con la opción SQL_MAX_DRIVER_CONNECTIONS para determinar el número de conexiones activo es compatible con un controlador en particular.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Origen de datos predeterminado](../../../odbc/reference/develop-app/default-data-source.md)  
  
-   [Conexión con SQLConnect](../../../odbc/reference/develop-app/connecting-with-sqlconnect.md)  
  
-   [Cadenas de conexión](../../../odbc/reference/develop-app/connection-strings.md)  
  
-   [Conexión con SQLDriverConnect](../../../odbc/reference/develop-app/connecting-with-sqldriverconnect.md)  
  
-   [Conectar con SQLBrowseConnect](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md)
