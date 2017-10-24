---
title: Al igual que (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ESCAPE
- LIKE
- ESCAPE_TSQL
- LIKE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ESCAPE keyword
- '% (wildcard - character(s) to match)'
- ASCII pattern matching
- pattern searching [SQL Server]
- wildcard characters [SQL Server]
- literals [SQL Server], using wildcards
- character strings [SQL Server], LIKE
- exact matches [SQL Server]
- Boolean functions
- LIKE comparisons
- matching patterns [SQL Server]
- NOT LIKE keyword
ms.assetid: 581fb289-29f9-412b-869c-18d33a9e93d5
caps.latest.revision: 50
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: 07a8bb8b08120f08cd54e42dcd332459544c206d
ms.contentlocale: es-es
ms.lasthandoff: 10/24/2017

---
# <a name="like-transact-sql"></a>LIKE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Determina si una cadena de caracteres específica coincide con un patrón especificado. Un patrón puede contener caracteres normales y caracteres comodín. Durante la operación de búsqueda de coincidencias de patrón, los caracteres normales deben coincidir exactamente con los caracteres especificados en la cadena de caracteres. Sin embargo, los caracteres comodín pueden coincidir con fragmentos arbitrarios de la cadena. El uso de caracteres comodín hace que el operador LIKE sea más flexible que los operadores de comparación de cadenas = y !=. Si alguno de los argumentos no es del tipo de datos de cadena de caracteres, [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] lo convierte al tipo de datos de cadena de caracteres, si es posible.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
match_expression [ NOT ] LIKE pattern [ ESCAPE escape_character ]  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
match_expression [ NOT ] LIKE pattern  
```  
  
## <a name="arguments"></a>Argumentos  
 *match_expression*  
 Se trata de cualquier [expresión](../../t-sql/language-elements/expressions-transact-sql.md) del tipo de datos de caracteres.  
  
 *patrón*  
 Es la cadena de caracteres que se va a buscar en específica *match_expression*y pueden incluir los siguientes caracteres comodín válidos. *patrón de* puede tener un máximo de 8.000 bytes.  
  
|Carácter comodín|Description|Ejemplo|  
|------------------------|-----------------|-------------|  
|%|Cualquier cadena de cero o más caracteres.|WHERE title LIKE '%computer%' busca todos los títulos de libros que contengan la palabra 'computer' en el título.|  
|_ (carácter de subrayado)|Cualquier carácter individual.|WHERE au_fname LIKE ‘_ean’ busca todos los nombres de cuatro letras que terminen en ean (Dean, Sean, etc.)|  
|[ ]|Cualquier carácter individual del intervalo ([a-f]) o del conjunto ([abcdef]) que se ha especificado.|WHERE au_lname LIKE ‘[C-P]arsen’ busca apellidos de autores que terminen en arsen y empiecen por cualquier carácter individual entre C y P, como Carsen, Larsen, Karsen, etc. En las búsquedas de intervalos, los caracteres incluidos en el intervalo pueden variar, dependiendo de las reglas de ordenación de la intercalación.|  
|[^]|Cualquier carácter individual que no se encuentre en el intervalo ([^a-f]) o el conjunto ([^abcdef]) que se ha especificado.|WHERE au_lname LIKE ‘de[^l]%’ busca todos los apellidos de autores que empiecen por de y en los que la siguiente letra no sea l.|  
  
 *escape_character*  
 Es un carácter que se coloca delante de un carácter comodín para indicar que el comodín no debe interpretarse como un comodín, sino como un carácter normal. *escape_character* es una expresión de caracteres que no tiene valor predeterminado y se debe evaluar como un único carácter.  
  
## <a name="result-types"></a>Tipos de resultado  
 **Boolean**  
  
## <a name="result-value"></a>Valor de resultado  
 LIKE devuelve TRUE si el *match_expression* coincide con la que se especifica *patrón*.  
  
## <a name="remarks"></a>Comentarios  
 Cuando se realizan comparaciones de cadenas con LIKE, todos los caracteres de la cadena patrón son significativos, incluso los espacios iniciales o finales. Si una comparación de una consulta debe devolver todas las filas con una cadena LIKE 'abc ' (abc seguido de un espacio), no se devolverán las filas en las que el valor de esa columna sea abc (sin espacio al final). Sin embargo, no se tienen en cuenta los espacios en blanco finales de la expresión con la que se compara el patrón. Si la comparación de una consulta debe devolver todas las filas con la cadena LIKE 'abc' (abc sin espacio), se devolverán todas las filas que empiecen por abc y tengan cero o más espacios al final.  
  
 Una comparación de cadenas con un patrón que contenga **char** y **varchar** datos pueden no pasar una comparación LIKE debido a cómo se almacenan los datos. Es importante conocer el almacenamiento de cada tipo de datos y dónde puede generar errores una comparación LIKE. En el ejemplo siguiente se pasa una variable local **char** variable a un procedimiento almacenado y, a continuación, para encontrar todos los empleados cuyo apellidos empiecen por un conjunto especificado de caracteres de coincidencia de patrón de usos.  
  
```tsql
-- Uses AdventureWorks  
  
CREATE PROCEDURE FindEmployee @EmpLName char(20)  
AS  
SELECT @EmpLName = RTRIM(@EmpLName) + '%';  
SELECT p.FirstName, p.LastName, a.City  
FROM Person.Person p JOIN Person.Address a ON p.BusinessEntityID = a.AddressID  
WHERE p.LastName LIKE @EmpLName;  
GO  
EXEC FindEmployee @EmpLName = 'Barb';  
GO  
```  
  
 En el `FindEmployee` procedimiento, no se devuelven filas porque la **char** variable (`@EmpLName`) contiene espacios en blanco finales siempre que el nombre contiene menos de 20 caracteres. Dado que la `LastName` columna es **varchar**, no hay espacios en blanco finales. Este procedimiento no funciona porque los espacios al final son significativos.  
  
 Sin embargo, en el ejemplo siguiente se realiza correctamente porque los espacios en blanco no se agregan a un **varchar** variable.  
  
```tsql
-- Uses AdventureWorks  
  
CREATE PROCEDURE FindEmployee @EmpLName varchar(20)  
AS  
SELECT @EmpLName = RTRIM(@EmpLName) + '%';  
SELECT p.FirstName, p.LastName, a.City  
FROM Person.Person p JOIN Person.Address a ON p.BusinessEntityID = a.AddressID  
WHERE p.LastName LIKE @EmpLName;  
GO  
EXEC FindEmployee @EmpLName = 'Barb';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 FirstName      LastName            City
 ----------     -------------------- --------------- 
 Angela         Barbariol            Snohomish
 David          Barber               Snohomish
 (2 row(s) affected)  
 ``` 
 
## <a name="pattern-matching-by-using-like"></a>Operación de búsqueda de coincidencias de patrón con LIKE  
 LIKE admite operaciones de búsqueda de coincidencias de patrón ASCII y Unicode. Cuando todos los argumentos (*match_expression*, *patrón*, y *escape_character*, si está presente) son tipos de datos de caracteres ASCII, se realiza la búsqueda de coincidencias de patrón ASCII. Si alguno de los argumentos es del tipo de datos Unicode, todos los argumentos se convierten a Unicode y se realiza la operación de búsqueda de coincidencias de patrón Unicode. Cuando se utilizan datos Unicode (**nchar** o **nvarchar** tipos de datos) con LIKE, los espacios en blanco finales son significativos; sin embargo, para los datos no Unicode, los espacios en blanco no son significativos. El uso que se hace de LIKE con Unicode es compatible con el estándar ISO. El uso que se hace de LIKE con ASCII es compatible con las versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 A continuación se ofrece una serie de ejemplos donde se muestran las diferencias entre las filas devueltas tras la operación de búsqueda de coincidencias de patrón con LIKE para ASCII y Unicode.  
  
```tsql  
-- ASCII pattern matching with char column  
CREATE TABLE t (col1 char(30));  
INSERT INTO t VALUES ('Robert King');  
SELECT *   
FROM t   
WHERE col1 LIKE '% King';   -- returns 1 row  
  
-- Unicode pattern matching with nchar column  
CREATE TABLE t (col1 nchar(30));  
INSERT INTO t VALUES ('Robert King');  
SELECT *   
FROM t   
WHERE col1 LIKE '% King';   -- no rows returned  
  
-- Unicode pattern matching with nchar column and RTRIM  
CREATE TABLE t (col1 nchar (30));  
INSERT INTO t VALUES ('Robert King');  
SELECT *   
FROM t   
WHERE RTRIM(col1) LIKE '% King';   -- returns 1 row  
```  
  
> [!NOTE]  
>  La intercalación influye en las comparaciones con LIKE. Para obtener más información, vea [COLLATE &#40;Transact-SQL&#41;](~/t-sql/statements/collations.md).  
  
## <a name="using-the--wildcard-character"></a>Utilizar el carácter comodín %  
 Si se especifica el símbolo LIKE '5%', el [!INCLUDE[ssDE](../../includes/ssde-md.md)] busca el número 5 seguido de cualquier cadena de cero o más caracteres.  
  
 Por ejemplo, la siguiente consulta muestra todas las vistas de administración dinámica de la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)], porque todas empiezan por las letras `dm`.  
  
```tsql  
-- Uses AdventureWorks  
  
SELECT Name  
FROM sys.system_views  
WHERE Name LIKE 'dm%';  
GO  
```  
  
 Para ver todos los objetos que no sean vistas de administración dinámica, utilice `NOT LIKE 'dm%'`. Si hay un total de 32 objetos y LIKE encuentra 13 nombres que coinciden con el patrón, NOT LIKE encuentra los 19 objetos que no coinciden con el patrón de LIKE.  
  
 Es posible que no siempre se encuentren los mismos nombres con un patrón como `LIKE '[^d][^m]%'`. En lugar de 19 nombres, puede que encuentre solo 14, quedando eliminados de los resultados todos los nombres que empiecen por `d` o tengan `m` como segunda letra, y los nombres de las vistas de administración dinámica. Esto se debe a que las cadenas de comparación con caracteres comodín negativos se evalúan por pasos, un comodín cada vez. Si la coincidencia genera un error en algún momento de la evaluación, se elimina.  
  
## <a name="using-wildcard-characters-as-literals"></a>Utilizar caracteres comodín como literales  
 Los caracteres comodín que se utilizan en la operación de búsqueda de coincidencias de patrón se pueden utilizar como literales. Para utilizar un carácter comodín como literal, inclúyalo entre corchetes. La tabla siguiente muestra varios ejemplos del uso de la palabra clave LIKE y los caracteres comodín [ ].  
  
|Símbolo|Significado|  
|------------|-------------|  
|LIKE ‘5[%]’|5 %|  
|LIKE ‘[_]n’|_N|  
|LIKE ‘[a-cdf]’|a, b, c, d o f|  
|LIKE ‘[-acdf]’|-, a, c, d o f|  
|LIKE ‘[ [ ]’|[|  
|LIKE ']'|]|  
|LIKE 'abc[_]d%'|abc_d y abc_de|  
|LIKE 'abc[def]'|abcd, abce y abcf|  
  
## <a name="pattern-matching-with-the-escape-clause"></a>Operación de búsqueda de coincidencias de patrón con la cláusula ESCAPE  
 Se pueden buscar cadenas de caracteres que incluyan uno o más caracteres comodín especiales. Por ejemplo, la tabla discounts de una base de datos customers puede almacenar valores de descuento que incluyan un signo de porcentaje (%). Para buscar el signo de porcentaje como carácter en lugar de como carácter comodín, deben suministrarse la palabra clave ESCAPE y el carácter de escape. Supongamos que una base de datos de ejemplo contiene una columna denominada comment que contiene el texto 30%. Para buscar filas que contengan la cadena 30% en cualquier parte de la columna de comentarios, especifique una cláusula WHERE como esta: `WHERE comment LIKE '%30!%%' ESCAPE '!'`. Si no se especifican ESCAPE y el carácter de escape, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] devolverá las filas con la cadena 30.  
  
 Si no hay ningún carácter después de un carácter de escape en el patrón de LIKE, el patrón no es válido y LIKE devuelve FALSE. Si el carácter posterior a un carácter de escape no es un carácter comodín, el carácter de escape se descarta y el carácter que sigue al escape se trata como un carácter normal del patrón. Esto afecta a los caracteres comodín del signo de porcentaje (%), carácter de subrayado (_) y corchete de apertura ([) cuando se encuentran entre corchetes dobles ([ ]). Asimismo, dentro de corchetes dobles ([ ]) se pueden aplicar caracteres de escape al símbolo de intercalación (^), guión (-) y corchete de cierre (]).  
  
 0 x 0000 (**char(0)**) es un carácter no definido en las intercalaciones de Windows y no se pueden incluir en LIKE.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-like-with-the--wildcard-character"></a>A. Utilizar LIKE con el carácter comodín %  
 En el siguiente ejemplo se buscan todos los números de teléfono de la tabla `415` cuyo código de área sea `PersonPhone`.  
  
```tsql  
-- Uses AdventureWorks  
  
SELECT p.FirstName, p.LastName, ph.PhoneNumber  
FROM Person.PersonPhone AS ph  
INNER JOIN Person.Person AS p  
ON ph.BusinessEntityID = p.BusinessEntityID  
WHERE ph.PhoneNumber LIKE '415%'  
ORDER by p.LastName;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
 
 ```
 FirstName             LastName             Phone
 -----------------     -------------------  ------------
 Ruben                 Alonso               415-555-124  
 Shelby                Cook                 415-555-0121  
 Karen                 Hu                   415-555-0114  
 John                  Long                 415-555-0147  
 David                 Long                 415-555-0123  
 Gilbert               Ma                   415-555-0138  
 Meredith              Moreno               415-555-0131  
 Alexandra             Nelson               415-555-0174  
 Taylor                Patterson            415-555-0170  
 Gabrielle              Russell             415-555-0197  
 Dalton                 Simmons             415-555-0115  
 (11 row(s) affected)  
 ``` 
 
### <a name="b-using-not-like-with-the--wildcard-character"></a>B. Utilizar NOT LIKE con el carácter comodín %  
 En el siguiente ejemplo se buscan todos los números de teléfono de la tabla `PersonPhone` cuyos códigos de área no sean `415`.  
  
```tsql  
-- Uses AdventureWorks  
  
SELECT p.FirstName, p.LastName, ph.PhoneNumber  
FROM Person.PersonPhone AS ph  
INNER JOIN Person.Person AS p  
ON ph.BusinessEntityID = p.BusinessEntityID  
WHERE ph.PhoneNumber NOT LIKE '415%' AND p.FirstName = 'Gail'  
ORDER BY p.LastName;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
 
 ```
FirstName              LastName            Phone
---------------------- -------------------- -------------------
Gail                  Alexander            1 (11) 500 555-0120  
Gail                  Butler               1 (11) 500 555-0191  
Gail                  Erickson             834-555-0132  
Gail                  Erickson             849-555-0139  
Gail                  Griffin              450-555-0171  
Gail                  Moore                155-555-0169  
Gail                  Russell              334-555-0170  
Gail                  Westover             305-555-0100  
(8 row(s) affected)  
```  

### <a name="c-using-the-escape-clause"></a>C. Utilizar la cláusula ESCAPE  
 En el ejemplo siguiente se utiliza la cláusula `ESCAPE` y el carácter de escape para buscar exactamente la cadena de caracteres `10-15%` en la columna `c1` de la tabla `mytbl2`.  
  
```tsql
USE tempdb;  
GO  
IF EXISTS(SELECT TABLE_NAME FROM INFORMATION_SCHEMA.TABLES  
      WHERE TABLE_NAME = 'mytbl2')  
   DROP TABLE mytbl2;  
GO  
USE tempdb;  
GO  
CREATE TABLE mytbl2  
(  
 c1 sysname  
);  
GO  
INSERT mytbl2 VALUES ('Discount is 10-15% off'), ('Discount is .10-.15 off');  
GO  
SELECT c1   
FROM mytbl2  
WHERE c1 LIKE '%10-15!% off%' ESCAPE '!';  
GO  
```  
  
### <a name="d-using-the---wildcard-characters"></a>D. Utilizar el carácter comodín [ ]  
 El ejemplo siguiente busca empleados en la `Person` tabla con el nombre de `Cheryl` o `Sheryl`.  
  
```tsql  
-- Uses AdventureWorks  
  
SELECT BusinessEntityID, FirstName, LastName   
FROM Person.Person   
WHERE FirstName LIKE '[CS]heryl';  
GO  
```  
  
 En el siguiente ejemplo se buscan las filas con empleados en la tabla `Person` con el apellido de `Zheng` o `Zhang`.  
  
```tsql  
-- Uses AdventureWorks  
  
SELECT LastName, FirstName  
FROM Person.Person  
WHERE LastName LIKE 'Zh[ae]ng'  
ORDER BY LastName ASC, FirstName ASC;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-using-like-with-the--wildcard-character"></a>E. Utilizar LIKE con el carácter comodín %  
 En el ejemplo siguiente se buscan todos los empleados en la `DimEmployee` tabla con números de teléfono que comiencen por `612`.  
  
```tsql  
-- Uses AdventureWorks  
  
SELECT FirstName, LastName, Phone  
FROM DimEmployee  
WHERE phone LIKE '612%'  
ORDER by LastName;  
```  
  
### <a name="f-using-not-like-with-the--wildcard-character"></a>F. Utilizar NOT LIKE con el carácter comodín %  
 En el ejemplo siguiente se busca todos los números de teléfono en el `DimEmployee` tabla que no se inician con `612`.  .  
  
```tsql  
-- Uses AdventureWorks  
  
SELECT FirstName, LastName, Phone  
FROM DimEmployee  
WHERE phone NOT LIKE '612%'  
ORDER by LastName;  
```  
  
### <a name="g-using-like-with-the--wildcard-character"></a>G. Utilizar LIKE con el carácter comodín _  
 En el ejemplo siguiente se busca todos los números de teléfono que tienen un código de área a partir de `6` y finales de `2` en el `DimEmployee` tabla. Tenga en cuenta que el carácter comodín % también se incluye al final del patrón de búsqueda, ya que el código de área es la primera parte del número de teléfono y existan los caracteres adicionales después del valor de columna.  
  
```tsql  
-- Uses AdventureWorks  
  
SELECT FirstName, LastName, Phone  
FROM DimEmployee  
WHERE phone LIKE '6_2%'  
ORDER by LastName;   
```  
  
## <a name="see-also"></a>Vea también  
 [Expresiones &#40; Transact-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Funciones integradas &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [DONDE &#40; Transact-SQL &#41;](../../t-sql/queries/where-transact-sql.md)  
 

