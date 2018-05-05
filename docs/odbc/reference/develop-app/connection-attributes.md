---
title: Atributos de conexión | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], connection attributes
- ODBC drivers [ODBC], connection attributes
- connecting to data source [ODBC], connection attributes
- connection attributes [ODBC]
- connecting to driver [ODBC], connection attributes
ms.assetid: e6d03089-30a3-4627-a642-591ba0980894
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 90119e72be2ea64da85fc6790b4e28b9e679a8f6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="connection-attributes"></a>Atributos de conexión
Atributos de conexión son las características de la conexión. Por ejemplo, dado que las transacciones se producen en el nivel de conexión, el nivel de aislamiento de transacción es un atributo de conexión. De igual forma, el tiempo de espera de inicio de sesión, o el número de segundos de espera al intentar conectarse antes de tiempo de espera, es un atributo de conexión.  
  
 Atributos de conexión se establecen con **SQLSetConnectAttr** y su configuración actual se recupera con **SQLGetConnectAttr**. Si **SQLSetConnectAttr** se llama antes de que el controlador se carga, los almacenes de administrador de controladores los atributos de su estructura de conexión y establece en el controlador como parte del proceso de conexión. No hay ningún requisito que una aplicación establezca los atributos de conexión; todos los atributos de conexión tienen valores predeterminados, algunos de los cuales son específicos del controlador.  
  
 Un atributo de conexión se puede establecer antes o después de la conexión, o bien, según el atributo y el controlador. El tiempo de espera de inicio de sesión (SQL_ATTR_LOGIN_TIMEOUT) se aplica para el proceso de conexión y se establece solo efectivo si antes de conectarse. Los atributos que especifican si debe usar la biblioteca de cursores ODBC (SQL_ATTR_ODBC_CURSORS) y el tamaño de paquete de red (SQL_ATTR_PACKET_SIZE) deben establecerse antes de conectarse, dado que la biblioteca de cursores ODBC reside entre el Administrador de controladores y el controlador y por lo tanto debe cargarse antes el controlador.  
  
 Los atributos para especificar si un origen de datos es de solo lectura o lectura / escritura (SQL_ATTR_ACCESS_MODE) y el catálogo actual (SQL_ATTR_CURRENT_CATALOG) se pueden establecer antes o después de conectarse, según el controlador. Sin embargo, aplicaciones interoperables establecerlas antes de conectarse porque algunos controladores no admiten cambiar estos después de conectarse.  
  
 Algunos atributos de conexión tienen un valor predeterminado antes de realizar la conexión, mientras que otros no. Aquellos que lo hacen son SQL_ATTR_ACCESS_MODE, SQL_ATTR_AUTOCOMMIT, SQL_ATTR_LOGIN_TIMEOUT, SQL_ATTR_ODBC_CURSORS, SQL_ATTR_TRACE y SQL_ATTR_TRACEFILE.  
  
 Después de conectarse, se deben establecer los atributos de conexión de traducción (SQL_ATTR_TRANSLATE_DLL y SQL_ATTR_TRANSLATE_OPTION).  
  
 Todos los demás atributos de conexión se pueden establecer en cualquier momento. Para obtener más información, consulte el [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md) descripción de la función. (No se puede establecer atributos de conexión en el nivel de entorno mediante una llamada a **SQLSetEnvAttr**.)
