---
title: SQLPrimaryKeys | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLPrimaryKeys function
ms.assetid: bc61cd5b-d2f4-4f87-abc7-743cf9ea772d
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: bf00ecd74b64b3910ba19365920baf914f86939c
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82705887"
---
# <a name="sqlprimarykeys"></a>SQLPrimaryKeys
  Una tabla puede tener una o varias columnas que pueden actuar como identificadores de fila únicos y las tablas creadas sin una restricción PRIMAry KEY devuelven un conjunto de resultados vacío a SQLPrimaryKeys. La función ODBC [SQLSpecialColumns](sqlspecialcolumns.md) informa de los candidatos de identificador de fila para las tablas sin claves principales.  
  
 SQLPrimaryKeys devuelve SQL_SUCCESS si existen o no valores para los parámetros *nombrecatálogo*, *SchemaName*o *TableName* . SQLFetch devuelve SQL_NO_DATA si se usan valores no válidos en estos parámetros.  
  
 SQLPrimaryKeys se puede ejecutar en un cursor de servidor estático. Un intento de ejecutar SQLPrimaryKeys en un cursor actualizable (dinámico o de conjunto de claves) devolverá SQL_SUCCESS_WITH_INFO que indica que se ha cambiado el tipo de cursor.  
  
 El controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client permite notificar información de tablas en servidores vinculados aceptando un nombre de dos partes para el parámetro *CatalogName* : *Linked_Server_Name.Catalog_Name*.  
  
## <a name="sqlprimarykeys-and-table-valued-parameters"></a>SQLPrimaryKeys y parámetros con valores de tabla  
 Si el atributo de instrucción SQL_SOPT_SS_NAME_SCOPE tiene el valor SQL_SS_NAME_SCOPE_TABLE_TYPE, en lugar de su valor predeterminado de SQL_SS_NAME_SCOPE_TABLE, SQLPrimaryKeys devolverá información sobre las columnas de clave principal de los tipos de tabla. Para obtener más información sobre SQL_SOPT_SS_NAME_SCOPE, vea [SQLSetStmtAttr](sqlsetstmtattr.md).  
  
 Para obtener más información sobre los parámetros con valores de tabla, vea [parámetros con valores de tabla &#40;ODBC&#41;](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="see-also"></a>Consulte también  
 [SQLPrimaryKeys función)](https://go.microsoft.com/fwlink/?LinkId=59361)   
 [ODBC API Implementation Details](odbc-api-implementation-details.md)  
  
  
