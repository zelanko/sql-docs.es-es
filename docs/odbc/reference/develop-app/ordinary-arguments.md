---
title: Argumentos normales | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- arguments in catalog functions [ODBC], ordinary
- catalog functions [ODBC], arguments
- ordinary arguments [ODBC]
ms.assetid: a18cdae1-6b85-41cb-875c-b5a01ec90aeb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 31d83b00fd70cd54587a19ebfea7310154167493
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62999281"
---
# <a name="ordinary-arguments"></a>Argumentos normales
Cuando un argumento de cadena de la función de catálogo es un argumento normal, se trata como una cadena literal. Un argumento normal acepta un patrón de búsqueda de cadena ni una lista de valores. El caso de un argumento normal es significativo, y los caracteres de comillas en la cadena se toman literalmente. Estos argumentos se tratan como argumentos normales, si se establece el atributo de instrucción SQL_ATTR_METADATA_ID en SQL_FALSE; se tratan como argumentos de identificador en su lugar, si este atributo está establecido en SQL_TRUE.  
  
 Si un argumento normal se establece en un puntero nulo y el argumento es un argumento necesario, la función devuelve SQL_ERROR y SQLSTATE HY009 (uso no válido del puntero nulo). Si un argumento normal se establece en un puntero nulo y el argumento no es un argumento necesario, comportamiento del argumento depende del controlador. Los argumentos necesarios se enumeran en la tabla siguiente.  
  
|Función|Argumentos necesarios|  
|--------------|------------------------|  
|**SQLColumnPrivileges**|*TableName*|  
|**SQLForeignKeys**|*PKTableName*, *FKTableName*|  
|**SQLPrimaryKeys**|*TableName*|  
|**SQLSpecialColumns**|*TableName*|  
|**SQLStatistics**|*TableName*|
