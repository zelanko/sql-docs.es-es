---
title: SQLColAttributes (controlador ODBC de Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLColAttribute function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: d403dfa0-c26d-47d4-91d9-2f29aa387399
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e34929315d3a3548799bc605dbb8f3c4a2f665d0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47820064"
---
# <a name="sqlcolattributes-visual-foxpro-odbc-driver"></a>SQLColAttributes (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Soporte técnico: completo  
  
 Conformidad de la API de ODBC: Nivel básico  
  
 Devuelve información del descriptor para una columna de un conjunto de resultados. Información del descriptor se devuelve como una cadena de caracteres, un valor dependiente del descriptor de 32 bits o un valor entero.  
  
> [!NOTE]  
>  **SQLColAttributes** no se puede usar para devolver información acerca de la columna de marcador (columna 0).  
  
 Admite el controlador ODBC de Visual FoxPro todos *fDescType* valores. En la tabla siguiente incluye los comentarios sobre la implementación del controlador de valores seleccionados.  
  
|*fDescType*|Comentario|  
|-----------------|-------------|  
|SQL_COLUMN_AUTO_INCREMENT|Devuelve FALSE: Visual FoxPro no tiene ningún campo de contador.|  
|SQL_COLUMN_CASE_SENSITIVE|Siempre devuelve TRUE si el tipo de columna es de carácter.|  
|SQL_COLUMN_LABEL|Devuelve el nombre de columna, se devuelve también por SQL_COLUMN_NAME.|  
|SQL_COLUMN_MONEY|Devuelve TRUE si el tipo de columna es la moneda (representado por una "Y" en el lenguaje de Visual FoxPro).|  
|SQL_COLUMN_OWNER_NAME|Siempre devuelve una cadena vacía.|  
|SQL_COLUMN_QUALIFIER_NAME|Siempre devuelve una cadena vacía.|  
|SQL_COLUMN_SEARCHABLE|Devuelve SQL_UNSEARCHABLE para las columnas de tipo General; Estas columnas no se puede usar en una cláusula WHERE.<br /><br /> No establezca devuelve SQL_SEARCHABLE para las columnas de tipo carácter o memorando con NOCPTRANS; Estas columnas se pueden usar en una cláusula WHERE con cualquier operador de comparación.<br /><br /> Devuelve SQL_ALL_EXCEPT_LIKE para todos los demás tipos de columna; Estas columnas se pueden usar en una cláusula WHERE con todos los operadores de comparación excepto similares.|  
|SQL_COLUMN_TABLE_NAME|Siempre devuelve una cadena vacía.|  
  
 Para obtener más información, consulte [SQLColAttributes](../../odbc/reference/syntax/sqlcolattributes-function.md) en el *referencia del programador de ODBC*.
