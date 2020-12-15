---
description: SQLCancel
title: SQLCancel | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLCancel function
ms.assetid: d4c965ae-c1ac-4e9d-b4b9-32b561401106
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8c6215abca068aa221d13303f53de3aa70ba11b5
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97473896"
---
# <a name="sqlcancel"></a>SQLCancel
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  El tema [SQLCancel](../../odbc/reference/syntax/sqlcancel-function.md) establece que en ODBC 2.x, si una aplicación llama a **SQLCancel** cuando no se está realizando ningún procesamiento en la instrucción, **SQLCancel** tiene el mismo efecto que **SQLFreeStmt** con la opción **SQL_CLOSE** ; este compotamiento se define solamente po razones de compleción y las aplicaciones deben llamar a **SQLFreeStmt** o **SQLCloseCurso** to close cursos. Pero aunque la aplicación [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client establezca que la versión de la API de ODBC ha de ser 3.5.x o posterior, la función **SQLCancel** utilizará el comportamiento de ODBC 2.x.  
  
## <a name="see-also"></a>Consulte también  
 [SQLCancel](../../odbc/reference/syntax/sqlcancel-function.md)   
 [ODBC API Implementation Details](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
