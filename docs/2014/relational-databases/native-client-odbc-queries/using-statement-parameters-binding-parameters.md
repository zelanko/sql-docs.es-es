---
title: Parámetros de enlace | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, parameters
- parameters [SQL Server Native Client], ODBC
- statements [ODBC], parameters
- binding parameters [SQL Server Native Client]
- parameter markers [ODBC]
- unbound parameter markers
- SQLBindParameter function
- ODBC applications, parameters
- bound parameter markers [SQL Server Native Client]
ms.assetid: d6c69739-8f89-475f-a60a-b2f6c06576e2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 89b124ea6c73b9ebb80ab5a047b6d7e4cafe2e81
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "78175862"
---
# <a name="binding-parameters"></a>Enlazar parámetros
  Cada marcador de parámetros de una instrucción SQL debe estar asociado o enlazado a una variable de la aplicación antes de que se pueda ejecutar la instrucción. Esto se realiza mediante una llamada a la función [SQLBindParameter](../native-client-odbc-api/sqlbindparameter.md) . **SQLBindParameter** describe la variable de programa (dirección, tipo de datos de C, etc.) al controlador. También identifica el marcador de parámetros indicando su valor ordinal y, a continuación, describe las características del objeto SQL que representa (tipo de datos SQL, precisión, etc.).

 Los marcadores de parámetros se pueden enlazar o reenlazar en cualquier momento antes de que se ejecute una instrucción. Un enlace de parámetro continúa activo hasta que se produce uno de los siguientes eventos:

-   Una llamada a [SQLFreeStmt](../native-client-odbc-api/sqlfreestmt.md) con el parámetro *Option* establecido en SQL_RESET_PARAMS libera todos los parámetros enlazados al identificador de instrucción.

-   Una llamada a **SQLBindParameter** con *ParameterNumber* establecido en el ordinal de un marcador de parámetro enlazado libera automáticamente el enlace anterior.

 Una aplicación también puede enlazar parámetros a matrices de variables de programa para procesar una instrucción SQL por lotes. Existen dos tipos de enlaces de matriz:

-   El enlace de modo de columna se hace cuando cada parámetro individual se enlaza a su propia matriz de variables.

     El enlace de modo de columna se especifica llamando a [SQLSetStmtAttr](../native-client-odbc-api/sqlsetstmtattr.md) con el *atributo* establecido en SQL_ATTR_PARAM_BIND_TYPE y *ValuePtr* establecido en SQL_PARAM_BIND_BY_COLUMN.

-   El enlace de modo de fila se hace cuando todos los parámetros de la instrucción SQL se enlazan como una unidad a una matriz de estructuras que contienen variables individuales para los parámetros.

     El enlace de modo de fila se especifica mediante una llamada a **SQLSetStmtAttr** con el *atributo* establecido en SQL_ATTR_PARAM_BIND_TYPE y *ValuePtr* establecido en el tamaño de la estructura que contiene las variables de programa.

 Cuando el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client envía parámetros de cadena binaria o de caracteres al servidor, rellena los valores con la longitud especificada en el parámetro **SQLBindParameter** *columnas* . Si una aplicación ODBC 2. x especifica 0 para *columnas*, el controlador rellena el valor del parámetro con la precisión del tipo de datos. La precisión es 8000 cuando se conecta con los servidores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 255 cuando se conecta con versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *Columnas* en bytes para las columnas Variant.

 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite definir nombres para parámetros de procedimiento almacenado. ODBC 3.5 también introdujo la compatibilidad con el uso de parámetros con nombre para llamar a procedimientos almacenados de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta compatibilidad se puede utilizar para:

-   Llamar a un procedimiento almacenado y proporcionar valores para un subconjunto de parámetros definido para el procedimiento almacenado.

-   Especifique los parámetros en la aplicación en un orden diferente que el orden especificado cuando se creó el procedimiento almacenado.

 Los parámetros con nombre solo se admiten [!INCLUDE[tsql](../../includes/tsql-md.md)] `EXECUTE` cuando se usa la instrucción o la secuencia de escape ODBC Call para ejecutar un procedimiento almacenado.

 Si `SQL_DESC_NAME` está establecido para un parámetro de procedimiento almacenado, todos los parámetros de procedimiento almacenado de la consulta también deben establecer `SQL_DESC_NAME`.  Si se usan literales en llamadas a procedimientos almacenados, donde los `SQL_DESC_NAME` parámetros tienen establecido, los literales deben usar el formato *' nombre*=*valor*', donde *nombre* es el nombre del parámetro del procedimiento almacenado @p1(por ejemplo,). Para obtener más información, vea [enlazar parámetros por nombre (parámetros con nombre)](https://go.microsoft.com/fwlink/?LinkId=167215).

## <a name="see-also"></a>Consulte también
 [Usar parámetros de instrucciones](using-statement-parameters.md)


