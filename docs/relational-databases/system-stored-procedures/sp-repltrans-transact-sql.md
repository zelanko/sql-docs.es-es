---
title: sp_repltrans (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_repltrans_TSQL
- sp_repltrans
helpviewer_keywords:
- sp_repltrans
ms.assetid: 738e2322-335b-44fa-820e-f31c02743978
author: stevestein
ms.author: sstein
ms.openlocfilehash: 40477973efebac9a484e89e7627f0996285b430b
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2019
ms.locfileid: "68770860"
---
# <a name="sprepltrans-transact-sql"></a>sp_repltrans (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Devuelve un conjunto de resultados con todas las transacciones del registro de transacciones de la base de datos de publicaciones que están marcadas para replicación pero que no se han marcado como distribuidas. Este procedimiento almacenado se ejecuta en el publicador de una base de datos de publicaciones.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_repltrans  
```  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 **sp_repltrans** devuelve información acerca de la base de datos de publicación desde la que se ejecuta, lo que le permite ver las transacciones que actualmente no están distribuidas (aquellas transacciones que permanecen en el registro de transacciones que no se han enviado al distribuidor). El conjunto de resultados muestra los números de secuencia del registro relativos al primer y último registro de cada transacción. **sp_repltrans** es similar a [sp_replcmds &#40;de Transact-&#41; SQL,](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md) pero no devuelve los comandos de las transacciones.  
  
## <a name="remarks"></a>Comentarios  
 **sp_repltrans** se utiliza en la replicación transaccional.  
  
 **sp_repltrans** no se admite para publicadores [!INCLUDE[msCoName](../../includes/msconame-md.md)] que no son de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** o del rol fijo de base de datos **db_owner** pueden ejecutar **sp_repltrans**.  
  
## <a name="see-also"></a>Vea también  
 [sp_repldone &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md)   
 [sp_replflush &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
