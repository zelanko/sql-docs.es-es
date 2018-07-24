---
title: DECOMPRESS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/30/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DECOMPRESS
- DECOMPRESS_TSQL
helpviewer_keywords:
- DECOMPRESS function
ms.assetid: 738d56be-3870-4774-b112-3dce27becc11
caps.latest.revision: 8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9c2eb8c020127211b25b762d96e6e376be7e234c
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38002697"
---
# <a name="decompress-transact-sql"></a>DECOMPRESS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Esta función descomprimirá un valor de expresión de entrada mediante el algoritmo GZIP. `DECOMPRESS` devolverá una matriz de bytes (de tipo VARBINARY(MAX)).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
DECOMPRESS ( expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *expression*  
Un valor **varbinary(***n***)**, **varbinary(max)** o **binary(***n***)**. Para más información, vea [Expresiones &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md).  
  
## <a name="return-types"></a>Tipos devueltos  
Un valor de tipo de datos **varbinary (max)**. `DECOMPRESS` usará el algoritmo ZIP para descomprimir el argumento de entrada. El usuario debe convertir explícitamente el resultado en un tipo de destino si es necesario.  
  
## <a name="remarks"></a>Notas  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-decompress-data-at-query-time"></a>A. Descomprimir datos en el tiempo de consulta  
En este ejemplo se muestra cómo devolver datos de tabla comprimidos:  
  
```  
SELECT _id, name, surname, datemodified,  
             CAST(DECOMPRESS(info) AS NVARCHAR(MAX)) AS info  
FROM player;  
```  
  
### <a name="b-display-compressed-data-using-computed-column"></a>B. Mostrar los datos comprimidos con columna calculada  
En este ejemplo se muestra cómo crear una tabla para almacenar los datos descomprimidos:  
  
```  
CREATE TABLE example_table (  
    _id int primary key identity,  
    name nvarchar(max),  
    surname nvarchar(max),  
    info varbinary(max),  
    info_json as CAST(decompress(info) as nvarchar(max))  
);  
```  
  
## <a name="see-also"></a>Ver también  
 [Funciones de cadena &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)   
 [COMPRESS &#40;Transact-SQL&#41;](../../t-sql/functions/compress-transact-sql.md)  
  
  
