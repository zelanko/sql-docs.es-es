---
title: CREAR valor predeterminado (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 11/25/2015
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE_DEFAULT_TSQL
- CREATE DEFAULT
dev_langs:
- TSQL
helpviewer_keywords:
- objects [SQL Server], default
- default objects
- CREATE DEFAULT statement
- objects [SQL Server], creating
- DEFAULT definition
ms.assetid: 08475db4-7d90-486a-814c-01a99d783d41
caps.latest.revision: 47
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 71c0f964d245be92fb8d2be19e074fbd34dd616e
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="create-default-transact-sql"></a>CREATE DEFAULT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Crea un objeto denominado valor predeterminado. Cuando se enlaza a una columna o a un tipo de datos del alias, un valor predeterminado especifica un valor que debe insertarse en la columna a la que está enlazado el objeto (o en todas las columnas, en el caso de un tipo de datos del alias) si no se proporciona explícitamente un valor durante la inserción.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] En su lugar, use definiciones predeterminadas creadas con la palabra clave DEFAULT de ALTER TABLE o CREATE TABLE.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
CREATE DEFAULT [ schema_name . ] default_name   
AS constant_expression [ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *schema_name*  
 Es el nombre del esquema al que pertenece el valor predeterminado.  
  
 *default_name*  
 Es el nombre del valor predeterminado. Nombres predeterminados deben cumplir las reglas de [identificadores](../../relational-databases/databases/database-identifiers.md). Especificar el nombre del propietario del valor predeterminado es opcional.  
  
 *expresiónConstante*  
 Es un [expresión](../../t-sql/language-elements/expressions-transact-sql.md) que contiene solo valores constantes (no puede incluir los nombres de las columnas u otros objetos de base de datos). Se puede utilizar cualquier constante, función integrada o expresión matemática, excepto las que contienen tipos de datos de alias. No se pueden utilizar funciones definidas por el usuario. Incluya las constantes de caracteres y fechas entre comillas simples (**'**); monetario, entero y constantes de punto flotante no necesitan comillas. Los datos binarios deben precederse de 0x y los datos de moneda deben precederse de un signo de dólar ($). El valor predeterminado debe ser compatible con el tipo de datos de la columna.  
  
## <a name="remarks"></a>Comentarios  
 El nombre de un valor predeterminado solo se puede crear en la base de datos actual. En una base de datos, los nombres predeterminados deben ser únicos para cada esquema. Cuando se crea un valor predeterminado, utilice **sp_bindefault** para enlazarlo a una columna o a un tipo de datos de alias.  
  
 Si el valor predeterminado no es compatible con la columna a la que está enlazado, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] genera un mensaje de error al intentar insertar el valor predeterminado. Por ejemplo, N/A no se puede usar como un valor predeterminado para un **numérico** columna.  
  
 Si el valor predeterminado es demasiado largo para la columna a la que está enlazado, el valor se trunca.  
  
 Las instrucciones CREATE DEFAULT no se pueden combinar con otras instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] en el mismo lote.  
  
 Valor predeterminado debe quitarse antes de crear uno nuevo el mismo nombre y el valor predeterminado debe ser independiente mediante la ejecución de **sp_unbindefault** antes de quitarla.  
  
 Si una columna tiene un valor predeterminado y una regla asociados, el valor predeterminado no debe infringir la regla. No se insertará nunca un valor predeterminado que esté en conflicto con una regla y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] genera un mensaje de error cada vez que se intente insertar el valor predeterminado.  
  
 Cuando se enlaza a una columna, un valor predeterminado se inserta cuando:  
  
-   No se ha insertado un valor explícitamente.  
  
-   Se utilizan las palabras clave DEFAULT VALUES o DEFAULT con INSERT para insertar valores predeterminados.  
  
 Si se especifica NOT NULL al crear una columna y no se crea un valor predeterminado para ésta, se generará un mensaje de error cada vez que el usuario no cree una entrada en esa columna. En la tabla siguiente se ilustra la relación entre la existencia de un valor predeterminado y la definición de una columna como NULL o NOT NULL. Las entradas de la tabla muestran el resultado.  
  
|Definición de columna|Sin entrada, sin valor predeterminado|Sin entrada, valor predeterminado|Entrada NULL, sin valor predeterminado|Entrada NULL, valor predeterminado|  
|-----------------------|--------------------------|-----------------------|----------------------------|-------------------------|  
|**NULL**|NULL|predeterminados|NULL|NULL|  
|**NOT NULL**|Error|predeterminados|error|error|  
  
 Para cambiar el nombre predeterminado, utilice **sp_rename**. Para obtener un informe sobre un valor predeterminado, utilice **sp_help**.  
  
## <a name="permissions"></a>Permissions  
 Para ejecutar CREATE DEFAULT, como mínimo, un usuario debe tener permiso CREATE DEFAULT en la base de datos actual y permiso ALTER en el esquema donde se va a crear el valor predeterminado.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-creating-a-simple-character-default"></a>A. Crear un valor predeterminado de caracteres de tipo sencillo  
 En el siguiente ejemplo se crea un valor predeterminado de caracteres denominado `unknown`.  
  
```tsql  
USE AdventureWorks2012;  
GO  
CREATE DEFAULT phonedflt AS 'unknown';  
```  
  
### <a name="b-binding-a-default"></a>B. Enlazar un valor predeterminado  
 En el siguiente ejemplo se enlaza el valor predeterminado creado en el ejemplo A. El valor predeterminado solo entra en efecto si no hay ninguna entrada especificada en la columna `Phone` de la tabla `Contact`. Tenga en cuenta que omitir una entrada no es lo mismo que incluir NULL explícitamente en una instrucción INSERT.  
  
 Como no existe un valor predeterminado llamado `phonedflt`, se producirá un error en la siguiente instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)]. Este ejemplo solo tiene propósitos ilustrativos.  
  
```tsql  
USE AdventureWorks2012;  
GO  
sp_bindefault 'phonedflt', 'Person.PersonPhone.PhoneNumber';  
```  
  
## <a name="see-also"></a>Vea también  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE RULE &#40;Transact-SQL&#41;](../../t-sql/statements/create-rule-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [ELIMINAR predeterminado &#40; Transact-SQL &#41;](../../t-sql/statements/drop-default-transact-sql.md)   
 [Eliminar regla &#40; Transact-SQL &#41;](../../t-sql/statements/drop-rule-transact-sql.md)   
 [Expresiones &#40; Transact-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [sp_bindefault &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-bindefault-transact-sql.md)   
 [sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sp_helptext &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [sp_rename &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)   
 [sp_unbindefault &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-unbindefault-transact-sql.md)  
  
  

