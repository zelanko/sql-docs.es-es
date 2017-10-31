---
title: '@@IDENTITY (Transact-SQL) | Documentos de Microsoft'
ms.custom: 
ms.date: 08/29/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@IDENTITY_TSQL'
- '@@IDENTITY'
dev_langs:
- TSQL
helpviewer_keywords:
- last-inserted identity values
- identity values [SQL Server], last-inserted
- '@@IDENTITY function'
ms.assetid: 912e4485-683c-41c2-97b3-8831c0289ee4
caps.latest.revision: 35
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 88cdaa1362e5d60b0f880c66c7fb7038ddb9f126
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="x40x40identity-transact-sql"></a>& #x 40; & #x 40; identidad (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Se trata de una función del sistema que devuelve el último valor de identidad insertado.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
@@IDENTITY  
```  
  
## <a name="return-types"></a>Tipos devueltos  
 **numeric(38,0)**  
  
## <a name="remarks"></a>Comentarios  
 Después de una INSERCIÓN, SELECT INTO o masiva se complete la instrucción de copia, @@IDENTITY contiene el último valor de identidad generado por la instrucción. Si la instrucción no afectó a ninguna tabla con columnas de identidad, @@IDENTITY devuelve NULL. Si se insertan varias filas, generar varios valores de identidad, @@IDENTITY devuelve el último valor de identidad generado. Si la instrucción activa uno o más desencadenadores que realizan inserciones que generan valores de identidad, al llamar a@IDENTITY inmediatamente después de la instrucción devuelve el último valor de identidad generado por los desencadenadores. Si un desencadenador se activa después de una acción insert en una tabla que tiene una columna de identidad, y se inserta en otra tabla que no tiene una columna de identidad, @@IDENTITY devuelve el valor de identidad de la primera instrucción insert. El @@IDENTITY valor no vuelve a un valor anterior si se produce un error en la copia de instrucción o bulk INSERT o SELECT INTO, o si se revierte la transacción.  
  
 Las instrucciones y transacciones con errores pueden cambiar la identidad actual de una tabla y crear huecos en los valores de columna de identidad. El valor de identidad jamás se revierte, aun cuando no se haya confirmado la transacción que intentó insertar el valor en la tabla. Por ejemplo, si se produce un error en una instrucción INSERT debido a una infracción de tipo IGNORE_DUP_KEY, el valor de identidad actual de la tabla se sigue incrementando.  
  
 @@IDENTITY, SCOPE_IDENTITY e IDENT_CURRENT son funciones parecidas ya que devuelven el último valor insertado en la columna de identidad de una tabla.  
  
 @@IDENTITY y SCOPE_IDENTITY devuelve el último valor de identidad generado en cualquier tabla en la sesión actual. No obstante, SCOPE_IDENTITY devuelve el valor dentro del ámbito actual; @@IDENTITY no está limitado a un ámbito concreto.  
  
 IDENT_CURRENT no está limitado por el ámbito y la sesión; se limita a una tabla especificada. IDENT_CURRENT devuelve el valor de identidad generado para una tabla específica en cualquier sesión y cualquier ámbito. Para obtener más información, vea [IDENT_CURRENT &#40; Transact-SQL &#41; ](../../t-sql/functions/ident-current-transact-sql.md).  
  
 El ámbito de la @@IDENTITY función es la sesión actual en el servidor local en el que se ejecuta. Esta función no se puede aplicar a servidores remotos o vinculados. Para obtener un valor de identidad de un servidor diferente, ejecute un procedimiento almacenado en ese servidor remoto o vinculado y haga que dicho procedimiento (que se está ejecutando en el contexto del servidor remoto o vinculado) recopile el valor de identidad y lo devuelva a la conexión que llama del servidor local.  
  
 La replicación puede afectar a las @@IDENTITY valor, puesto que se usa dentro de los procedimientos almacenados y desencadenadores de replicación. @@IDENTITY no es un indicador confiable de la identidad más reciente creada por el usuario si la columna forma parte de un artículo de replicación. Puede usar la sintaxis de la función SCOPE_IDENTITY () en lugar de @@IDENTITY. Para obtener más información, vea [SCOPE_IDENTITY &#40; Transact-SQL &#41;](../../t-sql/functions/scope-identity-transact-sql.md)  
  
> [!NOTE]  
>  La llamada a procedimiento almacenado o [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción se debe escribir para que utilicen el `SCOPE_IDENTITY()` función, que devuelve la última identidad usada dentro del ámbito de esa instrucción de usuario y no la identidad en el ámbito del desencadenador anidado usado por replicación.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se inserta una fila en una tabla con una columna de identidad (`LocationID`) y se utiliza `@@IDENTITY` para mostrar el valor de identidad empleado en la nueva fila.  
  
```  
USE AdventureWorks2012;  
GO  
--Display the value of LocationID in the last row in the table.  
SELECT MAX(LocationID) FROM Production.Location;  
GO  
INSERT INTO Production.Location (Name, CostRate, Availability, ModifiedDate)  
VALUES ('Damaged Goods', 5, 2.5, GETDATE());  
GO  
SELECT @@IDENTITY AS 'Identity';  
GO  
--Display the value of LocationID of the newly inserted row.  
SELECT MAX(LocationID) FROM Production.Location;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [IDENT_CURRENT &#40;Transact-SQL&#41;](../../t-sql/functions/ident-current-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [SCOPE_IDENTITY &#40; Transact-SQL &#41;](../../t-sql/functions/scope-identity-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)  
  
  

