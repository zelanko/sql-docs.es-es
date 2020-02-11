---
title: Resumen de la interfaz del proveedor de servicios ODBC | Microsoft Docs
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
ms.openlocfilehash: 0a97bed3bb921b9c881a98d8d9a9031ef7630f26
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68111905"
---
# <a name="odbc-service-provider-interface-summary"></a>Resumen de la interfaz del proveedor de servicios de ODBC
En la tabla siguiente se describen las funciones de la interfaz del proveedor de servicios ODBC. Para obtener más información sobre la sintaxis y la semántica de cada función, vea referencia de la [interfaz del proveedor de servicios ODBC (SPI)](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md).  
  
|Nombre de función|Propósito|  
|-------------------|-------------|  
|[SQLSetConnectAttrForDbcInfo](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Igual que [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md), pero establece el atributo en el token de información de conexión en lugar de en el identificador de conexión.|  
|[SQLSetDriverConnectInfo](../../../odbc/reference/syntax/sqldrivertodatasource-function.md)|Establece la cadena de conexión en el token de información de conexión para la llamada [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) de una aplicación.|  
|[SQLSetConnectInfo](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Establece el origen de datos, el identificador de usuario y la contraseña en el token de información de conexión de la llamada de [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) de una aplicación.|  
|[SQLGetPoolID](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Recupera el identificador del grupo.|  
|[SQLRateConnection](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Determina si un controlador puede reutilizar una conexión existente en el grupo de conexiones.|  
|[SQLPoolConnect](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Cree una nueva conexión si no se puede volver a usar una conexión en el grupo.|  
|[SQLCleanupConnectionPoolID](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Informa a un controlador de que se ha agotado el tiempo de espera de un ID. de grupo.|
