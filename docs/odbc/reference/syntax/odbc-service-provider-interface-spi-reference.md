---
title: Referencia de la interfaz de proveedor de servicios ODBC (SPI) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: cdeffb4a-f344-4abe-97f3-be2ede1c8e59
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e9739abd13bf2c4bed1b1b3a31c18c683594705a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298913"
---
# <a name="odbc-service-provider-interface-spi-reference"></a>Referencia de la interfaz del proveedor de servicios (SPI) de ODBC
Tradicionalmente, ODBC define una interfaz de programación de aplicaciones (API). Las aplicaciones pueden llamar a las funciones de la API y deben implementarse dentro del Administrador de controladores y el controlador.  
  
 Con la adición de la característica de agrupación de conexiones compatible con controladores, ODBC introduce la interfaz de proveedor de servicios (SPI). Las funciones del SPI se utilizan para la comunicación entre el Administrador de controladores y el controlador. Las funciones SPI son implementadas por el controlador; el Administrador de controladores no expone las funciones SPI a las aplicaciones. Las aplicaciones no deben llamar a estas funciones directamente.  
  
 Incluya sqlspi.h para el desarrollo de controladores ODBC.  
  
 Esta sección contiene los temas siguientes  
  
-   [SQLCleanupConnectionPoolID](../../../odbc/reference/syntax/sqlcleanupconnectionpoolid-function.md)  
  
-   [SQLGetPoolID](../../../odbc/reference/syntax/sqlgetpoolid-function.md)  
  
-   [SQLPoolConnect](../../../odbc/reference/syntax/sqlpoolconnect-function.md)  
  
-   [SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md)  
  
-   [SQLSetConnectAttrForDbcInfo](../../../odbc/reference/syntax/sqlsetconnectattrfordbcinfo-function.md)  
  
-   [SQLSetConnectInfo](../../../odbc/reference/syntax/sqlsetconnectinfo-function.md)  
  
-   [SQLSetDriverConnectInfo](../../../odbc/reference/syntax/installation-and-configuration-wwi-oltp.md)  
  
## <a name="see-also"></a>Consulte también  
 [Desarrollo de un controlador ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Desarrollo de la conciencia de la agrupación de conexiones en un controlador ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)   
 [Agrupación de conexiones de administrador de controladores](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md)
