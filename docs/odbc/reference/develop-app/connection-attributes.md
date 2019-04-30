---
title: Los atributos de conexión | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], connection attributes
- ODBC drivers [ODBC], connection attributes
- connecting to data source [ODBC], connection attributes
- connection attributes [ODBC]
- connecting to driver [ODBC], connection attributes
ms.assetid: e6d03089-30a3-4627-a642-591ba0980894
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f0fad1db10e40c71d22dd75417420c54cefa7803
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63194438"
---
# <a name="connection-attributes"></a>Atributos de conexión
Los atributos de conexión son características de la conexión. Por ejemplo, dado que las transacciones se producen en el nivel de conexión, el nivel de aislamiento de transacción es un atributo de conexión. De forma similar, el tiempo de espera de inicio de sesión o el número de segundos de espera al intentar conectarse antes de agotar el tiempo, es un atributo de conexión.  
  
 Los atributos de conexión se establecen con **SQLSetConnectAttr** y su configuración actual se recupera con **SQLGetConnectAttr**. Si **SQLSetConnectAttr** se llama antes de que el controlador se carga, los almacenes de administrador de controladores de los atributos en la estructura de la conexión y establece en el controlador como parte del proceso de conexión. No hay ningún requisito que una aplicación establecer los atributos de conexión; todos los atributos de conexión tienen valores predeterminados, algunos de los cuales son específicos del controlador.  
  
 Un atributo de conexión se puede establecer antes o después de la conexión, o bien, según el atributo y el controlador. El tiempo de espera de inicio de sesión (SQL_ATTR_LOGIN_TIMEOUT) se aplica al proceso de conexión y se establece solo si efectiva antes de conectarse. Los atributos que especifican si se debe usar la biblioteca de cursores ODBC (SQL_ATTR_ODBC_CURSORS) y el tamaño de paquete de red (SQL_ATTR_PACKET_SIZE) deben establecerse antes de conectarse, dado que la biblioteca de cursores ODBC reside entre el Administrador de controladores y el controlador y por lo tanto, debe cargarse antes del controlador.  
  
 Los atributos para especificar si un origen de datos es de solo lectura o lectura y escritura (SQL_ATTR_ACCESS_MODE) y el catálogo actual (SQL_ATTR_CURRENT_CATALOG) se pueden establecer antes o después de conectarse, según el controlador. Sin embargo, las aplicaciones interoperables establecerlos antes de conectarse porque algunos controladores no admiten el cambio estos después de conectarse.  
  
 Algunos atributos de conexión tienen un valor predeterminado antes de que se realiza la conexión, mientras que otros no. Aquellos que lo hacen son SQL_ATTR_ACCESS_MODE, SQL_ATTR_AUTOCOMMIT, SQL_ATTR_LOGIN_TIMEOUT, SQL_ATTR_ODBC_CURSORS, SQL_ATTR_TRACE y SQL_ATTR_TRACEFILE.  
  
 Después de conectarse, se deben establecer los atributos de conexión de traducción (SQL_ATTR_TRANSLATE_DLL y SQL_ATTR_TRANSLATE_OPTION).  
  
 Todos los demás atributos de conexión se pueden establecer en cualquier momento. Para obtener más información, consulte el [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md) descripción de la función. (Los atributos de conexión no se puede establecer en el nivel de entorno mediante una llamada a **SQLSetEnvAttr**.)
