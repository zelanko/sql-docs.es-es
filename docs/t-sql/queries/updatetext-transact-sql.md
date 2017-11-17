---
title: UPDATETEXT (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 10/23/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- UPDATETEXT
- UPDATETEXT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- text updates [SQL Server]
- updating data [SQL Server]
- data updates [SQL Server], UPDATETEXT statement
- UPDATETEXT statement
ms.assetid: d73c28ee-3972-4afd-af8d-ebbbd9e50793
caps.latest.revision: 34
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 49bd324f97f6ba1d2e8a8120bb502199b4ca0f06
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="updatetext-transact-sql"></a>UPDATETEXT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Actualiza una existente **texto**, **ntext**, o **imagen** campo. Utilice UPDATETEXT para cambiar únicamente una parte de un **texto**, **ntext**, o **imagen** columna en su lugar. Utilice WRITETEXT para actualizar y reemplazar todo **texto**, **ntext**, o **imagen** campo.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Utilice los tipos de datos de valor grande y la **.** Cláusula de escritura de la [actualización](../../t-sql/queries/update-transact-sql.md) instrucción en su lugar.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
UPDATETEXT [BULK] { table_name.dest_column_name dest_text_ptr }  
  { NULL | insert_offset }  
     { NULL | delete_length }  
     [ WITH LOG ]  
     [ inserted_data  
    | { table_name.src_column_name src_text_ptr } ]  
```  
  
## <a name="arguments"></a>Argumentos  
 BULK  
 Hace posible que las herramientas de carga carguen flujos de datos binarios. La herramienta debe proporcionar flujos en el nivel de protocolo TDS. Cuando el flujo de datos no esté presente el procesador de consultas omite la opción BULK.  
  
> [!IMPORTANT]  
>  Recomendamos que la opción BULK no se utilice en las aplicaciones basadas en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Es posible que esta opción se modifique o quite en versiones futuras de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 *table_name* **.** *dest_column_name*  
 Es el nombre de la tabla y **texto**, **ntext**, o **imagen** columna que se va a actualizar. Los nombres de tabla y los nombres de columna deben cumplir las reglas de [identificadores](../../relational-databases/databases/database-identifiers.md). La especificación de los nombres de la base de datos y del propietario es opcional.  
  
 *dest_text_ptr*  
 Es un puntero de texto valor (devuelto por la función TEXTPTR) que señala a la **texto**, **ntext**, o **imagen** que se actualicen los datos. *dest_text_ptr* debe ser **binario (**16**)**.  
  
 *insert_offset*  
 Es la posición de inicio de la actualización a partir de cero. Para **texto** o **imagen** columnas, *insert_offset* es el número de bytes que se van a omitir desde el principio de la columna existente antes de insertar nuevos datos. Para **ntext** columnas, *insert_offset*es el número de caracteres (cada **ntext** caracteres utiliza 2 bytes). Existente **texto**, **ntext**, o **imagen** datos a partir de esta posición inicial basada en cero se desplazan a la derecha para dejar espacio a los nuevos datos. Un valor 0 inserta los nuevos datos al principio de los datos existentes. Un valor NULL anexa los nuevos datos al valor de datos existente.  
  
 *delete_length*  
 Es la longitud de datos que se va a eliminar de las existentes **texto**, **ntext**, o **imagen** columna, empezando en el *insert_offset* posición. El *delete_length*se expresa en bytes para **texto** y **imagen** columnas y en caracteres para **ntext** columnas. Cada **ntext** caracteres utiliza 2 bytes. Con un valor 0 no se eliminan datos. Un valor null eliminan todos los datos de la *insert_offset* posición hasta el final de la existente **texto** o **imagen** columna.  
  
 WITH LOG  
 El registro está determinado por el modelo de recuperación vigente para la base de datos.  
  
 *i nserted_data*  
 Son los datos que se va a insertar en las existentes **texto**, **ntext**, o **imagen** columna en el *insert_offset* ubicación. Se trata de una sola **char**, **nchar**, **varchar**, **nvarchar**, **binario**,  **varbinary**, **texto**, **ntext**, o **imagen** valor. *i nserted_data* puede ser un literal o una variable.  
  
 *table_name.src_column_name*  
 Es el nombre de la tabla y **texto**, **ntext**, o **imagen** columna utilizada como el origen de los datos insertados. Los nombres de las tablas y de las columnas se deben ajustar a las reglas para los identificadores.  
  
 *src_text_ptr*  
 Es un puntero de texto valor (devuelto por la función TEXTPTR) que señala a un **texto**, **ntext**, o **imagen** columna utilizada como el origen de los datos insertados.  
  
> [!NOTE]  
>  *scr_text_ptr* valor no debe ser el mismo que *dest_text_ptr*valor.  
  
## <a name="remarks"></a>Comentarios  
 Los datos recién insertados pueden ser una sola *i nserted_data* constante, nombre de la tabla, nombre de columna o puntero de texto.  
  
|Acción de actualización|Parámetros de UPDATETEXT|  
|-------------------|---------------------------|  
|Para sustituir los datos existentes|Especifique un NULL *insert_offset* valor, un valor distinto de cero *delete_length* valor y los nuevos datos que se va a insertar.|  
|Para eliminar datos existentes|Especifique un NULL *insert_offset* valor y un valor distinto de cero *delete_length*. No especifique nuevos datos para la inserción.|  
|Para insertar nuevos datos|Especifique el *insert_offset* valor, un *delete_length* de 0 y los nuevos datos que se va a insertar.|  
  
 Para obtener el mejor rendimiento se recomienda **texto**, **ntext** y **imagen** se insertan o actualizan datos en tamaños de fragmentos que sean múltiplos de 8.040 bytes.  
  
 En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], punteros de texto en fila **texto**, **ntext**, o **imagen** datos puede existir, pero puede no ser válidos. Para obtener información acerca de la opción text in row, vea [sp_tableoption &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md). Para obtener información acerca de cómo invalidar punteros de texto, consulte [sp_invalidate_textptr &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-invalidate-textptr-transact-sql.md).  
  
 Para inicializar **texto** columnas con valores NULL, utilice WRITETEXT; UPDATETEXT inicializa **texto** columnas en una cadena vacía.  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso UPDATE en la base de datos especificada.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se coloca el puntero de texto en la variable local `@ptrval`; a continuación, se utiliza `UPDATETEXT` para actualizar un error de ortografía.  
  
> [!NOTE]  
>  Para ejecutar este ejemplo, debe instalar la base de datos pubs.  
  
```  
USE pubs;  
GO  
ALTER DATABASE pubs SET RECOVERY SIMPLE;  
GO  
DECLARE @ptrval binary(16);  
SELECT @ptrval = TEXTPTR(pr_info)   
   FROM pub_info pr, publishers p  
      WHERE p.pub_id = pr.pub_id   
      AND p.pub_name = 'New Moon Books'  
UPDATETEXT pub_info.pr_info @ptrval 88 1 'b';  
GO  
ALTER DATABASE pubs SET RECOVERY FULL;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [READTEXT &#40; Transact-SQL &#41;](../../t-sql/queries/readtext-transact-sql.md)   
 [TEXTPTR &#40; Transact-SQL &#41;](../../t-sql/functions/text-and-image-functions-textptr-transact-sql.md)   
 [WRITETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/writetext-transact-sql.md)  
  
  

