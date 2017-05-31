---
title: "Características admitidas en los módulos T-SQL compilados de forma nativa | Microsoft Docs"
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 05515013-28b5-4ccf-9a54-ae861448945b
caps.latest.revision: 44
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 16f09bada7bbf3ae964ecfa09aa33208aa2f3acf
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="supported-features-for-natively-compiled-t-sql-modules"></a>Características admitidas en los módulos T-SQL compilados de forma nativa
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]


  En este tema se incluye una lista de áreas expuestas y características admitidas de T-SQL en el cuerpo de los módulos T-SQL compilados de forma nativa, como procedimientos almacenados ([CREATE PROCEDURE (Transact-SQL)](../../t-sql/statements/create-procedure-transact-sql.md)), funciones escalares definidas por el usuario, funciones con valores de tabla insertadas y desencadenadores.  

 Si quiere conocer las características admitidas en torno a la definición de los módulos nativos, vea [Construcciones DDL admitidas para módulos T-SQL compilados de forma nativa](../../relational-databases/in-memory-oltp/supported-ddl-for-natively-compiled-t-sql-modules.md).  

-   [Área expuesta de consulta en los módulos nativos](#qsancsp)  

-   [Modificación de datos](#dml)  

-   [Idioma de control de flujo](#cof)  

-   [Operadores admitidos](#so)  

-   [Funciones integradas en módulos compilados de forma nativa](#bfncsp)  

-   [Auditoría](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md#auditing)  

-   [Sugerencias de consulta y tabla](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md#tqh)  

-   [Limitaciones de ordenación](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md#los)  

 Para tener información completa sobre las construcciones no admitidas y sobre cómo evitar algunas de las características no admitidas en los módulos compilados de forma nativa, consulte [Migration Issues for Natively Compiled Stored Procedures](../../relational-databases/in-memory-oltp/migration-issues-for-natively-compiled-stored-procedures.md). Para obtener más información sobre las características no compatibles, vea [Construcciones Transact-SQL no admitidas por OLTP en memoria](../../relational-databases/in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md).  

##  <a name="qsancsp"></a> Área expuesta de consulta en los módulos nativos  

Se admiten las siguientes construcciones de consulta:  

Cláusula SELECT:  

-   Alias de columnas y nombre (con sintaxis AS o =).  

-   Subconsultas escalares  

-   TOP*  

-   SELECT DISTINCT  

              DISTINCT aggregates are not supported.  

-   UNION y UNION ALL

-   Asignaciones de variables  

Cláusula FROM:  

-   FROM \<tabla con optimización para memoria o variable de tabla>  

-   FROM \<TVF insertada compilada de forma nativa>  

-   LEFT OUTER JOIN, RIGHT OUTER JOIN, CROSS JOIN y INNER JOIN.  

-   Subconsultas `[AS] table_alias`. Para obtener más información, vea [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md).  

Cláusula WHERE:  

-   Predicado de filtro IS [NOT] NULL  

-   AND, OR, NOT, IN, EXISTS, BETWEEN  


Cláusula[GROUP BY](../../t-sql/queries/select-group-by-transact-sql.md) :

- Funciones de agregado AVG, COUNT, COUNT_BIG, MIN, MAX y SUM.  

- MIN o MAX no se admiten para los tipos nvarchar, char, varchar, varchar, varbinary y binary.  

Cláusula[ORDER BY](../../t-sql/queries/select-order-by-clause-transact-sql.md) :


- No hay compatibilidad con **DISTINCT** en la cláusula **ORDER BY** .


- Se admite con [GROUP BY &#40;Transact-SQL&#41;](../../t-sql/queries/select-group-by-transact-sql.md) si una expresión de la lista ORDER BY aparece literalmente en la lista GROUP BY.
  - Por ejemplo, se admite GROUP BY a + b ORDER BY a + b pero no GROUP BY a, b ORDER BY a + b.  


Cláusula HAVING:

- Está sujeta a las mismas limitaciones de expresión que la cláusula WHERE.


#### <a name="order-by-and-top-are-supported-in-natively-compiled-modules-with-some-restrictions"></a>Se admiten ORDER BY y TOP en módulos compilados de forma nativa, con algunas restricciones.


- No hay compatibilidad con **WITH TIES** ni **PERCENT** en la cláusula **TOP** .


- No hay compatibilidad con **DISTINCT** en la cláusula **ORDER BY** .  


- **TOP** combinada con **ORDER BY** no admite más de 8.192 elementos cuando se utiliza una constante en la cláusula **TOP** .
  - Este límite puede reducirse en caso de que la consulta contenga combinaciones o funciones de agregado. (Por ejemplo, con una combinación (dos tablas), el límite es de 4.096 filas. Con dos combinaciones (tres tablas), el límite es de 2.730 filas).  
  - Puede obtener más de 8.192 resultados si almacena el número de filas en una variable:  

```tsql
DECLARE @v INT = 9000;
SELECT TOP (@v) … FROM … ORDER BY …
```

Sin embargo, una constante en la cláusula **TOP** produce un rendimiento mejor en comparación con el uso de una variable.  

Estas restricciones en [!INCLUDE[tsql](../../includes/tsql-md.md)] compilado de forma nativa no se aplican al acceso mediante [!INCLUDE[tsql](../../includes/tsql-md.md)] interpretado a las tablas con optimización para memoria.  


##  <a name="dml"></a> Modificación de datos  

Se admiten las siguientes instrucciones DML.  

-   INSERT VALUES (una fila por instrucción) e INSERT SELECT... SELECT  

-   UPDATE  

-   DELETE  

-   Se admite WHERE con instrucciones UPDATE y DELETE.  

##  <a name="cof"></a> Idioma de control de flujo  
 Se admiten las siguientes construcciones de lenguaje de control de flujo.  

-   [IF...ELSE &#40;Transact-SQL&#41;](../../t-sql/language-elements/if-else-transact-sql.md)  

-   [WHILE &#40;Transact-SQL&#41;](../../t-sql/language-elements/while-transact-sql.md)  

-   [RETURN &#40;Transact-SQL&#41;](../../t-sql/language-elements/return-transact-sql.md)  

-   [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md) puede usar todos los [tipos de datos admitidos para OLTP en memoria](../../relational-databases/in-memory-oltp/supported-data-types-for-in-memory-oltp.md), así como los tipos de tablas con optimización para memoria. Las variables se pueden declarar como NULL o NOT NULL.  

-   [SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)  

-   [TRY...CATCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)  

               To achieve optimal performance, use a single TRY/CATCH block for an entire natively compiled T-SQL module.  

-   [THROW &#40;Transact-SQL&#41;](../../t-sql/language-elements/throw-transact-sql.md)  

-   BEGIN ATOMIC (en el nivel externo del procedimiento almacenado). Para más información, consulte [Atomic Blocks](../../relational-databases/in-memory-oltp/atomic-blocks-in-native-procedures.md).  

##  <a name="so"></a> Operadores admitidos  
 Se admiten los siguientes operadores.  

-   [Operadores de comparación &#40;Transact-SQL&#41;](../../t-sql/language-elements/comparison-operators-transact-sql.md) (por ejemplo, >, \<, >= y <=)  

-   Operadores unarios (+, -).  

-   Operadores binarios ((*, /, +, -, % (módulo)).  

               The plus operator (+) is supported on both numbers and strings.  

-   Operadores lógicos (AND, OR, NOT).  

-   Operadores ~, &, | y ^ bit a bit  

-   APPLY, operador
    - **Applies to:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.  
      A partir de [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1, el operador APPLY se admite en los módulos compilados de forma nativa.

##  <a name="bfncsp"></a> Funciones integradas en módulos compilados de forma nativa  
 Las funciones siguientes se admiten en restricciones de tablas con optimización de memoria y en módulos T-SQL compilados de forma nativa.  

-   Todas las [funciones matemáticas &#40;Transact-SQL&#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)  

-   Funciones de fecha: CURRENT_TIMESTAMP, DATEADD, DATEDIFF, DATEFROMPARTS, DATEPART, DATETIME2FROMPARTS, DATETIMEFROMPARTS, DAY, EOMONTH, GETDATE, GETUTCDATE, MONTH, SMALLDATETIMEFROMPARTS, SYSDATETIME, SYSUTCDATETIME y YEAR.  

-   Funciones de cadena: LEN, LTRIM, RTRIM y SUBSTRING.  
    - **Applies to:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.  
      A partir de [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1, también se admiten las siguientes funciones integradas: TRIM, TRANSLATE y CONCAT_WS.  

-   Funciones de identidad: SCOPE_IDENTITY  

-   Funciones NULL: ISNULL  

-   Funciones uniqueidentifier: NEWID y NEWSEQUENTIALID  

-   Funciones JSON  
    - **Applies to:** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1.  
      A partir de [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.1, las funciones JSON se admiten en los módulos compilados de forma nativa.

-   Funciones de error: ERROR_LINE, ERROR_MESSAGE, ERROR_NUMBER, ERROR_PROCEDURE, ERROR_SEVERITY y ERROR_STATE  

-   Funciones del sistema: @@rowcount. Las instrucciones de los procedimientos almacenados compilados de forma nativa actualizan @@rowcount y puede usar @@rowcount en un procedimiento almacenado compilado de forma nativa para determinar el número de filas afectadas por la última instrucción ejecutada dentro de ese procedimiento almacenado compilado de forma nativa. Pero @@rowcount se restablece en 0 al principio y al final de la ejecución de un procedimiento almacenado compilado de forma nativa.  

-   Funciones de seguridad: IS_MEMBER({'group' | 'role'}), IS_ROLEMEMBER ('role' [, 'database_principal']), IS_SRVROLEMEMBER ('role' [, 'login']), ORIGINAL_LOGIN(), SESSION_USER, CURRENT_USER, SUSER_ID(['login']), SUSER_SID(['login'] [, Param2]), SUSER_SNAME([server_user_sid]), SYSTEM_USER, SUSER_NAME, USER, USER_ID(['user']), USER_NAME([id]), CONTEXT_INFO().

-   Se pueden anidar las ejecuciones de módulos nativos.

##  <a name="auditing"></a> Auditoría  
 Se admite la auditoría a nivel de procedimiento en los procedimientos almacenados compilados de forma nativa.  

 Para obtener más información sobre la auditoría, vea [Create a Server Audit and Database Audit Specification](../../relational-databases/security/auditing/create-a-server-audit-and-database-audit-specification.md).  

##  <a name="tqh"></a> Sugerencias de consulta y tabla  
 Se admite lo siguiente:  

-   Las sugerencias INDEX, FORCESCAN y FORCESEEK, ya sea en la sintaxis de sugerencias de tabla o en la [cláusula OPTION &#40;Transact-SQL&#41;](../../t-sql/queries/option-clause-transact-sql.md) de la consulta. Para obtener más información, vea [Sugerencias de tabla &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md).  

-   FORCE ORDER  

-   Sugerencia LOOP JOIN  

-   OPTIMIZE FOR  

 Para obtener más información, vea [Sugerencias de consulta &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md).  

##  <a name="los"></a> Limitaciones de ordenación  
 Puede ordenar más de 8000 filas en una consulta que use [TOP &#40;Transact-SQL&#41;](../../t-sql/queries/top-transact-sql.md) y una [cláusula ORDER BY &#40;Transact-SQL&#41;](../../t-sql/queries/select-order-by-clause-transact-sql.md). Pero sin la [cláusula ORDER BY &#40;Transact-SQL&#41;](../../t-sql/queries/select-order-by-clause-transact-sql.md), [TOP &#40;Transact-SQL&#41;](../../t-sql/queries/top-transact-sql.md) puede ordenar hasta 8000 filas (si hay combinaciones, menos filas).  

 Si la consulta usa el operador [TOP &#40;Transact-SQL&#41;](../../t-sql/queries/top-transact-sql.md) y una [cláusula ORDER BY &#40;Transact-SQL&#41;](../../t-sql/queries/select-order-by-clause-transact-sql.md), puede especificar hasta 8192 filas para el operador TOP. Si especifica más de 8192 filas obtendrá el mensaje de error: **Mensaje 41398, nivel 16, estado 1, procedimiento *\<<nombreDeProcedimiento>*, línea *\<númeroDeLínea>* El operador TOP puede devolver un máximo de 8192 filas; el número solicitado es *\<número>*.**  

 Si no tiene una cláusula TOP, puede ordenar cualquier número de filas con ORDER BY.  

 Si no utiliza una cláusula ORDER BY, puede utilizar un valor entero con el operador TOP.  

 Ejemplo con TOP n = 8192: se compila  

```tsql  
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

```tsql  
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

```tsql  
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

## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados compilados de forma nativa](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)   
 [Problemas de migración para los procedimientos almacenados compilados de forma nativa](../../relational-databases/in-memory-oltp/migration-issues-for-natively-compiled-stored-procedures.md)  



