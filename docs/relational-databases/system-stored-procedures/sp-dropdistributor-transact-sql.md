---
title: sp_dropdistributor (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropdistributor
- sp_dropdistributor_TSQL
helpviewer_keywords:
- sp_dropdistributor
ms.assetid: 0644032f-5ff0-4718-8dde-321bc9967a03
author: stevestein
ms.author: sstein
ms.openlocfilehash: 032ecf59a3ffba4a7a7a6f4739c92b688858d501
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2019
ms.locfileid: "68768870"
---
# <a name="spdropdistributor-transact-sql"></a>sp_dropdistributor (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Desinstala el distribuidor. Este procedimiento almacenado se ejecuta en el distribuidor de cualquier base de datos, excepto la de distribución.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_dropdistributor [ [ @no_checks= ] no_checks ]   
    [ , [ @ignore_distributor= ] ignore_distributor ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @no_checks = ] no_checks`Indica si se deben comprobar los objetos dependientes antes de quitar el distribuidor. *no_checks* es de **bit**y su valor predeterminado es 0.  
  
 Si es **0**, **sp_dropdistributor** comprueba para asegurarse de que se han quitado todos los objetos de publicación y distribución, además del distribuidor.  
  
 Si es **1**, **sp_dropdistributor** quita todos los objetos de publicación y distribución antes de desinstalar el distribuidor.  
  
`[ @ignore_distributor = ] ignore_distributor`Indica si este procedimiento almacenado se ejecuta sin conectarse al distribuidor. *ignore_distributor* es de **bit**y su valor predeterminado es **0**.  
  
 Si es **0**, **sp_dropdistributor** se conecta al distribuidor y quita todos los objetos de replicación. Si **sp_dropdistributor** no puede conectarse al distribuidor, se produce un error en el procedimiento almacenado.  
  
 Si es **1**, no se establece ninguna conexión con el distribuidor y los objetos de replicación no se quitan. Esta opción se utiliza cuando el distribuidor se va a desinstalar o cuando está permanentemente sin conexión. Los objetos de este publicador en el distribuidor no se quitan hasta que se vuelva a instalar el distribuidor.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_dropdistributor** se utiliza en todos los tipos de replicación.  
  
 Si existen otros objetos de publicador o de distribución en el servidor, **@no_checks** se produce un error en **sp_dropdistributor** a menos que se establezca en **1**.  
  
 Este procedimiento almacenado se debe ejecutar después de quitar la base de datos de distribución mediante la ejecución de **sp_dropdistributiondb**.  
  
## <a name="example"></a>Ejemplo  
 [!code-sql[HowTo#sp_DropDistPub](../../relational-databases/replication/codesnippet/tsql/sp-dropdistributor-trans_1.sql)]  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** pueden ejecutar **sp_dropdistributor**.  
  
## <a name="see-also"></a>Vea también  
 [Disable Publishing and Distribution](../../relational-databases/replication/disable-publishing-and-distribution.md)  (Deshabilitar la publicación y la distribución)  
 [sp_adddistributor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistributor-transact-sql.md)   
 [sp_changedistributor_property &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedistributor-property-transact-sql.md)   
 [sp_helpdistributor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md)   
 [Procedimientos almacenados de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
