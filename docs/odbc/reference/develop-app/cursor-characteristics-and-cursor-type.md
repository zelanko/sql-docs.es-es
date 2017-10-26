---
title: "Características del cursor y el tipo de Cursor | Documentos de Microsoft"
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
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
- cursors [ODBC], creating
ms.assetid: 6f67edd2-ae71-4ca0-9b2d-abf4c20dc17b
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 19a9e44523e1dc550b593bc83589177c03d8a842
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="cursor-characteristics-and-cursor-type"></a>Características del cursor y el tipo de Cursor
Una aplicación puede especificar las características de un cursor en lugar de especificar el tipo de cursor (solo avance, estático, controlado por conjunto de claves o dinámico). Para ello, la aplicación selecciona desplazamiento del cursor (estableciendo el atributo de instrucción SQL_ATTR_CURSOR_SCROLLABLE) y sensibilidad (estableciendo el atributo de instrucción SQL_ATTR_CURSOR_SENSITIVITY) antes de abrir el cursor en la instrucción identificador. El controlador, a continuación, elige al tipo de cursor que proporciona más eficazmente las características de la aplicación solicitada.  
  
 Siempre que una aplicación establece cualquiera de los atributos de instrucción SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_SCROLLABLE, SQL_ATTR_CURSOR_SENSITIVITY o SQL_ATTR_CURSOR_TYPE, el controlador realiza cualquier cambio necesario para los demás atributos de instrucción en este conjunto de cuatro atributos para que sus valores siguen siendo coherentes. Como resultado, cuando la aplicación especifica una característica de cursor, el controlador puede cambiar el atributo que indica el tipo de cursor basado en esta selección implícita; Cuando la aplicación especifica un tipo, el controlador puede cambiar cualquiera de los otros atributos para que sea coherente con las características del tipo seleccionado. Para obtener más información acerca de estos atributos de instrucción, consulte la [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md) descripción de la función.  
  
 Una aplicación que establece atributos de instrucción para especificar un tipo de cursor y las características del cursor, corre el riesgo de obtener un cursor que no es el método más eficaz disponible en ese controlador de satisfacer los requisitos de la aplicación.  
  
 La configuración implícita de los atributos de instrucción está definido por el controlador salvo que deben seguir estas reglas:  
  
-   Los cursores de solo avance nunca son desplazables; ver la definición de SQL_ATTR_CURSOR_SCROLLABLE en [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md).  
  
-   Los cursores de minúsculas nunca son actualizables (y, por tanto, su simultaneidad es de solo lectura); Esto se basa en su definición de los cursores de minúsculas en el estándar ISO SQL.  
  
 Por lo tanto, la configuración de atributos de instrucción implícita se produce en los casos descritos en la tabla siguiente.  
  
|Atributo de conjuntos de aplicaciones para|Otros atributos se establecen implícitamente|  
|-----------------------------------|-------------------------------------|  
|SQL_ATTR_CONCURRENCY en SQL_CONCUR_READ_ONLY|SQL_ATTR_CURSOR_SENSITIVITY en SQL_INSENSITIVE.|  
|SQL_ATTR_CONCURRENCY SQL_CONCUR_LOCK, SQL_CONCUR_ROWVER o SQL_CONCUR_VALUES|SQL_ATTR_CURSOR_SENSITIVITY como SQL_UNSPECIFIED o SQL_SENSITIVE, tal como se define por el controlador. Nunca se pueden establecer en SQL_INSENSITIVE, porque los cursores siempre son de solo lectura.|  
|SQL_ATTR_CURSOR_SCROLLABLE en SQL_NONSCROLLABLE|SQL_ATTR_CURSOR_TYPE a SQL_CURSOR_FORWARD_ONLY|  
|SQL_ATTR_CURSOR_SCROLLABLE como SQL_SCROLLABLE|SQL_ATTR_CURSOR_TYPE SQL_CURSOR_STATIC, SQL_CURSOR_KEYSET_DRIVEN o SQL_CURSOR_DYNAMIC, según lo especificado por el controlador. Nunca se establece en SQL_CURSOR_FORWARD_ONLY.|  
|SQL_ATTR_CURSOR_SENSITIVITY en SQL_INSENSITIVE|SQL_ATTR_CONCURRENCY en SQL_CONCUR_READ_ONLY.<br /><br /> SQL_ATTR_CURSOR_TYPE a SQL_CURSOR_STATIC.|  
|SQL_ATTR_CURSOR_SENSITIVITY como SQL_SENSITIVE|SQL_ATTR_CONCURRENCY SQL_CONCUR_LOCK, SQL_CONCUR_ROWVER o SQL_CONCUR_VALUES, según lo especificado por el controlador. Nunca se establece en SQL_CONCUR_READ_ONLY.<br /><br /> SQL_ATTR_CURSOR_TYPE SQL_CURSOR_FORWARD_ONLY, SQL_CURSOR_STATIC, SQL_CURSOR_KEYSET_DRIVEN o SQL_CURSOR_DYNAMIC, según lo especificado por el controlador.|  
|SQL_ATTR_CURSOR_SENSITIVITY a SQL_UNSPECIFIED|SQL_ATTR_CONCURRENCY en SQL_CONCUR_READ_ONLY, SQL_CONCUR_LOCK, SQL_CONCUR_ROWVER o SQL_CONCUR_VALUES, según lo especificado por el controlador.<br /><br /> SQL_ATTR_CURSOR_TYPE SQL_CURSOR_FORWARD_ONLY, SQL_CURSOR_STATIC, SQL_CURSOR_KEYSET_DRIVEN o SQL_CURSOR_DYNAMIC, según lo especificado por el controlador.|  
|SQL_ATTR_CURSOR_TYPE a SQL_CURSOR_DYNAMIC|SQL_ATTR_SCROLLABLE en SQL_SCROLLABLE.<br /><br /> SQL_ATTR_CURSOR_SENSITIVITY como SQL_SENSITIVE. (Pero solo si no es igual a SQL_CONCUR_READ_ONLY SQL_ATTR_CONCURRENCY. Los cursores dinámicos actualizables siempre son sensibles a los cambios realizados en su propia transacción.)|  
|SQL_ATTR_CURSOR_TYPE a SQL_CURSOR_FORWARD_ONLY|SQL_ATTR_CURSOR_SCROLLABLE en SQL_NONSCROLLABLE.|  
|SQL_ATTR_CURSOR_TYPE a SQL_CURSOR_KEYSET_DRIVEN|SQL_ATTR_SCROLLABLE en SQL_SCROLLABLE.<br /><br /> SQL_ATTR_SENSITIVITY SQL_UNSPECIFIED o SQL_SENSITIVE (criterios definidos por el controlador, si no se encuentra SQL_ATTR_CONCURRENCY SQL_CONCUR_READ_ONLY).|  
|SQL_ATTR_CURSOR_TYPE a SQL_CURSOR_STATIC|SQL_ATTR_SCROLLABLE en SQL_SCROLLABLE.<br /><br /> SQL_ATTR_SENSITIVITY en SQL_INSENSITIVE (si SQL_ATTR_CONCURRENCY es SQL_CONCUR_READ_ONLY).<br /><br /> SQL_ATTR_SENSITIVITY SQL_UNSPECIFIED o SQL_SENSITIVE (si SQL_ATTR_CONCURRENCY no es SQL_CONCUR_READ_ONLY).|

