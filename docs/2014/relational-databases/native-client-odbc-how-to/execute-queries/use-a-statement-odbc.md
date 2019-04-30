---
title: Usar una instrucción (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- statements [ODBC]
ms.assetid: f7573f8f-6f21-4e03-8dd5-a5f2ea4878cc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 842e862dff7eca85a05df0222989c6ee6390ab89
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63200323"
---
# <a name="use-a-statement-odbc"></a>Usar una instrucción (ODBC)
    
### <a name="to-use-a-statement"></a>Para utilizar una instrucción  
  
1.  Llame a [SQLAllocHandle](https://go.microsoft.com/fwlink/?LinkId=58396) con un *HandleType* de SQL_HANDLE_STMT para asignar un identificador de instrucción.  
  
2.  Opcionalmente, llame a [SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md) para establecer las opciones de la instrucción o a [SQLGetStmtAttr](../../native-client-odbc-api/sqlgetstmtattr.md) para obtener atributos de instrucción.  
  
     Para utilizar cursores de servidor, debe establecer los atributos de cursor en valores distintos de sus valores predeterminados.  
  
3.  Opcionalmente, si la instrucción se va a ejecutar varias veces, prepárela para la ejecución con [SQLPrepare Function](https://go.microsoft.com/fwlink/?LinkId=59360).  
  
4.  Opcionalmente, si la instrucción ha enlazado marcadores de parámetros, enlace los marcadores de parámetros a las variables del programa utilizando [SQLBindParameter](../../native-client-odbc-api/sqlbindparameter.md). Si se ha preparado la instrucción, puede llamar a [SQLNumParams](https://go.microsoft.com/fwlink/?LinkId=58404) y [SQLDescribeParam](../../native-client-odbc-api/sqldescribeparam.md) to find the number y characteristics of the parameters.  
  
5.  Ejecute directamente una instrucción utilizando SQLExecDirect.  
  
     \- o -  
  
     Si se ha preparado la instrucción, ejecútela varias veces utilizando [SQLExecute](https://go.microsoft.com/fwlink/?LinkId=58400).  
  
     \- o -  
  
     Llame a una función de catálogo, que devuelve los resultados.  
  
6.  Procese los resultados enlazando las columnas del conjunto de resultados a variables de programa, moviendo los datos de las columnas del conjunto de resultados a las variables del programa mediante [SQLGetData](../../native-client-odbc-api/sqlgetdata.md)o una combinación de los dos métodos.  
  
     Capture una fila cada vez del conjunto de resultados de una instrucción.  
  
     \- o -  
  
     Capture varias filas cada vez del conjunto de resultados mediante un cursor de bloque.  
  
     \- o -  
  
     Llame a [SQLRowCount](../../native-client-odbc-api/sqlrowcount.md) para determinar el número de filas afectado por una instrucción INSERT, UPDATE o DELETE.  
  
     Si la instrucción SQL puede tener varios conjuntos de resultados, llame a [SQLMoreResults](../../native-client-odbc-api/sqlmoreresults.md) al final de cada conjunto de resultados para determinar si hay más conjuntos de resultados que procesar.  
  
7.  Una vez procesados los resultados, pueden requerirse las acciones siguientes para que el identificador de instrucción esté disponible para ejecutar una nueva instrucción:  
  
    -   Si no llamó a [SQLMoreResults](../../native-client-odbc-api/sqlmoreresults.md) hasta que se devolvió SQL_NO_DATA, llame a [SQLCloseCursor](../../native-client-odbc-api/sqlclosecursor.md) para cerrar el cursor.  
  
    -   Si ha enlazado marcadores de parámetros a las variables del programa, llame a [SQLFreeStmt](../../native-client-odbc-api/sqlfreestmt.md) con *Option* establecido en SQL_RESET_PARAMS para liberar los parámetros enlazados.  
  
    -   Si ha enlazado columnas de conjuntos de resultados a las variables del programa, llame a [SQLFreeStmt](../../native-client-odbc-api/sqlfreestmt.md) con *Option* establecido en SQL_UNBIND para liberar las columnas enlazadas.  
  
    -   Para reutilizar el identificador de instrucción, vaya al paso 2.  
  
8.  Llame a [SQLFreeHandle](../../native-client-odbc-api/sqlfreehandle.md) con un *HandleType* de SQL_HANDLE_STMT para liberar el identificador de instrucción.  
  
## <a name="see-also"></a>Vea también  
 [Ejecutar consultas de temas de procedimientos &#40;ODBC&#41;](executing-queries-how-to-topics-odbc.md)  
  
  
