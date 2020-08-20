---
description: sp_replflush (Transact-SQL)
title: sp_replflush (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replflush
- sp_replflush_TSQL
helpviewer_keywords:
- sp_replflush
ms.assetid: 20809f5f-941d-427f-8f0c-de7a6c487584
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 144bffdd6076b73c8b10fca3c7d9f878d77091d2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88485774"
---
# <a name="sp_replflush-transact-sql"></a>sp_replflush (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Vacía la caché de artículos. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
> [!IMPORTANT]  
>  No debería ser necesario ejecutar este procedimiento manualmente. **sp_replflush** solo se debe usar para solucionar problemas de replicación según lo indicado por un profesional de soporte técnico de replicación experimentado.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_replflush  
```  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Observaciones  
 **sp_replflush** se utiliza en la replicación transaccional.  
  
 Las definiciones de los artículos se almacenan en caché para mejorar la eficacia. otros procedimientos almacenados de replicación utilizan **sp_replflush** siempre que se modifica o se quita una definición de artículo.  
  
 Solamente una conexión de cliente puede tener acceso al registro del LOG de una base de datos determinada. Si un cliente tiene acceso de lector del registro a una base de datos, la ejecución de **sp_replflush** hace que el cliente libere su acceso. Otros clientes pueden examinar el registro de transacciones mediante **sp_replcmds** o **sp_replshowcmds**.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** o del rol fijo de base de datos **db_owner** pueden ejecutar **sp_replflush**.  
  
## <a name="see-also"></a>Consulte también  
 [sp_replcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [sp_repldone &#40;&#41;de Transact-SQL ](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md)   
 [sp_repltrans &#40;&#41;de Transact-SQL ](../../relational-databases/system-stored-procedures/sp-repltrans-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
