---
title: Argumentos ordinarios ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 97362f93e91ccd8b592b4c05a0714b7602c1ba94
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282474"
---
# <a name="ordinary-arguments"></a>Argumentos normales
Cuando un argumento de cadena de función de catálogo es un argumento normal, se trata como una cadena literal. Un argumento ordinario no acepta ni un patrón de búsqueda de cadenas ni una lista de valores. El caso de un argumento ordinario es significativo y los caracteres de comillas de la cadena se toman literalmente. Estos argumentos se tratan como argumentos ordinarios si el atributo de instrucción SQL_ATTR_METADATA_ID se establece en SQL_FALSE; en su lugar, se tratan como argumentos de identificador si este atributo se establece en SQL_TRUE.  
  
 Si un argumento ordinario se establece en un puntero nulo y el argumento es un argumento obligatorio, la función devuelve SQL_ERROR y SQLSTATE HY009 (uso no válido del puntero nulo). Si un argumento ordinario se establece en un puntero nulo y el argumento no es un argumento necesario, el comportamiento del argumento depende del controlador. Los argumentos necesarios se enumeran en la tabla siguiente.  
  
|Función|Argumentos requeridos|  
|--------------|------------------------|  
|**SQLColumnPrivileges**|*TableName*|  
|**SQLForeignKeys**|*PKTableName*, *FKTableName*|  
|**SQLPrimaryKeys**|*TableName*|  
|**SQLSpecialColumns**|*TableName*|  
|**SQLStatistics**|*TableName*|
