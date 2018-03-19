---
title: READTEXT (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 10/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
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
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: c1659dfcc9ca8908ce756eb41b32fd30649decfa
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="readtext-transact-sql"></a>READTEXT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Lee los valores **text**, **ntext** o **image** de una columna **text**, **ntext** o **image**; comienza a partir de un desplazamiento especificado y lee el número de bytes determinado.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use la función [SUBSTRING](../../t-sql/functions/substring-transact-sql.md) en su lugar.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
READTEXT { table.column text_ptr offset size } [ HOLDLOCK ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *table* **.** *column*  
 Es el nombre de la tabla y de la columna donde se va a leer. Los nombres de tablas y columnas deben cumplir las reglas de los [identificadores](../../relational-databases/databases/database-identifiers.md). Es necesario especificar los nombres de la tabla y de la columna; sin embargo, es opcional especificar el nombre de la base de datos y del propietario.  
  
 *text_ptr*  
 Es un puntero de texto válido. *text_ptr* debe ser **binary(16)**.  
  
 *offset*  
 Es el número de bytes (cuando se usan los tipos de datos **text** o **image**) o de caracteres (cuando se usa el tipo de datos **ntext**) que se va a omitir antes de empezar a leer los datos de tipo **text**, **image** o **ntext**.  
  
 *size*  
 Es el número de bytes (cuando se usan los tipos de datos **text** o **image**) o de caracteres (cuando se usa el tipo de datos **ntext**) de los datos que se van a leer. Si *size* es 0, se leen 4 KB de datos.  
  
 HOLDLOCK  
 Hace que se bloquee el valor de texto para lectura hasta el final de la transacción. Otros usuarios pueden leer el valor, pero no pueden modificarlo.  
  
## <a name="remarks"></a>Notas  
 Use la función [TEXTPTR](../../t-sql/functions/text-and-image-functions-textptr-transact-sql.md) para obtener un valor de *text_ptr* válido. TEXTPTR devuelve un puntero para la columna **text**, **ntext** o **image** de la fila especificada o para la columna **text**, **ntext** o **image** de la última fila devuelta por la consulta si se devuelve más de una fila. Debido a que TEXTPTR devuelve una cadena binaria de 16 bytes, se recomienda declarar una variable local para que contenga el puntero de texto y, a continuación, utilizar la variable con READTEXT. Para más información sobre la declaración de una variable local, vea [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md).  
  
 En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], pueden existir punteros de texto consecutivos, aunque quizás no sean válidos. Para más información sobre la opción **text in row**, vea [sp_tableoption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md). Para más información sobre cómo invalidar punteros de texto, vea [sp_invalidate_textptr &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-invalidate-textptr-transact-sql.md).  
  
 El valor de la función @@TEXTSIZE reemplaza el tamaño especificado para READTEXT si es menor que este. La función @@TEXTSIZE especifica el límite que la instrucción SET TEXTSIZE establece sobre el número de bytes de datos que se va a devolver. Para más información sobre cómo establecer la configuración de sesión para TEXTSIZE, vea [SET TEXTSIZE &#40;Transact-SQL&#41;](../../t-sql/statements/set-textsize-transact-sql.md).  
  
## <a name="permissions"></a>Permisos  
 Los permisos READTEXT se conceden de manera predeterminada a los usuarios con permisos SELECT para la tabla especificada. Los permisos se pueden transferir cuando se transfieren los permisos SELECT.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se lee desde el carácter dos al veintiséis de la columna `pr_info` de la tabla `pub_info`.  
  
> [!NOTE]  
>  Para ejecutar este ejemplo, es necesario instalar la base de datos de ejemplo **pubs**.  
  
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
  
## <a name="see-also"></a>Ver también  
 [@@TEXTSIZE &#40;Transact-SQL&#41;](../../t-sql/functions/textsize-transact-sql.md)   
 [UPDATETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/updatetext-transact-sql.md)   
 [WRITETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/writetext-transact-sql.md)  
  
  
