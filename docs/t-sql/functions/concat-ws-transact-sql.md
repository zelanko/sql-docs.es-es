---
title: CONCAT_WS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
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
monikerRange: = azuresqldb-current || >= sql-server-2017 || = sqlallproducts-allversions
ms.openlocfilehash: e1a3d184ccdd0a1716fdace286b2bb8ed6a6cae6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "33055192"
---
# <a name="concatws-transact-sql"></a>CONCAT_WS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

Esta función devuelve una cadena resultante de la concatenación, o la combinación, de dos o más valores de cadena de una manera integral. Separa esos valores de cadena concatenados con el delimitador especificado en el primer argumento de función. (`CONCAT_WS` indica *concatenar con separador*).

##  <a name="syntax"></a>Sintaxis   
```sql
CONCAT_WS ( separator, argument1, argument1 [, argumentN]… ) 
```

## <a name="arguments"></a>Argumentos   
separador  
Una expresión de cualquier tipo de carácter (`char`', `nchar`', `nvarchar` o `varchar`).

argument1, argument2, argument*N*  
Una expresión de cualquier tipo.

## <a name="return-types"></a>Tipos de valores devueltos
Un valor de cadena cuya longitud y tipo dependen de la entrada.

## <a name="remarks"></a>Notas   
`CONCAT_WS` toma un número variable de argumentos de cadena y los concatena (o combina) en una sola cadena. Separa esos valores de cadena concatenados con el delimitador especificado en el primer argumento de función. `CONCAT_WS` requiere un argumento separador y un mínimo de otros dos argumentos de valor de cadena; de lo contrario, `CONCAT_WS` producirá un error. `CONCAT_WS` convierte implícitamente todos los argumentos en tipos de cadena antes de la concatenación. 

La conversión implícita de cadenas sigue las reglas existentes para las conversiones de tipos de datos. Para obtener más información sobre las conversiones de tipo de datos y comportamiento, consulte [CONCAT (Transact-SQL)](../../t-sql/functions/concat-transact-sql.md).

### <a name="treatment-of-null-values"></a>Tratamiento de valores NULL

`CONCAT_WS` omite el valor `SET CONCAT_NULL_YIELDS_NULL {ON|OFF}`.

Si `CONCAT_WS` recibe argumentos en los que todos los valores son NULL, devolverá una cadena vacía de tipo varchar(1).

`CONCAT_WS` omite los valores NULL durante la concatenación y no se agrega el separador entre ellos. Por lo tanto, `CONCAT_WS` puede tratar limpiamente la concatenación de cadenas que podrían tener valores "en blanco"; por ejemplo, un segundo campo de dirección. Para obtener más información, vea el ejemplo B.

Si un escenario implica valores nulos separados por un delimitador, considere la función `ISNULL`. Para obtener más información, vea el ejemplo C.

## <a name="examples"></a>Ejemplos   

### <a name="a--concatenating-values-with-separator"></a>A.  Concatenación de valores con separador
En este ejemplo se concatenan tres columnas de la tabla sys.databases separando los valores con `- `.   

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
En este ejemplo se ignoran valores `NULL` de la lista de argumentos.

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
En este ejemplo se utiliza una coma `,` como separador y se agrega el carácter de retorno de carro `char(13)` en el formato de valores separados de la columna del conjunto de resultados.

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

CONCAT_WS pasará por alto los valores NULL en las columnas. Encapsule una columna con valores NULL con la función `ISNULL` y proporcione un valor predeterminado. Para más información, vea este ejemplo:

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

