---
title: Usar conjuntos de filas (ODBC) de enlace | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- rowset binding [ODBC]
ms.assetid: a7be05f0-6b11-4b53-9fbc-501e591eef09
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 2ef6f3651cb1cb1c80247f5853b4d4bd05bc13fc
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2018
ms.locfileid: "35694446"
---
# <a name="use-rowset-binding-odbc"></a>Usar enlace de conjuntos de filas (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

    
### <a name="to-use-column-wise-binding"></a>Para utilizar el enlace de modo de columna  
  
1.  Para cada columna enlazada, haga lo siguiente:  
  
    -   Asigne una matriz de R (o más) búferes de columna para almacenar los valores de datos, donde R es el número de filas del conjunto de filas.  
  
    -   De modo opcional, asigne una matriz de R (o más) búferes de columna para almacenar las longitudes de los datos.  
  
    -   Llame a [SQLBindCol](../../../relational-databases/native-client-odbc-api/sqlbindcol.md) para enlazar los valores de datos y matrices de longitud de datos de la columna a la columna del conjunto de filas.  
  
2.  Llame a [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) para establecer los atributos siguientes:  
  
    -   Establezca SQL_ATTR_ROW_ARRAY_SIZE en el número de filas del conjunto de filas (R).  
  
    -   Establezca SQL_ATTR_ROW_BIND_TYPE en SQL_BIND_BY_COLUMN.  
  
    -   Establezca el atributo SQL_ATTR_ROWS FETCHED_PTR para que señale a una variable SQLUINTEGER que incluya el número de filas capturadas.  
  
    -   Establezca SQL_ATTR_ROW_STATUS_PTR para que señale a una matriz[R] de variables SQLUSSMALLINT que incluya indicadores de estado de filas.  
  
3.  Ejecute la instrucción.  
  
4.  Cada llamada a [SQLFetch](http://go.microsoft.com/fwlink/?LinkId=58401) o [SQLFetchScroll](../../../relational-databases/native-client-odbc-api/sqlfetchscroll.md) recupera R filas y transfiere los datos en las columnas enlazadas.  
  
### <a name="to-use-row-wise-binding"></a>Para utilizar el enlace de modo de fila  
  
1.  Asigne una matriz [R] de estructuras, donde R es el número de filas del conjunto de filas. La estructura tiene un elemento para cada columna y cada elemento tiene dos partes:  
  
    -   La primera parte es una variable del tipo de datos adecuado donde almacenar los datos de columnas.  
  
    -   La segunda parte es una variable SQLINTEGER donde almacenar el indicador de estado de columnas.  
  
2.  Llame a [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) para establecer los atributos siguientes:  
  
    -   Establezca SQL_ATTR_ROW_ARRAY_SIZE en el número de filas del conjunto de filas (R).  
  
    -   Establezca SQL_ATTR_ROW_BIND_TYPE en el tamaño de la estructura asignada en el paso 1.  
  
    -   Establezca el atributo SQL_ATTR_ROWS_FETCHED_PTR para que señale a una variable SQLUINTEGER que incluya el número de filas capturadas.  
  
    -   Establezca SQL_ATTR_PARAMS_STATUS_PTR para que señale a una matriz[R] de variables SQLUSSMALLINT que incluya indicadores de estado de filas.  
  
3.  Para cada columna del conjunto de resultados, llame a [SQLBindCol](../../../relational-databases/native-client-odbc-api/sqlbindcol.md) para el valor de datos y el puntero de longitud de datos de la columna señalen a sus variables en el primer elemento de la matriz de estructuras asignada en el paso 1.  
  
4.  Ejecute la instrucción.  
  
5.  Cada llamada a [SQLFetch](http://go.microsoft.com/fwlink/?LinkId=58401) o [SQLFetchScroll](../../../relational-databases/native-client-odbc-api/sqlfetchscroll.md) recupera R filas y transfiere los datos en las columnas enlazadas.  
  
## <a name="see-also"></a>Vea también  
 [Con los temas de procedimientos de los cursores &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-how-to/cursors/using-cursors-how-to-topics-odbc.md)   
 [Cómo se implementan los cursores](../../../relational-databases/native-client-odbc-cursors/implementation/how-cursors-are-implemented.md)   
 [Usar cursores &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-how-to/cursors/use-cursors-odbc.md)  
  
  
