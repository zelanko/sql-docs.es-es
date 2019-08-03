---
title: sp_removedbreplication (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_removedbreplication
- sp_removedbreplication_TSQL
helpviewer_keywords:
- sp_removedbreplication
ms.assetid: cb98d571-d1eb-467b-91f7-a6e091009672
author: stevestein
ms.author: sstein
ms.openlocfilehash: fdae843c3918013ec850c5d807853c10a8f3f190
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771038"
---
# <a name="spremovedbreplication-transact-sql"></a>sp_removedbreplication (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Este procedimiento almacenado quita todos los objetos de replicación de la base de datos de publicación en la instancia del publicador de SQL Server, o en la base de datos de suscripción en la instancia del suscriptor de SQL Server. Ejecute este procedimiento en una base de datos adecuada o, si la ejecución está en el contexto de otra base de datos en la misma instancia, especifique la base de datos donde se deben quitar los objetos de replicación. Este procedimiento no elimina los objetos de otras bases de datos como, por ejemplo, la base de datos de distribución.  
  
> [!NOTE]  
>  Este procedimiento solo debe usarse si los otros métodos para quitar objetos de replicación no han funcionado correctamente.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_removedbreplication [ [ @dbname = ] 'dbname' ]  
    [ , [ @type = ] type ]   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @dbname = ] 'dbname'`Es el nombre de la base de datos. *dbname* es de tipo **sysname**y su valor predeterminado es NULL. Si es NULL, se utiliza la base de datos actual.  
  
`[ @type = ] type`Es el tipo de replicación para la que se quitan los objetos de base de datos. *Type* es de tipo **nvarchar (5)** y puede tener uno de los valores siguientes.  
  
|||  
|-|-|  
|**tran**|Quita los objetos de publicación de replicación transaccional.|  
|**merge**|Quita los objetos de publicación de replicación de mezcla.|  
|**ambos** predeterminada|Quita todos los objetos de publicación de replicación.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_removedbreplication** se utiliza en todos los tipos de replicación.  
  
 **sp_removedbreplication** es útil cuando se restaura una base de datos replicada que no tiene ningún objeto de replicación que deba restaurarse.  
  
 **sp_removedbreplication** no se puede usar en una base de datos marcada como de solo lectura.  
  
## <a name="example"></a>Ejemplo  
 [!code-sql[HowTo#sp_removedbreplication](../../relational-databases/replication/codesnippet/tsql/sp-removedbreplication-t_1.sql)]  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** pueden ejecutar **sp_removedbreplication**.  
  
## <a name="example"></a>Ejemplo  
  
```  
-- Remove replication objects from the subscription database on MYSUB.  
DECLARE @subscriptionDB AS sysname  
SET @subscriptionDB = N'AdventureWorksReplica'  
  
-- Remove replication objects from a subscription database (if necessary).  
USE master  
EXEC sp_removedbreplication @subscriptionDB  
GO  
  
```  
  
## <a name="see-also"></a>Vea también  
 [Disable Publishing and Distribution](../../relational-databases/replication/disable-publishing-and-distribution.md)  (Deshabilitar la publicación y la distribución)  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
