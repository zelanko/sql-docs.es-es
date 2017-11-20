---
title: Referencia de interfaz (SPI) del proveedor de servicio ODBC | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: cdeffb4a-f344-4abe-97f3-be2ede1c8e59
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a4521d90f3e7eda4167062bd8bc1299921b0e31d
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

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

