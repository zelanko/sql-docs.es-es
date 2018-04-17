---
title: Conexión con SQLDriverConnect | Documentos de Microsoft
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
- data sources [ODBC], connection functions
- functions [ODBC], data source or driver connections
- connecting to data source [ODBC], SQLDriverConnect
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], functions
- connecting to driver [ODBC], functions
- SQLDriverConnect function [ODBC], connecting
- connection functions [ODBC]
- ODBC drivers [ODBC], connection functions
ms.assetid: e46e959f-d3c5-4ddb-810a-107bfcb83fd2
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: df0467bdcb168e219639f3518069faa265edfe9d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="connecting-with-sqldriverconnect"></a>Conexión con SQLDriverConnect
**SQLDriverConnect** se utiliza para conectarse a un origen de datos utilizando una cadena de conexión. **SQLDriverConnect** se utiliza en lugar de **SQLConnect** por las razones siguientes:  
  
-   Para permitir que la aplicación use información de conexión específicos del controlador.  
  
-   Para solicitar que el controlador solicite al usuario la información de conexión.  
  
-   Para conectarse sin especificar un origen de datos.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Información de conexión específicos del controlador](../../../odbc/reference/develop-app/driver-specific-connection-information.md)  
  
-   [Preguntar al usuario información de conexión](../../../odbc/reference/develop-app/prompting-the-user-for-connection-information.md)  
  
-   [Conectar con orígenes de datos de archivo](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)  
  
-   [Conectar directamente a los controladores](../../../odbc/reference/develop-app/connecting-directly-to-drivers.md)
