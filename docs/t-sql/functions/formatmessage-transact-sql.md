---
title: FORMATMESSAGE (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 07/12/2017
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
- FORMATMESSAGE
- FORMATMESSAGE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmessages system table
- sys.messages catalog view
- FORMATMESSAGE function
- messages [SQL Server], formats
- errors [SQL Server], formats
ms.assetid: 83f18102-2035-4a87-acd0-8d96d03efad5
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 3a45ab2e81daf6183d37ef67089cc6d1a1e6ac3a
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/18/2018
---
# <a name="formatmessage-transact-sql"></a>FORMATMESSAGE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Construye un mensaje desde un mensaje existente en sys.messages o desde una cadena proporcionada. La funcionalidad de FORMATMESSAGE es similar a la de la instrucción RAISERROR. Sin embargo, RAISERROR imprime el mensaje inmediatamente, mientras que FORMATMESSAGE devuelve el mensaje formateado para que se pueda seguir procesando.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
FORMATMESSAGE ( { msg_number  | ' msg_string ' } , [ param_value [ ,...n ] ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *msg_number*  
 Es el identificador del mensaje almacenado en sys.messages. Si *msg_number* es < = 13000, o si el mensaje no existe en sys.messages, se devuelve NULL.  
  
 *msg_string*  
 **Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a través de la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 Es que una cadena entre comillas simples y el valor del parámetro que contiene marcadores de posición. El mensaje de error puede tener 2.047 caracteres como máximo. Si el mensaje contiene más de 2.048 caracteres, solamente aparecerán los 2.044 primeros y se agregarán puntos suspensivos para indicar que el mensaje se ha truncado. Tenga en cuenta que los parámetros de sustitución utilizan más caracteres de lo que muestra la salida debido al comportamiento del almacenamiento interno.  Para obtener información acerca de la estructura de una cadena de mensaje y el uso de parámetros en la cadena, vea la descripción de la *msg_str* argumento en [RAISERROR &#40; Transact-SQL &#41; ](../../t-sql/language-elements/raiserror-transact-sql.md).  
  
 *param_value*  
 Valor de parámetro que se utiliza en el mensaje. Puede ser más de un valor. Los valores se deben especificar en el orden en el que las variables de marcador de posición aparezcan en el mensaje. El número máximo de valores es 20.  
  
## <a name="return-types"></a>Tipos devueltos  
 **nvarchar**  
  
## <a name="remarks"></a>Comentarios  
 Al igual que la instrucción RAISERROR, FORMATMESSAGE modifica el mensaje sustituyendo los valores de los parámetros suministrados por variables de marcador de posición del mensaje. Para obtener más información acerca de los marcadores de posición permitidos en los mensajes de error y el proceso de edición, vea [RAISERROR &#40; Transact-SQL &#41; ](../../t-sql/language-elements/raiserror-transact-sql.md).  
  
 FORMATMESSAGE busca el mensaje en el idioma actual del usuario. Si no hay una versión del mensaje en otro idioma, se utiliza la versión en inglés (EE.UU.).  
  
 En los mensajes en otros idiomas, los valores de los parámetros suministrados deben corresponder a los marcadores de posición de los parámetros de la versión en inglés (EE.UU.). Es decir, el parámetro 1 de la versión en otros idiomas debe corresponder al parámetro 1 de la versión en inglés (EE.UU.), el parámetro 2 debe corresponder al parámetro 2, etc.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-example-with-a-message-number"></a>A. Ejemplo con un número de mensaje  
 En el ejemplo siguiente se usa un mensaje de replicación `20009` almacenado en sys.messages como, "el artículo '%s' no se pudo agregar a la publicación '%s'." FORMATMESSAGE sustituye los valores `First Variable` y `Second Variable` por los marcadores de posición de los parámetros. La cadena resultante, "el artículo 'First Variable' no pudo agregarse a la publicación 'Second Variable'.", se almacena en la variable local `@var1`.  
  
```  
SELECT text FROM sys.messages WHERE message_id = 20009 AND language_id = 1033;  
DECLARE @var1 VARCHAR(200);   
SELECT @var1 = FORMATMESSAGE(20009, 'First Variable', 'Second Variable');   
SELECT @var1;  
```  
  
### <a name="b-example-with-a-message-string"></a>B. Ejemplo con una cadena de mensaje  
  
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a través de la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 En el ejemplo siguiente se toma una cadena como entrada.  
  
```  
SELECT FORMATMESSAGE('This is the %s and this is the %s.', 'first variable', 'second variable') AS Result;  
```  
  
 Devuelve:`This is the first variable and this is the second variable.`  
  
### <a name="c-additional-message-string-formatting-examples"></a>C. Ejemplos de formato de cadena de mensaje adicional  
 Los ejemplos siguientes muestran una variedad de opciones de formato.  
  
```  
SELECT FORMATMESSAGE('Signed int %i, %d %i, %d, %+i, %+d, %+i, %+d', 5, -5, 50, -50, -11, -11, 11, 11);  
SELECT FORMATMESSAGE('Signed int with leading zero %020i', 5);  
SELECT FORMATMESSAGE('Signed int with leading zero 0 %020i', -55);  
SELECT FORMATMESSAGE('Unsigned int %u, %u', 50, -50);  
SELECT FORMATMESSAGE('Unsigned octal %o, %o', 50, -50);  
SELECT FORMATMESSAGE('Unsigned hexadecimal %x, %X, %X, %X, %x', 11, 11, -11, 50, -50);  
SELECT FORMATMESSAGE('Unsigned octal with prefix: %#o, %#o', 50, -50);  
SELECT FORMATMESSAGE('Unsigned hexadecimal with prefix: %#x, %#X, %#X, %X, %x', 11, 11, -11, 50, -50);  
SELECT FORMATMESSAGE('Hello %s!', 'TEST');  
SELECT FORMATMESSAGE('Hello %20s!', 'TEST');  
SELECT FORMATMESSAGE('Hello %-20s!', 'TEST');  
SELECT FORMATMESSAGE('Hello %20s!', 'TEST');  
```  
  
## <a name="see-also"></a>Vea también  
 [RAISERROR &#40; Transact-SQL &#41;](../../t-sql/language-elements/raiserror-transact-sql.md)  
 [THROW &#40;Transact-SQL&#41;](../../t-sql/language-elements/throw-transact-sql.md)   
 [sp_addmessage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md)   
 [sys.messages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)   
 [CONCAT &#40;Transact-SQL&#41;](../../t-sql/functions/concat-transact-sql.md)  
 [CONCAT_WS &#40;Transact-SQL&#41;](../../t-sql/functions/concat-ws-transact-sql.md)  
 [QUOTENAME &#40;Transact-SQL&#41;](../../t-sql/functions/quotename-transact-sql.md)  
 [REPLACE &#40;Transact-SQL&#41;](../../t-sql/functions/replace-transact-sql.md)  
 [REVERSE &#40;Transact-SQL&#41;](../../t-sql/functions/reverse-transact-sql.md)  
 [STRING_AGG &#40;Transact-SQL&#41;](../../t-sql/functions/string-agg-transact-sql.md)  
 [STRING_ESCAPE &#40;Transact-SQL&#41;](../../t-sql/functions/string-escape-transact-sql.md)  
 [STUFF &#40;Transact-SQL&#41;](../../t-sql/functions/stuff-transact-sql.md)  
 [TRANSLATE &#40;Transact-SQL&#41;](../../t-sql/functions/translate-transact-sql.md)  
 [Funciones del sistema &#40; Transact-SQL &#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)   
  
  
