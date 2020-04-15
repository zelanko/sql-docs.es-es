---
title: Características del cursor y tipo de cursor ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
- cursors [ODBC], creating
ms.assetid: 6f67edd2-ae71-4ca0-9b2d-abf4c20dc17b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8354fdabf6830780ec2d128492c86cc1edd582ac
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301632"
---
# <a name="cursor-characteristics-and-cursor-type"></a>Características del cursor y el tipo de Cursor
Una aplicación puede especificar las características de un cursor en lugar de especificar el tipo de cursor (solo hacia delante, estático, controlado por conjunto de claves o dinámico). Para ello, la aplicación selecciona la capacidad de desplazamiento del cursor (estableciendo el atributo de instrucción SQL_ATTR_CURSOR_SCROLLABLE) y la sensibilidad (estableciendo el atributo de instrucción SQL_ATTR_CURSOR_SENSITIVITY) antes de abrir el cursor en el identificador de instrucción. A continuación, el controlador elige el tipo de cursor que proporciona de forma más eficaz las características que solicitó la aplicación.  
  
 Cada vez que una aplicación establece cualquiera de los atributos de instrucción SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_SCROLLABLE, SQL_ATTR_CURSOR_SENSITIVITY o SQL_ATTR_CURSOR_TYPE, el controlador realiza cualquier cambio necesario en los demás atributos de instrucción de este conjunto de cuatro atributos para que sus valores sigan siendo coherentes. Como resultado, cuando la aplicación especifica una característica de cursor, el controlador puede cambiar el atributo que indica el tipo de cursor basado en esta selección implícita; cuando la aplicación especifica un tipo, el controlador puede cambiar cualquiera de los demás atributos para que sean coherentes con las características del tipo seleccionado. Para obtener más información acerca de estos atributos de instrucción, vea la descripción de la función [SQLSetStmtAttr.](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)  
  
 Una aplicación que establece atributos de instrucción para especificar un tipo de cursor y características de cursor corre el riesgo de obtener un cursor que no es el método más eficaz disponible en ese controlador de cumplir los requisitos de la aplicación.  
  
 La configuración implícita de los atributos de instrucción está definida por el controlador, excepto que debe seguir estas reglas:  
  
-   Los cursores de solo avance nunca se pueden desplazar; vea la definición de SQL_ATTR_CURSOR_SCROLLABLE en [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md).  
  
-   Los cursores insensibles nunca son actualizables (y, por lo tanto, su simultaneidad es de solo lectura); esto se basa en su definición de cursores insensibles en el estándar ISO SQL.  
  
 Por consiguiente, la configuración implícita de los atributos de instrucción se produce en los casos descritos en la tabla siguiente.  
  
|Atributo de conjuntos de aplicaciones a|Otros atributos establecidos implícitamente|  
|-----------------------------------|-------------------------------------|  
|SQL_ATTR_CONCURRENCY a SQL_CONCUR_READ_ONLY|SQL_ATTR_CURSOR_SENSITIVITY a SQL_INSENSITIVE.|  
|SQL_ATTR_CONCURRENCY a SQL_CONCUR_LOCK, SQL_CONCUR_ROWVER o SQL_CONCUR_VALUES|SQL_ATTR_CURSOR_SENSITIVITY a SQL_UNSPECIFIED o SQL_SENSITIVE, según lo definido por el controlador. Nunca se puede establecer en SQL_INSENSITIVE, porque los cursores insensibles siempre son de solo lectura.|  
|SQL_ATTR_CURSOR_SCROLLABLE a SQL_NONSCROLLABLE|SQL_ATTR_CURSOR_TYPE a SQL_CURSOR_FORWARD_ONLY|  
|SQL_ATTR_CURSOR_SCROLLABLE a SQL_SCROLLABLE|SQL_ATTR_CURSOR_TYPE a SQL_CURSOR_STATIC, SQL_CURSOR_KEYSET_DRIVEN o SQL_CURSOR_DYNAMIC, según lo especificado por el controlador. Nunca se establece en SQL_CURSOR_FORWARD_ONLY.|  
|SQL_ATTR_CURSOR_SENSITIVITY a SQL_INSENSITIVE|SQL_ATTR_CONCURRENCY a SQL_CONCUR_READ_ONLY.<br /><br /> SQL_ATTR_CURSOR_TYPE a SQL_CURSOR_STATIC.|  
|SQL_ATTR_CURSOR_SENSITIVITY a SQL_SENSITIVE|SQL_ATTR_CONCURRENCY a SQL_CONCUR_LOCK, SQL_CONCUR_ROWVER o SQL_CONCUR_VALUES, según lo especificado por el controlador. Nunca está configurado para SQL_CONCUR_READ_ONLY.<br /><br /> SQL_ATTR_CURSOR_TYPE SQL_CURSOR_FORWARD_ONLY, SQL_CURSOR_STATIC, SQL_CURSOR_KEYSET_DRIVEN o SQL_CURSOR_DYNAMIC, según lo especificado por el controlador.|  
|SQL_ATTR_CURSOR_SENSITIVITY a SQL_UNSPECIFIED|SQL_ATTR_CONCURRENCY SQL_CONCUR_READ_ONLY, SQL_CONCUR_LOCK, SQL_CONCUR_ROWVER u SQL_CONCUR_VALUES, según lo especificado por el controlador.<br /><br /> SQL_ATTR_CURSOR_TYPE SQL_CURSOR_FORWARD_ONLY, SQL_CURSOR_STATIC, SQL_CURSOR_KEYSET_DRIVEN o SQL_CURSOR_DYNAMIC, según lo especificado por el controlador.|  
|SQL_ATTR_CURSOR_TYPE a SQL_CURSOR_DYNAMIC|SQL_ATTR_SCROLLABLE a SQL_SCROLLABLE.<br /><br /> SQL_ATTR_CURSOR_SENSITIVITY a SQL_SENSITIVE. (Pero sólo si SQL_ATTR_CONCURRENCY no es igual a SQL_CONCUR_READ_ONLY. Los cursores dinámicos actualizables siempre son sensibles a los cambios realizados en su propia transacción.)|  
|SQL_ATTR_CURSOR_TYPE a SQL_CURSOR_FORWARD_ONLY|SQL_ATTR_CURSOR_SCROLLABLE a SQL_NONSCROLLABLE.|  
|SQL_ATTR_CURSOR_TYPE a SQL_CURSOR_KEYSET_DRIVEN|SQL_ATTR_SCROLLABLE a SQL_SCROLLABLE.<br /><br /> SQL_ATTR_SENSITIVITY a SQL_UNSPECIFIED o SQL_SENSITIVE (según criterios definidos por el conductor, si no se SQL_CONCUR_READ_ONLY SQL_ATTR_CONCURRENCY).|  
|SQL_ATTR_CURSOR_TYPE a SQL_CURSOR_STATIC|SQL_ATTR_SCROLLABLE a SQL_SCROLLABLE.<br /><br /> SQL_ATTR_SENSITIVITY a SQL_INSENSITIVE (si SQL_ATTR_CONCURRENCY es SQL_CONCUR_READ_ONLY).<br /><br /> SQL_ATTR_SENSITIVITY a SQL_UNSPECIFIED o SQL_SENSITIVE (si no se SQL_CONCUR_READ_ONLY SQL_ATTR_CONCURRENCY).|
