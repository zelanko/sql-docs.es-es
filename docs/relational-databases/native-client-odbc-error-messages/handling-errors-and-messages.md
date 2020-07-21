---
title: Control de errores y mensajes | Microsoft Docs
description: Obtenga información acerca de qué información de diagnóstico se devuelve cuando una aplicación llama a una función ODBC, incluida la información completa o correcta.
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC error handling, about error handling
- errors [ODBC]
- SQL Server Native Client ODBC driver, errors
- messages [ODBC], about messages
- ODBC error handling
- SQL_INVALID_HANDLE return code
- errors [ODBC], about error handling
- messages [ODBC]
ms.assetid: 74ea9630-e482-4a46-bb45-f5234f079b48
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 64e6226c5f8260979b5cf83245f56bf77b9ff759
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2020
ms.locfileid: "85998517"
---
# <a name="handling-errors-and-messages"></a>Controlar errores y mensajes
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Cuando una aplicación llama a una función ODBC, el controlador ejecuta la función y devuelve información de diagnóstico de dos maneras: un código de retorno indica si la función ODBC se ha ejecutado o no correctamente en su totalidad, y los registros de diagnóstico proporcionan información detallada sobre la función. Los registros de diagnóstico incluyen un registro de encabezado y registros de estado. Por lo menos se devuelve un registro de diagnóstico, el registro de encabezado, aunque la función se ejecute correctamente.  
  
 La información de diagnóstico se usa en la fase de desarrollo para detectar errores de programación, como identificadores no válidos y errores de sintaxis en instrucciones SQL codificadas de forma rígida. También se utiliza en tiempo de ejecución para detectar errores y advertencias durante la ejecución, como truncamiento de datos, infracciones de reglas y errores de sintaxis en instrucciones SQL escritas por el usuario. La lógica del programa se suele basar en códigos de retorno.  
  
 Por ejemplo, después de que una aplicación llama a **SQLFetch** para recuperar las filas de un conjunto de resultados, el código de retorno indica si se alcanzó el final del conjunto de resultados (SQL_NO_DATA), si se devolvieron mensajes informativos (SQL_SUCCESS_WITH_INFO) o si se produjo un error (SQL_ERROR).  
  
 Si el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client devuelve un valor distinto de SQL_SUCCESS, la aplicación puede llamar a **SQLGetDiagRec** para recuperar los mensajes informativos o de error. Use **SQLGetDiagRec** para desplazarse hacia arriba y hacia abajo por el conjunto de mensajes si hay más de un mensaje.  
  
 El código de retorno SQL_INVALID_HANDLE siempre indica un error de programación y nunca debe encontrarse durante la ejecución. Todos los demás códigos de retorno proporcionan información en tiempo de ejecución, aunque SQL_ERROR puede indicar un error de programación.  
  
 La [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] API nativa original, DB-Library para C, permite que una aplicación Instale funciones de control de errores y de control de mensajes de devolución de llamada que devuelven errores o mensajes. Algunas instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)], como PRINT, RAISERROR, DBCC y SET, devuelven sus resultados a la función de controlador de mensajes DB-Library en lugar de a un conjunto de resultados. Sin embargo, la API de ODBC no tiene ninguna capacidad de devolución de llamada semejante. Cuando el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client detecta mensajes procedentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , establece el código de retorno de odbc en SQL_SUCCESS_WITH_INFO o SQL_ERROR y devuelve el mensaje como uno o más registros de diagnóstico. Por lo tanto, una aplicación ODBC debe comprobar cuidadosamente estos códigos de retorno y llamar a **SQLGetDiagRec** para recuperar los datos del mensaje.  
  
 Para obtener información sobre cómo realizar un seguimiento de los errores, vea [Data Access Tracing](https://go.microsoft.com/fwlink/?LinkId=125805) (Seguimiento de acceso a datos). Para información sobre las mejoras en el seguimiento de errores agregadas en [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], consulte [Acceso a información de diagnóstico en el registro de eventos extendidos](../../relational-databases/native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md).  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Procesar instrucciones que generan mensajes](../../relational-databases/native-client-odbc-error-messages/processing-statements-that-generate-messages.md)  
  
-   [Registros y campos de diagnóstico](../../relational-databases/native-client-odbc-error-messages/diagnostic-records-and-fields.md)  
  
-   [Números de errores nativos](../../relational-databases/native-client-odbc-error-messages/native-error-numbers.md)  
  
-   [Códigos de error ODBC de &#40;SQLSTATE&#41;](../../relational-databases/native-client-odbc-error-messages/sqlstate-odbc-error-codes.md)  
  
-   [Mensajes de error](../../relational-databases/native-client-odbc-error-messages/error-messages.md)  
  
## <a name="see-also"></a>Consulte también  
 [SQL Server Native Client &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
