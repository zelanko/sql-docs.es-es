---
title: Capturar y actualizar conjuntos de filas (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- rowsets [ODBC]
ms.assetid: cf0eb3b4-8b72-49fc-a845-95edc360cf93
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fc6a5254afc715a950f2d3c63d02bfca7a1890ea
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48076585"
---
# <a name="fetch-and-update-rowsets-odbc"></a>Capturar y actualizar conjuntos de filas (ODBC)
    
### <a name="to-fetch-and-update-rowsets"></a>Para capturar y actualizar conjuntos de filas  
  
1.  Opcionalmente, llame a [SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md) con SQL_ROW_ARRAY_SIZE para cambiar el número de filas (R) en el conjunto de filas.  
  
2.  Llame a [SQLFetch](http://go.microsoft.com/fwlink/?LinkId=58401) o [SQLFetchScroll](../../native-client-odbc-api/sqlfetchscroll.md) para obtener un conjunto de filas.  
  
3.  Si se usan columnas enlazadas, use ahora los valores de datos y las longitudes de datos disponibles de los búferes de la columna enlazada para el conjunto de filas.  
  
     Si se usan columnas desenlazadas, para cada fila llame a [SQLSetPos](http://go.microsoft.com/fwlink/?LinkId=58407) con SQL_POSITION establecer la posición del cursor; a continuación, para cada columna desenlazada:  
  
    -   Llame a [SQLGetData](../../native-client-odbc-api/sqlgetdata.md) uno o más veces para obtener los datos de las columnas desenlazadas, después de la última columna del conjunto de filas enlazada. Las llamadas a [SQLGetData](../../native-client-odbc-api/sqlgetdata.md) deben estar en orden creciente de número de columna.  
  
    -   Llame a [SQLGetData](../../native-client-odbc-api/sqlgetdata.md) varias veces para obtener datos de una columna de texto o de imagen.  
  
4.  Configure cualquier columna de imagen o texto de datos en ejecución.  
  
5.  Llame a [SQLSetPos](http://go.microsoft.com/fwlink/?LinkId=58407) o [SQLBulkOperations](http://go.microsoft.com/fwlink/?LinkId=58398) para establecer la posición del cursor, actualizar, eliminar o agregar filas dentro del conjunto de filas.  
  
     Si se usan columnas de imagen o texto de datos en ejecución para una operación de actualización o adición, contrólelas.  
  
6.  Opcionalmente, ejecute una instrucción de las UPDATE o DELETE colocada, especificando el nombre del cursor (disponible en [SQLGetCursorName](../../native-client-odbc-api/sqlgetcursorname.md)) y el uso de un identificador de instrucción diferente en la misma conexión.  
  
## <a name="see-also"></a>Vea también  
 [Uso de temas de procedimientos de los cursores &#40;ODBC&#41;](using-cursors-how-to-topics-odbc.md)  
  
  
