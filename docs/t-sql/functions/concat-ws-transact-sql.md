---
title: CONCAT_WS (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- CONCAT_WS
- CONCAT_WS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CONCAT_WS function
ms.assetid: f1375fd7-a2fd-48bf-922a-4f778f0deb1f
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 7d7932c1887c82b2a10702f9054706e4cf9bce71
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/18/2018
---
# <a name="concatws-transact-sql"></a>CONCAT_WS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

Concatena un número variable de argumentos con un delimitador especificado en el argumento 1. (`CONCAT_WS` indica *concatenar con separador*.)

##  <a name="syntax"></a>Sintaxis   
```sql
CONCAT_WS ( separator, argument1, argument1 [, argumentN]… ) 
```

## <a name="arguments"></a>Argumentos   
separador  
Es una expresión de cualquier tipo de caracteres (`nvarchar`, `varchar`, `nchar`, o `char`).

argumento1, argumento2, argumento*N*  
Es una expresión de cualquier tipo.

## <a name="return-types"></a>Tipos de valor devuelto
: cadena. El tipo y longitud dependen de la entrada.

## <a name="remarks"></a>Comentarios   
`CONCAT_WS`toma un número variable de argumentos y los concatena en una sola cadena con el primer argumento como separador. Requiere un separador y un mínimo de dos argumentos; en caso contrario, se produce un error. Todos los argumentos se convierten implícitamente en tipos de cadena y, a continuación, se concatenan. 

La conversión implícita de cadenas sigue las reglas existentes para las conversiones de tipos de datos. Para obtener más información acerca de las conversiones de tipo de comportamiento y los datos, vea [CONCAT (Transact-SQL)](../../t-sql/functions/concat-transact-sql.md).

### <a name="treatment-of-null-values"></a>Tratamiento de valores NULL

`CONCAT_WS`omite la `SET CONCAT_NULL_YIELDS_NULL {ON|OFF}` configuración.

Si todos los argumentos son null, una cadena vacía de tipo `varchar(1)` se devuelve. 

Valores NULL se omiten durante la concatenación y no agregan el separador. Esto facilita el escenario común de concatenación de cadenas que a menudo tienen valores en blanco, como un segundo campo de dirección. Vea el ejemplo B.

Si su escenario requiere que se incluye con un separador de valores null, vea el ejemplo C utiliza la `ISNULL` (función).

## <a name="examples"></a>Ejemplos   

### <a name="a--concatenating-values-with-separator"></a>A.  Concatenación de valores con separador
En el ejemplo siguiente se concatenan tres columnas de la tabla sys.databases, separe los valores con un `- `.   

```sql
SELECT CONCAT_WS( ' - ', database_id, recovery_model_desc, containment_desc) AS DatabaseInfo
FROM sys.databases;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   

|DatabaseInfo |  
|---------|
|1 - SIMPLE - NINGUNO |
|2 - SIMPLE - NINGUNO |
|3 - FULL - NINGUNO |
|4 - SIMPLE - NINGUNO |


### <a name="b--skipping-null-values"></a>B.  Omitir valores NULL
En el ejemplo siguiente se pasa por alto `NULL` valores en la lista de argumentos.

```sql
SELECT CONCAT_WS(',','1 Microsoft Way', NULL, NULL, 'Redmond', 'WA', 98052) AS Address;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   

```sql
Address
------------   
1 Microsoft Way,Redmond,WA,98052
```

### <a name="c--generating-csv-file-from-table"></a>C.  Generar el archivo CSV de tabla
En el ejemplo siguiente se utiliza una coma como separador y agrega el carácter de retorno de carro que dan como resultado en el formato de valores separados de la columna.

```sql
SELECT 
STRING_AGG(CONCAT_WS( ',', database_id, recovery_model_desc, containment_desc), char(13)) AS DatabaseInfo
FROM sys.databases
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   

```sql
DatabaseInfo
------------   
1,SIMPLE,NONE
2,SIMPLE,NONE
3,FULL,NONE 
4,SIMPLE,NONE 
```

CONCAT_WS pasará por alto los valores NULL en las columnas. Si alguna de las columnas que aceptan valores NULL, inclúyalo con `ISNULL` función y proporcionar el valor predeterminado como en el ejemplo siguiente:

```sql
SELECT 
STRING_AGG(CONCAT_WS( ',', database_id, ISNULL(recovery_model_desc,''), ISNULL(containment_desc,'N/A')), char(13)) AS DatabaseInfo
FROM sys.databases;
```

## <a name="see-also"></a>Vea también
 [CONCAT &#40;Transact-SQL&#41;](../../t-sql/functions/concat-transact-sql.md)  
 [FORMATMESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/formatmessage-transact-sql.md)  
 [QUOTENAME &#40;Transact-SQL&#41;](../../t-sql/functions/quotename-transact-sql.md)  
 [REPLACE &#40;Transact-SQL&#41;](../../t-sql/functions/replace-transact-sql.md)  
 [REVERSE &#40;Transact-SQL&#41;](../../t-sql/functions/reverse-transact-sql.md)  
 [STRING_AGG &#40;Transact-SQL&#41;](../../t-sql/functions/string-agg-transact-sql.md)  
 [STRING_ESCAPE &#40;Transact-SQL&#41;](../../t-sql/functions/string-escape-transact-sql.md)  
 [STUFF &#40;Transact-SQL&#41;](../../t-sql/functions/stuff-transact-sql.md)  
 [TRANSLATE &#40;Transact-SQL&#41;](../../t-sql/functions/translate-transact-sql.md)  
 [Funciones de cadena &#40; Transact-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  

