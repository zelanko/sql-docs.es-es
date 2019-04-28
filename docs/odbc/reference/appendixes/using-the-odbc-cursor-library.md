---
title: Uso de la biblioteca de cursores ODBC | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9fe19efb2d39e875cdafec76f2c50164f3a66f03
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62735031"
---
# <a name="using-the-odbc-cursor-library"></a>Uso de la biblioteca de cursores ODBC
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite usar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad de cursor del controlador.  
  
 Para usar la biblioteca de cursores ODBC, una aplicación:  
  
1.  Las llamadas **SQLSetConnectAttr** con un *atributo* de SQL_ATTR_ODBC_CURSORS para especificar cómo se debe usar la biblioteca de cursores con una conexión determinada. La biblioteca de cursores puede ser siempre usar (SQL_CUR_USE_ODBC), usa únicamente si el controlador no es compatible con los cursores desplazables (SQL_CUR_USE_IF_NEEDED) o nunca (al utilizar SQL_CUR_USE_DRIVER).  
  
2.  Las llamadas **SQLConnect**, **SQLDriverConnect**, o **SQLBrowseConnect** para conectarse al origen de datos.  
  
3.  Las llamadas **SQLSetStmtAttr** para especificar el tipo de cursor (SQL_ATTR_CURSOR_TYPE), la simultaneidad (SQL_ATTR_CONCURRENCY) y el tamaño del conjunto de filas (SQL_ATTR_ROW_ARRAY_SIZE). La biblioteca de cursores es compatible con cursores estáticos y de solo avance. Cursores de solo avance deben ser de solo lectura, mientras que los cursores estáticos pueden ser de solo lectura o pueden usar la comparación de valores de control de simultaneidad optimista.  
  
4.  Asigna uno o varios búferes de conjunto de filas y las llamadas **SQLBindCol** una o varias veces para enlazar estos búferes como resultado columnas del conjunto.  
  
5.  Genera un conjunto de resultados, ejecutando un **seleccione** instrucción o un procedimiento, o mediante una llamada a una función de catálogo. Si la aplicación ejecutará las instrucciones update posicionadas, debe ejecutar un **seleccione para actualizar** instrucción para generar el conjunto de resultados.  
  
6.  Las llamadas **SQLFetch** o **SQLFetchScroll** una o varias veces para desplazarse por el conjunto de resultados.  
  
 La aplicación puede cambiar los valores de datos en los búferes de conjunto de filas. Para actualizar los búferes de conjunto de filas con los datos de caché de la biblioteca de cursores, una aplicación llama a **SQLFetchScroll** con el *FetchOrientation* establecido en SQL_FETCH_RELATIVE y  *FetchOffset* argumento establecido en 0.  
  
 Para recuperar datos de una columna independiente, la aplicación llama a **SQLSetPos** para colocar el cursor en la fila deseada. A continuación, llama **SQLGetData** para recuperar los datos.  
  
 Para determinar el número de filas que se han recuperado del origen de datos, la aplicación llama a **SQLRowCount**.
