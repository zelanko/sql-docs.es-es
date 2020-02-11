---
title: Compatibilidad de los cursores de bloque y desplazables con ODBC 3. x | Microsoft Docs
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
ms.openlocfilehash: 7d12906f8dec0bfb12fc861c067e6e615e758a3b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68134989"
---
# <a name="block-cursors-scrollable-cursors-and-backward-compatibility-for-odbc-3x-applications"></a>Cursores de bloque y los cursores desplazables, compatibilidad con versiones anteriores de las aplicaciones ODBC 3.x
La existencia de **SQLFetchScroll** y **SQLExtendedFetch** representa la primera división clara en ODBC entre la interfaz de programación de aplicaciones (API), que es el conjunto de funciones a las que llama la aplicación y la interfaz del proveedor de servicios (SPI), que es el conjunto de funciones que implementa el controlador. Esta división es necesaria para equilibrar el requisito en ODBC *3. x*, que utiliza **SQLFetchScroll**, para alinear con los estándares y ser compatible con ODBC *2. x*, que utiliza **SQLExtendedFetch**.  
  
 La API de ODBC *3. x* , que es el conjunto de funciones a las que llama la aplicación, incluye **SQLFetchScroll** y atributos de instrucción relacionados. El SPI de ODBC *3. x* , que es el conjunto de funciones que implementa el controlador, incluye **SQLFetchScroll**, **SQLExtendedFetch**y atributos de instrucción relacionados. Dado que ODBC no aplica formalmente esta división entre la API y el SPI, es posible que las aplicaciones de ODBC *3. x* llamen a **SQLExtendedFetch** y a los atributos de instrucción relacionados. Sin embargo, no hay ninguna razón para que las aplicaciones ODBC *3. x* lo hagan. Para obtener más información sobre las API y el SPI, consulte la introducción a la [arquitectura de ODBC](../../../odbc/reference/odbc-architecture.md).  
  
 Para obtener información acerca de cómo el administrador de controladores ODBC *3. x* asigna llamadas a los controladores ODBC *2. x* y ODBC *3. x* , y qué funciones y atributos de instrucción debe implementar un controlador ODBC *3. x* para los cursores de bloque y desplazable, vea [lo que hace el controlador en el](../../../odbc/reference/appendixes/what-the-driver-does.md) Apéndice G: instrucciones del controlador para la compatibilidad con versiones anteriores.  
  
 En la tabla siguiente se resumen las funciones y los atributos de instrucción que debe usar una aplicación ODBC *3. x* con cursores de bloque y desplazables. También se muestran los cambios entre ODBC *2. x* y ODBC *3. x* en esta área en que las aplicaciones ODBC *3. x* deben tener en cuenta que son compatibles con los controladores ODBC *2. x* .  
  
|Función o<br /><br /> atributo de instrucción|Comentarios|  
|-----------------------------------------|--------------|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|Apunta al marcador que se va a usar con **SQLFetchScroll**.<br /><br /> Cuando una aplicación lo establece en un controlador ODBC *2. x* , debe apuntar a un marcador de longitud fija.|  
|SQL_ATTR_ROW_STATUS_PTR|Apunta a la matriz de estado de fila rellena por **SQLFetch**, **SQLFetchScroll**, **SQLBulkOperations**y **SQLSetPos**.<br /><br /> Si una aplicación lo establece en un controlador ODBC *2. x* y llama **a SQLBulkOperation** con una *operación* de SQL_ADD antes de llamar a **SQLFetchScroll**, **SQLFetch**o **SQLExtendedFetch**, se devuelve el valor de SQLSTATE HY011 (el atributo no se puede establecer ahora).<br /><br /> Cuando una aplicación llama a **SQLFetch** en un controlador ODBC *2. x* , **SQLFetch** se asigna a **SQLExtendedFetch** y, por tanto, devuelve valores en esta matriz.|  
|SQL_ATTR_ROWS_FETCHED_PTR|Apunta al búfer en el que **SQLFetch** y **SQLFetchScroll** devuelven el número de filas recuperadas.<br /><br /> Cuando una aplicación llama a **SQLFetch** en un controlador ODBC *2. x* , se asigna **SQLFetch** a **SQLExtendedFetch** y, por tanto, se devuelve un valor en este búfer.|  
|SQL_ATTR_ROW_ARRAY_SIZE|Establece el tamaño del conjunto de filas.<br /><br /> Si una aplicación llama a **SQLBulkOperations** con una *operación* de SQL_ADD en un controlador ODBC *2. x* , se usará SQL_ROWSET_SIZE para la llamada, no SQL_ATTR_ROW_ARRAY_SIZE, porque la llamada está asignada a **SQLSetPos** con una *operación* de SQL_ADD, que usa SQL_ROWSET_SIZE.<br /><br /> La llamada a **SQLSetPos** con una *operación* de SQL_ADD o **SQLExtendedFetch** en un controlador ODBC *2. x* usa SQL_ROWSET_SIZE.<br /><br /> La llamada a **SQLFetch** o **SQLFetchScroll** en un controlador ODBC *2. x* usa SQL_ATTR_ROW_ARRAY_SIZE.|  
|**SQLBulkOperations**|Realiza operaciones de inserción y marcador. Cuando se llama a **SQLBulkOperations** con una *operación* de SQL_ADD en un controlador ODBC *2. x* , se asigna a **SQLSetPos** con una *operación* de SQL_ADD. Estos son los detalles de la implementación:<br /><br /> -Cuando se trabaja con un controlador ODBC *2. x* , una aplicación debe usar solo los ARD asignados implícitamente asociados a *StatementHandle*; no puede asignar otro ARD para agregar filas, ya que no se admiten las operaciones de descriptor explícitas en un controlador ODBC *2. x* . Una aplicación debe usar **SQLBindCol** para enlazar con ARD, no con **SQLSetDescField** o **SQLSetDescRec**.<br />-Cuando se llama a un controlador ODBC *3. x* , una aplicación puede llamar a **SQLBulkOperations** con una *operación* de SQL_ADD antes de llamar a **SQLFetch** o **SQLFetchScroll**. Cuando se llama a un controlador ODBC *2. x* , una aplicación debe llamar a **SQLFetchScroll** antes de llamar a **SQLBulkOperations** con una operación de SQL_ADD.|  
|**SQLFetch**|Devuelve el conjunto de filas siguiente. Estos son los detalles de la implementación:<br /><br /> -Cuando una aplicación llama a **SQLFetch** en un controlador ODBC *2. x* , se asigna a **SQLExtendedFetch**.<br />-Cuando una aplicación llama a **SQLFetch** en un controlador ODBC *3. x* , devuelve el número de filas especificado con el atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE.|  
|**SQLFetchScroll**|Devuelve el conjunto de filas especificado. Estos son los detalles de la implementación:<br /><br /> -Cuando una aplicación llama a **SQLFetchScroll** en un controlador ODBC *2. x* , devuelve SQLSTATE 01S01 (error en la fila) antes de cada error que se aplica a una sola fila. Esto solo lo hace porque el administrador de controladores ODBC *3. x* lo asigna a **SQLExtendedFetch** y **SQLExtendedFetch** devuelve este SQLSTATE. Cuando una aplicación llama a **SQLFetchScroll** en un controlador ODBC *3. x* , nunca devuelve SQLSTATE 01S01 (error en la fila).<br />-Cuando una aplicación llama a **SQLFetchScroll** en un controlador ODBC *2. x* con *FetchOrientation* establecido en SQL_FETCH_BOOKMARK, el argumento *FetchOffset* se debe establecer en 0. SQLSTATE HYC00 (característica opcional no implementada) se devuelve si se intenta obtener un marcador basado en desplazamiento con un controlador ODBC *2. x* .|  
  
> [!NOTE]  
>  Las aplicaciones ODBC *3. x* no deben usar **SQLExtendedFetch** ni el atributo de instrucción SQL_ROWSET_SIZE. En su lugar, deben usar **SQLFetchScroll** y el atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE. Las aplicaciones ODBC *3. x* no deben usar **SQLSetPos** con una *operación* de SQL_ADD pero deben usar **SQLBulkOperations** con una *operación* de SQL_ADD.
