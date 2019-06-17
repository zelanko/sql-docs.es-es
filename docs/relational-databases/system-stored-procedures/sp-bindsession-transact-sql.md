---
title: sp_bindsession (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_bindsession
- sp_bindsession_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_bindsession
ms.assetid: 1436fe21-ad00-4a98-aca1-1451a5e571d2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a24c219937341b7c1f9d44515bf52c4de220d4c2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62996606"
---
# <a name="spbindsession-transact-sql"></a>sp_bindsession (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enlaza o desenlaza, una sesión en otras sesiones en la misma instancia de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Las sesiones enlazadas permiten que dos o más sesiones participen en la misma transacción y compartan bloqueos hasta que se emita una instrucción ROLLBACK TRANSACTION o COMMIT TRANSACTION.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] En su lugar, utilice conjuntos de resultados activos múltiples (MARS) o transacciones distribuidas. Para obtener más información, vea [Usar conjuntos de resultados activos múltiples &#40;MARS&#41;](../../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_bindsession { 'bind_token' | NULL }  
```  
  
## <a name="arguments"></a>Argumentos  
 **'** *bind_token* **'**  
 Es el token que identifica la transacción obtenido originalmente con **sp_getbindtoken** o los servicios abiertos de datos **srv_getbindtoken** función. *bind_token*is **varchar(255)** .  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="remarks"></a>Comentarios  
 Las dos sesiones enlazadas comparten solo una transacción y bloqueos. Cada sesión conserva su propio nivel de aislamiento y la configuración de un nivel de aislamiento nuevo en una sesión no afecta al nivel de aislamiento de la otra sesión. Cada sesión sigue siendo identificada por su cuenta de seguridad y solo puede tener acceso a los recursos de la base de datos para los que se ha concedido acceso a la cuenta.  
  
 **sp_bindsession** usa un token de enlace para enlazar dos o más sesiones de cliente existentes. Estas sesiones de cliente deben estar en la misma instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)] desde la que se obtuvo el token de enlace. Una sesión es un cliente que ejecuta un comando. Las sesiones de bases de datos enlazadas comparten la transacción y el espacio de bloqueo.  
  
 Un token de enlace obtenido a partir de una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)] no puede utilizarse en una sesión de cliente que esté en otra instancia, incluso si se trata de una transacción DTC. Un token de enlace solamente es válido dentro de cada instancia y no se puede compartir entre varias. Para enlazar las sesiones de cliente en otra instancia de la [!INCLUDE[ssDE](../../includes/ssde-md.md)], debe obtener un token de enlace distinto mediante la ejecución de **sp_getbindtoken**.  
  
 **sp_bindsession** se producirá un error si se utiliza un token que no está activo.  
  
 Desenlazar una sesión, ya sea mediante **sp_bindsession** sin especificar *bind_token* o si se pasa NULL en *bind_token*.  
  
## <a name="permissions"></a>Permisos  
 Debe pertenecer al rol **public** .  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se enlaza el token de enlace especificado a la sesión actual.  
  
> [!NOTE]  
>  El token de enlace que se muestra en el ejemplo se obtuvo ejecutando **sp_getbindtoken** antes de ejecutar **sp_bindsession**.  
  
```  
USE master;  
GO  
EXEC sp_bindsession 'BP9---5---->KB?-V'<>1E:H-7U-]ANZ';  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [sp_getbindtoken &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-getbindtoken-transact-sql.md)   
 [srv_getbindtoken &#40;API procedimiento almacenado extendido&#41;](../../relational-databases/extended-stored-procedures-reference/srv-getbindtoken-extended-stored-procedure-api.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
