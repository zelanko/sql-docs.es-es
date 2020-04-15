---
title: Atributos de conexión ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c295ce88eedf1d4cddc4173f5dea39c44b01f83d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299046"
---
# <a name="connection-attributes"></a>Atributos de conexión
Los atributos de conexión son características de la conexión. Por ejemplo, dado que las transacciones se producen en el nivel de conexión, el nivel de aislamiento de transacción es un atributo de conexión. De forma similar, el tiempo de espera de inicio de sesión, o el número de segundos que hay que esperar al intentar conectarse antes de agotar el tiempo de espera, es un atributo de conexión.  
  
 Los atributos de conexión se establecen con **SQLSetConnectAttr** y su configuración actual recuperada con **SQLGetConnectAttr**. Si **SQLSetConnectAttr** se llama antes de cargar el controlador, el Administrador de controladores almacena los atributos en su estructura de conexión y los establece en el controlador como parte del proceso de conexión. No hay ningún requisito de que una aplicación establezca atributos de conexión; todos los atributos de conexión tienen valores predeterminados, algunos de los cuales son específicos del controlador.  
  
 Un atributo de conexión se puede establecer antes o después de la conexión, o bien, dependiendo del atributo y el controlador. El tiempo de espera de inicio de sesión (SQL_ATTR_LOGIN_TIMEOUT) se aplica al proceso de conexión y solo es efectivo si se establece antes de conectarse. Los atributos que especifican si se debe utilizar la biblioteca de cursores ODBC (SQL_ATTR_ODBC_CURSORS) y el tamaño del paquete de red (SQL_ATTR_PACKET_SIZE) deben establecerse antes de conectarse, porque la biblioteca de cursores ODBC reside entre el Administrador de controladores y el controlador y, por lo tanto, debe cargarse antes que el controlador.  
  
 Los atributos para especificar si un origen de datos es de solo lectura o de lectura y escritura (SQL_ATTR_ACCESS_MODE) y el catálogo actual (SQL_ATTR_CURRENT_CATALOG) se puede establecer antes o después de la conexión, dependiendo del controlador. Sin embargo, las aplicaciones interoperables las establecen antes de conectarse porque algunos controladores no admiten cambiarlos después de la conexión.  
  
 Algunos atributos de conexión tienen un valor predeterminado antes de realizar la conexión, mientras que otros no. Los que lo hacen son SQL_ATTR_ACCESS_MODE, SQL_ATTR_AUTOCOMMIT, SQL_ATTR_LOGIN_TIMEOUT, SQL_ATTR_ODBC_CURSORS, SQL_ATTR_TRACE y SQL_ATTR_TRACEFILE.  
  
 Los atributos de conexión de traducción (SQL_ATTR_TRANSLATE_DLL y SQL_ATTR_TRANSLATE_OPTION) deben establecerse después de conectarse.  
  
 Todos los demás atributos de conexión se pueden establecer en cualquier momento. Para obtener más información, vea la descripción de la función [SQLSetConnectAttr.](../../../odbc/reference/syntax/sqlsetconnectattr-function.md) (Los atributos de conexión no se pueden establecer en el nivel de entorno mediante una llamada a **SQLSetEnvAttr**.)
