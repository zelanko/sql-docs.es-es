---
title: Resumen de interfaz del proveedor de servicio ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ace6085b-355b-435b-8734-503fc3c12ec2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d5f3c133b105c905b79589d86952658b6d39f0f6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62653392"
---
# <a name="odbc-service-provider-interface-summary"></a>Resumen de la interfaz del proveedor de servicios de ODBC
En la tabla siguiente se describe las funciones de interfaz de proveedor de servicios de ODBC. Para obtener más información sobre la sintaxis y semántica para cada función, vea [referencia de la interfaz de proveedor de servicios (SPI) de ODBC](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md).  
  
|Nombre de función|Finalidad|  
|-------------------|-------------|  
|[SQLSetConnectAttrForDbcInfo](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Igual que [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md), pero establece el atributo en el token de la información de conexión en lugar de en el identificador de conexión.|  
|[SQLSetDriverConnectInfo](../../../odbc/reference/syntax/sqldrivertodatasource-function.md)|Establece la cadena de conexión en el token de la información de conexión para una aplicación [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) llamar.|  
|[SQLSetConnectInfo](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Establece el origen de datos, el Id. de usuario y la contraseña en el símbolo (token) de información de conexión para una aplicación [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) llamar.|  
|[SQLGetPoolID](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Recupera el identificador de grupo.|  
|[SQLRateConnection](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Determina si un controlador puede reutilizar una conexión existente en el grupo de conexiones.|  
|[SQLPoolConnect](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Crear una nueva conexión si no se puede reutilizar conexión en el grupo.|  
|[SQLCleanupConnectionPoolID](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Informa a un controlador que se agotó un Id. de grupo.|
