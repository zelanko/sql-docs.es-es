---
title: Crear instrucciones SQL para los cursores | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-queries
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- cursors [ODBC], statement construction
- ODBC applications, cursors
- SQL Server Native Client ODBC driver, statements
- statements [ODBC], constructing
- ODBC applications, statements
- statements [ODBC], cursors
ms.assetid: 134003fd-9c93-4f5c-a988-045990933b80
caps.latest.revision: 36
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 6207d51509b4eed3ebb3ec0db5c40174b7b7ac9b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="constructing-sql-statements-for-cursors"></a>Crear instrucciones SQL para cursores
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC Native Client utiliza cursores de servidor para implementar la funcionalidad de cursor que se define en la especificación de ODBC. Una aplicación ODBC controla el comportamiento del cursor mediante el uso de [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) establecer distintos atributos de instrucción. Éstos son los atributos y sus valores predeterminados.  
  
|Atributo|Predeterminado|  
|---------------|-------------|  
|SQL_ATTR_CONCURRENCY|SQL_CONCUR_READ_ONLY|  
|SQL_ATTR_CURSOR_TYPE|SQL_CURSOR_FORWARD_ONLY|  
|SQL_ATTR_CURSOR_SCROLLABLE|SQL_NONSCROLLABLE|  
|SQL_ATTR_CURSOR_SENSITIVITY|SQL_UNSPECIFIED|  
|SQL_ATTR_ROW_ARRAY_SIZE|1|  
  
 Cuando estas opciones se establecen en sus valores predeterminados en el momento en que se ejecuta una instrucción SQL, la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client no utiliza un cursor de servidor para implementar el conjunto de resultados; en su lugar, usa un conjunto de resultados predeterminado. Si cualquiera de estas opciones se cambian los valores predeterminados en el momento en que se ejecuta una instrucción SQL, la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC Native Client intenta usar un cursor de servidor para implementar el conjunto de resultados.  
  
 Los conjuntos de resultados predeterminados admiten todas las instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)]. No hay ninguna restricción con respecto a los tipos de instrucciones SQL que pueden ejecutarse cuando se utiliza un conjunto de resultados predeterminado.  
  
 Los cursores de servidor no admiten todas las instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)]. Los cursores de servidor no admiten cualquier instrucción SQL que genere varios conjuntos de resultados.  
  
 Los cursores de servidor no admiten los siguientes tipos de instrucciones:  
  
-   Lotes  
  
     Instrucciones SQL generadas a partir de dos o más instrucciones SQL SELECT individuales como, por ejemplo:  
  
    ```  
    SELECT * FROM Authors; SELECT * FROM Titles  
    ```  
  
-   Procedimientos almacenados con varias instrucciones SELECT  
  
     Instrucciones SQL que ejecutan un procedimiento almacenado que contiene más de una instrucción SELECT. Entre estas instrucciones se incluyen las instrucciones SELECT que rellenan parámetros o variables.  
  
-   Palabras clave  
  
     Instrucciones SQL que contienen las palabras clave FOR BROWSE o INTO.  
  
 En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], si se ejecuta una instrucción SQL que se ajusta a alguna de estas condiciones con un cursor de servidor, el cursor de servidor se convierte de forma implícita en un conjunto de resultados predeterminado. Después de **SQLExecDirect** o **SQLExecute** devuelve SQL_SUCCESS_WITH_INFO, el cursor atributos volverán a establecerse a sus valores predeterminados.  
  
 Las instrucciones SQL que no se ajustan a las categorías anteriores pueden ejecutarse con cualquier valor de atributo de instrucción; funcionan igual de bien con un conjunto de resultados predeterminado que con un cursor de servidor.  
  
## <a name="errors"></a>Errores  
 En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 y versiones posteriores, un intento de ejecución de una instrucción que da lugar a varios conjuntos de resultados genera SQL_SUCCESS_WITH INFO y el mensaje siguiente:  
  
```  
SqlState: 01S02"  
pfNative: 0  
szErrorMsgString: "[Microsoft][SQL Server Native Client][SQL Server]  
               Cursor type changed."  
```  
  
 Aplicaciones ODBC que reciben este mensaje pueden llamar a [SQLGetStmtAttr](../../relational-databases/native-client-odbc-api/sqlgetstmtattr.md) para determinar la configuración actual del cursor.  
  
 Un intento de ejecutar un procedimiento con varias instrucciones SELECT cuando se utilizan los cursores de servidor genera el error siguiente:  
  
```  
SqlState: 42000  
pfNative: 16937  
szErrorMsgString: [Microsoft][SQL Server Native Client][SQL Server]  
               A server cursor is not allowed on a stored procedure  
               with more than one SELECT statement in it. Use a  
               default result set or client cursor.  
```  
  
 Un intento de ejecutar un lote con varias instrucciones SELECT cuando se utilizan los cursores de servidor genera el error siguiente:  
  
```  
SqlState: 42000  
pfNative: 16938  
szErrorMsgString: [Microsoft][SQL Server Native Client][SQL Server]  
               sp_cursoropen. The statement parameter can only  
               be a single SELECT statement or a single stored   
               procedure.  
```  
  
 Las aplicaciones ODBC que reciben estos errores deben restablecer todos los atributos de instrucción de cursor a sus valores predeterminados antes de intentar ejecutar la instrucción.  
  
## <a name="see-also"></a>Vea también  
 [Ejecutar consultas &#40;ODBC&#41;](../../relational-databases/native-client-odbc-queries/executing-queries-odbc.md)  
  
  
