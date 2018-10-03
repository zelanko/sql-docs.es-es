---
title: COMPRESS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: reference
f1_keywords:
- COMPRESS
- COMPRESS_TSQL
helpviewer_keywords:
- COMPRESS function
ms.assetid: c2bfe9b8-57a4-48b4-b028-e1a3ed5ece88
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6f773267d6ff65d4340ebf467e7293cb5952a390
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47722473"
---
# <a name="compress-transact-sql"></a>COMPRESS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Esta función comprime la expresión de entrada usando el algoritmo GZIP. La función devuelve una matriz de bytes del tipo **varbinary(max)**.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
COMPRESS ( expression )  
```  
  
## <a name="arguments"></a>Argumentos  
*expression*  
Un

* **binary(***n***)**
* **char(***n***)**
* **nchar(***n***)**
* **nvarchar(max)**
* **nvarchar(***n***)**
* **varbinary(max)**
* **varbinary(***n***)**
* **ntext**

o Administrador de configuración de

* **varchar(***n***)**

expression: Para más información, vea [Expresiones &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md).
  
## <a name="return-types"></a>Tipos de valores devueltos
**varbinary(max)** representa el contenido comprimido de la entrada.
  
## <a name="remarks"></a>Notas  
Los datos comprimidos no se pueden indexar.
  
La función `COMPRESS` comprime los datos de la expresión de entrada. Debe invocar esta función para cada sección de datos que se vaya a comprimir. Vea [Compresión de datos](../../relational-databases/data-compression/data-compression.md) para obtener más información acerca de la compresión de datos automática durante el almacenamiento en el nivel de fila o página.
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-compress-data-during-the-table-insert"></a>A. Comprimir datos durante la inserción de tabla  
En este ejemplo se muestra cómo comprimir los datos insertados en una tabla:
  
```sql
INSERT INTO player (name, surname, info )  
VALUES (N'Ovidiu', N'Cracium',   
        COMPRESS(N'{"sport":"Tennis","age": 28,"rank":1,"points":15258, turn":17}'));  
  
INSERT INTO player (name, surname, info )  
VALUES (N'Michael', N'Raheem', compress(@info));  
```  
  
### <a name="b-archive-compressed-version-of-deleted-rows"></a>B. Archivar una versión comprimida de filas eliminadas  
Esta instrucción primero elimina los registros antiguos del reproductor de la tabla `player`. Para ahorrar espacio, luego almacena los registros en la tabla `inactivePlayer`, en un formato comprimido.
  
```sql
DELETE player  
WHERE datemodified < @startOfYear  
OUTPUT id, name, surname datemodifier, COMPRESS(info)   
INTO dbo.inactivePlayers ;  
```  
  
## <a name="see-also"></a>Vea también
[Funciones de cadena &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)  
[DECOMPRESS &#40;Transact-SQL&#41;](../../t-sql/functions/decompress-transact-sql.md)
  
  
