---
title: Asignar un identificador de instrucción | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQLSetStmtAttr function
- statements [ODBC], statement handles
- ODBC applications, executing queries
- SQLGetStmtAttr function
- SQL Server Native Client ODBC driver, statements
- allocating statement handles
- ODBC applications, statements
- statement handles [ODBC]
- SQLAllocHandle function
ms.assetid: 9ee207f3-2667-45f5-87ca-e6efa1fd7a5c
caps.latest.revision: 29
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 22b207f02fd2cbf4cffa10af8ebab1cb6ba268e7
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37430444"
---
# <a name="allocating-a-statement-handle"></a>Asignar un identificador de instrucción
  Antes de que una aplicación pueda ejecutar una instrucción, debe asignar un identificador de instrucción. Esto hace una llamada a **SQLAllocHandle** con el *HandleType* parámetro establecido en SQL_HANDLE_STMT y *InputHandle* que apunta a un identificador de conexión.  
  
 Los atributos de instrucción son características del identificador de instrucción. Los atributos de instrucción de ejemplo pueden incluir la utilización de marcadores y el tipo de cursor que se debe utilizar con el conjunto de resultados de la instrucción. Atributos de instrucción se establecen con [SQLSetStmtAttr](../native-client-odbc-api/sqlsetstmtattr.md), y su configuración actual se recupera mediante el uso de [SQLGetStmtAttr](../native-client-odbc-api/sqlgetstmtattr.md). No es necesario que una aplicación establezca atributos de instrucción; todos los atributos de instrucción tienen valores predeterminados y algunos son específicos de controlador.  
  
 Actúe con precaución al usar varias opciones de instrucción y conexión de ODBC. Una llamada a [SQLSetConnectAttr](../native-client-odbc-api/sqlsetconnectattr.md) con *fOption* establecido en controles SQL_ATTR_LOGIN_TIMEOUT el tiempo que una aplicación espera un intento de conexión al tiempo de espera mientras se espera para establecer una conexión (0 Especifica una espera infinita). Los sitios con tiempos de respuesta lentos pueden establecer este valor alto para asegurarse de que las conexiones disponen de tiempo suficiente para completarse. Sin embargo, el intervalo siempre debe ser lo suficientemente bajo como para proporcionar al usuario una respuesta en un tiempo razonable si el controlador no puede conectar.  
  
 Una llamada a **SQLSetStmtAttr** con *fOption* establecido en SQL_ATTR_QUERY_TIMEOUT establece un intervalo de tiempo de espera de consulta para ayudar a proteger el servidor y el usuario de las consultas de larga ejecución.  
  
 Una llamada a **SQLSetStmtAttr** con *fOption* establecido en SQL_ATTR_MAX_LENGTH limita la cantidad de **texto** y **imagen** datos que un puede recuperar la instrucción individual. Una llamada a **SQLSetStmtAttr** con *fOption* establecido en SQL_ATTR_MAX_ROWS también limita un conjunto de filas de la primera *n* requiere filas si es toda la aplicación. Observe que el valor SQL_ATTR_MAX_ROWS hace que el controlador emita una instrucción SET ROWCOUNT al servidor. Esto afecta a todo [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instrucciones, incluidos los desencadenadores y las actualizaciones.  
  
 Actúe con precaución cuando establezca estas opciones. Es preferible que todos los identificadores de instrucción de un identificador de conexión tengan la misma configuración en SQL_ATTR_MAX_LENGTH y SQL_ATTR_MAX_ROWS. Si el controlador cambia de un identificador de instrucción a otro con valores diferentes en estas opciones, debe generar las instrucciones SET TEXTSIZE y SET ROWCOUNT adecuadas para cambiar los valores. El controlador no puede colocar estas instrucciones en el mismo lote que la instrucción SQL del usuario porque la instrucción SQL del usuario puede contener una instrucción que debe ser la primera de un lote. El controlador debe enviar las instrucciones SET TEXTSIZE y SET ROWCOUNT en un lote independiente, que genera automáticamente un viaje de ida y vuelta (round trip) adicional al servidor.  
  
## <a name="see-also"></a>Vea también  
 [Ejecución de consultas &#40;ODBC&#41;](executing-queries-odbc.md)  
  
  
