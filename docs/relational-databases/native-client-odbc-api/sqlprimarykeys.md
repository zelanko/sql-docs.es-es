---
title: SQLPrimaryKeys | Documentos de Microsoft
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
helpviewer_keywords: SQLPrimaryKeys function
ms.assetid: bc61cd5b-d2f4-4f87-abc7-743cf9ea772d
caps.latest.revision: "37"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4f58b1d5d7880f5e14c65895b5913dddd666905e
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="sqlprimarykeys"></a>SQLPrimaryKeys
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Una tabla puede tener una o varias columnas que pueden actuar como identificadores de fila únicos y tablas creadas sin una restricción PRIMARY KEY devuelven un conjunto a SQLPrimaryKeys de resultados vacío. La función ODBC [SQLSpecialColumns](../../relational-databases/native-client-odbc-api/sqlspecialcolumns.md) candidatos para las tablas sin claves principales del identificador de fila de informes.  
  
 SQLPrimaryKeys devuelve SQL_SUCCESS si existen o no valores para *CatalogName*, *SchemaName*, o *TableName* parámetros. SQLFetch devuelve SQL_NO_DATA cuando se usan valores no válidos en estos parámetros.  
  
 SQLPrimaryKeys se puede ejecutar en un cursor de servidor estático. Un intento de ejecutar SQLPrimaryKeys en un cursor actualizable (dinámico o conjunto de claves) devolverá SQL_SUCCESS_WITH_INFO, que indica que se ha cambiado el tipo de cursor.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC Native Client permite notificar información de tablas en servidores vinculados aceptando un nombre de dos partes para el *CatalogName* parámetro: *nombre_servidor_vinculado.nombre_catálogo*.  
  
## <a name="sqlprimarykeys-and-table-valued-parameters"></a>SQLPrimaryKeys y parámetros con valores de tabla  
 Si el atributo de instrucción SQL_SOPT_SS_NAME_SCOPE tiene el valor SQL_SS_NAME_SCOPE_TABLE_TYPE, en lugar de su valor predeterminado de SQL_SS_NAME_SCOPE_TABLE, SQLPrimaryKeys devolverá información sobre las columnas de clave principal de tipos de tabla. Para obtener más información sobre SQL_SOPT_SS_NAME_SCOPE, vea [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md).  
  
 Para obtener más información acerca de los parámetros con valores de tabla, vea [parámetros con valores de tabla &#40; ODBC &#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="see-also"></a>Vea también  
 [SQLPrimaryKeys, función](http://go.microsoft.com/fwlink/?LinkId=59361)   
 [Detalles de implementación de la API de ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
