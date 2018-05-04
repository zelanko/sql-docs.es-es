---
title: Usar la biblioteca de cursores ODBC | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], using cursor library
- cursor library [ODBC], using cursor library
ms.assetid: 9653f2f8-ccfc-4220-99ef-601dc0fa641c
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bd5d1d580545afa63865c5d23a70dc75c177f41e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="using-the-odbc-cursor-library"></a>Uso de la biblioteca de cursores ODBC
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del controlador cursor.  
  
 Para usar la biblioteca de cursores ODBC, una aplicación:  
  
1.  Llamadas **SQLSetConnectAttr** con una *atributo* de SQL_ATTR_ODBC_CURSORS para especificar cómo debería usarse la biblioteca de cursores con una conexión determinada. La biblioteca de cursores puede ser siempre utilizan (SQL_CUR_USE_ODBC), usa únicamente si el controlador no es compatible con los cursores desplazables (SQL_CUR_USE_IF_NEEDED) o no utilizar nunca (SQL_CUR_USE_DRIVER).  
  
2.  Llamadas **SQLConnect**, **SQLDriverConnect**, o **SQLBrowseConnect** para conectarse al origen de datos.  
  
3.  Llamadas **SQLSetStmtAttr** para especificar el tipo de cursor (SQL_ATTR_CURSOR_TYPE), la simultaneidad (SQL_ATTR_CONCURRENCY) y el tamaño del conjunto de filas (SQL_ATTR_ROW_ARRAY_SIZE). La biblioteca de cursores es compatible con los cursores estáticos y de solo avance. Cursores de solo avance deben ser de solo lectura, mientras que los cursores estáticos pueden ser de solo lectura o pueden usar comparación de valores de control de simultaneidad optimista.  
  
4.  Asigna uno o más búferes de conjunto de filas y llamadas **SQLBindCol** una o varias veces para enlazar estos búferes como resultado columnas del conjunto.  
  
5.  Genera un conjunto de resultados por ejecutar una **seleccione** instrucción o un procedimiento, o mediante una llamada a una función de catálogo. Si la aplicación ejecutará las instrucciones update posicionadas, debe ejecutar un **seleccione para actualizar** instrucción que se va a generar el conjunto de resultados.  
  
6.  Llamadas **SQLFetch** o **SQLFetchScroll** una o varias veces para desplazarse por el conjunto de resultados.  
  
 La aplicación puede cambiar los valores de datos de los búferes de conjunto de filas. Para actualizar los búferes de conjunto de filas con los datos de caché de la biblioteca de cursores, llama a una aplicación **SQLFetchScroll** con el *FetchOrientation* establecido en SQL_FETCH_RELATIVE y  *FetchOffset* establecido en 0.  
  
 Para recuperar datos de una columna sin enlazar, la aplicación llama **SQLSetPos** para colocar el cursor en la fila deseada. A continuación, se llama **SQLGetData** para recuperar los datos.  
  
 Para determinar el número de filas que han sido recuperados del origen de datos, la aplicación llama a **SQLRowCount**.
