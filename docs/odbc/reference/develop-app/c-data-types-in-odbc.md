---
title: Tipos de datos C en ODBC | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data types [ODBC], C data types
- C data types [ODBC], about C data types
- C data types [ODBC]
ms.assetid: c91bef31-3794-4736-966a-d50997b2233c
caps.latest.revision: "26"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 713b9448ecb70b57f0aace7f05aa9b977511323b
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="c-data-types-in-odbc"></a>Tipos de datos C en ODBC
ODBC define los tipos de datos de C que usan variables de aplicación y sus identificadores de tipo correspondiente. Se utilizan por los búferes que están enlazados a columnas del conjunto de resultados y parámetros de la instrucción. Por ejemplo, supongamos que desea que una aplicación recuperar datos de una columna de conjunto de resultados en formato de caracteres. Declara una variable con el SQLCHAR * tipo de datos y enlaza esta variable a la columna del conjunto de resultados con un identificador de tipo de SQL_C_CHAR. Para obtener una lista completa de tipos de datos de C y los identificadores de tipo, consulte [tipos de datos de apéndice D:](../../../odbc/reference/appendixes/appendix-d-data-types.md).  
  
 ODBC también define una asignación predeterminada de cada tipo de datos SQL a un tipo de datos de C. Por ejemplo, un entero de 2 bytes en el origen de datos se asigna a un entero de 2 bytes en la aplicación. Para usar la asignación predeterminada, una aplicación especifica el identificador de tipo SQL_C_DEFAULT. Sin embargo, el uso de este identificador se desaconseja por motivos de interoperabilidad.  
  
 Todos los tipos de datos entero C definidos en ODBC 1*.x* han sido firmadas. Se han agregado los tipos de datos de C sin signo y sus identificadores de tipo correspondiente en ODBC 2.0. Por este motivo, las aplicaciones y controladores necesitan tener especial cuidado cuando se trabaja con 1*.x* versiones.  
  
## <a name="c-data-type-extensibility"></a>Extensibilidad del tipo de datos c.  
 En ODBC 3.8, puede especificar tipos de datos C específicos del controlador. Esto le permite enlazar un tipo SQL como un tipo de C específicos del controlador en las aplicaciones ODBC cuando se llama a [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md), [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md), o [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md). Esto puede ser útil para admitir nuevos tipos de servidor, porque los tipos de datos C existentes podrían no representar correctamente los nuevos tipos de datos de servidor. Uso de tipos de C específicos del controlador puede aumentar el número de conversiones que pueden realizar los controladores.  
  
 Por ejemplo, suponga que un sistema de administración de bases de datos (DBMS) introdujo un nuevo tipo SQL, **DATETIMEOFFSET**, para representar la fecha y hora con información de zona horaria. No habría ningún tipo específico de C en ODBC que correspondía a **DATETIMEOFFSET**. Una aplicación podría tener que enlazar **DATETIMEOFFSET** como SQL_C_BINARY y conversión a una de datos definido por el usuario escriba. A partir de ODBC 3.8 con extensibilidad del tipo de datos de C, un controlador puede definir un nuevo tipo de C correspondiente. Por ejemplo, para el nuevo tipo SQL DATETIMEOFFSET, el controlador puede definir un nuevo tipo de C correspondiente como SQL_C_DATETIMEOFFSET. A continuación, una aplicación puede enlazar el nuevo tipo SQL como un tipo de C específicos del controlador.  
  
 Un tipo de datos de C se define en el controlador como sigue:  
  
-   El nivel de compatibilidad de ODBC para una aplicación, el controlador ODBC y el Administrador de controladores es 3.8 (o superior).  
  
-   El intervalo de datos de un tipo de C específicos del controlador está entre 0 x 4000 y 0x7FFF.  
  
-   El controlador define la estructura de los datos correspondientes al tipo de C.  Esto puede hacerse en el SDK específicos del controlador.  
  
 El Administrador de controladores no validará un tipo C definido en el intervalo de 0 x 4000 y 0x7FFF; el controlador llevará a cabo la validación y cualquier conversión de tipos de datos. Pero si el intervalo de datos de un tipo de C que se pasa al administrador de controladores es entre 0 x 0000 y 0x3FFF o entre 0 x 8000 y 0xFFFF, el Administrador de controladores validará el tipo de datos de C.  
  
> [!NOTE]  
>  Tipos de datos C específicos del controlador deben describirse en la documentación del controlador.  
  
 Para especificar un nivel de compatibilidad de ODBC de 3.8, llama a una aplicación [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md) con el SQL_ATTR_ODBC_VERSION atributo establecido en **SQL_OV_ODBC3_80**. Para determinar la versión del controlador, una aplicación llama **SQLGetInfo** con SQL_DRIVER_ODBC_VER.  
  
 Para obtener más información acerca de ODBC 3.8, consulte [What's New en ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md).  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos C](../../../odbc/reference/appendixes/c-data-types.md)
