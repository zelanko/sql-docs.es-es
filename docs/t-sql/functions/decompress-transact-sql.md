---
title: DESCOMPRIMIR (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 11/30/2015
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DECOMPRESS
- DECOMPRESS_TSQL
helpviewer_keywords:
- DECOMPRESS function
ms.assetid: 738d56be-3870-4774-b112-3dce27becc11
caps.latest.revision: 8
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7918a9bce5afcd7ce59551a60fc7e3f2f318f492
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="decompress-transact-sql"></a>DESCOMPRIMIR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Descomprimir la expresión de entrada mediante el algoritmo GZIP. Resultado de la compresión es la matriz de bytes (tipo varbinary (max)).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
DECOMPRESS ( expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *expression*  
 Es un **varbinary (***n***)**, **varbinary (max)**, o **binario (** *n***)**. Para obtener más información, vea [Expresiones &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md).  
  
## <a name="return-types"></a>Tipos devueltos  
 Devuelve el tipo de datos de **varbinary (max)** tipo. El argumento de entrada se descomprime mediante el algoritmo ZIP. El usuario debe convertir explícitamente el resultado a un tipo de destino si es necesario.  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-decompress-data-at-query-time"></a>A. Descomprimir los datos en tiempo de consulta  
 En el ejemplo siguiente se muestra cómo mostrar comprimir los datos de una tabla:  
  
```  
SELECT _id, name, surname, datemodified,  
             CAST(DECOMPRESS(info) AS NVARCHAR(MAX)) AS info  
FROM player;  
```  
  
### <a name="b-display-compressed-data-using-computed-column"></a>B. Mostrar los datos comprimidos con la columna calculada  
 En el ejemplo siguiente se muestra cómo crear una tabla para almacenar datos descomprimidos:  
  
```  
CREATE TABLE (  
    _id int primary key identity,  
    name nvarchar(max),  
    surname nvarchar(max),  
    info varbinary(max),  
    info_json as CAST(decompress(info) as nvarchar(max))  
);  
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones de cadena &#40; Transact-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)   
 [COMPRESS &#40; Transact-SQL &#41;](../../t-sql/functions/compress-transact-sql.md)  
  
  

