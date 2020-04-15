---
title: Resumen de la interfaz del proveedor de servicios ODBC (ODBC Service Provider Interface Summary) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ace6085b-355b-435b-8734-503fc3c12ec2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b2f7e459cc7b89106bf1b7ebcd49c699d43da9f6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298902"
---
# <a name="odbc-service-provider-interface-summary"></a>Resumen de la interfaz del proveedor de servicios de ODBC
En la tabla siguiente se describen las funciones de interfaz del proveedor de servicios ODBC. Para obtener más información acerca de la sintaxis y la semántica de cada función, vea Referencia de la interfaz de proveedor de servicios [ODBC (SPI).](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md)  
  
|Nombre de función|Propósito|  
|-------------------|-------------|  
|[SQLSetConnectAttrForDbcInfo](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Igual que [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md), pero establece el atributo en el token de información de conexión en lugar de en el identificador de conexión.|  
|[SQLSetDriverConnectInfo](../../../odbc/reference/syntax/sqldrivertodatasource-function.md)|Establece la cadena de conexión en el token de información de conexión para la llamada [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) de una aplicación.|  
|[SQLSetConnectInfo](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Establece el origen de datos, el identificador de usuario y la contraseña en el token de información de conexión para la llamada [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) de una aplicación.|  
|[SQLGetPoolID](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Recupera el identificador del grupo.|  
|[SQLRateConnection](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Determina si un controlador puede reutilizar una conexión existente en el grupo de conexiones.|  
|[SQLPoolConnect](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Cree una nueva conexión si no se puede reutilizar ninguna conexión en el grupo.|  
|[SQLCleanupConnectionPoolID](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|Informa a un conductor de que se ha acabo el tiempo de espera de un identificador de grupo.|
