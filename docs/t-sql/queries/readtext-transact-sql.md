---
title: READTEXT (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 10/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- READTEXT_TSQL
- READTEXT
dev_langs:
- TSQL
helpviewer_keywords:
- column reading [SQL Server]
- READTEXT statement
- reading columns
ms.assetid: 91b69853-1381-4306-8343-afdb73105738
caps.latest.revision: 27
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2c501fe8ea8146b4b2ec6e138f72fc2604b4b374
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="readtext-transact-sql"></a>READTEXT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Lee **texto**, **ntext**, o **imagen** los valores de un **texto**, **ntext**, o **imagen**  columna, empezando por un desplazamiento especificado y el número especificado de bytes de lectura.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Use la [SUBCADENA](../../t-sql/functions/substring-transact-sql.md) funcione en su lugar.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
READTEXT { table.column text_ptr offset size } [ HOLDLOCK ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *tabla* **.** *columna*  
 Es el nombre de la tabla y de la columna donde se va a leer. Nombres de tablas y columnas deben cumplir las reglas de [identificadores](../../relational-databases/databases/database-identifiers.md). Es necesario especificar los nombres de la tabla y de la columna; sin embargo, es opcional especificar el nombre de la base de datos y del propietario.  
  
 *text_ptr*  
 Es un puntero de texto válido. *text_ptr* debe ser **binary (16)**.  
  
 *desplazamiento*  
 Es el número de bytes (cuando la **texto** o **imagen** se utilizan tipos de datos) o caracteres (cuando la **ntext** se utiliza el tipo de datos) que se omiten antes de comenzar a leer el **texto**, **imagen**, o **ntext** datos.  
  
 *tamaño*  
 Es el número de bytes (cuando la **texto** o **imagen** se utilizan tipos de datos) o caracteres (cuando la **ntext** se utiliza el tipo de datos) de datos que se va a leer. Si *tamaño* es 0, se leen 4 KB de datos.  
  
 HOLDLOCK  
 Hace que se bloquee el valor de texto para lectura hasta el final de la transacción. Otros usuarios pueden leer el valor, pero no pueden modificarlo.  
  
## <a name="remarks"></a>Comentarios  
 Use la [TEXTPTR](../../t-sql/functions/text-and-image-functions-textptr-transact-sql.md) función para obtener un válido *text_ptr* valor. TEXTPTR devuelve un puntero a la **texto**, **ntext**, o **imagen** columna de la fila especificada o a la **texto**, **ntext** , o **imagen** columna en la última fila devuelta por la consulta si se devuelve más de una fila. Debido a que TEXTPTR devuelve una cadena binaria de 16 bytes, se recomienda declarar una variable local para que contenga el puntero de texto y, a continuación, utilizar la variable con READTEXT. Para obtener más información acerca de cómo declarar una variable local, consulte [DECLARE @local_variable &#40; Transact-SQL &#41; ](../../t-sql/language-elements/declare-local-variable-transact-sql.md).  
  
 En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], pueden existir punteros de texto consecutivos, aunque quizás no sean válidos. Para obtener más información sobre la **texto de fila** opción, vea [sp_tableoption &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md). Para obtener más información acerca de cómo invalidar punteros de texto, consulte [sp_invalidate_textptr &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-invalidate-textptr-transact-sql.md).  
  
 El valor de la @@TEXTSIZE función reemplaza el tamaño especificado para READTEXT si es menor que el tamaño especificado para READTEXT. El @@TEXTSIZE función especifica el límite del número de bytes de datos que se devolverán conjunto mediante la instrucción SET TEXTSIZE. Para obtener más información sobre cómo establecer la configuración de sesión para TEXTSIZE, consulte [SET TEXTSIZE &#40; Transact-SQL &#41; ](../../t-sql/statements/set-textsize-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 Los permisos READTEXT se conceden de manera predeterminada a los usuarios con permisos SELECT para la tabla especificada. Los permisos se pueden transferir cuando se transfieren los permisos SELECT.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se lee desde el carácter dos al veintiséis de la columna `pr_info` de la tabla `pub_info`.  
  
> [!NOTE]  
>  Para ejecutar este ejemplo, debe instalar la **pubs** base de datos de ejemplo.  
  
```  
USE pubs;  
GO  
DECLARE @ptrval varbinary(16);  
SELECT @ptrval = TEXTPTR(pr_info)   
   FROM pub_info pr INNER JOIN publishers p  
      ON pr.pub_id = p.pub_id   
      AND p.pub_name = 'New Moon Books'  
READTEXT pub_info.pr_info @ptrval 1 25;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [@@TEXTSIZE &#40;Transact-SQL&#41;](../../t-sql/functions/textsize-transact-sql.md)   
 [UPDATETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/updatetext-transact-sql.md)   
 [WRITETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/writetext-transact-sql.md)  
  
  

