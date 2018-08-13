---
title: SQLExecute | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQLExecute function
ms.assetid: 4d7db8b6-611f-4fe4-be85-2a407059de45
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: b5d4cb8fa1c8492f7f42633e113eee6d27f4de06
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2018
ms.locfileid: "39547685"
---
# <a name="sqlexecute"></a>SQLExecute
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Si el atributo de instrucción que sql_sopt_ss_param_focus no está establecido en 0, SQLExecute devolverá SQL_ERROR y generará un registro de diagnóstico con SQLSTATE = HY024 y el mensaje "valor de atributo no válido, SQL_SOPT_SS_PARAM_FOCUS (debe ser cero en tiempo de ejecución)". Para obtener más información acerca de SQL_SOPT_SS_PARAM_FOCUS, vea [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md).  
  
## <a name="remarks"></a>Notas  
 Para obtener más información acerca de los parámetros con valores de tabla, vea [parámetros con valores de tabla &#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="see-also"></a>Vea también  
 [SQLExecute](http://go.microsoft.com/fwlink/?LinkId=80708)   
 [Detalles de implementación de la API de ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
