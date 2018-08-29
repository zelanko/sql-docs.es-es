---
title: sysmail_stop_sp (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sysmail_stop_sp_TSQL
- sysmail_stop_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_stop_sp
ms.assetid: 045ee36f-5bf0-4626-b5ee-e84db06ce16f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0d52e7f18373303673afc3e5ef67aeb91e094360
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43021139"
---
# <a name="sysmailstopsp-transact-sql"></a>sysmail_stop_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Detiene el Correo electrónico de base de datos deteniendo los objetos de [!INCLUDE[ssSB](../../includes/sssb-md.md)] que usa el programa externo.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sysmail_stop_sp  
```  
  
## <a name="arguments"></a>Argumentos  
 None  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Notas  
 Este procedimiento almacenado se encuentra en la **msdb** base de datos.  
  
 Este procedimiento almacenado detiene la cola de Correo electrónico de base de datos que contiene las solicitudes de mensajes salientes y desactiva la activación de [!INCLUDE[ssSB](../../includes/sssb-md.md)] para el programa externo.  
  
 Cuando las colas se detienen, el programa externo de Correo electrónico de base de datos no procesa mensajes. Este procedimiento almacenado permite detener el Correo electrónico de base de datos para solucionar problemas o realizar tareas de mantenimiento.  
  
 Para iniciar el correo electrónico de base de datos, use **sysmail_start_sp**. Tenga en cuenta que **sp_send_dbmail** sigue aceptando correo cuando el [!INCLUDE[ssSB](../../includes/sssb-md.md)] se detienen los objetos.  
  
> [!NOTE]  
>  Este procedimiento almacenado solamente detiene las colas del Correo electrónico de base de datos. No desactiva la entrega de mensajes de [!INCLUDE[ssSB](../../includes/sssb-md.md)] en la base de datos. Este procedimiento almacenado no deshabilita los procedimientos almacenados extendidos del Correo electrónico de base de datos para reducir el área expuesta. Para deshabilitar los procedimientos almacenados extendidos, vea el [opción Database Mail XPs](../../database-engine/configure-windows/database-mail-xps-server-configuration-option.md) de la **sp_configure** procedimiento almacenado del sistema.  
  
## <a name="permissions"></a>Permisos  
 Permisos de ejecución de este procedimiento de forma predeterminada a los miembros de la **sysadmin** rol fijo de servidor.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente muestra la detención de correo electrónico de base de datos en el **msdb** base de datos. En este ejemplo se da por supuesto que el Correo electrónico de base de datos está habilitado.  
  
```  
USE msdb ;  
GO  
  
EXECUTE dbo.sysmail_stop_sp ;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Correo electrónico de base de datos](../../relational-databases/database-mail/database-mail.md)   
 [sysmail_start_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-start-sp-transact-sql.md)   
 [Procedimientos almacenados de correo electrónico de base de datos &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
