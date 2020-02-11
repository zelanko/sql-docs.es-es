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
ms.openlocfilehash: 9fb35211160cb7cba866c2b1c9b1cf72340e92ce
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68132618"
---
# <a name="sqlcolattributes-visual-foxpro-odbc-driver"></a>SQLColAttributes (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general sobre esta función, vea el tema correspondiente en referencia de la [API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Compatibilidad: completa  
  
 Conformidad con la API de ODBC: nivel básico  
  
 Devuelve información del descriptor de una columna de un conjunto de resultados. La información del descriptor se devuelve como una cadena de caracteres, un valor dependiente del descriptor de 32 bits o un valor entero.  
  
> [!NOTE]  
>  No se puede usar **SQLColAttributes** para devolver información sobre la columna de marcador (columna 0).  
  
 El controlador ODBC de Visual FoxPro admite todos los valores de *fDescType* . En la tabla siguiente se incluyen comentarios sobre la implementación del controlador de valores seleccionados.  
  
|*fDescType*|Comentario|  
|-----------------|-------------|  
|SQL_COLUMN_AUTO_INCREMENT|Devuelve FALSE: Visual FoxPro no tiene campos de contador.|  
|SQL_COLUMN_CASE_SENSITIVE|Siempre devuelve TRUE si el tipo de columna es character.|  
|SQL_COLUMN_LABEL|Devuelve el nombre de columna, que también se devuelve mediante SQL_COLUMN_NAME.|  
|SQL_COLUMN_MONEY|Devuelve TRUE si el tipo de columna es Currency (representado por una "Y" en el lenguaje Visual FoxPro).|  
|SQL_COLUMN_OWNER_NAME|Siempre devuelve una cadena vacía.|  
|SQL_COLUMN_QUALIFIER_NAME|Siempre devuelve una cadena vacía.|  
|SQL_COLUMN_SEARCHABLE|Devuelve SQL_UNSEARCHABLE para las columnas de tipo general; estas columnas no se pueden usar en una cláusula WHERE.<br /><br /> Devuelve SQL_SEARCHABLE para las columnas de tipo character o Memo con NOCPTRANS no establecido; estas columnas se pueden usar en una cláusula WHERE con cualquier operador de comparación.<br /><br /> Devuelve SQL_ALL_EXCEPT_LIKE para todos los demás tipos de columna; estas columnas se pueden usar en una cláusula WHERE con todos los operadores de comparación excepto LIKE.|  
|SQL_COLUMN_TABLE_NAME|Siempre devuelve una cadena vacía.|  
  
 Para obtener más información, vea [SQLColAttributes](../../odbc/reference/syntax/sqlcolattributes-function.md) en la *Referencia del programador de ODBC*.
