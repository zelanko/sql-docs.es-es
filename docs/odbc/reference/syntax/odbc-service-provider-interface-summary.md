---
title: Resumen de interfaz del proveedor de servicio ODBC | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ace6085b-355b-435b-8734-503fc3c12ec2
caps.latest.revision: "4"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d5cd2ab9be5c49365e0a398677c901c4f2d46d9f
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="odbc-service-provider-interface-summary"></a>Resumen de interfaz del proveedor de servicio ODBC
En la tabla siguiente describe las funciones de la interfaz de proveedor de servicios de ODBC. Para obtener más información sobre la sintaxis y semántica para cada función, consulte [referencia de interfaz de proveedor de servicio de ODBC (SPI)](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md).  
  
|Nombre de función|Finalidad|  
|-------------------|-------------|  
|[SQLSetConnectAttrForDbcInfo](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Igual que [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md), sino que establece el atributo en el token de la información de conexión en lugar de en el identificador de conexión.|  
|[SQLSetDriverConnectInfo](../../../odbc/reference/syntax/sqldrivertodatasource-function.md)|Establece la cadena de conexión en el símbolo (token) de información de conexión para una aplicación [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) llamar.|  
|[SQLSetConnectInfo](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Establece el origen de datos, el Id. de usuario y la contraseña en el símbolo (token) de información de conexión para una aplicación [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) llamar.|  
|[SQLGetPoolID](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Recupera el identificador de grupo.|  
|[SQLRateConnection](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Determina si un controlador puede reutilizar una conexión existente en la agrupación de conexiones.|  
|[SQLPoolConnect](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Crear una nueva conexión si no se puede reutilizar conexión en el grupo.|  
|[SQLCleanupConnectionPoolID](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Informa a un controlador que se agotó un Id. de grupo.|
