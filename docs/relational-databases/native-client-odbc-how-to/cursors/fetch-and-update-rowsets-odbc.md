---
description: Capturar y actualizar conjuntos de filas (ODBC)
title: Capturar y actualizar conjuntos de filas (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- rowsets [ODBC]
ms.assetid: cf0eb3b4-8b72-49fc-a845-95edc360cf93
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: bd2605fcad1e9942dca546a86661dd67991b8b27
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/09/2020
ms.locfileid: "91867792"
---
# <a name="fetch-and-update-rowsets-odbc"></a>Capturar y actualizar conjuntos de filas (ODBC)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

    
### <a name="to-fetch-and-update-rowsets"></a>Para capturar y actualizar conjuntos de filas  
  
1.  Opcionalmente, llame a [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) con SQL_ROW_ARRAY_SIZE para cambiar el número de filas (R) del conjunto de filas.  
  
2.  Llame a [SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md) o [SQLFetchScroll](../../../relational-databases/native-client-odbc-api/sqlfetchscroll.md) para obtener un conjunto de filas.  
  
3.  Si se usan columnas enlazadas, use ahora los valores de datos y las longitudes de datos disponibles de los búferes de la columna enlazada para el conjunto de filas.  
  
     Si se usan columnas desenlazadas, para cada fila llame a [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md) con SQL_POSITION establecer la posición del cursor; a continuación, para cada columna desenlazada:  
  
    -   Llame a [SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md) una o más veces para obtener los datos para las columnas desenlazadas después de la última columna enlazada del conjunto de filas. Las llamadas a [SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md) deber estar en orden de número de columna creciente.  
  
    -   Llame a [SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md) varias veces para obtener datos de una columna de texto o de imagen.  
  
4.  Configure cualquier columna de imagen o texto de datos en ejecución.  
  
5.  Llame a [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md) o [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md) para establecer la posición del cursor, actualizar, eliminar o agregar filas dentro del conjunto de filas.  
  
     Si se usan columnas de imagen o texto de datos en ejecución para una operación de actualización o adición, contrólelas.  
  
6.  Opcionalmente, ejecute una instrucción UPDATE o DELETE colocada, especificando el nombre del cursor (disponible desde [SQLGetCursorName](../../../relational-databases/native-client-odbc-api/sqlgetcursorname.md)) y usando un identificador de instrucción diferente en la misma conexión.  
  
## <a name="see-also"></a>Consulte también  
 [Temas de procedimientos de uso de cursores &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-how-to/cursors/using-cursors-how-to-topics-odbc.md)  
  
