---
title: Tipos de datos de C en ODBC | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306300"
---
# <a name="c-data-types-in-odbc"></a>Tipos de datos C en ODBC
ODBC define los tipos de datos de C que utilizan las variables de aplicación y sus identificadores de tipo correspondientes. Los búferes que se enlazan a las columnas del conjunto de resultados y los parámetros de la instrucción usan estos parámetros. Por ejemplo, supongamos que una aplicación desea recuperar datos de una columna de conjunto de resultados en formato de caracteres. Declara una variable con el tipo de datos SQLCHAR * y enlaza esta variable a la columna del conjunto de resultados con un identificador de tipo de SQL_C_CHAR. Para obtener una lista completa de los tipos de datos de C y de los identificadores de tipo, vea [Apéndice D: tipos de datos](../../../odbc/reference/appendixes/appendix-d-data-types.md).  
  
 ODBC también define una asignación predeterminada de cada tipo de datos de SQL a un tipo de datos de C. Por ejemplo, un entero de 2 bytes del origen de datos se asigna a un entero de 2 bytes en la aplicación. Para usar la asignación predeterminada, una aplicación especifica el identificador de tipo de SQL_C_DEFAULT. Sin embargo, no se recomienda el uso de este identificador por motivos de interoperabilidad.  
  
 Todos los tipos de datos enteros de C definidos en ODBC *1. x* están firmados. Se han agregado los tipos de datos de C sin signo y sus identificadores de tipo correspondientes en ODBC 2,0. Por este motivo, las aplicaciones y los controladores deben ser especialmente cuidadosos al tratar con las versiones *1. x* .  
  
## <a name="c-data-type-extensibility"></a>Extensibilidad de tipos de datos de C  
 En ODBC 3,8, puede especificar tipos de datos de C específicos del controlador. Esto permite enlazar un tipo SQL como un tipo de C específico del controlador en aplicaciones ODBC cuando se llama a [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md), [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)o [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md). Esto puede ser útil para admitir nuevos tipos de servidor, porque los tipos de datos de C existentes podrían no representar correctamente los nuevos tipos de datos de servidor. El uso de tipos de C específicos del controlador puede aumentar el número de conversiones que pueden realizar los controladores.  
  
 Por ejemplo, suponga que un sistema de administración de bases de datos (DBMS) incorporó un nuevo tipo SQL, **DateTimeOffset**, para representar la fecha y la hora con información de zona horaria. No habrá ningún tipo de C específico en ODBC que corresponda a **DateTimeOffset**. Una aplicación tendría que enlazar **DateTimeOffset** como SQL_C_BINARY y convertirlo en un tipo de datos definido por el usuario. A partir de ODBC 3,8 con extensibilidad de tipos de datos de C, un controlador puede definir un nuevo tipo de C correspondiente. Por ejemplo, para el nuevo tipo de SQL DATETIMEOFFSET, el controlador puede definir un nuevo tipo de C correspondiente, como SQL_C_DATETIMEOFFSET. A continuación, una aplicación puede enlazar el nuevo tipo SQL como un tipo C específico del controlador.  
  
 Un tipo de datos de C se define en el controlador de la siguiente manera:  
  
-   El nivel de cumplimiento de ODBC de una aplicación, un controlador ODBC y el administrador de controladores es 3,8 (o posterior).  
  
-   El rango de datos de un tipo C específico del controlador se encuentra entre 0x4000 y 0x7FFF.  
  
-   El controlador define la estructura de los datos correspondientes al tipo C.  Esto puede hacerse en el SDK específico del controlador.  
  
 El administrador de controladores no validará un tipo C definido en el intervalo de 0x4000 y 0x7FFF; el controlador realizará la validación y cualquier conversión de tipo de datos. Pero si el intervalo de datos de un tipo C pasado al administrador de controladores se encuentra entre 0x0000 y 0x3FFF, o entre 0x8000 y 0xFFFF, el administrador de controladores validará el tipo de datos C.  
  
> [!NOTE]  
>  Los tipos de datos de C específicos del controlador deben describirse en la documentación del controlador.  
  
 Para especificar un nivel de cumplimiento de ODBC de 3,8, una aplicación llama a [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md) con el atributo SQL_ATTR_ODBC_VERSION establecido en **SQL_OV_ODBC3_80**. Para determinar la versión del controlador, una aplicación llama a **SQLGetInfo** con SQL_DRIVER_ODBC_VER.  
  
 Para obtener más información acerca de ODBC 3,8, vea [novedades de odbc 3,8](../../../odbc/reference/what-s-new-in-odbc-3-8.md).  
  
## <a name="see-also"></a>Consulte también  
 [Tipos de datos C](../../../odbc/reference/appendixes/c-data-types.md)
