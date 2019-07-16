---
title: Establecer opciones de Cursor (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- cursors [ODBC], options
ms.assetid: 0e72b48a-fc5a-4656-8cf5-39f57d8c1565
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 185040c174608d2f3a14d23047d63ab8ccf8c0a8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67898524"
---
# <a name="set-cursor-options-odbc"></a>Establecer las opciones del cursor (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Para establecer las opciones de cursor, llame a [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) para establecer o [SQLGetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlgetstmtattr.md) para obtener las opciones de instrucción que controlan el comportamiento del cursor.  
  
|*Atributo*|Especifica|  
|-----------------|---------------|  
|SQL_ATTR_CURSOR_TYPE|Tipo de cursor de solo avance, estático, dinámico o controlado por conjunto de claves|  
|SQL_ATTR_CONCURRENCY|Opción de control de simultaneidad de solo lectura, bloqueo, marcas de tiempo de uso optimista o valores de uso optimista|  
|SQL_ATTR_ROW_ARRAY_SIZE|Número de filas obtenido en cada captura|  
|SQL_ATTR_CURSOR_SENSITIVITY|Cursor que puede mostrar o no las actualizaciones realizadas por otras conexiones en las filas del cursor|  
|SQL_ATTR_CURSOR_SCROLLABLE|Cursor que puede desplazarse hacia delante y hacia atrás|  
  
 Los valores predeterminados de estos atributos (solo avance, solo lectura, tamaño del conjunto de filas igual a 1) no usan los cursores del servidor. Para usar los cursores del servidor, al menos uno de estos atributos debe establecerse en un valor distinto del predeterminado y la instrucción en ejecución debe ser una instrucción SELECT única o un procedimiento almacenado que contenga una instrucción SELECT única. Cuando se utilizan cursores de servidor, las instrucciones SELECT no pueden utilizar cláusulas no compatibles con los cursores de servidor: COMPUTE, COMPUTE BY, FOR BROWSE e INTO.  
  
 Puede controlar el tipo de cursor utilizando estableciendo SQL_ATTR_CURSOR_TYPE y SQL_ATTR_CONCURRENCY o estableciendo SQL_ATTR_CURSOR_SENSITIVITY y SQL_ATTR_CURSOR_SCROLLABLE. No debe mezclar los dos métodos que se utilizan para especificar el comportamiento del cursor.  
  
## <a name="example"></a>Ejemplo  
 En el siguiente ejemplo se asigna un identificador de instrucción, se establece un tipo de cursor dinámico con simultaneidad optimista de versiones de fila y, a continuación, se ejecuta una instrucción SELECT.  
  
```  
retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
retcode = SQLSetStmtAttr(hstmt1, SQL_ATTR_CURSOR_TYPE, (SQLPOINTER)SQL_CURSOR_DYNAMIC, SQL_IS_INTEGER);  
retcode = SQLSetStmtAttr(hstmt1, SQL_ATTR_CONCURRENCY, SQLPOINTER)SQL_CONCUR_ROWVER, SQL_IS_INTEGER);  
retcode = SQLExecDirect(hstmt1, SELECT au_lname FROM authors", SQL_NTS);  
```  
  
## <a name="example"></a>Ejemplo  
 En el siguiente ejemplo se asigna un identificador de instrucción, se establece un cursor desplazable de tipo SENSITIVE y, a continuación, se ejecuta una instrucción SELECT  
  
```  
retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
  
// Set the cursor options and execute the statement.  
retcode = SQLSetStmtAttr(hstmt1, SQL_ATTR_CURSOR_SCROLLABLE, SQLPOINTER)SQL_SCROLLABLE, SQL_IS_INTEGER);  
retcode = SQLSetStmtAttr(hstmt1, SQL_ATTR_CURSOR_SENSITIVITY, SQLPOINTER)SQL_INSENSITIVE, SQL_IS_INTEGER);  
retcode = SQLExecDirect(hstmt1, select au_lname from authors", SQL_NTS);  
```  
  
## <a name="see-also"></a>Vea también  
 [Ejecutar consultas de temas de procedimientos &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-how-to/execute-queries/executing-queries-how-to-topics-odbc.md)  
  
  
