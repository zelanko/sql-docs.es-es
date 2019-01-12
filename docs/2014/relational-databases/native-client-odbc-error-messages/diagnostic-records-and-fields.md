---
title: Campos y registros de diagnóstico | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
ms.assetid: 4949530c-62d1-4f1a-b592-144244444ce0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 173d0287ba1b63e8811e2d340448d03c3bbf961d
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/09/2019
ms.locfileid: "54133145"
---
# <a name="diagnostic-records-and-fields"></a>Registros y campos de diagnóstico
  Los registros de diagnóstico se asocian a controladores de entorno, conexión, instrucción o descriptor de ODBC. Cuando una función de ODBC genera un código de retorno distinto de SQL_SUCCESS o SQL_INVALID_HANDLE, el identificador que llama la función incluye registros de diagnóstico asociados que contienen mensajes informativos o de error. Estos registros se conservan hasta que se llama a otra función con el mismo identificador, momento en el cual se descartan. No hay ningún límite al número de registros de diagnóstico que pueden estar asociados a un identificador en un momento determinado.  
  
 Existen dos tipos de registros de diagnóstico: encabezado y estado. El registro de encabezado es el registro 0; cuando hay registros de estado, son registros 1 y posteriores. Los registros de diagnóstico contienen diferentes campos para el registro de encabezado y los registros de estado. Los componentes ODBC también pueden definir sus propios campos de registro de diagnóstico.  
  
 Los campos del registro de encabezado contienen información general sobre la ejecución de una función, incluido el código de retorno, el recuento de filas, el número de registros de estado y tipo de instrucción ejecutada. El registro de encabezado se crea siempre, a menos que una función de ODBC devuelva SQL_INVALID_HANDLE. Para obtener una lista completa de campos en el registro de encabezado, vea [SQLGetDiagField](../native-client-odbc-api/sqlgetdiagfield.md).  
  
 Los campos de los registros de estado contienen información sobre errores o advertencias concretos devueltos por el Administrador de controladores ODBC, el controlador o el origen de datos, incluidos SQLSTATE, el número de error nativo, el mensaje de diagnóstico, el número de columna y el número de fila. Los registros de estado solamente se crean si la función devuelve SQL_ERROR, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_NEED_DATA o SQL_STILL_EXECUTING. Para obtener una lista completa de los campos de los registros de estado, vea **SQLGetDiagField**.  
  
 **SQLGetDiagRec** recupera un único registro de diagnóstico, junto con su ODBC SQLSTATE, el número de error nativo y los campos de mensaje de diagnóstico. Esta funcionalidad es similar a la API ODBC 2. _x_**SQLError** función. La función de control de errores más simple en ODBC 3. *x* consiste en llamar repetidamente a **SQLGetDiagRec** a partir de la *RecNumber* parámetro establecido en 1 e incrementando *RecNumber* en 1 hasta que **SQLGetDiagRec** devuelve SQL_NO_DATA. Esto es equivalente a ODBC 2. *x* aplicación que llama a **SQLError** hasta que devuelve SQL_NO_DATA_FOUND.  
  
 ODBC 3. *x* es compatible con mucha más información de diagnóstico que ODBC 2. *x*. Esta información se almacena en campos adicionales de los registros de diagnóstico recuperados mediante **SQLGetDiagField**.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client tiene campos de diagnóstico específicos del controlador que se pueden recuperar con **SQLGetDiagField**. Las etiquetas de estos campos específicos de controlador se definen en sqlncli.h. Utilice estas etiquetas para recuperar el estado de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el nivel de gravedad, el nombre de servidor, el nombre de procedimiento y el número de línea asociados a cada registro de diagnóstico. Además, sqlncli.h contiene definiciones de los códigos que el controlador utiliza para identificar instrucciones Transact-SQL si una aplicación llama a **SQLGetDiagField** con *DiagIdentifier* establecido en SQL_DIAG_DYNAMIC_ FUNCTION_CODE.  
  
 **SQLGetDiagField** se procesa mediante el Administrador de controladores ODBC utilizando la información de error almacena en caché desde el controlador subyacente. El Administrador de controladores ODBC no almacena en caché los campos de diagnóstico específicos del controlador hasta que no se ha realizado una conexión correcta. **SQLGetDiagField** devuelve SQL_ERROR si se llama para obtener los campos de diagnóstico específicos del controlador antes de que se ha completado una conexión correcta. Si una función de conexión de ODBC devuelve SQL_SUCCESS_WITH_INFO, los campos de diagnóstico específicos del controlador todavía no están disponibles en la función de conexión. Puede empezar a llamar a **SQLGetDiagField** para campos de diagnóstico específicos del controlador solo después de haber realizado ODBC otra llamada de función después de la función de conexión.  
  
 Mayoría de los errores notificada por el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client se puede diagnosticar eficazmente solo con la información devuelta por **SQLGetDiagRec**. En algunos casos, sin embargo, la información que devuelven los campos de diagnóstico específicos del controlador es importante para diagnosticar un error. Al codificar un controlador de errores ODBC para aplicaciones que usan el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client, es una buena idea usar también **SQLGetDiagField** para recuperar al menos el sql_diag_ss_severity y sql_diag_ss_msgstate campos específicos del controlador. Si un error determinado se puede producir en varias ubicaciones del código de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], SQL_DIAG_SS_MSGSTATE indica a un ingeniero de soporte técnico de Microsoft de forma específica dónde se ha producido el error, lo que en ocasiones ayuda a diagnosticar un problema.  
  
## <a name="see-also"></a>Vea también  
 [Controlar errores y mensajes](handling-errors-and-messages.md)  
  
  
