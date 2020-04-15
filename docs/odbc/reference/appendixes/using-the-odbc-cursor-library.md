---
title: Uso de la biblioteca de cursores ODBC ( ODBC Cursor Library) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], using cursor library
- cursor library [ODBC], using cursor library
ms.assetid: 9653f2f8-ccfc-4220-99ef-601dc0fa641c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8c740ed78de51684eac38ad0c54ab2224986018d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301406"
---
# <a name="using-the-odbc-cursor-library"></a>Uso de la biblioteca de cursores ODBC
> [!IMPORTANT]  
>  Esta característica se eliminará en una versión futura de Windows. Evite usar esta característica en el nuevo trabajo de desarrollo y planee modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del cursor del controlador.  
  
 Para utilizar la biblioteca de cursores ODBC, una aplicación:  
  
1.  Llama a **SQLSetConnectAttr** con un *atributo* de SQL_ATTR_ODBC_CURSORS para especificar cómo se debe usar la biblioteca de cursores con una conexión determinada. La biblioteca de cursores siempre se puede utilizar (SQL_CUR_USE_ODBC), solo se puede utilizar si el controlador no admite cursores desplazables (SQL_CUR_USE_IF_NEEDED) o nunca se utiliza (SQL_CUR_USE_DRIVER).  
  
2.  Llama a **SQLConnect**, **SQLDriverConnect**o **SQLBrowseConnect** para conectarse al origen de datos.  
  
3.  Llama a **SQLSetStmtAttr** para especificar el tipo de cursor (SQL_ATTR_CURSOR_TYPE), la simultaneidad (SQL_ATTR_CONCURRENCY) y el tamaño del conjunto de filas (SQL_ATTR_ROW_ARRAY_SIZE). La biblioteca de cursores admite cursores estáticos y de solo avance. Los cursores de solo avance deben ser de solo lectura, mientras que los cursores estáticos pueden ser de solo lectura o pueden usar valores de comparación de control de simultaneidad optimista.  
  
4.  Asigna uno o varios búferes de conjunto de filas y llama a **SQLBindCol** una o varias veces para enlazar estos búferes a columnas de conjunto de resultados.  
  
5.  Genera un conjunto de resultados ejecutando una instrucción **SELECT** o un procedimiento, o llamando a una función de catálogo. Si la aplicación ejecutará instrucciones de actualización posicionadas, debe ejecutar una instrucción **SELECT FOR UPDATE** para generar el conjunto de resultados.  
  
6.  Llama a **SQLFetch** o **SQLFetchScroll** una o más veces para desplazarse por el conjunto de resultados.  
  
 La aplicación puede cambiar los valores de datos en los búferes del conjunto de filas. Para actualizar los búferes de conjunto de filas con datos de la memoria caché de la biblioteca de cursores, una aplicación llama a **SQLFetchScroll** con el *FetchOrientation* argumento establecido en SQL_FETCH_RELATIVE y el *FetchOffset* argumento establecido en 0.  
  
 Para recuperar datos de una columna sin enlazar, la aplicación llama a **SQLSetPos** para colocar el cursor en la fila deseada. A continuación, llama a **SQLGetData** para recuperar los datos.  
  
 Para determinar el número de filas que se han recuperado del origen de datos, la aplicación llama a **SQLRowCount**.
