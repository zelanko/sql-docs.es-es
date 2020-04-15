---
title: Compatibilidad de bloques y cursores desplazables para ODBC 3.x Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c526eff6e19014c923f05ad91551a7d7c66f5294
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306346"
---
# <a name="block-cursors-scrollable-cursors-and-backward-compatibility-for-odbc-3x-applications"></a>Cursores de bloque y los cursores desplazables, compatibilidad con versiones anteriores de las aplicaciones ODBC 3.x
La existencia de **SQLFetchScroll** y **SQLExtendedFetch** representa la primera división clara en ODBC entre la interfaz de programación de aplicaciones (API), que es el conjunto de funciones que llama la aplicación y la interfaz de proveedor de servicios (SPI), que es el conjunto de funciones que implementa el controlador. Esta división es necesaria para equilibrar el requisito de ODBC *3.x*, que utiliza **SQLFetchScroll**, para alinearse con los estándares y ser compatible con ODBC *2.x*, que utiliza **SQLExtendedFetch**.  
  
 La API ODBC *3.x,* que es el conjunto de funciones a las que llama la aplicación, incluye **SQLFetchScroll** y atributos de instrucción relacionados. El SPI de ODBC *3.x,* que es el conjunto de funciones que implementa el controlador, incluye **SQLFetchScroll**, **SQLExtendedFetch**y atributos de instrucción relacionados. Dado que ODBC no aplica formalmente esta división entre la API y el SPI, es posible que las aplicaciones ODBC *3.x* llamen a **SQLExtendedFetch** y atributos de instrucción relacionados. Sin embargo, no hay ninguna razón para que las aplicaciones ODBC *3.x* hagan esto. Para obtener más información acerca de las API y los SPI, vea la introducción a la [arquitectura ODBC](../../../odbc/reference/odbc-architecture.md).  
  
 Para obtener información acerca de cómo el Administrador de controladores ODBC *3.x* asigna llamadas a controladores ODBC *2.x* y ODBC *3.x,* y qué funciones y atributos de instrucción debe implementar un controlador ODBC *3.x* para cursores de bloque y desplazables, vea [Lo que hace el controlador](../../../odbc/reference/appendixes/what-the-driver-does.md) en el Apéndice G: Directrices de controlador para la compatibilidad con versiones anteriores.  
  
 En la tabla siguiente se resumen las funciones y atributos de instrucción que una aplicación ODBC *3.x* debe usar con cursores de bloque y desplazables. También enumera los cambios entre ODBC *2.x* y ODBC *3.x* en esta área que las aplicaciones ODBC *3.x* deben tener en cuenta para ser compatibles con controladores ODBC *2.x.*  
  
|Función o<br /><br /> atributo de instrucción|Comentarios|  
|-----------------------------------------|--------------|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|Apunta al marcador que se va a utilizar con **SQLFetchScroll**.<br /><br /> Cuando una aplicación establece esto en un controlador ODBC *2.x,* esto debe apuntar a un marcador de longitud fija.|  
|SQL_ATTR_ROW_STATUS_PTR|Apunta a la matriz de estado de fila rellenada por **SQLFetch**, **SQLFetchScroll**, **SQLBulkOperations**y **SQLSetPos**.<br /><br /> Si una aplicación establece esto en un controlador ODBC *2.x* y llama a **SQLBulkOperation** con una *operación* de SQL_ADD antes de llamar a **SQLFetchScroll**, **SQLFetch**o **SQLExtendedFetch**, SQLSTATE HY011 (atributo no se puede establecer ahora) se devuelve.<br /><br /> Cuando una aplicación llama a **SQLFetch** en un controlador ODBC *2.x,* **SQLFetch** se asigna a **SQLExtendedFetch** y, por lo tanto, devuelve valores en esta matriz.|  
|SQL_ATTR_ROWS_FETCHED_PTR|Apunta al búfer en el que **SQLFetch** y **SQLFetchScroll** devuelven el número de filas recuperadas.<br /><br /> Cuando una aplicación llama a **SQLFetch** en un controlador ODBC *2.x,* **SQLFetch** se asigna a **SQLExtendedFetch** y, por lo tanto, devuelve un valor en este búfer.|  
|SQL_ATTR_ROW_ARRAY_SIZE|Establece el tamaño del conjunto de filas.<br /><br /> Si una aplicación llama a **SQLBulkOperations** con una *operación* de SQL_ADD en un controlador ODBC *2.x,* se usará SQL_ROWSET_SIZE para la llamada, no SQL_ATTR_ROW_ARRAY_SIZE, porque la llamada se asigna a **SQLSetPos** con una *operación* de SQL_ADD, que usa SQL_ROWSET_SIZE.<br /><br /> Llamar a **SQLSetPos** con una *operación* de SQL_ADD o **SQLExtendedFetch** en un controlador ODBC *2.x* usa SQL_ROWSET_SIZE.<br /><br /> Llamar a **SQLFetch** o **SQLFetchScroll** en un controlador ODBC *2.x* usa SQL_ATTR_ROW_ARRAY_SIZE.|  
|**SQLBulkOperations**|Realiza operaciones de inserción y marcador. Cuando **SQLBulkOperations** con una *operación* de SQL_ADD se llama en un controlador ODBC *2.x,* se asigna a **SQLSetPos** con una *operación* de SQL_ADD. Los siguientes son detalles de implementación:<br /><br /> - Cuando se trabaja con un controlador ODBC *2.x,* una aplicación debe utilizar solo el ARD asignado implícitamente asociado con el *StatementHandle*; no puede asignar otro ARD para agregar filas, porque las operaciones de descriptor explícito no se admiten en un controlador ODBC *2.x.* Una aplicación debe usar **SQLBindCol** para enlazar a la ARD, no **SQLSetDescField** o **SQLSetDescRec**.<br />- Al llamar a un controlador ODBC *3.x,* una aplicación puede llamar a **SQLBulkOperations** con una *operación* de SQL_ADD antes de llamar a **SQLFetch** o **SQLFetchScroll**. Al llamar a un controlador ODBC *2.x,* una aplicación debe llamar a **SQLFetchScroll** antes de llamar a **SQLBulkOperations** con una operación de SQL_ADD.|  
|**SQLFetch**|Devuelve el siguiente conjunto de filas. Los siguientes son detalles de implementación:<br /><br /> - Cuando una aplicación llama a **SQLFetch** en un controlador ODBC *2.x,* se asigna a **SQLExtendedFetch**.<br />- Cuando una aplicación llama a **SQLFetch** en un controlador ODBC *3.x,* devuelve el número de filas especificadas con el atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE.|  
|**SQLFetchScroll**|Devuelve el conjunto de filas especificado. Los siguientes son detalles de implementación:<br /><br /> - Cuando una aplicación llama a **SQLFetchScroll** en un controlador ODBC *2.x,* devuelve SQLSTATE 01S01 (Error en fila) antes de cada error que se aplica a una sola fila. Lo hace solo porque el Administrador de controladores ODBC *3.x* asigna esto a **SQLExtendedFetch** y **SQLExtendedFetch** devuelve este SQLSTATE. Cuando una aplicación llama a **SQLFetchScroll** en un controlador ODBC *3.x,* nunca devuelve SQLSTATE 01S01 (Error en la fila).<br />- Cuando una aplicación llama a **SQLFetchScroll** en un controlador ODBC *2.x* con *FetchOrientation* establecido en SQL_FETCH_BOOKMARK, el *FetchOffset* argumento debe establecerse en 0. SQLSTATE HYC00 (característica opcional no implementada) se devuelve si se intenta la obtención de marcadores basada en desplazamiento con un controlador ODBC *2.x.*|  
  
> [!NOTE]  
>  Las aplicaciones ODBC *3.x* no deben usar **SQLExtendedFetch** ni el atributo de instrucción SQL_ROWSET_SIZE. En su lugar, deben usar **SQLFetchScroll** y el atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE. Las aplicaciones ODBC *3.x* no deben usar **SQLSetPos** con una *operación* de SQL_ADD pero deben usar **SQLBulkOperations** con una *operación* de SQL_ADD.
