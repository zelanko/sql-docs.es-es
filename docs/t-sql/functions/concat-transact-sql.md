---
title: CONCAT (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 07/24/2017
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
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: 046278bb3016b39df8039a1450a58b177d2bc180
ms.contentlocale: es-es
ms.lasthandoff: 10/17/2017

---
# <a name="concat-transact-sql"></a>CONCAT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

Devuelve una cadena que es el resultado de concatenar dos o más valores de cadena. (Para agregar un valor de separación durante la concatenación, consulte [CONCAT_WS](../../t-sql/functions/concat-ws-transact-sql.md).)
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
CONCAT ( string_value1, string_value2 [, string_valueN ] )  
```  
  
## <a name="arguments"></a>Argumentos  
*valor_cadena*  
Valor de cadena que se va a concatenar con los demás valores.
  
## <a name="return-types"></a>Tipos de valor devuelto
Cadena cuyo tipo y longitud dependen de la entrada.
  
## <a name="remarks"></a>Comentarios  
**CONCAT** toma un número variable de argumentos de cadena y los concatena en una sola cadena. Necesita un mínimo de dos valores de entrada; de lo contrario, se produce un error. Todos los argumentos se convierten implícitamente a tipos string y después se concatenan. Los valores NULL se convierten implícitamente a una cadena vacía. Si todos los argumentos son null, una cadena vacía de tipo **varchar**(1) se devuelve. La conversión implícita de cadenas sigue las reglas existentes para las conversiones de tipos de datos. Para obtener más información acerca de las conversiones de tipo de datos, vea [CAST y CONVERT &#40; Transact-SQL &#41; ](../../t-sql/functions/cast-and-convert-transact-sql.md).
  
El tipo devuelto depende del tipo de los argumentos. En la tabla siguiente se muestra la asignación.
  
|Tipo de entrada|Tipo de salida y longitud de datos|  
|---|---|
|Si cualquier argumento es un tipo de sistema SQL-CLR, SQL-CLR UDT o `nvarchar(max)`|**nvarchar(max)**|  
|En caso contrario, si algún argumento es **varbinary (max)** o **varchar (max)**|**varchar (max)** a menos que uno de los parámetros sea un **nvarchar** de cualquier longitud. Si es así, a continuación, el resultado es **nvarchar (max)**.|  
|En caso contrario, si algún argumento es **nvarchar**(< = 4000)|**nvarchar**(< = 4000)|  
|De lo contrario, en todos los demás casos|**varchar**(< = 8000) a menos que uno de los parámetros sea un nvarchar de cualquier longitud. Si es así, a continuación, el resultado es **nvarchar (max)**.|  
  
Cuando los argumentos son < = 4000 para **nvarchar**, o < = 8000 para **varchar**, las conversiones implícitas pueden afectar a la longitud del resultado. Otros tipos de datos tienen distintas longitudes cuando se convierten implícitamente a cadenas. Por ejemplo, un **int** (14) tiene una longitud de cadena de 12, mientras que un **float** tiene una longitud de 32. Por tanto, el resultado de concatenar dos enteros tiene una longitud no menor que 24.
  
Si ninguno de los argumentos de entrada es de un tipo de objeto grande (LOB) admitido, el tipo devuelto se trunca a una longitud de 8000, independientemente del tipo de valor devuelto. Este truncamiento ahorra espacio y admite eficacia en la generación del plan.
  
CONCAT (función) se puede ejecutar de forma remota en un servidor vinculado que es la versión [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y versiones posteriores. Para los servidores vinculados anteriores, la operación de CONCAT se realizará localmente después de que los valores concatenados no se devuelven desde el servidor vinculado.
  
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
[Funciones de cadena (Transact-SQL)](../../t-sql/functions/string-functions-transact-sql.md)  
[CONCAT_WS (Transact-SQL)](../../t-sql/functions/concat-ws-transact-sql.md)   
  



