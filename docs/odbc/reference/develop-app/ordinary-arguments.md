---
title: Argumentos normales | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- arguments in catalog functions [ODBC], ordinary
- catalog functions [ODBC], arguments
- ordinary arguments [ODBC]
ms.assetid: a18cdae1-6b85-41cb-875c-b5a01ec90aeb
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7ecdcf5e697bcf3235cadbe3d8f3f8f981406575
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="ordinary-arguments"></a>Argumentos normales
Cuando un argumento de cadena de la función de catálogo es un argumento normal, se trata como una cadena literal. Un argumento normal acepta un patrón de búsqueda de cadena ni una lista de valores. El caso de un argumento normal es significativo, y caracteres de comillas en la cadena se toman literalmente. Estos argumentos se tratan como argumentos normales, si se establece el atributo de instrucción de SQL_ATTR_METADATA_ID en SQL_FALSE; se tratan como argumentos de identificador en su lugar, si este atributo está establecido en SQL_TRUE.  
  
 Si se establece un argumento normal a un puntero null y el argumento es un argumento requerido, la función devuelve SQL_ERROR y SQLSTATE HY009 (uso no válido del puntero null). Si se establece un argumento normal a un puntero null y el argumento no es un argumento requerido, comportamiento del argumento depende del controlador. Los argumentos necesarios se enumeran en la tabla siguiente.  
  
|Función|Argumentos necesarios|  
|--------------|------------------------|  
|**SQLColumnPrivileges**|*TableName*|  
|**SQLForeignKeys**|*PKTableName*, *FKTableName*|  
|**SQLPrimaryKeys**|*TableName*|  
|**SQLSpecialColumns**|*TableName*|  
|**SQLStatistics**|*TableName*|
