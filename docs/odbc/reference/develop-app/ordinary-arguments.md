---
title: Argumentos normales | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- arguments in catalog functions [ODBC], ordinary
- catalog functions [ODBC], arguments
- ordinary arguments [ODBC]
ms.assetid: a18cdae1-6b85-41cb-875c-b5a01ec90aeb
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9aaaa374817d84eaa01dc96fa3783623e7b4b905
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="ordinary-arguments"></a>Argumentos normales
Cuando un argumento de cadena de la función de catálogo es un argumento normal, se trata como una cadena literal. Un argumento normal acepta un patrón de búsqueda de cadena ni una lista de valores. El caso de un argumento normal es significativo, y caracteres de comillas en la cadena se toman literalmente. Estos argumentos se tratan como argumentos normales, si se establece el atributo de instrucción de SQL_ATTR_METADATA_ID en SQL_FALSE; se tratan como argumentos de identificador en su lugar, si este atributo está establecido en SQL_TRUE.  
  
 Si se establece un argumento normal a un puntero null y el argumento es un argumento requerido, la función devuelve SQL_ERROR y SQLSTATE HY009 (uso no válido del puntero null). Si se establece un argumento normal a un puntero null y el argumento no es un argumento requerido, comportamiento del argumento depende del controlador. Los argumentos necesarios se enumeran en la tabla siguiente.  
  
|Función|Argumentos necesarios|  
|--------------|------------------------|  
|**SQLColumnPrivileges**|*Nombre de tabla*|  
|**SQLForeignKeys**|*PKTableName*, *FKTableName*|  
|**SQLPrimaryKeys**|*Nombre de tabla*|  
|**SQLSpecialColumns**|*Nombre de tabla*|  
|**SQLStatistics**|*Nombre de tabla*|

