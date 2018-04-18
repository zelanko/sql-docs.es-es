---
title: Referencia de interfaz (SPI) del proveedor de servicio ODBC | Documentos de Microsoft
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
ms.assetid: cdeffb4a-f344-4abe-97f3-be2ede1c8e59
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1bd481d7344345578f830374f7049a917e60eb68
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="odbc-service-provider-interface-spi-reference"></a>Referencia de interfaz (SPI) del proveedor de servicio ODBC
Tradicionalmente, ODBC define una interfaz de programación de aplicaciones (API). Las funciones de la API pueden llamarse mediante aplicaciones y se deben implementar en el Administrador de controladores y el controlador.  
  
 Con la adición de la característica de agrupación de conexiones dependientes del controlador, ODBC presenta la interfaz de proveedor de servicio (SPI). Las funciones en el SPI se utilizan para la comunicación entre el Administrador de controladores y el controlador. Funciones SPI se implementan con el controlador; el Administrador de controladores no exponen funciones SPI para las aplicaciones. Las aplicaciones no deben llamar directamente a estas funciones.  
  
 Incluir sqlspi.h para el desarrollo del controlador ODBC.  
  
 Esta sección contiene los temas siguientes  
  
-   [SQLCleanupConnectionPoolID](../../../odbc/reference/syntax/sqlcleanupconnectionpoolid-function.md)  
  
-   [SQLGetPoolID](../../../odbc/reference/syntax/sqlgetpoolid-function.md)  
  
-   [SQLPoolConnect](../../../odbc/reference/syntax/sqlpoolconnect-function.md)  
  
-   [SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md)  
  
-   [SQLSetConnectAttrForDbcInfo](../../../odbc/reference/syntax/sqlsetconnectattrfordbcinfo-function.md)  
  
-   [SQLSetConnectInfo](../../../odbc/reference/syntax/sqlsetconnectinfo-function.md)  
  
-   [SQLSetDriverConnectInfo](../../../odbc/reference/syntax/installation-and-configuration-wwi-oltp.md)  
  
## <a name="see-also"></a>Vea también  
 [Desarrollar un controlador ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Desarrollar el conocimiento de la agrupación de conexiones en un controlador ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)   
 [Agrupación de conexiones de administrador de controladores](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md)
