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
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0bd400221a3e199deb50ac8cb384984dc64bca83
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63014261"
---
# <a name="sqlprocedures"></a>SQLProcedures
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Todos los procedimientos almacenados de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelven un valor. **SQLProcedures** informa a SQL_PT_FUNCTION para el conjunto de resultados PROCEDURE_TYPE de columna.  
  
 **SQLProcedures** devuelve SQL_SUCCESS si existen o no valores para *CatalogName, SchemaName* o *ProcName* parámetros. **SQLFetch** devuelve SQL_NO_DATA si se usan valores no válidos en estos parámetros.  
  
 **SQLProcedures** se puede ejecutar en un cursor de servidor estático. Un intento de ejecutar **SQLProcedures** en un cursor actualizable (dinámico o conjunto de claves) devolverá SQL_SUCCESS_WITH_INFO, que indica que se ha cambiado el tipo de cursor.  
  
 **SQLProcedures** devuelve información sobre cualquier procedimiento cuyos nombres coincidan con *ProcName* y puede ser ejecutadas por el usuario actual, o para que el usuario actual se ha concedido el permiso VIEW DEFINITION.  
  
## <a name="see-also"></a>Vea también  
 [Función SQLProcedures](https://go.microsoft.com/fwlink/?LinkId=59364)   
 [Detalles de implementación de la API de ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
