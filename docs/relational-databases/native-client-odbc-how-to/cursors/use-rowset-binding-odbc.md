---
title: Usar enlace de conjuntos de filas (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- rowset binding [ODBC]
ms.assetid: a7be05f0-6b11-4b53-9fbc-501e591eef09
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 05277e548dab36b22c023fe674e404d8b9014c7c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81284618"
---
# <a name="use-rowset-binding-odbc"></a>Usar enlace de conjuntos de filas (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

    
### <a name="to-use-column-wise-binding"></a>Para utilizar el enlace de modo de columna  
  
1.  Para cada columna enlazada, haga lo siguiente:  
  
    -   Asigne una matriz de R (o más) búferes de columna para almacenar los valores de datos, donde R es el número de filas del conjunto de filas.  
  
    -   De modo opcional, asigne una matriz de R (o más) búferes de columna para almacenar las longitudes de los datos.  
  
    -   Llame a [SQLBindCol](../../../relational-databases/native-client-odbc-api/sqlbindcol.md) para enlazar las matrices de valores de datos y de longitud de datos de columna a la columna del conjunto de filas.  
  
2.  Llame a [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) para establecer los atributos siguientes:  
  
    -   Establezca SQL_ATTR_ROW_ARRAY_SIZE en el número de filas del conjunto de filas (R).  
  
    -   Establezca SQL_ATTR_ROW_BIND_TYPE en SQL_BIND_BY_COLUMN.  
  
    -   Establezca el atributo SQL_ATTR_ROWS FETCHED_PTR para que señale a una variable SQLUINTEGER que incluya el número de filas capturadas.  
  
    -   Establezca SQL_ATTR_ROW_STATUS_PTR para que señale a una matriz[R] de variables SQLUSSMALLINT que incluya indicadores de estado de filas.  
  
3.  Ejecute la instrucción.  
  
4.  Cada llamada a [SQLFetch](https://go.microsoft.com/fwlink/?LinkId=58401) o a [SQLFetchScroll](../../../relational-databases/native-client-odbc-api/sqlfetchscroll.md) recupera R filas y transfiere los datos a las columnas enlazadas.  

### <a name="to-use-row-wise-binding"></a>Para utilizar el enlace de modo de fila  
  
1.  Asigne una matriz [R] de estructuras, donde R es el número de filas del conjunto de filas. La estructura tiene un elemento para cada columna y cada elemento tiene dos partes:  
  
    -   La primera parte es una variable del tipo de datos adecuado donde almacenar los datos de columnas.  
  
    -   La segunda parte es una variable SQLINTEGER donde almacenar el indicador de estado de columnas.  
  
2.  Llame a [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) para establecer los atributos siguientes:  
  
    -   Establezca SQL_ATTR_ROW_ARRAY_SIZE en el número de filas del conjunto de filas (R).  
  
    -   Establezca SQL_ATTR_ROW_BIND_TYPE en el tamaño de la estructura asignada en el paso 1.  
  
    -   Establezca el atributo SQL_ATTR_ROWS_FETCHED_PTR para que señale a una variable SQLUINTEGER que incluya el número de filas capturadas.  
  
    -   Establezca SQL_ATTR_PARAMS_STATUS_PTR para que señale a una matriz[R] de variables SQLUSSMALLINT que incluya indicadores de estado de filas.  
  
3.  Para cada columna del conjunto de resultados, llame a [SQLBindCol](../../../relational-databases/native-client-odbc-api/sqlbindcol.md) para que el valor de datos y puntero de longitud de datos de la columna señalen a sus variables en el primer elemento de la matriz de estructuras asignada en el paso 1.  
  
4.  Ejecute la instrucción.  
  
5.  Cada llamada a [SQLFetch](https://go.microsoft.com/fwlink/?LinkId=58401) o a [SQLFetchScroll](../../../relational-databases/native-client-odbc-api/sqlfetchscroll.md) recupera R filas y transfiere los datos a las columnas enlazadas.  
  
## <a name="see-also"></a>Consulte también  
 [Temas de procedimientos de uso de cursores &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-how-to/cursors/using-cursors-how-to-topics-odbc.md)   
 [Cómo se implementan los cursores](../../../relational-databases/native-client-odbc-cursors/implementation/how-cursors-are-implemented.md)   
 [Usar cursores &#40;&#41;ODBC](../../../relational-databases/native-client-odbc-how-to/cursors/use-cursors-odbc.md)  
  
  
