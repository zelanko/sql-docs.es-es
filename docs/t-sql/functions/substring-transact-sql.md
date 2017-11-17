---
title: SUBSTRING (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 10/21/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SUBSTRING
- SUBSTRING_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- portion of expression returned [SQL Server]
- part of expression returned [SQL Server]
- SUBSTRING function
- offsets [SQL Server]
- binary [SQL Server], returning part of
- expressions [SQL Server], part returned
- characters [SQL Server], returning part of
ms.assetid: a19c808f-aaf9-4a69-af59-b1a5fc3e5c4c
caps.latest.revision: 65
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7f36ec82c65e5d52c2186c67033adddbf1700c4d
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="substring-transact-sql"></a>SUBSTRING (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve parte de una expresión de caracteres, binaria, de texto o de imagen en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
SUBSTRING ( expression ,start , length )  
```  
  
## <a name="arguments"></a>Argumentos  
 *expression*  
 Es un **caracteres**, **binario**, **texto**, **ntext**, o **imagen**[expresión](../../t-sql/language-elements/expressions-transact-sql.md).  
  
 *Inicio*  
 Es un entero o **bigint** expresión que especifica dónde comienzan los caracteres devueltos. (La numeración es 1 significado en función, que el primer carácter de la expresión es 1). Si *iniciar* es menor que 1, la expresión devuelta comenzará en el primer carácter que se especifica en *expresión*. En este caso, el número de caracteres que se devuelve es el mayor valor de la suma de *iniciar* + *longitud*– 1 o 0. Si *iniciar* es mayor que el número de caracteres de la expresión de valor, se devuelve una expresión de longitud cero.  
  
 *length*  
 Es un entero positivo o **bigint** expresión que especifica cuántos caracteres de la *expresión* se devolverá. Si *longitud* es negativo, se genera un error y finaliza la instrucción. Si la suma de *iniciar* y *longitud* es mayor que el número de caracteres en *expresión*, la expresión de conjunto de valores comenzando en *iniciar*se devuelve.  
  
## <a name="return-types"></a>Tipos devueltos  
 Devuelve datos de caracteres si *expresión* es uno de los tipos de datos de caracteres admitidos. Devuelve datos binarios si *expresión* es uno de los admitidos **binario** tipos de datos. La cadena devuelta es del mismo tipo que la expresión indicada, con las excepciones mostradas en la tabla:  
  
|Expresión especificada|Tipo de valor devuelto|  
|--------------------------|-----------------|  
|**char**/**varchar**/**texto**|**varchar**|  
|**nchar**/**nvarchar**/**ntext**|**nvarchar**|  
|**binario**/**varbinary**/**imagen**|**varbinary**|  
  
## <a name="remarks"></a>Comentarios  
 Los valores de *iniciar* y *longitud* debe especificarse en el número de caracteres de **ntext**, **char**, o **varchar**  tipos de datos y los bytes de **texto**, **imagen**, **binario**, o **varbinary** tipos de datos.  
  
 El *expresión* debe ser **varchar (max)** o **varbinary (max)** cuando el *iniciar* o *longitud* contiene un valor mayor que 2147483647.  
  
## <a name="supplementary-characters-surrogate-pairs"></a>Caracteres adicionales (pares suplentes)  
 Al utilizar intercalaciones de caracteres suplementarios (SC), ambos *iniciar* y *longitud* contarán cada par suplente *expresión* como un único carácter. Para más información, consulte [Compatibilidad con la intercalación y Unicode](../../relational-databases/collations/collation-and-unicode-support.md).  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-substring-with-a-character-string"></a>A. Usar SUBSTRING con una cadena de caracteres  
 En el siguiente ejemplo se muestra cómo devolver únicamente una parte de una cadena de caracteres. Desde el `sys.databases` tabla, esta consulta devuelve el sistema de nombres de base de datos en la primera columna, la primera letra de la base de datos en la segunda columna y el terceros y cuarto caracteres en la última columna.  
  
```  
SELECT name, SUBSTRING(name, 1, 1) AS Initial ,
SUBSTRING(name, 3, 2) AS ThirdAndFourthCharacters
FROM sys.databases  
WHERE database_id < 5;   
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  

|name |Initial |ThirdAndFourthCharacters|
|---|--|--|
|maestra  |m  |St |
|tempdb  |t  |módulo de administración |
|model   |m  |de |
|msdb    |m  |base de datos |


  
 He aquí cómo mostrar el segundo, tercer y cuarto caracteres de la constante de cadena `abcdef`.  
  
```  
SELECT x = SUBSTRING('abcdef', 2, 3);  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
x  
----------  
bcd  
  
(1 row(s) affected)
```  
  
### <a name="b-using-substring-with-text-ntext-and-image-data"></a>B. Usar SUBSTRING con datos de tipo text, ntext e image  
  
> [!NOTE]  
>  Para ejecutar los ejemplos siguientes, debe instalar la **pubs** base de datos.  
  
 En el ejemplo siguiente se muestra cómo devolver los 10 primeros caracteres de cada uno de un **texto** y **imagen** columna de datos en el `pub_info` tabla de la `pubs` base de datos. **texto** datos se devuelven como **varchar**, y **imagen** datos se devuelven como **varbinary**.  
  
```  
USE pubs;  
SELECT pub_id, SUBSTRING(logo, 1, 10) AS logo,   
   SUBSTRING(pr_info, 1, 10) AS pr_info  
FROM pub_info  
WHERE pub_id = '1756';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 pub_id logo    pr_info
------ ---------------------- ----------
1756   0x474946383961E3002500 This is sa

(1 row(s) affected)
```  
  
 En el ejemplo siguiente se muestra el efecto de SUBSTRING en ambos **texto** y **ntext** datos. En primer lugar, este ejemplo crea una nueva tabla en la base de datos `pubs` denominada `npub_info`. En segundo lugar, crea la columna `pr_info` en la tabla `npub_info` a partir de los primeros 80 caracteres de la columna `pub_info.pr_info` y agrega una `ü` como primer carácter. Por último, un `INNER JOIN` recupera todos los números de identificación de publicador y el `SUBSTRING` de ambos el **texto** y **ntext** columnas de información de publicador.  
  
```  
IF EXISTS (SELECT table_name FROM INFORMATION_SCHEMA.TABLES   
      WHERE table_name = 'npub_info')  
   DROP TABLE npub_info;  
GO  
-- Create npub_info table in pubs database. Borrowed from instpubs.sql.  
USE pubs;  
GO  
CREATE TABLE npub_info  
(  
 pub_id char(4) NOT NULL  
    REFERENCES publishers(pub_id)  
    CONSTRAINT UPKCL_npubinfo PRIMARY KEY CLUSTERED,  
pr_info ntext NULL  
);  
  
GO  
  
-- Fill the pr_info column in npub_info with international data.  
RAISERROR('Now at the inserts to pub_info...',0,1);  
  
GO  
  
INSERT npub_info VALUES('0736', N'üThis is sample text data for New Moon Books, publisher 0736 in the pubs database')  
,('0877', N'üThis is sample text data for Binnet & Hardley, publisher 0877 in the pubs databa')  
,('1389', N'üThis is sample text data for Algodata Infosystems, publisher 1389 in the pubs da')  
,('9952', N'üThis is sample text data for Scootney Books, publisher 9952 in the pubs database')  
,('1622', N'üThis is sample text data for Five Lakes Publishing, publisher 1622 in the pubs d')  
,('1756', N'üThis is sample text data for Ramona Publishers, publisher 1756 in the pubs datab')  
,('9901', N'üThis is sample text data for GGG&G, publisher 9901 in the pubs database. GGG&G i')  
,('9999', N'üThis is sample text data for Lucerne Publishing, publisher 9999 in the pubs data');  
GO  
-- Join between npub_info and pub_info on pub_id.  
SELECT pr.pub_id, SUBSTRING(pr.pr_info, 1, 35) AS pr_info,  
   SUBSTRING(npr.pr_info, 1, 35) AS npr_info  
FROM pub_info pr INNER JOIN npub_info npr  
   ON pr.pub_id = npr.pub_id  
ORDER BY pr.pub_id ASC;  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-substring-with-a-character-string"></a>C. Usar SUBSTRING con una cadena de caracteres  
 En el siguiente ejemplo se muestra cómo devolver únicamente una parte de una cadena de caracteres. En la tabla `dbo.DimEmployee`, esta consulta devuelve el apellido en una columna y solo la primera inicial en la segunda columna.  
  
```  
-- Uses AdventureWorks  
  
SELECT LastName, SUBSTRING(FirstName, 1, 1) AS Initial  
FROM dbo.DimEmployee  
WHERE LastName LIKE 'Bar%'  
ORDER BY LastName;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
LastName             Initial
-------------------- -------
Barbariol            A
Barber               D
Barreto de Mattos    P
```  
  
 En el ejemplo siguiente se muestra cómo devolver el segundo, tercer y cuarto caracteres de la constante de cadena `abcdef`.  
  
```  
USE ssawPDW;  
  
SELECT TOP 1 SUBSTRING('abcdef', 2, 3) AS x FROM dbo.DimCustomer;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
x
-----
bcd
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones de cadena &#40; Transact-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  



