---
title: COMPRIMIR (Transact-SQL) | Documentos de Microsoft
ms.custom:
- SQL2016_New_Updated
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c30cb5f351d9a84beec608483380edb94b8c7844
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="compress-transact-sql"></a>COMPRIMIR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Comprime la expresión de entrada utilizando el algoritmo GZIP. El resultado de la compresión es la matriz de bytes del tipo **varbinary (max)**.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
COMPRESS ( expression )  
```  
  
## <a name="arguments"></a>Argumentos  
*expression*  
Es un **nvarchar (***n***)**, **nvarchar (max)**, **varchar (**  *n*  **)**, **varchar (max)**, **varbinary (**  *n*  **)**, **varbinary (max)**, **char (***n***)**, **(nchar**   *n*  **)**, o **binario (***n***)** expresión. Para obtener más información, vea [Expresiones &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md).
  
## <a name="return-types"></a>Tipos de valor devuelto
Devuelve el tipo de datos de **varbinary (max)** que representa el contenido comprimido de entrada.
  
## <a name="remarks"></a>Comentarios  
No se puede indizar los datos comprimidos.
  
La función de COMPRESS comprime los datos proporcionados como la expresión de entrada y se debe invocar para cada sección de datos que se va a comprimir. Para la compresión automática en el nivel de fila o página durante el almacenamiento, consulte [compresión de datos](../../relational-databases/data-compression/data-compression.md).
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-compress-data-during-the-table-insert"></a>A. Comprimir los datos durante la inserción de tabla  
En el ejemplo siguiente se muestra cómo comprimir los datos insertados en la tabla:
  
```sql
INSERT INTO player (name, surname, info )  
VALUES (N'Ovidiu', N'Cracium',   
        COMPRESS(N'{"sport":"Tennis","age": 28,"rank":1,"points":15258, turn":17}'));  
  
INSERT INTO player (name, surname, info )  
VALUES (N'Michael', N'Raheem', compress(@info));  
```  
  
### <a name="b-archive-compressed-version-of-deleted-rows"></a>B. Archivar una versión comprimida de filas eliminadas  
La siguiente instrucción elimina los registros antiguos del Reproductor desde el `player` tabla y almacena los registros de la `inactivePlayer` tabla en un formato comprimido para ahorrar espacio.
  
```sql
DELETE player  
WHERE datemodified < @startOfYear  
OUTPUT id, name, surname datemodifier, COMPRESS(info)   
INTO dbo.inactivePlayers ;  
```  
  
## <a name="see-also"></a>Vea también
[Funciones de cadena &#40; Transact-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
[DESCOMPRIMIR &#40; Transact-SQL &#41;](../../t-sql/functions/decompress-transact-sql.md)
  
  

