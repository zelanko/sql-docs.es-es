---
title: Usar una instrucción (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- statements [ODBC]
ms.assetid: f7573f8f-6f21-4e03-8dd5-a5f2ea4878cc
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 62c422e0fb5c5afe481b2d11a477523ca1466df3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81284456"
---
# <a name="use-a-statement-odbc"></a>Usar una instrucción (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

    
### <a name="to-use-a-statement"></a>Para utilizar una instrucción  
  
1.  Llame a [SQLAllocHandle](https://go.microsoft.com/fwlink/?LinkId=58396) con un *HandleType* de SQL_HANDLE_STMT para asignar un identificador de instrucción.  
  
2.  Opcionalmente, llame a [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) para establecer las opciones de la instrucción o a [SQLGetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlgetstmtattr.md) para obtener atributos de instrucción.  
  
     Para utilizar cursores de servidor, debe establecer los atributos de cursor en valores distintos de sus valores predeterminados.  
  
3.  Opcionalmente, si la instrucción se va a ejecutar varias veces, prepárela para la ejecución con [SQLPrepare Function](https://go.microsoft.com/fwlink/?LinkId=59360).  
  
4.  Opcionalmente, si la instrucción ha enlazado marcadores de parámetros, enlace los marcadores de parámetros a las variables del programa utilizando [SQLBindParameter](../../../relational-databases/native-client-odbc-api/sqlbindparameter.md). Si se ha preparado la instrucción, puede llamar a [SQLNumParams](https://go.microsoft.com/fwlink/?LinkId=58404) y [SQLDescribeParam](../../../relational-databases/native-client-odbc-api/sqldescribeparam.md) to find the number y characteristics of the parameters.  
  
5.  Ejecute directamente una instrucción utilizando SQLExecDirect.  
  
     \- o -  
  
     Si se ha preparado la instrucción, ejecútela varias veces utilizando [SQLExecute](https://go.microsoft.com/fwlink/?LinkId=58400).  
  
     \- o -  
  
     Llame a una función de catálogo, que devuelve los resultados.  
  
6.  Procese los resultados enlazando las columnas del conjunto de resultados a variables de programa, moviendo los datos de las columnas del conjunto de resultados a las variables del programa mediante [SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md)o una combinación de los dos métodos.  
  
     Capture una fila cada vez del conjunto de resultados de una instrucción.  
  
     \- o -  
  
     Capture varias filas cada vez del conjunto de resultados mediante un cursor de bloque.  
  
     \- o -  
  
     Llame a [SQLRowCount](../../../relational-databases/native-client-odbc-api/sqlrowcount.md) para determinar el número de filas afectado por una instrucción INSERT, UPDATE o DELETE.  
  
     Si la instrucción SQL puede tener varios conjuntos de resultados, llame a [SQLMoreResults](../../../relational-databases/native-client-odbc-api/sqlmoreresults.md) al final de cada conjunto de resultados para determinar si hay más conjuntos de resultados que procesar.  
  
7.  Una vez procesados los resultados, pueden requerirse las acciones siguientes para que el identificador de instrucción esté disponible para ejecutar una nueva instrucción:  
  
    -   Si no llamó a [SQLMoreResults](../../../relational-databases/native-client-odbc-api/sqlmoreresults.md) hasta que se devolvió SQL_NO_DATA, llame a [SQLCloseCursor](../../../relational-databases/native-client-odbc-api/sqlclosecursor.md) para cerrar el cursor.  
  
    -   Si ha enlazado marcadores de parámetros a las variables del programa, llame a [SQLFreeStmt](../../../relational-databases/native-client-odbc-api/sqlfreestmt.md) con *Option* establecido en SQL_RESET_PARAMS para liberar los parámetros enlazados.  
  
    -   Si ha enlazado columnas de conjuntos de resultados a las variables del programa, llame a [SQLFreeStmt](../../../relational-databases/native-client-odbc-api/sqlfreestmt.md) con *Option* establecido en SQL_UNBIND para liberar las columnas enlazadas.  
  
    -   Para reutilizar el identificador de instrucción, vaya al paso 2.  
  
8.  Llame a [SQLFreeHandle](../../../relational-databases/native-client-odbc-api/sqlfreehandle.md) con un *HandleType* de SQL_HANDLE_STMT para liberar el identificador de instrucción.  
  
## <a name="see-also"></a>Consulte también  
 [Temas de procedimientos de ejecución de consultas &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-how-to/execute-queries/executing-queries-how-to-topics-odbc.md)  
  
  
