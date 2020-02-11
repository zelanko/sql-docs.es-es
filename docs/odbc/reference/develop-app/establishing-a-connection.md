---
title: Establecer una conexión | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7ef6f3d50382d810dd9df246c4d857d9467674f2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "76941027"
---
# <a name="establishing-a-connection"></a>Establecer una conexión
Después de asignar el entorno y los identificadores de conexión y establecer los atributos de conexión, la aplicación está lista para conectarse al origen de datos o al controlador. Hay tres funciones diferentes que la aplicación puede usar para ello: **SQLConnect** (nivel de conformidad de la interfaz principal), **SQLDriverConnect** (Core) y **SQLBrowseConnect** (nivel 1). Cada uno de los tres está diseñado para usarse en un escenario diferente. Antes de la conexión, la aplicación puede determinar cuál de estas funciones es compatible con la palabra clave **ConnectFunctions** devuelta por **SQLDrivers**.  
  
> [!NOTE]  
>  Algunos controladores limitan el número de conexiones activas que admiten. Una aplicación llama a **SQLGetInfo** con la opción SQL_MAX_DRIVER_CONNECTIONS para determinar el número de conexiones activas que admite un controlador determinado.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Origen de datos predeterminado](../../../odbc/reference/develop-app/default-data-source.md)  
  
-   [Conexión con SQLConnect](../../../odbc/reference/develop-app/connecting-with-sqlconnect.md)  
  
-   [Cadenas de conexión](../../../odbc/reference/develop-app/connection-strings.md)  
  
-   [Conexión con SQLDriverConnect](../../../odbc/reference/develop-app/connecting-with-sqldriverconnect.md)  
  
-   [Conectar con SQLBrowseConnect](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md)
