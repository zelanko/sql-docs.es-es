---
title: Tipo SQL de ODBC para parámetros con valores de tabla | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL_SS_TABLE
ms.assetid: 6725bfb9-5f10-4115-be09-fd9c9f5779ea
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: beafe79839842f530d4864339da53a7781123447
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "73776412"
---
# <a name="odbc-sql-type-for-table-valued-parameters"></a>Tipo SQL de ODBC para parámetros con valores de tabla
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Un nuevo tipo de SQL de ODBC, SQL_SS_TABLE, proporciona compatibilidad con parámetros con valores de tabla.  
  
## <a name="remarks"></a>Observaciones  
 SQL_SS_TABLE no se puede convertir en ningún otro tipo de datos ODBC o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Si se usa SQL_SS_TABLE como un tipo de datos de C en el parámetro *ValueType* de SQLBindParameter, o se intenta establecer SQL_DESC_TYPE en un registro de descriptor de parámetros de la aplicación (APD) en SQL_SS_TABLE, se devuelve SQL_ERROR y se genera un registro de diagnóstico con SQLSTATE = HY003, "tipo de búfer de aplicación no válido".  
  
 Si SQL_DESC_TYPE está establecido en SQL_SS_TABLE en un registro IPD y el registro del descriptor de parámetros de la aplicación correspondiente no es SQL_C_DEFAULT, se devuelve SQL_ERROR y se genera un registro de diagnóstico con SQLSTATE=HY003, "Tipo de búfer de aplicación no válido". Esto puede ocurrir con el *ParameterType* de SQLSetDescField, SQLSetDescRec o SQLBindParameter.  
  
 Si el parámetro *TargetType* es SQL_SS_TABLE al llamar a SQLGetData, se devuelve SQL_ERROR y se genera un registro de diagnóstico con SQLSTATE = HY003, "tipo de búfer de aplicación no válido".  
  
 Una columna de parámetro con valores de tabla no se puede enlazar como tipo SQL_SS_TABLE. Si se llama a **SQLBindParameter** con *ParameterType* establecido en SQL_SS_TABLE, se devuelve SQL_ERROR y se genera un registro de diagnóstico con SQLSTATE=HY004, "Tipo de datos SQL no válido". Esto también puede ocurrir con SQLSetDescField y SQLSetDescRec.  
  
 Los valores de las columnas de parámetros con valores de tabla tienen las mismas opciones de conversión de datos que las columnas de parámetros y resultado.  
  
 Un parámetro con valores de tabla puede ser solamente un parámetro de entrada en [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o posterior. Si se realiza un intento de establecer SQL_DESC_PARAMETER_TYPE en un valor distinto de SQL_PARAM_INPUT a través de SQLBindParameter o SQLSetDescField, se devuelve SQL_ERROR y se agrega un registro de diagnóstico a la instrucción con SQLSTATE = HY105 y el mensaje "parámetro no válido Escriba ".  
  
 Las columnas de parámetros con valores de tabla no pueden utilizar SQL_DEFAULT_PARAM en *StrLen_or_IndPtr*, porque los valores predeterminados por fila no se admiten con los parámetros con valores de tabla. En su lugar, una aplicación puede establecer el atributo de columna SQL_CA_SS_COL_HAS_DEFAULT_VALUE en 1. Esto significa que la columna tendrá los valores predeterminados para todas las filas. Si *StrLen_or_IndPtr* se establece en SQL_DEFAULT_PARAM, SQLExecute o SQLExecDirect devolverán SQL_ERROR y se agregará un registro de diagnóstico a la instrucción con SQLSTATE = HY090 y el mensaje "longitud de búfer o cadena no válida".  
  
## <a name="see-also"></a>Consulte también  
 [Parámetros con valores de tabla &#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
