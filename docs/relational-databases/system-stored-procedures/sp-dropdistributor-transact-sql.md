---
title: sp_dropdistributor (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_dropdistributor
- sp_dropdistributor_TSQL
helpviewer_keywords:
- sp_dropdistributor
ms.assetid: 0644032f-5ff0-4718-8dde-321bc9967a03
caps.latest.revision: 33
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dfb681d5022e5a5f9ada3f0815513ce020250e79
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="spdropdistributor-transact-sql"></a>sp_dropdistributor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Desinstala el distribuidor. Este procedimiento almacenado se ejecuta en el distribuidor de cualquier base de datos, excepto la de distribución.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_dropdistributor [ [ @no_checks= ] no_checks ]   
    [ , [ @ignore_distributor= ] ignore_distributor ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@no_checks=**] *no_checks*  
 Indica si se comprobará si existen objetos dependientes antes de quitar el distribuidor. *no_checks* es **bits**, con un valor predeterminado es 0.  
  
 Si **0**, **sp_dropdistributor** comprobaciones para asegurarse de que se han quitado todos los objetos de publicación y distribución además del distribuidor.  
  
 Si **1**, **sp_dropdistributor** quita todos los objetos de publicación y distribución antes de desinstalar el distribuidor.  
  
 [  **@ignore_distributor=**] *ignore_distributor*  
 Indica si este procedimiento almacenado se ejecuta sin conectarse al distribuidor. *ignore_distributor* es **bits**, su valor predeterminado es **0**.  
  
 Si **0**, **sp_dropdistributor** se conecta al distribuidor y quita todos los objetos de replicación. Si **sp_dropdistributor** no puede conectarse al distribuidor, el procedimiento almacenado, produce un error.  
  
 Si **1**, se realiza ninguna conexión al distribuidor y no se quitan los objetos de replicación. Esta opción se utiliza cuando el distribuidor se va a desinstalar o cuando está permanentemente sin conexión. Los objetos de este publicador en el distribuidor no se quitan hasta que se vuelva a instalar el distribuidor.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_dropdistributor** se utiliza en todos los tipos de replicación.  
  
 Si existen otros publicador u objetos de distribución en el servidor, **sp_dropdistributor** se produce un error a menos que **@no_checks** está establecido en **1**.  
  
 Este procedimiento almacenado se debe ejecutar después de quitar la base de datos de distribución mediante la ejecución de **sp_dropdistributiondb**.  
  
## <a name="example"></a>Ejemplo  
 [!code-sql[HowTo#sp_DropDistPub](../../relational-databases/replication/codesnippet/tsql/sp-dropdistributor-trans_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor puede ejecutar **sp_dropdistributor**.  
  
## <a name="see-also"></a>Vea también  
 [Disable Publishing and Distribution](../../relational-databases/replication/disable-publishing-and-distribution.md)  (Deshabilitar la publicación y la distribución)  
 [sp_adddistributor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistributor-transact-sql.md)   
 [sp_changedistributor_property &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedistributor-property-transact-sql.md)   
 [sp_helpdistributor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md)   
 [Procedimientos almacenados de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
