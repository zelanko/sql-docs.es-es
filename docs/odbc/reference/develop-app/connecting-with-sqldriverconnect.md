---
title: Conexión con SQLDriverConnect | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 78cdaabe867ae67e3a1dfcb80e82cfaf95a94ed1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63042221"
---
# <a name="connecting-with-sqldriverconnect"></a>Conexión con SQLDriverConnect
**SQLDriverConnect** se usa para conectarse a un origen de datos mediante una cadena de conexión. **SQLDriverConnect** se utiliza en lugar de **SQLConnect** por las razones siguientes:  
  
-   Para permitir que la aplicación use información de conexión específicos del controlador.  
  
-   Para solicitar que el controlador solicite al usuario la información de conexión.  
  
-   Para conectarse sin especificar un origen de datos.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Información de conexión específicos del controlador](../../../odbc/reference/develop-app/driver-specific-connection-information.md)  
  
-   [Preguntar al usuario información de conexión](../../../odbc/reference/develop-app/prompting-the-user-for-connection-information.md)  
  
-   [Conectar con orígenes de datos de archivo](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)  
  
-   [Conectar directamente a los controladores](../../../odbc/reference/develop-app/connecting-directly-to-drivers.md)
