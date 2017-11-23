---
title: SQLProcedures | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-api
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apitype: DLLExport
helpviewer_keywords: SQLProcedures function
ms.assetid: ec41f017-f5e0-40ef-913a-65d206068631
caps.latest.revision: "35"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0bb243692d3781449f1f3da4e4cc3cc316e7b8b4
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="sqlprocedures"></a>SQLProcedures
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Todos los procedimientos almacenados de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelven un valor. **SQLProcedures** informa a SQL_PT_FUNCTION para el conjunto de resultados PROCEDURE_TYPE de columna.  
  
 **SQLProcedures** devuelve SQL_SUCCESS si existen o no valores para *CatalogName, SchemaName* o *ProcName* parámetros. **SQLFetch** devuelve SQL_NO_DATA si se usan valores no válidos en estos parámetros.  
  
 **SQLProcedures** se puede ejecutar en un cursor de servidor estático. Un intento de ejecutar **SQLProcedures** en un cursor actualizable (dinámico o conjunto de claves) devolverá SQL_SUCCESS_WITH_INFO, que indica que se ha cambiado el tipo de cursor.  
  
 **SQLProcedures** devuelve información sobre cualquier procedimiento cuyos nombres coincidan con *ProcName* y se puede ejecutar el usuario actual, o para que el usuario actual se ha concedido el permiso VIEW DEFINITION.  
  
## <a name="see-also"></a>Vea también  
 [SQLProcedures, función](http://go.microsoft.com/fwlink/?LinkId=59364)   
 [Detalles de implementación de la API de ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
