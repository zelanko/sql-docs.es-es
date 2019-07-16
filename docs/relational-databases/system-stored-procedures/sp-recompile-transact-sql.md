---
title: sp_recompile (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_recompile_TSQL
- sp_recompile
dev_langs:
- TSQL
helpviewer_keywords:
- sp_recompile
ms.assetid: 6192ca87-febd-4075-8199-14b4fa609b8c
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0f9b72c1a97c17f975144ad0fd364260afab1fb8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68002565"
---
# <a name="sprecompile-transact-sql"></a>sp_recompile (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Hace que se vuelvan a compilar los procedimientos almacenados, los desencadenadores y las funciones definidas por el usuario la próxima vez que se ejecuten. Para ello, quita el plan existente de la memoria cache de procedimientos que fuerza la creación de un nuevo plan la próxima vez que se ejecuten el procedimiento o el desencadenador. En una colección de [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], se registra el evento SP:CacheInsert en lugar del evento SP:Recompile.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
  
sp_recompile [ @objname = ] 'object'  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @objname=] '*objeto*'  
 El nombre calificado o no calificado de un desencadenador, tabla, vista, procedimiento almacenado o función definida por el usuario de la base de datos actual. *objeto* es **nvarchar(776)** , no tiene ningún valor predeterminado. Si *objeto* es el nombre de un desencadenador de función definido por el usuario, el procedimiento almacenado, desencadenador o procedimiento almacenado o función se volverá a compilar la próxima vez que se ejecute. Si *objeto* es el nombre de una tabla o vista, todos los procedimientos almacenados, desencadenadores o funciones definidas por el usuario que hacen referencia a la tabla o vista se recompilarán la próxima vez que se ejecuten.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o un número distinto de cero (error)  
  
## <a name="remarks"></a>Comentarios  
 sp_recompile busca un objeto solo en la base de datos actual.  
  
 Las consultas que utilizan los procedimientos almacenados o desencadenadores y funciones definidas por el usuario solo se optimizan cuando se compilan. A medida que se crean índices o se realizan otros cambios que afectan a las estadísticas de la base de datos, los procedimientos almacenados, desencadenadores y funciones definidas por el usuario compilados pueden perder eficacia. Al volver a compilar los procedimientos almacenados y desencadenadores que actúan sobre una tabla, puede volver a optimizar las consultas.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vuelve a compilar automáticamente los procedimientos almacenados, desencadenadores y funciones definidas por el usuario cuando esto supone una mejora.  
  
## <a name="permissions"></a>Permisos  
 Requiere el permiso ALTER en el objeto especificado.  
  
## <a name="examples"></a>Ejemplos  
 El siguiente ejemplo provoca que los procedimientos almacenados, desencadenadores y funciones definidas por el usuario que actúan en la tabla `Customer` se vuelvan a compilar la próxima vez que se ejecuten.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_recompile N'Sales.Customer';  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
