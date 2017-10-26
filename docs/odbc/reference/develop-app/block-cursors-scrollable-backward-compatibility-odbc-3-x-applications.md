---
title: Bloque y la compatibilidad con cursores desplazables ODBC 3.x | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- compatibility [ODBC], cursors
- backward compatibility [ODBC], cursors
- SQLExtendedFetch function [ODBC], block cursors
- cursors [ODBC], compatibility issues
- SQLFetchScroll function [ODBC], block cursors
ms.assetid: 82f6cf68-cfde-4417-9788-d6382ca14bf8
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 56543f0de0d95bad6fa85fc415dddd7da58f3667
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="block-cursors-scrollable-cursors-and-backward-compatibility-for-odbc-3x-applications"></a>Cursores de bloque y los cursores desplazables, compatibilidad con versiones anteriores de las aplicaciones ODBC 3.x
La existencia de ambos **SQLFetchScroll** y **SQLExtendedFetch** representa el primer clear divide en ODBC entre la aplicación de interfaz de programación (API), que es el conjunto de funciones de la las llamadas de la aplicación y la interfaz de proveedor de servicio (SPI), que es el conjunto de funciones el controlador implementa. Esta división es necesario para equilibrar el requisito en ODBC 3. *x*, que usa **SQLFetchScroll**, para alinear con los estándares y ser compatible con ODBC 2.* x*, que usa **SQLExtendedFetch**.  
  
 ODBC 3*.x* API, que es el conjunto de funciones de la aplicación llama, incluye **SQLFetchScroll** y relacionados con los atributos de instrucción. ODBC 3*.x* SPI, que es el conjunto de funciones implementa el controlador, incluye **SQLFetchScroll**, **SQLExtendedFetch**y relacionados con los atributos de instrucción. Dado que ODBC no exige formalmente esta división entre la API y el SPI, es posible que ODBC 3*.x* las aplicaciones llamen a **SQLExtendedFetch** y relacionados con los atributos de instrucción. Sin embargo, no hay ninguna razón para ODBC 3*.x* aplicaciones para hacer esto. Para obtener más información acerca de las API y el SPI, vea la introducción a [arquitectura ODBC](../../../odbc/reference/odbc-architecture.md).  
  
 Para obtener información acerca de cómo ODBC 3. *x* el Administrador de controladores asigna las llamadas a API ODBC 2.* x* y ODBC 3.* x* controladores y qué funciones y la declaración de atributos de una aplicación ODBC 3.* x* controlador debe implementar para bloqueo y los cursores desplazables, vea [lo que el controlador hace](../../../odbc/reference/appendixes/what-the-driver-does.md) en Apéndice G: controlador directrices para la compatibilidad con versiones anteriores.  
  
 En la tabla siguiente se resume las funciones y los atributos de instrucción una aplicación ODBC 3. *x* aplicación debe utilizar con los cursores desplazables y el bloque. También se muestran los cambios entre 2 de ODBC. *x* y ODBC 3.* x* en esta área que ODBC 3.* x* las aplicaciones deben tener en cuenta ser compatible con ODBC 2.* x* controladores.  
  
|Función o<br /><br /> atributo de instrucción|Comentarios|  
|-----------------------------------------|--------------|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|Señala el marcador que se va a usar con **SQLFetchScroll**.<br /><br /> Cuando una aplicación establece este en una API ODBC 2. *x* controlador, esto debe apuntar a un marcador de longitud fija.|  
|SQL_ATTR_ROW_STATUS_PTR|Apunta a la matriz de Estados de fila se rellena por **SQLFetch**, **SQLFetchScroll**, **SQLBulkOperations**, y **SQLSetPos**.<br /><br /> Si una aplicación establece este en una API ODBC 2. *x* controlador y llamadas **SQLBulkOperation** con una *operación* de SQL_ADD antes de llamar a **SQLFetchScroll**, ** SQLFetch**, o **SQLExtendedFetch**, SQLSTATE HY011 (atributo no se puede establecer ahora) se devuelve.<br /><br /> Cuando una aplicación llama **SQLFetch** en una API ODBC 2.* x* controlador, **SQLFetch** se asigna a **SQLExtendedFetch** y, por tanto, devuelve los valores de esta matriz.|  
|SQL_ATTR_ROWS_FETCHED_PTR|Señala al búfer en el que **SQLFetch** y **SQLFetchScroll** devuelve el número de filas recuperadas.<br /><br /> Cuando una aplicación llama **SQLFetch** en una API ODBC 2.* x* controlador, **SQLFetch** se asigna a **SQLExtendedFetch** y, por tanto, se devuelve un valor en este búfer.|  
|SQL_ATTR_ROW_ARRAY_SIZE|Establece el tamaño del conjunto de filas.<br /><br /> Si una aplicación llama **SQLBulkOperations** con una *operación* de SQL_ADD en una API ODBC 2.* x* porque la llamada está asignada a, se usará para la llamada, no SQL_ATTR_ROW_ARRAY_SIZE, controlador, SQL_ROWSET_SIZE **SQLSetPos** con una *operación* de SQL_ADD, que usa SQL_ROWSET_SIZE.<br /><br /> Al llamar a **SQLSetPos** con una *operación* de SQL_ADD o **SQLExtendedFetch** en un ODBC 2.* x* controlador utiliza SQL_ROWSET_SIZE.<br /><br /> Al llamar a **SQLFetch** o **SQLFetchScroll** en un ODBC 2.* x* controlador utiliza SQL_ATTR_ROW_ARRAY_SIZE.|  
|**SQLBulkOperations**|Realiza operaciones de inserción y de marcador. Cuando **SQLBulkOperations** con una *operación* de SQL_ADD se llama en una API ODBC 2.* x* controlador, se asigna a **SQLSetPos** con una *operación* de SQL_ADD. Éstos son los detalles de implementación:<br /><br /> -Cuando se trabaja con una API ODBC 2. *x* controlador, una aplicación debe utilizar solo el descartar implícitamente asignado asociado a la *StatementHandle*; no se puede asignar otro Descartar para agregar filas, ya que éstas descriptor explícita no se admite en una API ODBC 2. *x* controlador. Una aplicación debe usar **SQLBindCol** para enlazar a descartar, no **SQLSetDescField** o **SQLSetDescRec**.<br />-Cuando se llama a una aplicación ODBC 3. *x* controlador, una aplicación puede llamar a **SQLBulkOperations** con una *operación* de SQL_ADD antes de llamar a **SQLFetch** o **SQLFetchScroll**. Al llamar a una API ODBC 2. *x* controlador, una aplicación debe llamar a **SQLFetchScroll** antes de llamar a **SQLBulkOperations** con una operación de SQL_ADD.|  
|**SQLFetch**|Devuelve el siguiente conjunto de filas. Éstos son los detalles de implementación:<br /><br /> -Cuando una aplicación llama **SQLFetch** en una API ODBC 2.* x* controlador, se asigna a **SQLExtendedFetch**.<br />-Cuando una aplicación llama **SQLFetch** en una aplicación ODBC 3.* x* controlador, devuelve el número de filas especificado con el atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE.|  
|**SQLFetchScroll**|Devuelve el conjunto de filas especificado. Éstos son los detalles de implementación:<br /><br /> -Cuando una aplicación llama **SQLFetchScroll** en una API ODBC 2.* x* controlador, devuelve SQLSTATE 01S01 (Error en la fila) antes de cada error que se aplica a una sola fila. Ya que sólo ODBC 3*.x* el Administrador de controladores se asigna a **SQLExtendedFetch** y **SQLExtendedFetch** devuelve este valor de SQLSTATE. Cuando una aplicación llama **SQLFetchScroll** en una aplicación ODBC 3.* x* controlador, no devuelve nunca SQLSTATE 01S01 (Error en la fila).<br />-Cuando una aplicación llama **SQLFetchScroll** en una API ODBC 2.* x* controlador con *FetchOrientation* establecido en SQL_FETCH_BOOKMARK, el *FetchOffset* argumento debe establecerse en 0. SQLSTATE HYC00 (característica opcional no implementada) se devuelve si se intenta la obtención de marcador basado en el desplazamiento con una API ODBC 2. *x* controlador.|  
  
> [!NOTE]  
>  ODBC 3. *x* aplicaciones no deben utilizar **SQLExtendedFetch** o el atributo de instrucción SQL_ROWSET_SIZE. En su lugar, deben usar **SQLFetchScroll** y el atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE. ODBC 3. *x* aplicaciones no deben utilizar **SQLSetPos** con una *operación* de SQL_ADD sino que debe utilizar **SQLBulkOperations** con un *Operación* de SQL_ADD.

