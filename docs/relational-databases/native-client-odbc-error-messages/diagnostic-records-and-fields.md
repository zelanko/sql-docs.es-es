---
title: Registros y campos de diagnóstico | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- header records [ODBC]
- SQL Server Native Client ODBC driver, errors
- messages [ODBC], diagnostic records
- ODBC error handling, diagnostic records
- SQLGetDiagField function
- diagnostic records [ODBC]
- errors [ODBC], diagnostic records
- fields [ODBC]
- status information [ODBC]
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5bffbd7ce22bf3e1e906e68e880fb76bee36c4b3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "73783661"
---
# <a name="diagnostic-records-and-fields"></a>Registros y campos de diagnóstico
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Los registros de diagnóstico se asocian a controladores de entorno, conexión, instrucción o descriptor de ODBC. Cuando una función de ODBC genera un código de retorno distinto de SQL_SUCCESS o SQL_INVALID_HANDLE, el identificador que llama la función incluye registros de diagnóstico asociados que contienen mensajes informativos o de error. Estos registros se conservan hasta que se llama a otra función con el mismo identificador, momento en el cual se descartan. No hay ningún límite al número de registros de diagnóstico que pueden estar asociados a un identificador en un momento determinado.  
  
 Existen dos tipos de registros de diagnóstico: encabezado y estado. El registro de encabezado es el registro 0; cuando hay registros de estado, son registros 1 y posteriores. Los registros de diagnóstico contienen diferentes campos para el registro de encabezado y los registros de estado. Los componentes ODBC también pueden definir sus propios campos de registro de diagnóstico.  
  
 Los campos del registro de encabezado contienen información general sobre la ejecución de una función, incluido el código de retorno, el recuento de filas, el número de registros de estado y tipo de instrucción ejecutada. El registro de encabezado se crea siempre, a menos que una función de ODBC devuelva SQL_INVALID_HANDLE. Para obtener una lista completa de los campos del registro de encabezado, vea [SQLGetDiagField](../../relational-databases/native-client-odbc-api/sqlgetdiagfield.md).  
  
 Los campos de los registros de estado contienen información sobre errores o advertencias concretos devueltos por el Administrador de controladores ODBC, el controlador o el origen de datos, incluidos SQLSTATE, el número de error nativo, el mensaje de diagnóstico, el número de columna y el número de fila. Los registros de estado solamente se crean si la función devuelve SQL_ERROR, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_NEED_DATA o SQL_STILL_EXECUTING. Para obtener una lista completa de los campos de los registros de estado, vea **SQLGetDiagField**.  
  
 **SQLGetDiagRec** recupera un solo registro de diagnóstico junto con su SQLSTATE ODBC, el número de error nativo y los campos de mensaje de diagnóstico. Esta funcionalidad es similar a la de ODBC 2. _x_**SQLError** (función). La función de control de errores más sencilla en ODBC 3. *x* es llamar repetidamente a **SQLGetDiagRec** a partir del parámetro *RecNumber* establecido en 1 e incrementar *RecNumber* en 1 hasta que **SQLGetDiagRec** devuelva SQL_NO_DATA. Esto es equivalente a ODBC 2. aplicación *x* que llama a **SQLError** hasta que devuelve SQL_NO_DATA_FOUND.  
  
 ODBC 3. *x* admite mucha más información de diagnóstico que ODBC 2. *x*. Esta información se almacena en campos adicionales en los registros de diagnóstico recuperados mediante **SQLGetDiagField**.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client tiene campos de diagnóstico específicos del controlador que se pueden recuperar con **SQLGetDiagField**. Las etiquetas de estos campos específicos de controlador se definen en sqlncli.h. Utilice estas etiquetas para recuperar el estado de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el nivel de gravedad, el nombre de servidor, el nombre de procedimiento y el número de línea asociados a cada registro de diagnóstico. Además, SQLNCLI. h contiene definiciones de los códigos que el controlador utiliza para identificar las instrucciones Transact-SQL si una aplicación llama a **SQLGetDiagField** con *DiagIdentifier* establecido en SQL_DIAG_DYNAMIC_FUNCTION_CODE.  
  
 El administrador de controladores ODBC procesa **SQLGetDiagField** con la información de error que almacena en caché desde el controlador subyacente. El Administrador de controladores ODBC no almacena en caché los campos de diagnóstico específicos del controlador hasta que no se ha realizado una conexión correcta. **SQLGetDiagField** devuelve SQL_ERROR si se llama para obtener campos de diagnóstico específicos del controlador antes de que se haya completado una conexión correcta. Si una función de conexión de ODBC devuelve SQL_SUCCESS_WITH_INFO, los campos de diagnóstico específicos del controlador todavía no están disponibles en la función de conexión. Puede empezar a llamar a **SQLGetDiagField** para los campos de diagnóstico específicos del controlador solo después de haber realizado otra llamada a una función ODBC después de la función de conexión.  
  
 La mayoría de los errores [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] detectados por el controlador ODBC de Native Client se pueden diagnosticar de forma eficaz usando únicamente la información devuelta por **SQLGetDiagRec**. En algunos casos, sin embargo, la información que devuelven los campos de diagnóstico específicos del controlador es importante para diagnosticar un error. Al codificar un controlador de errores ODBC para aplicaciones [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que usan el controlador ODBC de Native Client, se recomienda usar también **SQLGetDiagField** para recuperar al menos los campos específicos del controlador SQL_DIAG_SS_MSGSTATE y SQL_DIAG_SS_SEVERITY. Si un error determinado se puede producir en varias ubicaciones del código de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], SQL_DIAG_SS_MSGSTATE indica a un ingeniero de soporte técnico de Microsoft de forma específica dónde se ha producido el error, lo que en ocasiones ayuda a diagnosticar un problema.  
  
## <a name="see-also"></a>Consulte también  
 [Controlar errores y mensajes](../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  
