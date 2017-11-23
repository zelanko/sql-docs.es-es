---
title: "Campos y registros de diagnóstico | Documentos de Microsoft"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-error-messages
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
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
caps.latest.revision: "30"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e4f1f7c5f8eb78ce45d380cc337ca0ab3c6796d2
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="diagnostic-records-and-fields"></a>Registros y campos de diagnóstico
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Los registros de diagnóstico se asocian a controladores de entorno, conexión, instrucción o descriptor de ODBC. Cuando una función de ODBC genera un código de retorno distinto de SQL_SUCCESS o SQL_INVALID_HANDLE, el identificador que llama la función incluye registros de diagnóstico asociados que contienen mensajes informativos o de error. Estos registros se conservan hasta que se llama a otra función con el mismo identificador, momento en el cual se descartan. No hay ningún límite al número de registros de diagnóstico que pueden estar asociados a un identificador en un momento determinado.  
  
 Existen dos tipos de registros de diagnóstico: encabezado y estado. El registro de encabezado es el registro 0; cuando hay registros de estado, son registros 1 y posteriores. Los registros de diagnóstico contienen diferentes campos para el registro de encabezado y los registros de estado. Los componentes ODBC también pueden definir sus propios campos de registro de diagnóstico.  
  
 Los campos del registro de encabezado contienen información general sobre la ejecución de una función, incluido el código de retorno, el recuento de filas, el número de registros de estado y tipo de instrucción ejecutada. El registro de encabezado se crea siempre, a menos que una función de ODBC devuelva SQL_INVALID_HANDLE. Para obtener una lista completa de campos en el registro de encabezado, vea [SQLGetDiagField](../../relational-databases/native-client-odbc-api/sqlgetdiagfield.md).  
  
 Los campos de los registros de estado contienen información sobre errores o advertencias concretos devueltos por el Administrador de controladores ODBC, el controlador o el origen de datos, incluidos SQLSTATE, el número de error nativo, el mensaje de diagnóstico, el número de columna y el número de fila. Los registros de estado solamente se crean si la función devuelve SQL_ERROR, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_NEED_DATA o SQL_STILL_EXECUTING. Para obtener una lista completa de campos de los registros de estado, consulte **SQLGetDiagField**.  
  
 **SQLGetDiagRec** recupera un único registro de diagnóstico junto con su ODBC SQLSTATE, el número de error nativo y los campos de mensaje de diagnóstico. Esta funcionalidad es similar a la API ODBC 2. *x***SQLError** función. La función de control de errores más simple en ODBC 3. *x* consiste en llamar repetidamente a **SQLGetDiagRec** a partir de la *RecNumber* parámetro establecido en 1 y se incrementa *RecNumber* en 1 hasta que **SQLGetDiagRec** devuelve SQL_NO_DATA. Esto es equivalente a una API ODBC 2. *x* aplicación que llama a **SQLError** hasta que devuelve SQL_NO_DATA_FOUND.  
  
 ODBC 3. *x* admite mucha más información de diagnóstico que ODBC 2. *x*. Esta información se almacena en campos adicionales de los registros de diagnóstico recuperados mediante **SQLGetDiagField**.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC Native Client tiene los campos de diagnóstico específicos del controlador que se pueden recuperar con **SQLGetDiagField**. Las etiquetas de estos campos específicos de controlador se definen en sqlncli.h. Utilice estas etiquetas para recuperar el estado de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el nivel de gravedad, el nombre de servidor, el nombre de procedimiento y el número de línea asociados a cada registro de diagnóstico. Además, sqlncli.h contiene definiciones de los códigos de los controladores que se utiliza para identificar instrucciones Transact-SQL si una aplicación llama **SQLGetDiagField** con *DiagIdentifier* establecido en SQL_DIAG_DYNAMIC_ FUNCTION_CODE.  
  
 **SQLGetDiagField** se procesa mediante el Administrador de controladores ODBC con información de error almacena en memoria caché del controlador subyacente. El Administrador de controladores ODBC no almacena en caché los campos de diagnóstico específicos del controlador hasta que no se ha realizado una conexión correcta. **SQLGetDiagField** devuelve SQL_ERROR si se llama para obtener los campos de diagnóstico específicos del controlador antes de que se ha completado una conexión correcta. Si una función de conexión de ODBC devuelve SQL_SUCCESS_WITH_INFO, los campos de diagnóstico específicos del controlador todavía no están disponibles en la función de conexión. Puede iniciar una llamada a **SQLGetDiagField** para campos de diagnóstico específicos del controlador solo después de haber realizado ODBC otra llamada a la función después de la función de conexión.  
  
 Mayoría de los errores notificada por el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC Native Client se puede diagnosticar eficazmente solo con la información devuelta por **SQLGetDiagRec**. En algunos casos, sin embargo, la información que devuelven los campos de diagnóstico específicos del controlador es importante para diagnosticar un error. Al codificar un controlador de errores ODBC para las aplicaciones que usan el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client, es una buena idea usar **SQLGetDiagField** para recuperar al menos el sql_diag_ss_severity y sql_diag_ss_msgstate campos específicos del controlador. Si un error determinado se puede producir en varias ubicaciones del código de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], SQL_DIAG_SS_MSGSTATE indica a un ingeniero de soporte técnico de Microsoft de forma específica dónde se ha producido el error, lo que en ocasiones ayuda a diagnosticar un problema.  
  
## <a name="see-also"></a>Vea también  
 [Controlar errores y mensajes](../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  
