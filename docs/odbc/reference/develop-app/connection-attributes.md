---
title: Atributos de conexión | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299046"
---
# <a name="connection-attributes"></a>Atributos de conexión
Los atributos de conexión son características de la conexión. Por ejemplo, dado que las transacciones se producen en el nivel de conexión, el nivel de aislamiento de transacción es un atributo de conexión. Del mismo modo, el tiempo de espera de inicio de sesión, o el número de segundos que se espera mientras se intenta conectar antes de agotarse el tiempo de espera, es un atributo de conexión.  
  
 Los atributos de conexión se establecen con **SQLSetConnectAttr** y su configuración actual se recupera con **SQLGetConnectAttr**. Si se llama a **SQLSetConnectAttr** antes de cargar el controlador, el administrador de controladores almacena los atributos en su estructura de conexión y los establece en el controlador como parte del proceso de conexión. No es necesario que una aplicación establezca ningún atributo de conexión; todos los atributos de conexión tienen valores predeterminados, algunos de los cuales son específicos del controlador.  
  
 Un atributo de conexión se puede establecer antes o después de la conexión, o bien, en función del atributo y del controlador. El tiempo de espera de inicio de sesión (SQL_ATTR_LOGIN_TIMEOUT) se aplica al proceso de conexión y solo es efectivo si se establece antes de la conexión. Los atributos que especifican si se debe establecer el uso de la biblioteca de cursores ODBC (SQL_ATTR_ODBC_CURSORS) y el tamaño de paquete de red (SQL_ATTR_PACKET_SIZE) antes de la conexión, ya que la biblioteca de cursores ODBC reside entre el administrador de controladores y el controlador y, por tanto, debe cargarse antes del controlador.  
  
 Los atributos para especificar si un origen de datos es de solo lectura o de lectura y escritura (SQL_ATTR_ACCESS_MODE) y el catálogo actual (SQL_ATTR_CURRENT_CATALOG) se puede establecer antes o después de la conexión, en función del controlador. Sin embargo, las aplicaciones interoperables las establecen antes de la conexión porque algunos controladores no admiten el cambio de estos después de la conexión.  
  
 Algunos atributos de conexión tienen un valor predeterminado antes de que se realice la conexión, mientras que otros no. Las que sí lo hacen son SQL_ATTR_ACCESS_MODE, SQL_ATTR_AUTOCOMMIT, SQL_ATTR_LOGIN_TIMEOUT, SQL_ATTR_ODBC_CURSORS, SQL_ATTR_TRACE y SQL_ATTR_TRACEFILE.  
  
 Los atributos de conexión de traducción (SQL_ATTR_TRANSLATE_DLL y SQL_ATTR_TRANSLATE_OPTION) deben establecerse después de la conexión.  
  
 Todos los demás atributos de conexión se pueden establecer en cualquier momento. Para obtener más información, consulte la descripción de la función [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md) . (Los atributos de conexión no se pueden establecer en el nivel de entorno mediante una llamada a **SQLSetEnvAttr**).
