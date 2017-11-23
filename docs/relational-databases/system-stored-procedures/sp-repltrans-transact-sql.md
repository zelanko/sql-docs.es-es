---
title: sp_repltrans (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_repltrans_TSQL
- sp_repltrans
helpviewer_keywords: sp_repltrans
ms.assetid: 738e2322-335b-44fa-820e-f31c02743978
caps.latest.revision: "15"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2123841f5819842df4a4833e1a243dbfbeddf7dc
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="sprepltrans-transact-sql"></a>sp_repltrans (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve un conjunto de resultados con todas las transacciones del registro de transacciones de la base de datos de publicaciones que están marcadas para replicación pero que no se han marcado como distribuidas. Este procedimiento almacenado se ejecuta en el publicador de una base de datos de publicaciones.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_repltrans  
```  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 **sp_repltrans** devuelve información acerca de la base de datos de publicación desde la que se ejecuta, lo que le permite ver las transacciones que actualmente no están distribuidas (aquellas transacciones que permanecen en el registro de transacciones que no se han enviado a la Distribuidor). El conjunto de resultados muestra los números de secuencia del registro relativos al primer y último registro de cada transacción. **sp_repltrans** es similar a [sp_replcmds &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md) pero no devuelve los comandos de las transacciones.  
  
## <a name="remarks"></a>Comentarios  
 **sp_repltrans** se utiliza en la replicación transaccional.  
  
 **sp_repltrans** no se admite para no -[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicadores.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor o el **db_owner** rol fijo de base de datos puede ejecutar **sp_repltrans**.  
  
## <a name="see-also"></a>Vea también  
 [sp_repldone &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md)   
 [sp_replflush &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
