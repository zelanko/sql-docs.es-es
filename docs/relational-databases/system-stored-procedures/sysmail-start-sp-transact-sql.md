---
title: sysmail_start_sp (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sysmail_start_sp
- sysmail_start_sp_TSQL
dev_langs: TSQL
helpviewer_keywords: sysmail_start_sp
ms.assetid: 25fd7bb6-cfdd-463f-bea8-c6fcb805d3f5
caps.latest.revision: "32"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: b71422c584a9afad2617aceacfeb73ea4bd6f6e8
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="sysmailstartsp-transact-sql"></a>sysmail_start_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Inicia el Correo electrónico de base de datos iniciando los objetos de [!INCLUDE[ssSB](../../includes/sssb-md.md)] que usa el programa externo.  
  
||  
|-|  
|**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sysmail_start_sp  
```  
  
## <a name="arguments"></a>Argumentos  
 Ninguno  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Ninguno  
  
## <a name="remarks"></a>Comentarios  
 Correo electrónico de base de datos no está habilitada o instalada[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalación. Utilice el Asistente para configuración de Correo electrónico de base de datos con el fin de habilitar e instalar los objetos de Correo electrónico de base de datos.  
  
 Este procedimiento almacenado se encuentra en la **msdb** base de datos. Este procedimiento almacenado inicia la cola de Correo electrónico de base de datos que contiene las solicitudes de mensajes salientes y habilita la activación de [!INCLUDE[ssSB](../../includes/sssb-md.md)] para el programa externo.  
  
 Cuando las colas se inician, el programa externo de Correo electrónico de base de datos puede procesar mensajes. Este procedimiento permite reiniciar las colas después de las colas se han detenido con el **sysmail_stop_sp** procedimiento almacenado.  
  
> [!NOTE]  
>  Este procedimiento almacenado solamente inicia las colas del Correo electrónico de base de datos. No activa la entrega de mensajes de [!INCLUDE[ssSB](../../includes/sssb-md.md)] en la base de datos.  
  
## <a name="permissions"></a>Permissions  
 Permisos de ejecución para este procedimiento de forma predeterminada a los miembros de la **sysadmin** rol fijo de servidor.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se muestra a partir de correo electrónico de base de datos de la **msdb** base de datos. En este ejemplo se da por supuesto que el Correo electrónico de base de datos está habilitado.  
  
```  
USE msdb ;  
GO  
  
EXECUTE dbo.sysmail_start_sp ;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Correo electrónico de base de datos](../../relational-databases/database-mail/database-mail.md)   
 [Opción de configuración de servidor de XPs de correo electrónico de base de datos](../../database-engine/configure-windows/database-mail-xps-server-configuration-option.md)   
 [sysmail_stop_sp &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sysmail-stop-sp-transact-sql.md)   
 [Correo electrónico de base de datos almacenados procedimientos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
