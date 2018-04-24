---
title: CONCAT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CONCAT
- CONCAT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CONCAT function
ms.assetid: fce5a8d4-283b-4c47-95e5-4946402550d5
caps.latest.revision: 22
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 71f52ba08f2fd5fe94af4b16dbcac06746564e09
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="concat-transact-sql"></a>CONCAT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

Devuelve una cadena que es el resultado de concatenar dos o más valores de cadena. (Para agregar un valor de separación durante la concatenación, vea [CONCAT_WS](../../t-sql/functions/concat-ws-transact-sql.md)).
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
CONCAT ( string_value1, string_value2 [, string_valueN ] )  
```  
  
## <a name="arguments"></a>Argumentos  
*string_value*  
Valor de cadena que se va a concatenar con los demás valores.
  
## <a name="return-types"></a>Tipos de valores devueltos
Cadena cuyo tipo y longitud dependen de la entrada.
  
## <a name="remarks"></a>Notas  
**CONCAT** toma un número variable de argumentos de cadena y los concatena en una sola cadena. Necesita un mínimo de dos valores de entrada; de lo contrario, se produce un error. Todos los argumentos se convierten implícitamente a tipos string y después se concatenan. Los valores NULL se convierten implícitamente a una cadena vacía. Si todos los argumentos son NULL, se devuelve una cadena vacía de tipo **varchar**(1). La conversión implícita de cadenas sigue las reglas existentes para las conversiones de tipos de datos. Para más información sobre las conversiones de tipo de datos, vea [CAST y CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md).
  
El tipo devuelto depende del tipo de los argumentos. En la tabla siguiente se muestra la asignación.
  
|Tipo de entrada|Tipo de salida y longitud de datos|  
|---|---|
|Si cualquier argumento es un tipo de sistema SQL-CLR, SQL-CLR UDT o `nvarchar(max)`|**nvarchar(max)**|  
|De lo contrario, si algún argumento es **varbinary(max)** o **varchar(max)**|**varchar(max)** a menos que uno de los parámetros sea un **nvarchar** de cualquier longitud. En tal caso, el resultado es de tipo **nvarchar(max)**.|  
|De lo contrario, si algún argumento es de tipo **nvarchar**(<= 4000)|**nvarchar**(<= 4000)|  
|De lo contrario, en todos los demás casos|**varchar**(<= 8000) a menos que uno de los parámetros sea un nvarchar de cualquier longitud. En tal caso, el resultado es de tipo **nvarchar(max)**.|  
  
Cuando los argumentos son <= 4000 para **nvarchar**, o <= 8000 para **varchar**, las conversiones implícitas pueden afectar a la longitud del resultado. Otros tipos de datos tienen distintas longitudes cuando se convierten implícitamente a cadenas. Por ejemplo, un tipo **int** (14) tiene una longitud de cadena de 12, mientras que un tipo **float** tiene una longitud de 32. Por tanto, el resultado de concatenar dos enteros tiene una longitud no menor que 24.
  
Si ninguno de los argumentos de entrada es de un tipo de objeto grande (LOB) admitido, el tipo devuelto se trunca a una longitud de 8000, independientemente del tipo de valor devuelto. Este truncamiento ahorra espacio y admite eficacia en la generación del plan.
  
La función CONCAT se puede ejecutar de forma remota en un servidor vinculado que tenga la versión [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] o versiones posteriores. Para servidores vinculados anteriores, la operación de CONCAT se realizará localmente después de que se devuelvan los valores no concatenados desde el servidor vinculado.
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-concat"></a>A. Usar CONCAT  
  
```sql
SELECT CONCAT ( 'Happy ', 'Birthday ', 11, '/', '25' ) AS Result;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result  
-------------------------  
Happy Birthday 11/25  
  
(1 row(s) affected)  
```  
  
### <a name="b-using-concat-with-null-values"></a>B. Usar CONCAT con valores NULL  
  
```sql
CREATE TABLE #temp (  
    emp_name nvarchar(200) NOT NULL,  
    emp_middlename nvarchar(200) NULL,  
    emp_lastname nvarchar(200) NOT NULL  
);  
INSERT INTO #temp VALUES( 'Name', NULL, 'Lastname' );  
SELECT CONCAT( emp_name, emp_middlename, emp_lastname ) AS Result  
FROM #temp;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result  
------------------  
NameLastname  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Vea también
 [CONCAT_WS &#40;Transact-SQL&#41;](../../t-sql/functions/concat-ws-transact-sql.md)   
 [FORMATMESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/formatmessage-transact-sql.md)  
 [QUOTENAME &#40;Transact-SQL&#41;](../../t-sql/functions/quotename-transact-sql.md)  
 [REPLACE &#40;Transact-SQL&#41;](../../t-sql/functions/replace-transact-sql.md)  
 [REVERSE &#40;Transact-SQL&#41;](../../t-sql/functions/reverse-transact-sql.md)  
 [STRING_AGG &#40;Transact-SQL&#41;](../../t-sql/functions/string-agg-transact-sql.md)  
 [STRING_ESCAPE &#40;Transact-SQL&#41;](../../t-sql/functions/string-escape-transact-sql.md)  
 [STUFF &#40;Transact-SQL&#41;](../../t-sql/functions/stuff-transact-sql.md)  
 [TRANSLATE &#40;Transact-SQL&#41;](../../t-sql/functions/translate-transact-sql.md)  
 [Funciones de cadena &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  


