---
title: SET @local_variable (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- SET @local_variable
- variables [SQL Server], assigning
- SET statement, @local_variable
- local variables [SQL Server]
ms.assetid: d410e06e-061b-4c25-9973-b2dc9b60bd85
caps.latest.revision: "52"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 56f38e166249f13bb50d1bf0188a5066da52ea78
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="set-localvariable-transact-sql"></a>ESTABLECER @local_variable (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Establece la variable local indicada, creada previamente con DECLARE @*local_variable* instrucción, en el valor especificado.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
SET   
{ @local_variable  
    [ . { property_name | field_name } ] = { expression | udt_name { . | :: } method_name }  
}  
|  
{ @SQLCLR_local_variable.mutator_method  
}  
|  
{ @local_variable  
    {+= | -= | *= | /= | %= | &= | ^= | |= } expression  
}  
|   
  { @cursor_variable =   
    { @cursor_variable | cursor_name   
    | { CURSOR [ FORWARD_ONLY | SCROLL ]   
        [ STATIC | KEYSET | DYNAMIC | FAST_FORWARD ]   
        [ READ_ONLY | SCROLL_LOCKS | OPTIMISTIC ]   
        [ TYPE_WARNING ]   
    FOR select_statement   
        [ FOR { READ ONLY | UPDATE [ OF column_name [ ,...n ] ] } ]   
      }   
    }  
}   
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
SET @local_variable {+= | -= | *= | /= | %= | &= | ^= | |= } expression  
  
```  
  
## <a name="arguments"></a>Argumentos  
 **@** *local_variable*  
 Es el nombre de una variable de cualquier tipo excepto **cursor**, **texto**, **ntext**, **imagen**, o **tabla**. Los nombres de variable deben comenzar con un signo de arroba (**@**). Los nombres de variable deben cumplir las reglas de [identificadores](../../relational-databases/databases/database-identifiers.md).  
  
 *property_name*  
 Es el nombre de una propiedad definida por el usuario.  
  
 *field_name*  
 Es un campo público de un tipo definido por el usuario.  
  
 *udt_name*  
 Es el nombre de un tipo definido por el usuario CLR (Common Language Runtime).  
  
 { **.** | **::** }  
 Especifica el método de un tipo definido por el usuario CLR. Para un método de instancia (no estáticos), use un punto (**.**). Un método estático, utilice dos puntos dobles (**::**). Para invocar un método, propiedad o campo de un tipo definido por el usuario CLR, debe tener el permiso EXECUTE para el tipo.  
  
 *NombreMétodo* **(** *argumento* [ **,**... *n* ] **)**  
 Es un método de un tipo definido por el usuario que toma uno o más argumentos para modificar el estado de la instancia de un tipo. Los métodos estáticos deben ser públicos.  
  
 **@** *SQLCLR_local_variable*  
 Es una variable cuyo tipo se encuentra en un ensamblado. Para obtener más información, consulte [Conceptos de programación en el ámbito de la integración de Common Language Runtime &#40;CLR&#41;](../../relational-databases/clr-integration/common-language-runtime-clr-integration-programming-concepts.md).  
  
 *mutator_method*  
 Es un método del ensamblado que puede cambiar el estado del objeto. SQLMethodAttribute.IsMutator se aplicará a este método.  
  
 { **+=** | **-=** | **\*=** | **/=** | **%=** | **&=** | **^=** | **|=** }  
 Operador de asignación compuesta:  
  
 += Sumar y asignar  
  
 -= Restar y asignar  
  
 * = Multiplicar y asignar  
  
 / = Dividir y asignar  
  
 % = Módulo y asignar  
  
 & = AND bit a bit y asignar  
  
 ^ = XOR bit a bit y asignar  
  
 | = OR bit a bit y asignar  
  
 *expression*  
 Se trata de cualquier [expresión](../../t-sql/language-elements/expressions-transact-sql.md).  
  
 *cursor_variable*  
 Es el nombre de una variable de cursor. Si la variable de cursor de destino indicada anteriormente hacía referencia a un cursor diferente, esa referencia se pierde.  
  
 *cursor_name*  
 Es el nombre de un cursor declarado con la instrucción DECLARE CURSOR.  
  
 CURSOR  
 Especifica que la instrucción SET contiene una declaración de un cursor.  
  
 SCROLL  
 Especifica que el cursor admite todas las opciones de captura: FIRST, LAST, NEXT, PRIOR, RELATIVE y ABSOLUTE. No es posible especificar SCROLL si se incluye también FAST_FORWARD.  
  
 FORWARD_ONLY  
 Especifica que el cursor solo admite la opción FETCH NEXT. El cursor solo se puede recuperar en una dirección, desde la primera fila hacia la última. Si se especifica FORWARD_ONLY sin las palabras clave STATIC, KEYSET o DYNAMIC, el cursor se implementa como DYNAMIC. Cuando no se especifica FORWARD_ONLY ni SCROLL, FORWARD_ONLY es la opción predeterminada, salvo que se incluyan las palabras clave STATIC, KEYSET o DYNAMIC. Los cursores STATIC, KEYSET y DYNAMIC toman como valor predeterminado SCROLL.  
  
 STATIC  
 Define un cursor que hace una copia temporal de los datos que utiliza. Todas las solicitudes al cursor se responden desde esta tabla temporal de tempdb; por ello, las modificaciones realizadas en las tablas base no se reflejarán en los datos obtenidos de las capturas realizadas en el cursor y, además, este cursor no admite modificaciones.  
  
 KEYSET  
 Especifica que la pertenencia y el orden de las filas del cursor se fijan cuando se abre este cursor. El conjunto de claves que identifican de forma única las filas está integrado en el keysettable en tempdb. Los cambios efectuados en valores que no sean claves de las tablas base, ya sean realizados por el propietario del cursor o confirmados por otros usuarios, son visibles cuando el propietario del cursor se desplaza por el cursor. Las inserciones realizadas por otros usuarios no son visibles y no es posible hacer inserciones a través de un cursor de servidor [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 Si se elimina una fila, un intento para capturar la fila devuelve un @@FETCH_STATUS -2. Actualizaciones de valores de clave desde fuera del cursor son similares a la eliminación de la fila antigua seguida de una inserción de la nueva fila. La fila con los nuevos valores no está visible e intenta capturar la fila con los valores antiguos devuelve un @@FETCH_STATUS -2. Los nuevos valores son visibles si la actualización se realiza a través del cursor especificando la cláusula WHERE CURRENT OF.  
  
 DYNAMIC  
 Define un cursor que refleja en su conjunto de resultados todos los cambios realizados en los datos de las filas cuando el propietario del cursor se desplaza por éste. Los valores de los datos, el orden y la pertenencia de las filas pueden cambiar en cada captura. Las opciones de captura absoluta y relativa no se pueden utilizar en los cursores dinámicos.  
  
 FAST_FORWARD  
 Especifica un cursor FORWARD_ONLY, READ_ONLY con las optimizaciones habilitadas. No es posible especificar FAST_FORWARD si también se incluye SCROLL.  
  
 READ_ONLY  
 Impide que se realicen actualizaciones a través de este cursor. No es posible hacer referencia al cursor en una cláusula WHERE CURRENT OF de una instrucción UPDATE o DELETE. Esta opción reemplaza la capacidad predeterminada de actualizar el cursor.  
  
 SCROLL LOCKS  
 Especifica que existan garantías de que las actualizaciones o las cancelaciones posicionadas realizadas a través del cursor se lleven a cabo correctamente. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bloquea las filas mientras se leen en el cursor para garantizar su disponibilidad en modificaciones posteriores. No es posible especificar SCROLL_LOCKS si se incluye también FAST_FORWARD.  
  
 OPTIMISTIC  
 Especifica que las actualizaciones o las cancelaciones posicionadas realizadas a través del cursor no se lleven a cabo correctamente si la fila se ha actualizado desde que se leyó en el cursor. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no bloquea las filas cuando se leen en el cursor. En su lugar, utiliza comparaciones de valores de columna timestamp o un valor de suma de comprobación si la tabla no tiene columnas timestamp, para determinar si la fila se ha modificado después de leerla en el cursor. Si la fila se ha modificado, la actualización o eliminación posicionada fracasa. No es posible especificar OPTIMISTIC si se incluye también FAST_FORWARD.  
  
 TYPE_WARNING  
 Especifica que se envía un mensaje de advertencia al cliente si el cursor se convierte implícitamente del tipo solicitado a otro.  
  
 PARA *select_statement*  
 Es una instrucción SELECT estándar que define el conjunto de resultados del cursor. Las palabras clave FOR BROWSE e INTO no están permitidas dentro de la *select_statement* de una declaración de cursor.  
  
 Si se utilizan DISTINCT, UNION, GROUP BY o HAVING, o una expresión de agregado se incluye en el *select_list*, el cursor se creará como STATIC.  
  
 Si ninguna de las tablas subyacentes tiene un índice único y se solicita un cursor ISO SCROLL o [!INCLUDE[tsql](../../includes/tsql-md.md)] KEYSET, éste será automáticamente un cursor de tipo STATIC.  
  
 Si *select_statement* contiene una cláusula ORDER BY en que las columnas no son identificadores de fila únicos, un cursor dinámico se convierte en cursores KEYSET o en cursores STATIC si no se puede abrir un cursor KEYSET. Lo mismo ocurre en el caso de un cursor definido con la sintaxis ISO, pero sin la palabra clave STATIC.  
  
 READ ONLY  
 Impide que se realicen actualizaciones a través de este cursor. No es posible hacer referencia al cursor en una cláusula WHERE CURRENT OF de una instrucción UPDATE o DELETE. Esta opción reemplaza la capacidad predeterminada de actualizar el cursor. Esta palabra clave varía con respecto a la READ_ONLY anterior en que contiene un espacio en lugar de un carácter de subrayado entre READ y ONLY.  
  
 UPDATE [OF *column_name*[ **,**... *n* ] ]  
 Define las columnas actualizables en el cursor. Si se especifica OF *column_name* [**,**...  *n* ] se proporciona, solo las columnas enumeradas admitirán modificaciones. Si no se especifica ninguna lista, se podrán actualizar todas las columnas, a menos que el cursor se haya definido como READ_ONLY.  
  
## <a name="remarks"></a>Comentarios  
 Después de declarada una variable, ésta se inicializa en NULL. Puede usar la instrucción SET para asignar a una variable declarada un valor distinto de NULL. La instrucción SET que asigna un valor a la variable devuelve un solo valor. Cuando inicialice varias variables, utilice una instrucción SET distinta para cada variable local.  
  
 Las variables solo se pueden utilizar en expresiones y no en lugar de nombres de objeto o palabras clave. Para formar instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] dinámicas, utilice EXECUTE.  
  
 Las reglas de sintaxis de SET **@*** cursor_variable* no incluyen las palabras clave LOCAL y GLOBAL. Cuando el conjunto **@*** cursor_variable* = CURSOR... se utilizan la sintaxis, el cursor se crea como GLOBAL o LOCAL, según la configuración de manera predeterminada para la opción de base de datos de cursor local.  
  
 Las variables de cursor son siempre locales, incluso cuando hacen referencia a un cursor global. Cuando una variable de cursor hace referencia a un cursor global, éste tiene a la vez una referencia de cursor global y otra local. Para obtener más información, vea el ejemplo C.  
  
 Para obtener más información, vea [DECLARE CURSOR &#40; Transact-SQL &#41; ](../../t-sql/language-elements/declare-cursor-transact-sql.md).  
  
 Se puede utilizar el operador de asignación compuesta en cualquier lugar donde haya una asignación con una expresión en el lado derecho del operador, incluso las variables, y un SET en una instrucción UPDATE, SELECT y RECEIVE.  
  
 No use una variable en una instrucción SELECT para concatenar valores (es decir, para calcular valores de agregado). Pueden producirse resultados de consulta inesperados. Esto se debe a que no se garantiza que todas las expresiones de la lista de SELECT (incluidas las asignaciones) se ejecuten exactamente una vez por cada fila de salida. Para obtener más información, consulte [este artículo de KB](http://support.microsoft.com/kb/287515).  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer al rol public. Todos los usuarios pueden usar conjunto **@*** local_variable*.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-printing-the-value-of-a-variable-initialized-by-using-set"></a>A. Imprimir el valor de una variable inicializada con SET  
 En el ejemplo siguiente se crea el `@myvar` variable, coloca un valor de cadena en la variable y se imprime el valor de la `@myvar` variable.  
  
```  
DECLARE @myvar char(20);  
SET @myvar = 'This is a test';  
SELECT @myvar;  
GO  
```  
  
### <a name="b-using-a-local-variable-assigned-a-value-by-using-set-in-a-select-statement"></a>B. Utilizar en una instrucción SELECT una variable local a la que se ha asignado un valor con SET  
 En el ejemplo siguiente se crea una variable local llamada `@state` que después se usa en una instrucción `SELECT` para buscar todos los nombres y apellidos de los empleados residentes en el estado de `Oregon`.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @state char(25);  
SET @state = N'Oregon';  
SELECT RTRIM(FirstName) + ' ' + RTRIM(LastName) AS Name, City  
FROM HumanResources.vEmployee  
WHERE StateProvinceName = @state;  
```  
  
### <a name="c-using-a-compound-assignment-for-a-local-variable"></a>C. Utilizar una asignación compuesta para una variable local  
 Los dos ejemplos los siguientes producen el mismo resultado. Crean una variable local denominada `@NewBalance`, la multiplican por 10 y muestran el nuevo valor de la variable local en una instrucción `SELECT`. El segundo ejemplo utiliza a un operador de asignación compuesta.  
  
```  
/* Example one */  
DECLARE  @NewBalance  int ;  
SET  @NewBalance  =  10;  
SET  @NewBalance  =  @NewBalance  *  10;  
SELECT  @NewBalance;  
  
/* Example Two */  
DECLARE @NewBalance int = 10;  
SET @NewBalance *= 10;  
SELECT @NewBalance;  
```  
  
### <a name="d-using-set-with-a-global-cursor"></a>D. Utilizar SET con un cursor global  
 En el ejemplo siguiente se crea una variable local y después se establece en la variable de cursor el nombre del cursor global.  
  
```  
DECLARE my_cursor CURSOR GLOBAL   
FOR SELECT * FROM Purchasing.ShipMethod  
DECLARE @my_variable CURSOR ;  
SET @my_variable = my_cursor ;   
--There is a GLOBAL cursor declared(my_cursor) and a LOCAL variable  
--(@my_variable) set to the my_cursor cursor.  
DEALLOCATE my_cursor;   
--There is now only a LOCAL variable reference  
--(@my_variable) to the my_cursor cursor.  
```  
  
### <a name="e-defining-a-cursor-by-using-set"></a>E. Definir un cursor con SET  
 En el ejemplo siguiente se usa la instrucción `SET` para definir un cursor.  
  
```  
DECLARE @CursorVar CURSOR;  
  
SET @CursorVar = CURSOR SCROLL DYNAMIC  
FOR  
SELECT LastName, FirstName  
FROM AdventureWorks2012.HumanResources.vEmployee  
WHERE LastName like 'B%';  
  
OPEN @CursorVar;  
  
FETCH NEXT FROM @CursorVar;  
WHILE @@FETCH_STATUS = 0  
BEGIN  
    FETCH NEXT FROM @CursorVar  
END;  
  
CLOSE @CursorVar;  
DEALLOCATE @CursorVar;  
```  
  
### <a name="f-assigning-a-value-from-a-query"></a>F. Asignar un valor desde una consulta  
 En el ejemplo siguiente se utiliza una consulta para asignar un valor a una variable.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @rows int;  
SET @rows = (SELECT COUNT(*) FROM Sales.Customer);  
SELECT @rows;  
```  
  
### <a name="g-assigning-a-value-to-a-user-defined-type-variable-by-modifying-a-property-of-the-type"></a>G. Asignar un valor a una variable de tipo definido por el usuario mediante la modificación de una propiedad del tipo  
 El ejemplo siguiente establece un valor para el tipo definido por el usuario `Point` a través de la modificación del valor de la propiedad `X` del tipo.  
  
```  
DECLARE @p Point;  
SET @p.X = @p.X + 1.1;  
SELECT @p;  
GO  
```  
  
### <a name="h-assigning-a-value-to-a-user-defined-type-variable-by-invoking-a-method-of-the-type"></a>H. Asignar un valor a una variable de tipo definido por el usuario mediante la invocación de un método del tipo  
 En el ejemplo siguiente se establece un valor de tipo definido por el usuario **punto** mediante la invocación de método `SetXY` del tipo.  
  
```  
DECLARE @p Point;  
SET @p=point.SetXY(23.5, 23.5);  
```  
  
### <a name="i-creating-a-variable-for-a-clr-type-and-calling-a-mutator-method"></a>I. Crear una variable para un tipo CLR y llamar a un método mutador  
 En el ejemplo siguiente se crea una variable para el tipo `Point` y, a continuación, se ejecuta un método mutador en `Point`.  
  
```  
CREATE ASSEMBLY mytest from 'c:\test.dll' WITH PERMISSION_SET = SAFE  
CREATE TYPE Point EXTERNAL NAME mytest.Point  
GO  
DECLARE @p Point = CONVERT(Point, '')  
SET @p.SetXY(22, 23);  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="j-printing-the-value-of-a-variable-initialized-by-using-set"></a>J. Imprimir el valor de una variable inicializada con SET  
 En el ejemplo siguiente se crea el `@myvar` variable, coloca un valor de cadena en la variable y se imprime el valor de la `@myvar` variable.  
  
```  
DECLARE @myvar char(20);  
SET @myvar = 'This is a test';  
SELECT top 1 @myvar FROM sys.databases;  
  
```  
  
### <a name="k-using-a-local-variable-assigned-a-value-by-using-set-in-a-select-statement"></a>K. Utilizar en una instrucción SELECT una variable local a la que se ha asignado un valor con SET  
 En el ejemplo siguiente se crea una variable local denominada `@dept` y utiliza esta variable local en un `SELECT` instrucción para buscar los nombres y apellidos de todos los empleados que trabajan en el `Marketing` departamento.  
  
```  
-- Uses AdventureWorks  
  
DECLARE @dept char(25);  
SET @dept = N'Marketing';  
SELECT RTRIM(FirstName) + ' ' + RTRIM(LastName) AS Name  
FROM DimEmployee   
WHERE DepartmentName = @dept;  
```  
  
### <a name="l-using-a-compound-assignment-for-a-local-variable"></a>L. Utilizar una asignación compuesta para una variable local  
 Los dos ejemplos los siguientes producen el mismo resultado. Crean una variable local denominada `@NewBalance`, la multiplican por `10` y muestran el nuevo valor de la variable local en una instrucción `SELECT`. El segundo ejemplo utiliza a un operador de asignación compuesta.  
  
```  
/* Example one */  
DECLARE  @NewBalance  int ;  
SET  @NewBalance  =  10;  
SET  @NewBalance  =  @NewBalance  *  10;  
SELECT  TOP 1 @NewBalance FROM sys.tables;  
  
/* Example Two */  
DECLARE @NewBalance int = 10;  
SET @NewBalance *= 10;  
SELECT TOP 1 @NewBalance FROM sys.tables;  
```  
  
### <a name="m-assigning-a-value-from-a-query"></a>M. Asignar un valor desde una consulta  
 En el ejemplo siguiente se utiliza una consulta para asignar un valor a una variable.  
  
```  
-- Uses AdventureWorks  
  
DECLARE @rows int;  
SET @rows = (SELECT COUNT(*) FROM dbo.DimCustomer);  
SELECT TOP 1 @rows FROM sys.tables;  
```  
  
## <a name="see-also"></a>Vea también  
 [Compuesta operadores &#40; Transact-SQL &#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)   
 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [Instrucciones SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  

