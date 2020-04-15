---
title: Asignación de un identificador de declaración ? Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 85678c5b03a77910c73bd5b8bac8d0e40d52c252
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81291613"
---
# <a name="allocating-a-statement-handle"></a>Asignar un identificador de instrucción
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Antes de que una aplicación pueda ejecutar una instrucción, debe asignar un identificador de instrucción. Para ello, se llama a **SQLAllocHandle** con el parámetro *HandleType* establecido en SQL_HANDLE_STMT y *InputHandle* que apunta a un identificador de conexión.  
  
 Los atributos de instrucción son características del identificador de instrucción. Los atributos de instrucción de ejemplo pueden incluir la utilización de marcadores y el tipo de cursor que se debe utilizar con el conjunto de resultados de la instrucción. Los atributos de instrucción se establecen con [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)y su configuración actual se recupera mediante [SQLGetStmtAttr](../../relational-databases/native-client-odbc-api/sqlgetstmtattr.md). No es necesario que una aplicación establezca atributos de instrucción; todos los atributos de instrucción tienen valores predeterminados y algunos son específicos de controlador.  
  
 Actúe con precaución al usar varias opciones de instrucción y conexión de ODBC. Llamar a [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) con *fOption* establecido en SQL_ATTR_LOGIN_TIMEOUT controla el tiempo que una aplicación espera un intento de conexión para tiempo de espera mientras espera para establecer una conexión (0 especifica una espera infinita). Los sitios con tiempos de respuesta lentos pueden establecer este valor alto para asegurarse de que las conexiones disponen de tiempo suficiente para completarse. Sin embargo, el intervalo siempre debe ser lo suficientemente bajo como para proporcionar al usuario una respuesta en un tiempo razonable si el controlador no puede conectar.  
  
 Llamar a **SQLSetStmtAttr** con *fOption* establecido en SQL_ATTR_QUERY_TIMEOUT establece un intervalo de tiempo de espera de consulta para ayudar a proteger el servidor y el usuario de consultas de ejecución prolongada.  
  
 Llamar a **SQLSetStmtAttr** con *fOption* establecido en SQL_ATTR_MAX_LENGTH limita la cantidad de datos de **texto** e **imagen** que una instrucción individual puede recuperar. Llamar a **SQLSetStmtAttr** con *fOption* establecido en SQL_ATTR_MAX_ROWS también limita un conjunto de filas a las primeras *n* filas si eso es todo lo que requiere la aplicación. Observe que el valor SQL_ATTR_MAX_ROWS hace que el controlador emita una instrucción SET ROWCOUNT al servidor. Esto afecta [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a todas las instrucciones, incluidos los desencadenadores y las actualizaciones.  
  
 Actúe con precaución cuando establezca estas opciones. Es preferible que todos los identificadores de instrucción de un identificador de conexión tengan la misma configuración en SQL_ATTR_MAX_LENGTH y SQL_ATTR_MAX_ROWS. Si el controlador cambia de un identificador de instrucción a otro con valores diferentes en estas opciones, debe generar las instrucciones SET TEXTSIZE y SET ROWCOUNT adecuadas para cambiar los valores. El controlador no puede colocar estas instrucciones en el mismo lote que la instrucción SQL del usuario porque la instrucción SQL del usuario puede contener una instrucción que debe ser la primera de un lote. El controlador debe enviar las instrucciones SET TEXTSIZE y SET ROWCOUNT en un lote independiente, que genera automáticamente un viaje de ida y vuelta (round trip) adicional al servidor.  
  
## <a name="see-also"></a>Consulte también  
 [Ejecución de consultas &#40;&#41;ODBC](../../relational-databases/native-client-odbc-queries/executing-queries-odbc.md)  
  
  
