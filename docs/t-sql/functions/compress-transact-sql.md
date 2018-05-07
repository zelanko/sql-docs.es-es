---
title: COMPRESS (Transact-SQL) | Microsoft Docs
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
ms.topic: reference
f1_keywords:
- COMPRESS
- COMPRESS_TSQL
helpviewer_keywords:
- COMPRESS function
ms.assetid: c2bfe9b8-57a4-48b4-b028-e1a3ed5ece88
caps.latest.revision: 9
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 51324f00da71597a8a2dd37d8f0077c4b3bc8b55
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="compress-transact-sql"></a>COMPRESS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Comprime la expresión de entrada usando el algoritmo GZIP. El resultado de la compresión es una matriz de bytes de tipo **varbinary(max)**.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
COMPRESS ( expression )  
```  
  
## <a name="arguments"></a>Argumentos  
*expression*  
Es una expresión **nvarchar(***n***)**, **nvarchar(max)**, **varchar(***n***)**, **varchar(max)**, **varbinary(***n***)**, **varbinary(max)**, **char(***n***)**, **nchar(***n***)** o **binary(***n***)**. Para obtener más información, vea [Expresiones &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md).
  
## <a name="return-types"></a>Tipos de valores devueltos
Devuelve el tipo de datos **varbinary (max)** que representa el contenido comprimido de la entrada.
  
## <a name="remarks"></a>Notas  
Los datos comprimidos no se pueden indexar.
  
La función COMPRESS comprime los datos proporcionados como expresión de entrada, y se debe invocar en cada sección de datos que se vaya a comprimir. Para más información sobre la compresión automática en el nivel de fila o de página durante el almacenamiento, vea [Compresión de datos](../../relational-databases/data-compression/data-compression.md).
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-compress-data-during-the-table-insert"></a>A. Comprimir datos durante la inserción de tabla  
En el siguiente ejemplo se muestra cómo comprimir los datos insertados en una tabla:
  
```sql
INSERT INTO player (name, surname, info )  
VALUES (N'Ovidiu', N'Cracium',   
        COMPRESS(N'{"sport":"Tennis","age": 28,"rank":1,"points":15258, turn":17}'));  
  
INSERT INTO player (name, surname, info )  
VALUES (N'Michael', N'Raheem', compress(@info));  
```  
  
### <a name="b-archive-compressed-version-of-deleted-rows"></a>B. Archivar una versión comprimida de filas eliminadas  
Con la siguiente instrucción se eliminan los registros de player antiguos de la tabla `player` y los registros se almacenan en la tabla `inactivePlayer` en un formato comprimido para ahorrar espacio.
  
```sql
DELETE player  
WHERE datemodified < @startOfYear  
OUTPUT id, name, surname datemodifier, COMPRESS(info)   
INTO dbo.inactivePlayers ;  
```  
  
## <a name="see-also"></a>Vea también
[Funciones de cadena &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)  
[DECOMPRESS &#40;Transact-SQL&#41;](../../t-sql/functions/decompress-transact-sql.md)
  
  
