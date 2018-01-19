---
title: WRITETEXT (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 10/23/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- WRITETEXT_TSQL
- WRITETEXT
dev_langs: TSQL
helpviewer_keywords:
- replacing data
- WRITETEXT statement
- updating data [SQL Server]
- nonlogged updating
- minimally logged updating [SQL Server]
- overwriting data
- data updates [SQL Server], WRITETEXT statement
ms.assetid: 80c252fd-a8b8-4a2e-888a-059081ed4109
caps.latest.revision: "52"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: d8c66e4a785fd1d731bd55730a8439f5e796b01f
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/19/2018
---
# <a name="writetext-transact-sql"></a>WRITETEXT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Permite la actualización interactiva, registrada al mínimo de un miembro de **texto**, **ntext**, o **imagen** columna. WRITETEXT sobrescribe completamente los datos existentes en la columna afectada. No se puede utilizar WRITETEXT en **texto**, **ntext**, y **imagen** columnas de vistas.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Utilice los tipos de datos de valor grande y la **.** Cláusula de escritura de la [actualización](../../t-sql/queries/update-transact-sql.md) instrucción en su lugar.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
WRITETEXT [BULK]  
  { table.column text_ptr }  
  [ WITH LOG ] { data }  
```  
  
## <a name="arguments"></a>Argumentos  
 BULK  
 Hace posible que las herramientas de carga carguen flujos de datos binarios. La herramienta debe proporcionar flujos en el nivel de protocolo TDS. Cuando el flujo de datos no esté presente el procesador de consultas omite la opción BULK.  
  
> [!IMPORTANT]  
>  Recomendamos que la opción BULK no se utilice en las aplicaciones basadas en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Es posible que esta opción se modifique o quite en versiones futuras de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 *table* **.column**  
 Es el nombre de la tabla y **texto**, **ntext**, o **imagen** columna que se va a actualizar. Nombres de tablas y columnas deben cumplir las reglas de [identificadores](../../relational-databases/databases/database-identifiers.md). La especificación de los nombres de la base de datos y del propietario es opcional.  
  
 *text_ptr*  
 Es un valor que almacena el puntero a la **texto**, **ntext**, o **imagen** datos. *text_ptr* debe ser **binary (16)**. Para crear un puntero de texto, ejecute una [insertar](../../t-sql/statements/insert-transact-sql.md) o [actualización](../../t-sql/queries/update-transact-sql.md) instrucción con datos que no sean nulos para la **texto**, **ntext**, o **imagen** columna.  
  
 WITH LOG  
 Omitido por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El registro está determinado por el modelo de recuperación vigente para la base de datos.  
  
 *data*  
 Es el nombre de **texto**, **ntext** o **imagen** datos que se va a almacenar. *datos* puede ser un literal o un parámetro. La longitud máxima del texto que se pueden insertar interactivamente con WRITETEXT es de 120 KB aproximadamente para **texto**, **ntext**, y **imagen** datos.  
  
## <a name="remarks"></a>Comentarios  
 Utilice WRITETEXT para reemplazar **texto**, **ntext**, y **imagen** datos y UPDATETEXT para modificar **texto**, **ntext**, y **imagen** datos. UPDATETEXT es más flexible debido a que cambia solo una parte de un **texto**, **ntext**, o **imagen** columna en lugar de toda la columna.  
  
 Para obtener el mejor rendimiento se recomienda **texto**, **ntext**, y **imagen** se insertan o actualizan datos en tamaños de fragmento que sean múltiplos de 8.040 bytes.  
  
 Si el modelo de recuperación de base de datos es simple o masivo, **texto**, **ntext**, y **imagen** operaciones que utilice WRITETEXT son operaciones registradas al mínimo cuando los nuevos datos estuviesen Insertar o anexar.  
  
> [!NOTE]  
>  El registro mínimo no se utiliza cuando se actualizan los datos existentes.  
  
 Para que WRITETEXT funcione correctamente, la columna ya debe contener un puntero de texto válido.  
  
 Si la tabla no existe texto de fila, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ahorra espacio al no inicializar **texto** columnas cuando se agregan valores null explícitos o implícitos en **texto** pueden ser columnas con INSERT y ningún puntero de texto obtener para estos valores NULL. Para inicializar **texto** columnas con valores NULL, utilice la instrucción UPDATE. Si en la tabla existe texto de fila, no es necesario inicializar a valores NULL la columna de texto y siempre es posible obtener un puntero de texto.  
  
 La función de ODBC SQLPutData es más rápida y utiliza menos memoria dinámica que WRITETEXT. Esta función puede insertar hasta 2 gigabytes de **texto**, **ntext**, o **imagen** datos.  
  
 En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], en punteros de texto de fila **texto**, **ntext**, o **imagen** datos puede existir, pero puede no ser válidos. Para obtener información acerca de la opción text in row, vea [sp_tableoption &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md). Para obtener información acerca de cómo invalidar punteros de texto, consulte [sp_invalidate_textptr &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-invalidate-textptr-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso UPDATE en la base de datos especificada. El permiso se puede transferir cuando se transfiere el permiso UPDATE.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente el puntero de texto se sitúa en la variable local `@ptrval` y, a continuación, `WRITETEXT` sitúa la nueva cadena de texto en la fila a la que señala `@ptrval`.  
  
> [!NOTE]  
>  Para ejecutar este ejemplo, debe instalar la base de datos de ejemplo pubs.  
  
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
WRITETEXT pub_info.pr_info @ptrval 'New Moon Books (NMB) has just released another top ten publication. With the latest publication this makes NMB the hottest new publisher of the year!';  
GO  
ALTER DATABASE pubs SET RECOVERY SIMPLE;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [Instrucciones SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [UPDATETEXT &#40; Transact-SQL &#41;](../../t-sql/queries/updatetext-transact-sql.md)  
  
  
