---
title: SQLExecDirect ? Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLExecDirect function
ms.assetid: e7c2a5b5-83f4-4c72-9aca-7b9fb4748b11
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 52d5e1bffc49b13289c063154affd517cb8866f6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298479"
---
# <a name="sqlexecdirect"></a>SQLExecDirect
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Si el atributo de instrucción SQL_SOPT_SS_PARAM_FOCUS no es 0, SQLExecDirect devolverá SQL_ERROR y generará un registro de diagnóstico con SQLSTATE-HY024 y el mensaje "Valor de atributo no válido, SQL_SOPT_SS_PARAM_FOCUS (debe ser cero en tiempo de ejecución)". Para obtener más información acerca de SQL_SOPT_SS_PARAM_FOCUS, vea [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md).  
  
 Para obtener más información acerca de los parámetros con valores de tabla, vea [Parámetros con valores ](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)de tabla &#40;&#41;ODBC .  
  
## <a name="see-also"></a>Consulte también  
 [SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=80709)   
 [ODBC API Implementation Details](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
