---
title: sp_scriptdynamicupdproc (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_scriptdynamicupdproc_TSQL
- sp_scriptdynamicupdproc
helpviewer_keywords:
- sp_scriptdynamicupdproc
ms.assetid: b4c18863-ed92-4aa2-a04f-7ed832fc9e07
author: stevestein
ms.author: sstein
ms.openlocfilehash: 67ba388871720ff804063f27a378b838d300baf0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68126394"
---
# <a name="spscriptdynamicupdproc-transact-sql"></a>sp_scriptdynamicupdproc (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Genera la instrucción CREATE PROCEDURE que crea un procedimiento almacenado de actualización dinámica. La instrucción UPDATE del procedimiento almacenado personalizado se genera dinámicamente a partir de la sintaxis MCALL que indica las columnas que deben modificarse. Utilice este procedimiento almacenado si el número de índices de la tabla de suscripción va en aumento y el número de columnas modificadas es relativamente pequeño. Este procedimiento almacenado se ejecuta en el publicador en la base de datos de publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_scriptdynamicupdproc [ @artid =] artid  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @artid = ] artid` Es el identificador de artículo. *artid* es **int**, no tiene ningún valor predeterminado.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Devuelve un conjunto de resultados que consta de una sola **nvarchar (4000)** columna. El conjunto de resultados forma la instrucción CREATE PROCEDURE completa que se utiliza para crear el procedimiento almacenado personalizado.  
  
## <a name="remarks"></a>Comentarios  
 **sp_scriptdynamicupdproc** se utiliza en la replicación transaccional. La lógica de scripting predeterminada de MCALL incluye todas las columnas de la instrucción UPDATE y utiliza un mapa de bits para determinar las columnas modificadas. En el supuesto de que una columna no haya cambiado, ésta se restablece a su propio valor, lo que no suele generar ningún problema. Si la columna estuviera indizada, tendría lugar un procesamiento adicional. El enfoque dinámico incluye únicamente las columnas modificadas, lo cual optimiza la cadena UPDATE. No obstante, se incurrirá en un procesamiento adicional en tiempo de ejecución a fin de generar la instrucción UPDATE dinámica. Se recomienda probar los enfoques dinámico y estático y elegir la mejor solución.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor o **db_owner** rol fijo de base de datos se puede ejecutar **sp_scriptdynamicupdproc**.  
  
## <a name="examples"></a>Ejemplos  
 Este ejemplo crea un artículo (con *artid* establecido en **1**) en el **autores** de tabla en la **pubs** de base de datos y especifica que la actualización instrucción es el procedimiento personalizado para ejecutar:  
  
```  
'MCALL sp_mupd_authors'  
```  
  
 Genere los procedimientos almacenados personalizados que debe ejecutar el Agente de distribución en el suscriptor. Para hacerlo, ejecute el siguiente procedimiento almacenado en el publicador:  
  
```  
EXEC sp_scriptdynamicupdproc @artid = '1'  
  
The statement returns:  
  
CREATE PROCEDURE [sp_mupd_authors]   
  @c1 varchar(11),@c2 varchar(40),@c3 varchar(20),@c4 char(12),@c5 varchar(40),@c6 varchar(20),  
  @c7 char(2),@c8 char(5),@c9 bit,@pkc1 varchar(11),@bitmap binary(2)  
as  
  
declare @stmt nvarchar(4000), @spacer nvarchar(1)  
SELECT @spacer =N''  
SELECT @stmt = N'UPDATE [authors] SET '  
  
if substring(@bitmap,1,1) & 2 = 2  
begin  
  select @stmt = @stmt + @spacer + N'[au_lname]' + N'=@2'  
  select @spacer = N','  
end  
if substring(@bitmap,1,1) & 4 = 4  
begin  
  select @stmt = @stmt + @spacer + N'[au_fname]' + N'=@3'  
  select @spacer = N','  
end  
if substring(@bitmap,1,1) & 8 = 8  
begin  
  select @stmt = @stmt + @spacer + N'[phone]' + N'=@4'  
  select @spacer = N','  
end  
if substring(@bitmap,1,1) & 16 = 16  
begin  
  select @stmt = @stmt + @spacer + N'[address]' + N'=@5'  
  select @spacer = N','  
end  
if substring(@bitmap,1,1) & 32 = 32  
begin  
  select @stmt = @stmt + @spacer + N'[city]' + N'=@6'  
  select @spacer = N','  
end  
if substring(@bitmap,1,1) & 64 = 64  
begin  
  select @stmt = @stmt + @spacer + N'[state]' + N'=@7'  
  select @spacer = N','  
end  
if substring(@bitmap,1,1) & 128 = 128  
begin  
  select @stmt = @stmt + @spacer + N'[zip]' + N'=@8'  
  select @spacer = N','  
end  
if substring(@bitmap,2,1) & 1 = 1  
begin  
  select @stmt = @stmt + @spacer + N'[contract]' + N'=@9'  
  select @spacer = N','  
end  
select @stmt = @stmt + N' where [au_id] = @1'  
exec sp_executesql @stmt, N' @1 varchar(11),@2 varchar(40),@3 varchar(20),@4 char(12),@5 varchar(40),  
                             @6 varchar(20),@7 char(2),@8 char(5),@9 bit',@pkc1,@c2,@c3,@c4,@c5,@c6,@c7,@c8,@c9  
  
if @@rowcount = 0  
   if @@microsoftversion>0x07320000  
      exec sp_MSreplraiserror 20598  
```  
  
 Una vez ejecutado este procedimiento almacenado, puede utilizar el script resultante para crear de forma manual el procedimiento almacenado en los suscriptores.  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
