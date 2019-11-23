---
title: SQLGetDiagField | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLGetDiagField function
ms.assetid: 395245ba-0372-43ec-b9a4-a29410d85a6d
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f2a3d8d829794692cff6ecb9879e6f62f0b0b91b
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/07/2019
ms.locfileid: "73786474"
---
# <a name="sqlgetdiagfield"></a>SQLGetDiagField
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  El controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client especifica los siguientes campos de diagnóstico adicionales para **SQLGetDiagField**. Estos campos admiten el informe de errores enriquecido para aplicaciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y están disponible en todos los registros de diagnóstica que se generan en los identificadores de conexión de ODBC e identificadores de instrucciones de ODBC conectados. Los campos se definen en sqlncli.h.  
  
|Campo del registro de diagnóstico|Descripción|  
|------------------------------|-----------------|  
|SQL_DIAG_SS_LINE|Indica el número de línea de un procedimiento almacenado que genera un error. El valor de SQL_DIAG_SS_LINE solamente es significativo si SQL_DIAG_SS_PROCNAME devuelve un valor. El valor se devuelve como un entero sin signo de 16 bits.|  
|SQL_DIAG_SS_MSGSTATE|El estado de un mensaje de error. Para obtener información sobre el estado del mensaje de error, vea [RAISERROR](../../t-sql/language-elements/raiserror-transact-sql.md). El valor se devuelve como un entero con signo de 32 bits.|  
|SQL_DIAG_SS_PROCNAME|Nombre del procedimiento almacenado que genera un error, si procede. El valor se devuelve como una cadena de caracteres. La longitud de la cadena (en caracteres) depende de la versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se puede determinar mediante una llamada a [SQLGetInfo](../../relational-databases/native-client-odbc-api/sqlgetinfo.md) que solicita el valor de SQL_MAX_PROCEDURE_NAME_LEN.|  
|SQL_DIAG_SS_SEVERITY|El nivel de gravedad del mensaje de error asociado. El valor se devuelve como un entero con signo de 32 bits.|  
|SQL_DIAG_SS_SRVNAME|El nombre del servidor donde se ha producido el error. El valor se devuelve como una cadena de caracteres. La longitud de la cadena (en caracteres) se define en la macro SQL_MAX_SQLSERVERNAME de sqlncli.h.|  
  
 Los campos de diagnóstico específicos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que contienen datos de caracteres, SQL_DIAG_SS_PROCNAME y SQL_DIAG_SS_SRVNAME, devuelven estos datos al cliente como cadenas terminadas en NULL, ANSI o Unicode. Si es necesario, el ancho de caracteres debe ajustar el recuento de caracteres. También se puede utilizar un tipo de datos de C portátil como TCHAR o SQLTCHAR para garantizar la longitud correcta de la variable de programa.  
  
 El controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client notifica los siguientes códigos de función dinámica adicionales que identifican la última instrucción [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] intentada. El código de función dinámica se devuelve en el encabezado (registro 0) del conjunto de registros de diagnóstico y está por tanto disponible en cada ejecución (correcta o no).  
  
|Código de función dinámica|Origen|  
|---------------------------|------------|  
|SQL_DIAG_DFC_SS_ALTER_DATABASE|instrucción ALTER DATABASE|  
|SQL_DIAG_DFC_SS_CHECKPOINT|Instrucción CHECKPOINT|  
|SQL_DIAG_DFC_SS_CONDITION|Error surgido en las cláusulas WHERE o HAVING de una instrucción.|  
|SQL_DIAG_DFC_SS_CREATE_DATABASE|Instrucción CREATE DATABASE|  
|SQL_DIAG_DFC_SS_CREATE_DEFAULT|Instrucción CREATE DEFAULT|  
|SQL_DIAG_DFC_SS_CREATE_PROCEDURE|CREATE PROCEDURE, instrucción|  
|SQL_DIAG_DFC_SS_CREATE_RULE|Instrucción CREATE RULE|  
|SQL_DIAG_DFC_SS_CREATE_TRIGGER|CREATE TRIGGER, instrucción|  
|SQL_DIAG_DFC_SS_CURSOR_DECLARE|DECLARE CURSOR, instrucción|  
|SQL_DIAG_DFC_SS_CURSOR_OPEN|OPEN, instrucción|  
|SQL_DIAG_DFC_SS_CURSOR_FETCH|FETCH, instrucción|  
|SQL_DIAG_DFC_SS_CURSOR_CLOSE|Instrucción CLOSE|  
|SQL_DIAG_DFC_SS_DEALLOCATE_CURSOR|DEALLOCATE, instrucción|  
|SQL_DIAG_DFC_SS_DBCC|Instrucción DBCC|  
|SQL_DIAG_DFC_SS_DENY|DENY, instrucción|  
|SQL_DIAG_DFC_SS_DROP_DATABASE|DROP DATABASE, instrucción|  
|SQL_DIAG_DFC_SS_DROP_DEFAULT|Instrucción DROP DEFAULT|  
|SQL_DIAG_DFC_SS_DROP_PROCEDURE|Instrucción DROP PROCEDURE|  
|SQL_DIAG_DFC_SS_DROP_RULE|Instrucción DROP RULE|  
|SQL_DIAG_DFC_SS_DROP_TRIGGER|Instrucción DROP TRIGGER|  
|SQL_DIAG_DFC_SS_DUMP_DATABASE|Instrucción BACKUP o DUMP DATABASE|  
|SQL_DIAG_DFC_SS_DUMP_TABLE|Instrucción DUMP TABLE|  
|SQL_DIAG_DFC_SS_DUMP_TRANSACTION|Instrucción BACKUP o DUMP TRANSACTION. También se devuelve para una instrucción CHECKPOINT si el archivo **trunc. log on chkpt.** la opción de base de datos está activada.|  
|SQL_DIAG_DFC_SS_GOTO|Instrucción GOTO de control de flujo|  
|SQL_DIAG_DFC_SS_INSERT_BULK|Instrucción INSERT BULK|  
|SQL_DIAG_DFC_SS_KILL|Instrucción KILL|  
|SQL_DIAG_DFC_SS_LOAD_DATABASE|Instrucción LOAD o RESTORE DATABASE|  
|SQL_DIAG_DFC_SS_LOAD_HEADERONLY|Instrucción LOAD o RESTORE HEADERONLY|  
|SQL_DIAG_DFC_SS_LOAD_TABLE|Instrucción LOAD TABLE|  
|SQL_DIAG_DFC_SS_LOAD_TRANSACTION|Instrucción LOAD o RESTORE TRANSACTION|  
|SQL_DIAG_DFC_SS_PRINT|PRINT, instrucción|  
|SQL_DIAG_DFC_SS_RAISERROR|RAISERROR, instrucción|  
|SQL_DIAG_DFC_SS_READTEXT|Instrucción READTEXT|  
|SQL_DIAG_DFC_SS_RECONFIGURE|Instrucción RECONFIGURE|  
|SQL_DIAG_DFC_SS_RETURN|Instrucción RETURN de control de flujo|  
|SQL_DIAG_DFC_SS_SELECT_INTO|SELECT INTO, instrucción|  
|SQL_DIAG_DFC_SS_SET|Instrucción SET (genérico, todas las opciones)|  
|SQL_DIAG_DFC_SS_SET_IDENTITY_INSERT|SET IDENTITY_INSERT, instrucción|  
|SQL_DIAG_DFC_SS_SET_ROW_COUNT|SET ROWCOUNT, instrucción|  
|SQL_DIAG_DFC_SS_SET_STATISTICS|Instrucción SET STATISTICS IO o SET STATISTICS TIME|  
|SQL_DIAG_DFC_SS_SET_TEXTSIZE|SET TEXTSIZE, instrucción|  
|SQL_DIAG_DFC_SS_SETUSER|SETUSER, instrucción|  
|SQL_DIAG_DFC_SS_SET_XCTLVL|Instrucción SET TRANSACTION ISOLATION LEVEL|  
|SQL_DIAG_DFC_SS_SHUTDOWN|Instrucción SHUTDOWN|  
|SQL_DIAG_DFC_SS_TRANS_BEGIN|Instrucción BEGIN TRAN|  
|SQL_DIAG_DFC_SS_TRANS_COMMIT|Instrucción COMMIT TRAN|  
|SQL_DIAG_DFC_SS_TRANS_PREPARE|Preparación para confirmar una transacción distribuida|  
|SQL_DIAG_DFC_SS_TRANS_ROLLBACK|Instrucción ROLLBACK TRAN|  
|SQL_DIAG_DFC_SS_TRANS_SAVE|Instrucción SAVE TRAN|  
|SQL_DIAG_DFC_SS_TRUNCATE_TABLE|TRUNCATE TABLE, instrucción|  
|SQL_DIAG_DFC_SS_UPDATE_STATISTICS|UPDATE STATISTICS, instrucción|  
|SQL_DIAG_DFC_SS_UPDATETEXT|instrucción UPDATETEXT|  
|SQL_DIAG_DFC_SS_USE|USE, instrucción|  
|SQL_DIAG_DFC_SS_WAITFOR|Instrucción WAITFOR de control de flujo|  
|SQL_DIAG_DFC_SS_WRITETEXT|Instrucción WRITETEXT|  
  
## <a name="sqlgetdiagfield-and-table-valued-parameters"></a>SQLGetDiagField y parámetros con valores de tabla  
 SQLGetDiagField se puede utilizar para recuperar dos campos de diagnóstico: SQL_DIAG_SS_TABLE_COLUMN_NUMBER y SQL_DIAG_SS_TABLE_ROW_NUMBER. Estos campos ayudan a determinar qué valor produjo el error o la advertencia asociados al registro de diagnóstico.  
  
 Para obtener más información sobre los parámetros con valores de tabla, vea [parámetros &#40;con&#41;valores de tabla ODBC](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="see-also"></a>Vea también  
   de la [función SQLGetDiagField](https://go.microsoft.com/fwlink/?LinkId=59352)  
 [Detalles de implementación de la API de ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
