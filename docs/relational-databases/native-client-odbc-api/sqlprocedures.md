---
title: SQLProcedures | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLProcedures function
ms.assetid: ec41f017-f5e0-40ef-913a-65d206068631
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 41d7f8058b753991186a9bbadc1b7badc02ef29d
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2020
ms.locfileid: "86011135"
---
# <a name="sqlprocedures"></a>SQLProcedures
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Todos los procedimientos almacenados de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelven un valor. **SQLProcedures** informa SQL_PT_FUNCTION para la columna del conjunto de resultados PROCEDURE_TYPE.  
  
 **SQLProcedures** devuelve SQL_SUCCESS si existen o no valores para los parámetros *nombrecatálogo, SchemaName* o *NombreProc* . **SQLFetch** devuelve SQL_NO_DATA si se usan valores no válidos en estos parámetros.  
  
 **SQLProcedures** se puede ejecutar en un cursor de servidor estático. Un intento de ejecutar **SQLProcedures** en un cursor actualizable (dinámico o de conjunto de claves) devolverá SQL_SUCCESS_WITH_INFO, lo que indica que se ha cambiado el tipo de cursor.  
  
 **SQLProcedures** devuelve información sobre los procedimientos cuyos nombres coinciden con *NombreProc* y que el usuario actual puede ejecutar o para los que el usuario actual tiene el permiso View definition.  
  
## <a name="see-also"></a>Consulte también  
 [SQLProcedures función)](https://go.microsoft.com/fwlink/?LinkId=59364)   
 [ODBC API Implementation Details](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
