---
title: Tipos de datos de C en ODBC ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], C data types
- C data types [ODBC], about C data types
- C data types [ODBC]
ms.assetid: c91bef31-3794-4736-966a-d50997b2233c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5e1efba2187e2c1f2d813d43640fc9259ad4f2b3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306300"
---
# <a name="c-data-types-in-odbc"></a>Tipos de datos C en ODBC
ODBC define los tipos de datos de C que usan las variables de aplicación y sus identificadores de tipo correspondientes. Estos son utilizados por los búferes que están enlazados a columnas de conjunto de resultados y parámetros de instrucción. Por ejemplo, supongamos que una aplicación desea recuperar datos de una columna de conjunto de resultados en formato de carácter. Declara una variable con el tipo de datos SQLCHAR * y enlaza esta variable a la columna del conjunto de resultados con un identificador de tipo de SQL_C_CHAR. Para obtener una lista completa de los tipos de datos de C y los identificadores de tipo, vea [Apéndice D: Tipos](../../../odbc/reference/appendixes/appendix-d-data-types.md)de datos .  
  
 ODBC también define una asignación predeterminada de cada tipo de datos SQL a un tipo de datos C. Por ejemplo, un entero de 2 bytes en el origen de datos se asigna a un entero de 2 bytes en la aplicación. Para usar la asignación predeterminada, una aplicación especifica el identificador de tipo SQL_C_DEFAULT. Sin embargo, se desaconseja el uso de este identificador por razones de interoperabilidad.  
  
 Se firmaron todos los tipos de datos enteros de C definidos en ODBC *1.x.* Los tipos de datos C sin firmar y sus identificadores de tipo correspondientes se agregaron en ODBC 2.0. Debido a esto, las aplicaciones y los controladores deben tener especial cuidado al tratar con versiones *1.x.*  
  
## <a name="c-data-type-extensibility"></a>C Extensibilidad del tipo de datos  
 En ODBC 3.8, puede especificar tipos de datos C específicos del controlador. Esto permite enlazar un tipo SQL como un tipo C específico del controlador en aplicaciones ODBC cuando se llama a [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md), [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)o [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md). Esto puede ser útil para admitir nuevos tipos de servidor, porque los tipos de datos de C existentes podrían no representar correctamente los nuevos tipos de datos de servidor. El uso de tipos c específicos del controlador puede aumentar el número de conversiones que los controladores pueden realizar.  
  
 Por ejemplo, supongamos que un sistema de administración de bases de datos (DBMS) introdujo un nuevo tipo SQL, **DATETIMEOFFSET**, para representar la fecha y hora con información de zona horaria. No habría ningún tipo C específico en ODBC que correspondiera a **DATETIMEOFFSET**. Una aplicación tendría que enlazar **DATETIMEOFFSET** como SQL_C_BINARY y convertirlo a un tipo de datos definido por el usuario. A partir de ODBC 3.8 con extensibilidad de tipo de datos C, un controlador puede definir un nuevo tipo c correspondiente. Por ejemplo, para el nuevo tipo SQL DATETIMEOFFSET, el controlador puede definir un nuevo tipo c correspondiente, como SQL_C_DATETIMEOFFSET. A continuación, una aplicación puede enlazar el nuevo tipo SQL como un tipo C específico del controlador.  
  
 Un tipo de datos C se define en el controlador de la siguiente manera:  
  
-   El nivel de cumplimiento ODBC para una aplicación, controlador ODBC y Administrador de controladores es 3.8 (o superior).  
  
-   El rango de datos de un tipo C específico del controlador está entre 0x4000 y 0x7FFF.  
  
-   El controlador define la estructura de los datos correspondientes al tipo C.  Esto se puede hacer en el SDK específico del controlador.  
  
 El administrador de controladores no validará un tipo C definido en el intervalo de 0x4000 y 0x7FFF; el controlador realizará la validación y cualquier conversión de tipo de datos. Pero si el rango de datos de un tipo C pasado al administrador de controladores está entre 0x0000 y 0x3FFF o entre 0x8000 y 0xFFFF, el administrador de controladores validará el tipo de datos C.  
  
> [!NOTE]  
>  Los tipos de datos C específicos del controlador deben describirse en la documentación del controlador.  
  
 Para especificar un nivel de cumplimiento ODBC de 3.8, una aplicación llama a [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md) con el atributo SQL_ATTR_ODBC_VERSION establecido en **SQL_OV_ODBC3_80**. Para determinar la versión del controlador, una aplicación llama a **SQLGetInfo** con SQL_DRIVER_ODBC_VER.  
  
 Para obtener más información acerca de ODBC 3.8, vea [Novedades de ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md).  
  
## <a name="see-also"></a>Consulte también  
 [Tipos de datos C](../../../odbc/reference/appendixes/c-data-types.md)
