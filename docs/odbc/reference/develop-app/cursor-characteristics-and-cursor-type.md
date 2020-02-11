---
title: Características de cursor y tipo de cursor | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e8803e7827102f564be63454b0387df938064d84
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68002055"
---
# <a name="cursor-characteristics-and-cursor-type"></a>Características del cursor y el tipo de Cursor
Una aplicación puede especificar las características de un cursor en lugar de especificar el tipo de cursor (solo avance, estático, controlado por conjunto de claves o dinámico). Para ello, la aplicación selecciona la posibilidad de desplazamiento del cursor (estableciendo el atributo de instrucción SQL_ATTR_CURSOR_SCROLLABLE) y la sensibilidad (estableciendo el atributo de instrucción SQL_ATTR_CURSOR_SENSITIVITY) antes de abrir el cursor en la instrucción. asa. Después, el controlador elige el tipo de cursor que proporciona más eficazmente las características que la aplicación solicitó.  
  
 Cada vez que una aplicación establece cualquiera de los atributos de instrucción SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_SCROLLABLE, SQL_ATTR_CURSOR_SENSITIVITY o SQL_ATTR_CURSOR_TYPE, el controlador realiza cualquier cambio necesario en los demás atributos de instrucción de este conjunto de cuatro atributos para que sus valores permanezcan coherentes. Como resultado, cuando la aplicación especifica una característica de cursor, el controlador puede cambiar el atributo que indica el tipo de cursor basado en esta selección implícita. Cuando la aplicación especifica un tipo, el controlador puede cambiar cualquiera de los demás atributos para que sea coherente con las características del tipo seleccionado. Para obtener más información sobre estos atributos de instrucción, vea la descripción de la función [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md) .  
  
 Una aplicación que establece atributos de instrucción para especificar un tipo de cursor y las características del cursor corre el riesgo de obtener un cursor que no sea el método más eficaz disponible en ese controlador que cumpla los requisitos de la aplicación.  
  
 La configuración implícita de los atributos de instrucción está definida por el controlador, pero debe seguir estas reglas:  
  
-   Los cursores de solo avance nunca se pueden desplazar; Consulte la definición de SQL_ATTR_CURSOR_SCROLLABLE en [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md).  
  
-   Los cursores insensitive nunca se pueden actualizar (y, por tanto, su simultaneidad es de solo lectura). Esto se basa en su definición de cursores insensitive en el estándar ISO SQL.  
  
 Por consiguiente, la configuración implícita de los atributos de instrucción se produce en los casos descritos en la tabla siguiente.  
  
|El atributo conjuntos de aplicaciones en|Otros atributos establecidos implícitamente|  
|-----------------------------------|-------------------------------------|  
|SQL_ATTR_CONCURRENCY a SQL_CONCUR_READ_ONLY|SQL_ATTR_CURSOR_SENSITIVITY que se va a SQL_INSENSITIVE.|  
|SQL_ATTR_CONCURRENCY a SQL_CONCUR_LOCK, SQL_CONCUR_ROWVER o SQL_CONCUR_VALUES|SQL_ATTR_CURSOR_SENSITIVITY a SQL_UNSPECIFIED o SQL_SENSITIVE, tal y como se define en el controlador. Nunca se puede establecer en SQL_INSENSITIVE, ya que los cursores insensitiven siempre son de solo lectura.|  
|SQL_ATTR_CURSOR_SCROLLABLE a SQL_NONSCROLLABLE|SQL_ATTR_CURSOR_TYPE a SQL_CURSOR_FORWARD_ONLY|  
|SQL_ATTR_CURSOR_SCROLLABLE a SQL_SCROLLABLE|SQL_ATTR_CURSOR_TYPE a SQL_CURSOR_STATIC, SQL_CURSOR_KEYSET_DRIVEN o SQL_CURSOR_DYNAMIC, según lo especificado por el controlador. Nunca se establece en SQL_CURSOR_FORWARD_ONLY.|  
|SQL_ATTR_CURSOR_SENSITIVITY a SQL_INSENSITIVE|SQL_ATTR_CONCURRENCY que se va a SQL_CONCUR_READ_ONLY.<br /><br /> SQL_ATTR_CURSOR_TYPE que se va a SQL_CURSOR_STATIC.|  
|SQL_ATTR_CURSOR_SENSITIVITY a SQL_SENSITIVE|SQL_ATTR_CONCURRENCY a SQL_CONCUR_LOCK, SQL_CONCUR_ROWVER o SQL_CONCUR_VALUES, según lo especificado por el controlador. Nunca se establece en SQL_CONCUR_READ_ONLY.<br /><br /> SQL_ATTR_CURSOR_TYPE a SQL_CURSOR_FORWARD_ONLY, SQL_CURSOR_STATIC, SQL_CURSOR_KEYSET_DRIVEN o SQL_CURSOR_DYNAMIC, tal y como especifica el controlador.|  
|SQL_ATTR_CURSOR_SENSITIVITY a SQL_UNSPECIFIED|SQL_ATTR_CONCURRENCY a SQL_CONCUR_READ_ONLY, SQL_CONCUR_LOCK, SQL_CONCUR_ROWVER o SQL_CONCUR_VALUES, tal y como especifica el controlador.<br /><br /> SQL_ATTR_CURSOR_TYPE a SQL_CURSOR_FORWARD_ONLY, SQL_CURSOR_STATIC, SQL_CURSOR_KEYSET_DRIVEN o SQL_CURSOR_DYNAMIC, tal y como especifica el controlador.|  
|SQL_ATTR_CURSOR_TYPE a SQL_CURSOR_DYNAMIC|SQL_ATTR_SCROLLABLE que se va a SQL_SCROLLABLE.<br /><br /> SQL_ATTR_CURSOR_SENSITIVITY que se va a SQL_SENSITIVE. (Pero solo si SQL_ATTR_CONCURRENCY no es igual a SQL_CONCUR_READ_ONLY. Los cursores dinámicos actualizables siempre son sensibles a los cambios realizados en su propia transacción).|  
|SQL_ATTR_CURSOR_TYPE a SQL_CURSOR_FORWARD_ONLY|SQL_ATTR_CURSOR_SCROLLABLE que se va a SQL_NONSCROLLABLE.|  
|SQL_ATTR_CURSOR_TYPE a SQL_CURSOR_KEYSET_DRIVEN|SQL_ATTR_SCROLLABLE que se va a SQL_SCROLLABLE.<br /><br /> SQL_ATTR_SENSITIVITY a SQL_UNSPECIFIED o SQL_SENSITIVE (según los criterios definidos por el controlador, si SQL_ATTR_CONCURRENCY no se SQL_CONCUR_READ_ONLY).|  
|SQL_ATTR_CURSOR_TYPE a SQL_CURSOR_STATIC|SQL_ATTR_SCROLLABLE que se va a SQL_SCROLLABLE.<br /><br /> SQL_ATTR_SENSITIVITY que se va a SQL_INSENSITIVE (si SQL_ATTR_CONCURRENCY es SQL_CONCUR_READ_ONLY).<br /><br /> SQL_ATTR_SENSITIVITY a SQL_UNSPECIFIED o SQL_SENSITIVE (si SQL_ATTR_CONCURRENCY no se SQL_CONCUR_READ_ONLY).|
