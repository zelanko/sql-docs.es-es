---
title: "Tipo SQL de ODBC para parámetros con valores de tabla | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-table-valued-parameters
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: SQL_SS_TABLE
ms.assetid: 6725bfb9-5f10-4115-be09-fd9c9f5779ea
caps.latest.revision: "17"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a781dd635a0c1c17e67415101536d7af69db60b2
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="odbc-sql-type-for-table-valued-parameters"></a>Tipo SQL de ODBC para parámetros con valores de tabla
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Un nuevo tipo de SQL de ODBC, SQL_SS_TABLE, proporciona compatibilidad con parámetros con valores de tabla.  
  
## <a name="remarks"></a>Comentarios  
 SQL_SS_TABLE no se puede convertir en ningún otro tipo de datos ODBC o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Si se utiliza SQL_SS_TABLE como un tipo de datos C en el *ValueType* parámetro de SQLBindParameter o un intento se realiza para establecer SQL_DESC_TYPE en un registro de descriptor (APD) del parámetro de aplicación en SQL_SS_TABLE, se devuelve SQL_ERROR y un se genera un registro de diagnóstico con SQLSTATE = HY003, "tipo de búfer de aplicación no válido".  
  
 Si SQL_DESC_TYPE está establecido en SQL_SS_TABLE en un registro IPD y el registro del descriptor de parámetros de la aplicación correspondiente no es SQL_C_DEFAULT, se devuelve SQL_ERROR y se genera un registro de diagnóstico con SQLSTATE=HY003, "Tipo de búfer de aplicación no válido". Esto puede ocurrir con los *ParameterType* de SQLSetDescField, SQLSetDescRec o SQLBindParameter.  
  
 Si el *TargetType* parámetro es SQL_SS_TABLE al llamar a SQLGetData, se devuelve SQL_ERROR y se genera un registro de diagnóstico con SQLSTATE = HY003, "tipo de búfer de aplicación no válido".  
  
 Una columna de parámetro con valores de tabla no se puede enlazar como tipo SQL_SS_TABLE. Si se llama a **SQLBindParameter** con *ParameterType* establecido en SQL_SS_TABLE, se devuelve SQL_ERROR y se genera un registro de diagnóstico con SQLSTATE=HY004, "Tipo de datos SQL no válido". Esto también puede ocurrir con SQLSetDescField y SQLSetDescRec.  
  
 Los valores de las columnas de parámetros con valores de tabla tienen las mismas opciones de conversión de datos que las columnas de parámetros y resultado.  
  
 Un parámetro con valores de tabla puede ser solamente un parámetro de entrada en [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o posterior. Si se realiza un intento para establecer SQL_DESC_PARAMETER_TYPE en un valor distinto de SQL_PARAM_INPUT a través de SQLBindParameter o SQLSetDescField, se devuelve SQL_ERROR y se agrega un registro de diagnóstico a la instrucción con SQLSTATE = HY105 y el mensaje "parámetro no válido Escriba".  
  
 Las columnas de parámetros con valores de tabla no pueden utilizar SQL_DEFAULT_PARAM en *StrLen_or_IndPtr*, porque los valores predeterminados por fila no se admiten con los parámetros con valores de tabla. En su lugar, una aplicación puede establecer el atributo de columna SQL_CA_SS_COL_HAS_DEFAULT_VALUE en 1. Esto significa que la columna tendrá los valores predeterminados para todas las filas. Si *StrLen_or_IndPtr* está establecido en SQL_DEFAULT_PARAM, SQLExecute o SQLExecDirect devolverá SQL_ERROR y se agregará un registro de diagnóstico a la instrucción con SQLSTATE = HY090 y el mensaje "Longitud de búfer o cadena no válida".  
  
## <a name="see-also"></a>Vea también  
 [Con valores de tabla parámetros &#40; ODBC &#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
