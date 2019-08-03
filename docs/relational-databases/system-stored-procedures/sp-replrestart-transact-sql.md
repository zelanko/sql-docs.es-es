---
title: sp_replrestart (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replrestart_TSQL
- sp_replrestart
helpviewer_keywords:
- sp_replrestart
ms.assetid: 111b3dbf-92f8-4670-b156-1468c63e4fc1
author: stevestein
ms.author: sstein
ms.openlocfilehash: a9108ab25d1a23e06ccd93daad5f755a3a65aa44
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2019
ms.locfileid: "68770891"
---
# <a name="spreplrestart-transact-sql"></a>sp_replrestart (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Se utiliza en la replicación transaccional durante las copias de seguridad y restauración para sincronizar los datos replicados del distribuidor con los datos del publicador. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
> [!IMPORTANT]  
>  **sp_replrestart** es un procedimiento almacenado de replicación interno y solo se debe usar al restaurar una base de datos Publicada en una topología de replicación transaccional como se indica en el tema [estrategias para realizar copias de seguridad y restaurar instantáneas y Replicación transaccional](../../relational-databases/replication/administration/strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_replrestart  
```  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_replrestart** se utiliza cuando el valor de número de secuencia de registro (LSN) más alto del distribuidor no coincide con el valor de LSN más alto del publicador.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** o del rol fijo de base de datos **db_owner** pueden ejecutar **sp_replrestart**.  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
