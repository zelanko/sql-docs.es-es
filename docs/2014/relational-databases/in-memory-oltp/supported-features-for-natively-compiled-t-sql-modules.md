---
title: Construcciones admitidas en procedimientos almacenados compilados de forma nativa | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 05515013-28b5-4ccf-9a54-ae861448945b
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 6b875808a5a9379f917b246cb871420a339519f7
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718803"
---
# <a name="supported-constructs-in-natively-compiled-stored-procedures"></a>Construcciones admitidas en procedimientos almacenados compilados de forma nativa
  Este tema contiene una lista de características admitidas para los procedimientos almacenados compilados de forma nativa ([CREATE PROCEDURE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-procedure-transact-sql)):  
  
-   [Programación en procedimientos almacenados compilados de forma nativa](#pncsp)  
  
-   [Operadores admitidos](#so)  
  
-   [Funciones integradas en procedimientos almacenados compilados de forma nativa](#bfncsp)  
  
-   [Área expuesta de consulta en procedimientos almacenados compilados de forma nativa](#qsancsp)  
  
-   [Auditoría](#auditing)  
  
-   [Sugerencias de tablas, consultas y combinaciones](#tqh)  
  
-   [Limitaciones de ordenación](#los)  
  
 Para obtener información sobre los tipos de datos que se admiten en los procedimientos almacenados compilados de forma nativa, consulte [Supported Data Types](supported-data-types-for-in-memory-oltp.md).  
  
 Para obtener información completa sobre las construcciones no admitidas y sobre cómo evitar algunas de las características no admitidas en los procedimientos almacenados compilados de forma nativa, vea [Migration Issues for Natively Compiled Stored Procedures](migration-issues-for-natively-compiled-stored-procedures.md). Para obtener más información sobre las características no compatibles, vea [Construcciones Transact-SQL no admitidas por OLTP en memoria](transact-sql-constructs-not-supported-by-in-memory-oltp.md).  
  
##  <a name="programmability-in-natively-compiled-stored-procedures"></a><a name="pncsp"></a>Programación en procedimientos almacenados compilados de forma nativa  
 Se admite lo siguiente:  
  
-   BEGIN ATOMIC (en el nivel externo del procedimiento almacenado), LANGUAGE, ISOLATION LEVEL, DATEFORMAT y DATEFIRST.  
  
-   Declaración de variables como NULL o NOT NULL. Si una variable se declara como NOT NULL, la declaración debe tener un inicializador. Si una variable se declara como NOT NULL, el inicializador es opcional.  
  
-   IF y WHILE  
  
-   INSERT/UPDATE/DELETE  
  
     No se admiten las subconsultas. En las cláusulas WHERE o HAVING, AND y BETWEEN son compatibles; OR, NOT, y IN no se admiten.  
  
-   Variables de tabla y tipos de tabla con optimización para memoria.  
  
-   RETURN  
  
-   SELECT  
  
-   SET  
  
-   TRY/CATCH/THROW  
  
     Para optimizar el rendimiento, use un solo bloque TRY/CATCH para un procedimiento almacenado compilado de forma nativa completo.  
  
##  <a name="supported-operators"></a><a name="so"></a>Operadores admitidos  
 Se admiten los siguientes operadores.  
  
-   Los [operadores de comparación &#40;&#41;de Transact-SQL](/sql/t-sql/language-elements/comparison-operators-transact-sql) (por ejemplo, >, \< , >= y <=) se admiten en los condicionales (si, while).  
  
-   Operadores unarios (+, -).  
  
-   Operadores binarios ((*, /, +, -, % (módulo)).  
  
     Se admite el operador más (+) en ambos números y cadenas.  
  
-   Operadores lógicos (AND, OR, NOT). OR y NOT se admiten en las instrucciones IF y WHILE pero no en las cláusulas WHERE o HAVING.  
  
-   Operadores ~, &, | y ^ bit a bit  
  
##  <a name="built-in-functions-in-natively-compiled-stored-procedures"></a><a name="bfncsp"></a>Funciones integradas en procedimientos almacenados compilados de forma nativa  
 Se admiten las funciones siguientes en restricciones DEFAULT de tablas optimizadas para memoria y procedimientos almacenados compilados de forma nativa.  
  
-   Funciones matemáticas: ACOS, ASIN, ATAN, ATN2, COS, COT, DEGREES, EXP, LOG, LOG10, PI, POWER, RADIANES, RAND, SIN, SQRT, SQUARE y TAN  
  
-   Funciones de fecha: CURRENT_TIMESTAMP, DATEADD, DATEDIFF, DATEFROMPARTS, DATEPART, DATETIME2FROMPARTS, DATETIMEFROMPARTS, DAY, EOMONTH, GETDATE, GETUTCDATE, MONTH, SMALLDATETIMEFROMPARTS, SYSDATETIME, SYSUTCDATETIME y YEAR.  
  
-   Funciones de cadena: LEN, LTRIM, RTRIM y SUBSTRING  
  
-   Función de identidad: SCOPE_IDENTITY  
  
-   Funciones NULL: ISNULL  
  
-   Funciones uniqueidentifier: NEWID y NEWSEQUENTIALID  
  
-   Funciones de error: ERROR_LINE, ERROR_MESSAGE, ERROR_NUMBER, ERROR_PROCEDURE, ERROR_SEVERITY y ERROR_STATE  
  
-   Conversiones: CAST y CONVERT. No se admiten las conversiones entre cadenas de caracteres Unicode y no Unicode (n(var)char y (var)char).  
  
-   Funciones del sistema: @@rowcount. Las instrucciones de los procedimientos almacenados compilados de forma nativa actualizan @@rowcount y puede usar @@rowcount en un procedimiento almacenado compilado de forma nativa para determinar el número de filas afectadas por la última instrucción ejecutada dentro de ese procedimiento almacenado compilado de forma nativa. Pero @@rowcount se restablece en 0 al principio y al final de la ejecución de un procedimiento almacenado compilado de forma nativa.  
  
##  <a name="query-surface-area-in-natively-compiled-stored-procedures"></a><a name="qsancsp"></a>Área expuesta de consulta en procedimientos almacenados compilados de forma nativa  
 Se admite lo siguiente:  
  
-   BETWEEN  
  
-   Alias de nombre de columna (con sintaxis AS o =).  
  
-   CROSS JOIN y INNER JOIN, solo se admiten con consultas SELECT.  
  
-   Las expresiones se admiten en la lista de selección y [donde &#40;cláusula de Transact-SQL&#41;](/sql/t-sql/queries/where-transact-sql) si usan un operador admitido. Consulte [Operadores admitidos](#so) para ver la lista de los operadores que se admiten actualmente.  
  
-   Predicado de filtro IS [NOT] NULL  
  
-   Desde la \< tabla con optimización para memoria>  
  
-   Se admite [GROUP BY &#40;&#41;de Transact-SQL](/sql/t-sql/queries/select-group-by-transact-sql) , junto con las funciones de agregado AVG, COUNT, COUNT_BIG, min, Max y sum. MIN o MAX no se admiten para los tipos nvarchar, char, varchar, varchar, varbinary y binary. La [cláusula order by &#40;Transact-sql&#41;](/sql/t-sql/queries/select-order-by-clause-transact-sql) es compatible con [Group by &#40;transact-SQL&#41;](/sql/t-sql/queries/select-group-by-transact-sql) si una expresión de la lista order by aparece literalmente en la lista Group by. Por ejemplo, se admite GROUP BY a + b ORDER BY a + b pero no GROUP BY a, b ORDER BY a + b.  
  
-   HAVING, sujeto a las mismas limitaciones de expresión que la cláusula WHERE.  
  
-   INSERT VALUES (una fila por instrucción) e INSERT SELECT  
  
-   ORDENAR por <sup>1</sup>  
  
-   Predicados que no hacen referencia a una columna.  
  
-   SELECT, UPDATE y DELETE  
  
-   TOP <sup>1</sup>  
  
-   Asignación de variable de la lista de selección.  
  
-   DÓNDE... ETC  
  
 <sup>1</sup> order by y Top se admiten en procedimientos almacenados compilados de forma nativa, con algunas restricciones:  
  
-   No hay compatibilidad con `DISTINCT` en la cláusula `SELECT` ni `ORDER BY`.  
  
-   No hay compatibilidad con `WITH TIES` ni `PERCENT` en la cláusula `TOP`.  
  
-   `TOP` combinada con `ORDER BY` no admite más de 8.192 elementos cuando se utiliza una constante en la cláusula `TOP`. Este límite puede reducirse en caso de que la consulta contenga combinaciones o funciones de agregado. (Por ejemplo, con una combinación (dos tablas), el límite es de 4.096 filas. Con dos combinaciones (tres tablas), el límite es de 2.730 filas).  
  
     Puede obtener más de 8.192 resultados si almacena el número de filas en una variable:  
  
    ```sql  
    DECLARE @v INT = 9000  
    SELECT TOP (@v) ... FROM ... ORDER BY ...  
    ```  
  
 Sin embargo, una constante en la cláusula `TOP` produce un rendimiento mejor en comparación con el uso de una variable.  
  
 Estas restricciones no se aplican al acceso mediante [!INCLUDE[tsql](../../includes/tsql-md.md)] interpretado a las tablas optimizadas para memoria.  
  
##  <a name="auditing"></a><a name="auditing"></a>Auditoría  
 Se admite la auditoría a nivel de procedimiento en los procedimientos almacenados compilados de forma nativa. La auditoría de nivel de instrucción no se admite.  
  
 Para obtener más información sobre la auditoría, vea [Crear una especificación de auditoría de servidor y de auditoría de base de datos](../security/auditing/create-a-server-audit-and-database-audit-specification.md)  
  
##  <a name="table-query-and-join-hints"></a><a name="tqh"></a>Sugerencias de tabla, consulta y combinación  
 Se admite lo siguiente:  
  
-   Las sugerencias INDEX, FORCESCAN y FORCESEEK, ya sea en la sintaxis de sugerencias de tabla o en la [cláusula OPTION &#40;Transact-SQL&#41;](/sql/t-sql/queries/option-clause-transact-sql) de la consulta.  
  
-   FORCE ORDER  
  
-   INNER LOOP JOIN  
  
-   OPTIMIZE FOR  
  
 Para obtener más información, vea [sugerencias &#40;&#41;de Transact-SQL ](/sql/t-sql/queries/hints-transact-sql).  
  
##  <a name="limitations-on-sorting"></a><a name="los"></a>Limitaciones de la ordenación  
 Puede ordenar más de 8000 filas en una consulta que use [TOP &#40;Transact-SQL&#41;](/sql/t-sql/queries/top-transact-sql) y una [cláusula ORDER BY &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-order-by-clause-transact-sql). Pero sin la [cláusula ORDER BY &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-order-by-clause-transact-sql), [TOP &#40;Transact-SQL&#41;](/sql/t-sql/queries/top-transact-sql) puede ordenar hasta 8000 filas (si hay combinaciones, menos filas).  
  
 Si la consulta usa el operador [TOP &#40;Transact-SQL&#41;](/sql/t-sql/queries/top-transact-sql) y una [cláusula ORDER BY &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-order-by-clause-transact-sql), puede especificar hasta 8192 filas para el operador TOP. Si especifica más de 8192 filas obtendrá el mensaje de error: **Mensaje 41398, nivel 16, estado 1, procedimiento *\<<nombreDeProcedimiento>*, línea *\<númeroDeLínea>* El operador TOP puede devolver un máximo de 8192 filas; el número solicitado es *\<número>*.**  
  
 Si no tiene una cláusula TOP, puede ordenar cualquier número de filas con ORDER BY.  
  
 Si no utiliza una cláusula ORDER BY, puede utilizar un valor entero con el operador TOP.  
  
 Ejemplo con TOP n = 8192: se compila  
  
```sql  
CREATE PROCEDURE testTop  
WITH EXECUTE AS OWNER, SCHEMABINDING, NATIVE_COMPILATION  
  AS  
  BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
    SELECT TOP 8192 ShoppingCartId, CreatedDate, TotalPrice FROM dbo.ShoppingCart  
    ORDER BY ShoppingCartId DESC  
  END;  
GO  
```  
  
 Ejemplo con TOP N > 8192: error al compilar.  
  
```sql  
CREATE PROCEDURE testTop  
WITH EXECUTE AS OWNER, SCHEMABINDING, NATIVE_COMPILATION  
  AS  
  BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
    SELECT TOP 8193 ShoppingCartId, CreatedDate, TotalPrice FROM dbo.ShoppingCart  
    ORDER BY ShoppingCartId DESC  
  END;  
GO  
```  
  
 La limitación de 8192 filas solo se aplica a `TOP N` donde `N` es una constante, como en los ejemplos anteriores.  Si necesita un número `N` mayor que 8192 puede asignar el valor a una variable y utilizar esa variable con `TOP`.  
  
 Ejemplo usando una variable: se compila  
  
```sql  
CREATE PROCEDURE testTop  
WITH EXECUTE AS OWNER, SCHEMABINDING, NATIVE_COMPILATION  
  AS  
  BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
    DECLARE @v int = 8193   
    SELECT TOP (@v) ShoppingCartId, CreatedDate, TotalPrice FROM dbo.ShoppingCart  
    ORDER BY ShoppingCartId DESC  
  END;  
GO  
```  
  
 **Limitaciones para las filas devueltas:** hay dos casos en los que se puede reducir el número de filas que puede devolver el operador TOP:  
  
-   Usar JOIN en la consulta.  El efecto de JOIN en la limitación depende del plan de consulta.  
  
-   Usar funciones de agregado o referencias a funciones de agregado en la cláusula ORDER BY.  
  
 La fórmula para calcular un N máximo de peor caso admitido en TOP N es: `N = floor ( 65536 / number_of_tables * 8 + total_size+of+aggs )`.  
  
## <a name="see-also"></a>Consulte también  
 [Procedimientos almacenados compilados de forma nativa](natively-compiled-stored-procedures.md)   
 [Problemas de migración para los procedimientos almacenados compilados de forma nativa](migration-issues-for-natively-compiled-stored-procedures.md)  
  
  
