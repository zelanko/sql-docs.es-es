---
title: CONCAT_WS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- CONCAT_WS
- CONCAT_WS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CONCAT_WS function
ms.assetid: f1375fd7-a2fd-48bf-922a-4f778f0deb1f
caps.latest.revision: 5
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
monikerRange: = azuresqldb-current || >= sql-server-2017 || = sqlallproducts-allversions
ms.openlocfilehash: 171d063e746393709629720dae40eb207d45d584
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="concatws-transact-sql"></a>CONCAT_WS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

Concatena un número variable de argumentos con un delimitador especificado en el primer argumento. (`CONCAT_WS` indica *concatenar con separador*).

##  <a name="syntax"></a>Sintaxis   
```sql
CONCAT_WS ( separator, argument1, argument1 [, argumentN]… ) 
```

## <a name="arguments"></a>Argumentos   
separador  
Es una expresión de cualquier tipo de carácter (`nvarchar`, `varchar`, `nchar` o `char`).

argument1, argument2, argument*N*  
Es una expresión de cualquier tipo.

## <a name="return-types"></a>Tipos de valores devueltos
: cadena. El tipo y longitud dependen de la entrada.

## <a name="remarks"></a>Notas   
`CONCAT_WS` toma un número variable de argumentos y los concatena en una sola cadena utilizando el primer argumento como separador. Necesita un separador y un mínimo de dos argumentos; de lo contrario, se produce un error. Todos los argumentos se convierten implícitamente a tipos de cadena y después se concatenan. 

La conversión implícita de cadenas sigue las reglas existentes para las conversiones de tipos de datos. Para obtener más información sobre las conversiones de tipo de datos y comportamiento, consulte [CONCAT (Transact-SQL)](../../t-sql/functions/concat-transact-sql.md).

### <a name="treatment-of-null-values"></a>Tratamiento de valores NULL

`CONCAT_WS` omite el valor `SET CONCAT_NULL_YIELDS_NULL {ON|OFF}`.

Si todos los argumentos son NULL, se devuelve una cadena vacía de tipo `varchar(1)`. 

Los valores NULL se omiten durante la concatenación y no se agrega el separador. Esto facilita el escenario común de cadenas concatenadas que a menudo tienen valores en blanco, como un segundo campo de dirección. Vea el ejemplo B.

Si su escenario requiere que se incluyan valores NULL con un separador, vea el ejemplo C utilizando la función `ISNULL`.

## <a name="examples"></a>Ejemplos   

### <a name="a--concatenating-values-with-separator"></a>A.  Concatenación de valores con separador
En el ejemplo siguiente se concatenan tres columnas de la tabla sys.databases separando los valores con `- `.   

```sql
SELECT CONCAT_WS( ' - ', database_id, recovery_model_desc, containment_desc) AS DatabaseInfo
FROM sys.databases;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   

|DatabaseInfo |  
|---------|
|1 - SIMPLE - NONE |
|2 - SIMPLE - NONE |
|3 - FULL - NONE |
|4 - SIMPLE - NONE |


### <a name="b--skipping-null-values"></a>B.  Omitir valores NULL
En el ejemplo siguiente se pasan por alto valores `NULL` de la lista de argumentos.

```sql
SELECT CONCAT_WS(',','1 Microsoft Way', NULL, NULL, 'Redmond', 'WA', 98052) AS Address;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   

```sql
Address
------------   
1 Microsoft Way,Redmond,WA,98052
```

### <a name="c--generating-csv-file-from-table"></a>C.  Generar el archivo CSV a partir de la tabla
En el ejemplo siguiente se utiliza una coma como separador y se agrega el carácter de retorno de carro que resulta en el formato de valores separados de la columna.

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

CONCAT_WS pasará por alto los valores NULL en las columnas. Si alguna de las columnas acepta valores NULL, incluya la función `ISNULL` y proporcione el valor predeterminado como en el ejemplo siguiente:

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
 [Funciones de cadena &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)  

