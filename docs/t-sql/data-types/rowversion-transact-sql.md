---
title: rowversion (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 07/22/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- timestamp_TSQL
- timestamp
dev_langs:
- TSQL
helpviewer_keywords:
- rowversion data type
- size [SQL Server], rowversion
- row version-stamping [SQL Server]
- rowversion columns
- version-stamping table rows
- unique rowversion numbers
- unique timestamp numbers
- timestamp data type
- timestamp columns
- size [SQL Server], timestamp
ms.assetid: 65c9cf0e-3e8a-45f8-87b3-3460d96afb0b
caps.latest.revision: 57
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 47bcf3007657c1cf8f77c364aa21839cdd27d1ba
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="rowversion-transact-sql"></a>rowversion (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Es un tipo de datos que expone números binarios únicos generados automáticamente en una base de datos. **rowversion** suele utilizarse como un mecanismo para marcar la versión filas de la tabla. El tamaño de almacenamiento es de 8 bytes. El **rowversion** tipo de datos es simplemente un número que se incrementa y no conserva una fecha o una hora. Para registrar una fecha u hora, use un **datetime2** tipo de datos.
  
## <a name="remarks"></a>Comentarios  
Cada base de datos tiene un contador que se incrementa para cada inserción o una operación de actualización que se realiza en una tabla que contiene un **rowversion** columna dentro de la base de datos. Este contador es la versión de fila (rowversion) de la base de datos. Realiza un seguimiento de una hora relativa de una base de datos, no una hora real que pueda asociarse con un reloj. Una tabla puede tener sólo una **rowversion** columna. Cada vez que una fila con un **rowversion** columna se ha modificado o insertada, el valor rowversion de base de datos incrementado se inserta en la **rowversion** columna. Esta propiedad hace que sea un **rowversion** columna un mal candidato para claves, especialmente claves principales. Cualquier actualización de la fila hace que cambie el valor rowversion, con lo que cambia el valor de la clave. Si la columna está en una clave principal, el valor de la clave principal antigua deja de ser válido, así como las claves externas que hacen referencia al valor antiguo. Si se hace referencia a la tabla en un cursor dinámico, todas las actualizaciones cambian la posición de las filas en el cursor. Si la columna es una clave de índice, todas las actualizaciones de la fila de datos también generan actualizaciones del índice.  El **rowversion** valor se incrementa con cualquier instrucción de actualización, incluso si se cambia ningún valor de fila. (Por ejemplo, si un valor de columna es 5, y una instrucción update establece el valor en 5, esta acción se considera una actualización incluso si no hay ningún cambio y el **rowversion** se incrementa.)
  
**marca de tiempo** es el sinónimo para el **rowversion** tipo de datos y está sujeto al comportamiento de datos sinónimos de tipos. En las instrucciones de DDL, use **rowversion** en lugar de **timestamp** siempre que sea posible. Para obtener más información, vea [sinónimos de tipos de datos &#40; Transact-SQL &#41; ](../../t-sql/data-types/data-type-synonyms-transact-sql.md).
  
El [!INCLUDE[tsql](../../includes/tsql-md.md)] **timestamp** tipo de datos es diferente de la **marca de tiempo** tipo de datos definido en el estándar ISO.
  
> [!NOTE]  
>  El **timestamp** sintaxis está en desuso. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
En una instrucción CREATE TABLE o ALTER TABLE, no es necesario especificar un nombre de columna para la **timestamp** tipo de datos, por ejemplo:
  
```sql
CREATE TABLE ExampleTable (PriKey int PRIMARY KEY, timestamp);  
```  
  
Si no especifica un nombre de columna, el [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] genera el **timestamp** nombre de columna; sin embargo, el **rowversion** sinónimo no sigue este comportamiento. Cuando usas **rowversion**, debe especificar un nombre de columna, por ejemplo:
  
```sql
CREATE TABLE ExampleTable2 (PriKey int PRIMARY KEY, VerCol rowversion) ;  
```  
  
> [!NOTE]  
>  Duplicar **rowversion** valores pueden generarse mediante la instrucción SELECT INTO en la que un **rowversion** columna está en la lista de selección. Se recomienda no usar **rowversion** de esta manera.  
  
Una no admiten valores NULL **rowversion** columna es semánticamente equivalente a una **binary (8)** columna. Un que aceptan valores NULL **rowversion** columna es semánticamente equivalente a una **varbinary (8)** columna.
  
Puede usar el **rowversion** columna de una fila para determinar con facilidad si la fila ha tenido una instrucción update se ejecutó en el mismo desde la última vez que se leyó. Si se ejecutó una instrucción update en la fila, se actualiza el valor rowversion. Si no hay ninguna actualización instrucciones son se ejecutó en la fila, el valor rowversion es el mismo que cuando se ha leído previamente. Para devolver el valor rowversion actual para una base de datos, utilice [@@DBTS](../../t-sql/functions/dbts-transact-sql.md).
  
Puede agregar un **rowversion** columna a una tabla para ayudar a mantener la integridad de la base de datos cuando varios usuarios actualizan filas al mismo tiempo. También puede que desee conocer cuántas filas y qué filas se actualizaron sin volver a consultar la tabla.
  
Por ejemplo, suponga que crea una tabla denominada `MyTest`. Rellene algunos datos en la tabla ejecutando la siguiente [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucciones.
  
```sql
CREATE TABLE MyTest (myKey int PRIMARY KEY  
    ,myValue int, RV rowversion);  
GO   
INSERT INTO MyTest (myKey, myValue) VALUES (1, 0);  
GO   
INSERT INTO MyTest (myKey, myValue) VALUES (2, 0);  
GO  
```  
  
A continuación, puede utilizar las instrucciones de [!INCLUDE[tsql](../../includes/tsql-md.md)] de ejemplo siguientes para implementar el control de simultaneidad optimista en la tabla `MyTest` durante la actualización.
  
```sql
DECLARE @t TABLE (myKey int);  
UPDATE MyTest  
SET myValue = 2  
    OUTPUT inserted.myKey INTO @t(myKey)   
WHERE myKey = 1   
    AND RV = myValue;  
IF (SELECT COUNT(*) FROM @t) = 0  
    BEGIN  
        RAISERROR ('error changing row with myKey = %d'  
            ,16 -- Severity.  
            ,1 -- State   
            ,1) -- myKey that was changed   
    END;  
```  
  
`myValue`es el **rowversion** valor de la columna de la fila que indica la última vez que lee la fila. Este valor debe ser reemplazado por los datos reales **rowversion** valor. Un ejemplo de los datos reales **rowversion** valor es 0x00000000000007D3.
  
También puede colocar el ejemplo [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucciones en una transacción. Al consultar la variable `@t` en el ámbito de la transacción, puede recuperar la columna `myKey` actualizada de la tabla sin consultar de nuevo la tabla `MyTes`.
  
Éste es el mismo ejemplo utilizando la **timestamp** sintaxis:
  
```sql
CREATE TABLE MyTest2 (myKey int PRIMARY KEY  
    ,myValue int, TS timestamp);  
GO   
INSERT INTO MyTest2 (myKey, myValue) VALUES (1, 0);  
GO   
INSERT INTO MyTest2 (myKey, myValue) VALUES (2, 0);  
GO  
DECLARE @t TABLE (myKey int);  
UPDATE MyTest2  
SET myValue = 2  
    OUTPUT inserted.myKey INTO @t(myKey)   
WHERE myKey = 1   
    AND TS = myValue;  
IF (SELECT COUNT(*) FROM @t) = 0  
    BEGIN  
        RAISERROR ('error changing row with myKey = %d'  
            ,16 -- Severity.  
            ,1 -- State   
            ,1) -- myKey that was changed   
    END;  
```  
  
## <a name="see-also"></a>Vea también
[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CAST y CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)  
[INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)  
[MIN_ACTIVE_ROWVERSION &#40; Transact-SQL &#41;](../../t-sql/functions/min-active-rowversion-transact-sql.md)  
[SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
[UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)
  
  

