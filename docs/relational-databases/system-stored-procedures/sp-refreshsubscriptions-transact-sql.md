---
title: sp_refreshsubscriptions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_refreshsubscriptions
- sp_refreshsubscriptions_TSQL
helpviewer_keywords:
- sp_refreshsubscriptions
ms.assetid: 6cb9b1ce-1ce7-43ab-9451-201f79ed1ffa
author: stevestein
ms.author: sstein
ms.openlocfilehash: 548285b08ceedab49674b35128216bed320c3e7c
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771184"
---
# <a name="sprefreshsubscriptions-transact-sql"></a>sp_refreshsubscriptions (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Agregue suscripciones a nuevos artículos para todos los suscriptores existentes a una publicación de actualización inmediata. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_refreshsubscriptions [ @publication = ] 'publication'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'`Es la publicación para la que se van a actualizar las suscripciones. *Publication* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Comentarios  
 **sp_refreshsubscriptions** se utiliza en la replicación de instantáneas, transaccional y de mezcla.  
  
 **sp_addarticle** llama a **sp_refreshsubscriptions** para una publicación de actualización inmediata.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** o del rol fijo de base de datos **db_owner** pueden ejecutar **sp_refreshsubscriptions**.  
  
## <a name="see-also"></a>Vea también  
 [sp_addarticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
