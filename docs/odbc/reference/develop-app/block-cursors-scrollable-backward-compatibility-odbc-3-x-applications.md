---
title: Bloque y la compatibilidad de los cursores desplazables para ODBC 3.x | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], cursors
- backward compatibility [ODBC], cursors
- SQLExtendedFetch function [ODBC], block cursors
- cursors [ODBC], compatibility issues
- SQLFetchScroll function [ODBC], block cursors
ms.assetid: 82f6cf68-cfde-4417-9788-d6382ca14bf8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b0bc45169a3c5eee2e23f581a66d5232c22e89b0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63199261"
---
# <a name="block-cursors-scrollable-cursors-and-backward-compatibility-for-odbc-3x-applications"></a>Cursores de bloque y los cursores desplazables, compatibilidad con versiones anteriores de las aplicaciones ODBC 3.x
La existencia de ambas **SQLFetchScroll** y **SQLExtendedFetch** representa divide entre la aplicación de interfaz de programación (API), que es el conjunto de funciones ODBC sin cifrar primero el las llamadas de aplicación y la interfaz de proveedor de servicio (SPI), que es el conjunto de funciones implementa el controlador. Esta división es necesario para equilibrar el requisito en ODBC 3. *x*, que usa **SQLFetchScroll**para alinearse con los estándares y ser compatible con ODBC 2. *x*, que usa **SQLExtendedFetch**.  
  
 El 3 de ODBC *.x* API, que es el conjunto de funciones de la aplicación llama, incluye **SQLFetchScroll** y relacionados con los atributos de instrucción. El 3 de ODBC *.x* SPI, que es el conjunto de funciones implementa el controlador, incluye **SQLFetchScroll**, **SQLExtendedFetch**y relacionados con los atributos de instrucción. Dado que ODBC no aplica esta diferencia entre la API y el SPI formalmente, es posible que ODBC 3 *.x* las aplicaciones llamen a **SQLExtendedFetch** y relacionados con los atributos de instrucción. Sin embargo, no hay ninguna razón para ODBC 3 *.x* aplicaciones para hacer esto. Para obtener más información acerca de las API y SPI, vea la introducción a [arquitectura ODBC](../../../odbc/reference/odbc-architecture.md).  
  
 Para obtener información acerca de cómo el ODBC 3. *x* Driver Manager asigna las llamadas a ODBC 2. *x* y ODBC 3. *x* controladores y qué funciones y la declaración de atributos de una aplicación ODBC 3. *x* controlador debe implementar para los cursores desplazables y de bloque, vea [lo que el controlador hace](../../../odbc/reference/appendixes/what-the-driver-does.md) en Apéndice G: Directrices de controlador para la compatibilidad con versiones anteriores.  
  
 En la tabla siguiente se resume las funciones y atributos de instrucción de una aplicación ODBC 3. *x* aplicación debe usar con los cursores desplazables y de bloque. También se muestran los cambios entre el 2 de ODBC. *x* y ODBC 3. *x* en esta área que ODBC 3. *x* deben ser conscientes de las aplicaciones que sean compatibles con ODBC 2. *x* controladores.  
  
|Función o<br /><br /> atributo de instrucción|Comentarios|  
|-----------------------------------------|--------------|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|Señala a usar con el marcador **SQLFetchScroll**.<br /><br /> Cuando una aplicación establece esto en un ODBC 2. *x* controlador, esto debe apuntar a un marcador de longitud fija.|  
|SQL_ATTR_ROW_STATUS_PTR|Apunta a la matriz de Estados de fila se rellena mediante **SQLFetch**, **SQLFetchScroll**, **SQLBulkOperations**, y **SQLSetPos**.<br /><br /> Si una aplicación establece esto en un ODBC 2. *x* controladores y llama a **SQLBulkOperation** con un *operación* de SQL_ADD antes de llamar a **SQLFetchScroll**,  **SQLFetch**, o **SQLExtendedFetch**, SQLSTATE HY011 (atributo no se puede establecer ahora) se devuelve.<br /><br /> Cuando una aplicación llama **SQLFetch** en un ODBC 2. *x* controlador, **SQLFetch** se asigna a **SQLExtendedFetch** y, por tanto, devuelve los valores de esta matriz.|  
|SQL_ATTR_ROWS_FETCHED_PTR|Apunta al búfer en el que **SQLFetch** y **SQLFetchScroll** devuelve el número de filas recuperadas.<br /><br /> Cuando una aplicación llama **SQLFetch** en un ODBC 2. *x* controlador, **SQLFetch** se asigna a **SQLExtendedFetch** y, por tanto, se devuelve un valor de este búfer.|  
|SQL_ATTR_ROW_ARRAY_SIZE|Establece el tamaño del conjunto de filas.<br /><br /> Si una aplicación llama a **SQLBulkOperations** con un *operación* de SQL_ADD en un ODBC 2. *x* porque la llamada está asignada a, se usará para la llamada, no SQL_ATTR_ROW_ARRAY_SIZE, controlador, SQL_ROWSET_SIZE **SQLSetPos** con un *operación* de SQL_ADD, que usa SQL_ROWSET_SIZE.<br /><br /> Una llamada a **SQLSetPos** con un *operación* de SQL_ADD o **SQLExtendedFetch** en un ODBC 2. *x* controlador utiliza SQL_ROWSET_SIZE.<br /><br /> Una llamada a **SQLFetch** o **SQLFetchScroll** en un ODBC 2. *x* controlador utiliza SQL_ATTR_ROW_ARRAY_SIZE.|  
|**SQLBulkOperations**|Realiza operaciones insert y el marcador. Cuando **SQLBulkOperations** con un *operación* de SQL_ADD se llama en un ODBC 2. *x* controlador, se asigna a **SQLSetPos** con un *operación* de SQL_ADD. Estos son los detalles de implementación:<br /><br /> -Cuando se trabaja con un ODBC 2. *x* controlador, una aplicación debe usar sólo la descartar implícitamente asignado asociado con el *StatementHandle*; no se puede asignar otro Descartar para agregar filas, ya que éstas descriptor explícita no se admite en un ODBC 2. *x* controlador. Una aplicación debe usar **SQLBindCol** para enlazar con el descartar, no **SQLSetDescField** o **SQLSetDescRec**.<br />-Cuando se llama a una aplicación ODBC 3. *x* controlador, puede llamar una aplicación **SQLBulkOperations** con un *operación* de SQL_ADD antes de llamar a **SQLFetch** o **SQLFetchScroll**. Al llamar a una API ODBC 2. *x* controlador, debe llamar una aplicación **SQLFetchScroll** antes de llamar a **SQLBulkOperations** con una operación de SQL_ADD.|  
|**SQLFetch**|Devuelve el siguiente conjunto de filas. Estos son los detalles de implementación:<br /><br /> -Cuando una aplicación llama a **SQLFetch** en un ODBC 2. *x* controlador, se asigna a **SQLExtendedFetch**.<br />-Cuando una aplicación llama a **SQLFetch** en una aplicación ODBC 3. *x* controlador, devuelve el número de filas especificado con el atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE.|  
|**SQLFetchScroll**|Devuelve el conjunto de filas especificado. Estos son los detalles de implementación:<br /><br /> -Cuando una aplicación llama a **SQLFetchScroll** en un ODBC 2. *x* controlador, devuelve SQLSTATE 01S01 (Error en la fila) antes de cada error que se aplica a una sola fila. Ya que solo el 3 de ODBC *.x* Administrador de controladores lo asigna a **SQLExtendedFetch** y **SQLExtendedFetch** devuelve este valor de SQLSTATE. Cuando una aplicación llama **SQLFetchScroll** en una aplicación ODBC 3. *x* controlador, nunca devuelve SQLSTATE 01S01 (Error en la fila).<br />-Cuando una aplicación llama a **SQLFetchScroll** en un ODBC 2. *x* controlador con *FetchOrientation* establecido en SQL_FETCH_BOOKMARK, el *FetchOffset* argumento debe establecerse en 0. SQLSTATE HYC00 (característica opcional no implementada) se devuelve si se intenta la capturar marcador basado en el desplazamiento con una API ODBC 2. *x* controlador.|  
  
> [!NOTE]  
>  ODBC 3. *x* las aplicaciones no deben usar **SQLExtendedFetch** o el atributo de instrucción SQL_ROWSET_SIZE. En su lugar, deben usar **SQLFetchScroll** y el atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE. ODBC 3. *x* las aplicaciones no deben usar **SQLSetPos** con un *operación* de SQL_ADD, pero debe usar **SQLBulkOperations** con un *Operación* de SQL_ADD.
