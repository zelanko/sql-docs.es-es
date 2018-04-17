---
title: sp_bindsession (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_bindsession
- sp_bindsession_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_bindsession
ms.assetid: 1436fe21-ad00-4a98-aca1-1451a5e571d2
caps.latest.revision: 38
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f7d47d969caa2e4f93482f4f457971d32c179264
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="spbindsession-transact-sql"></a>sp_bindsession (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enlaza o desenlaza, una sesión con otras sesiones en la misma instancia de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Las sesiones enlazadas permiten que dos o más sesiones participen en la misma transacción y compartan bloqueos hasta que se emita una instrucción ROLLBACK TRANSACTION o COMMIT TRANSACTION.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] En su lugar, utilice conjuntos de resultados activos múltiples (MARS) o transacciones distribuidas. Para obtener más información, vea [utilizando conjuntos de resultados activos múltiples & #40; MARS & #41; ](../../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_bindsession { 'bind_token' | NULL }  
```  
  
## <a name="arguments"></a>Argumentos  
 **'** *bind_token* **'**  
 Es el símbolo (token) que identifica la transacción obtenida originalmente con **sp_getbindtoken** o los servicios abiertos de datos **srv_getbindtoken** función. *bind_token*es **varchar (255)**.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="remarks"></a>Comentarios  
 Las dos sesiones enlazadas comparten solo una transacción y bloqueos. Cada sesión conserva su propio nivel de aislamiento y la configuración de un nivel de aislamiento nuevo en una sesión no afecta al nivel de aislamiento de la otra sesión. Cada sesión sigue siendo identificada por su cuenta de seguridad y solo puede tener acceso a los recursos de la base de datos para los que se ha concedido acceso a la cuenta.  
  
 **sp_bindsession** usa un token de enlace para enlazar dos o más sesiones de cliente existentes. Estas sesiones de cliente deben estar en la misma instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)] desde la que se obtuvo el token de enlace. Una sesión es un cliente que ejecuta un comando. Las sesiones de bases de datos enlazadas comparten la transacción y el espacio de bloqueo.  
  
 Un token de enlace obtenido a partir de una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)] no puede utilizarse en una sesión de cliente que esté en otra instancia, incluso si se trata de una transacción DTC. Un token de enlace solamente es válido dentro de cada instancia y no se puede compartir entre varias. Para enlazar las sesiones de cliente en otra instancia de la [!INCLUDE[ssDE](../../includes/ssde-md.md)], debe obtener un token de enlace distinto mediante la ejecución de **sp_getbindtoken**.  
  
 **sp_bindsession** producirá un error si se utiliza un token que no está activo.  
  
 Desenlazar una sesión mediante **sp_bindsession** sin especificar *bind_token* o si se pasa NULL en *bind_token*.  
  
## <a name="permissions"></a>Permissions  
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
 [sp_getbindtoken & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-getbindtoken-transact-sql.md)   
 [srv_getbindtoken &#40;API procedimiento almacenado extendido&#41;](../../relational-databases/extended-stored-procedures-reference/srv-getbindtoken-extended-stored-procedure-api.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
