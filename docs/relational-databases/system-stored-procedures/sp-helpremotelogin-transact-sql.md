---
title: sp_helpremotelogin (Transact-SQL) | Documentos de Microsoft
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
- sp_helpremotelogin_TSQL
- sp_helpremotelogin
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpremotelogin
ms.assetid: 93f50869-2627-4642-899f-8f626f8833f4
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1c47b54288d561377444ed8797b2e493c483f8bb
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sphelpremotelogin-transact-sql"></a>sp_helpremotelogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Presenta información acerca de los inicios de sesión remotos de un servidor remoto específico o acerca de todos los servidores remotos definidos en el servidor local.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)] Utilice servidores vinculados y procedimientos almacenados de servidores vinculados en su lugar.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helpremotelogin [ [ @remoteserver = ] 'remoteserver' ]   
     [ , [ @remotename = ] 'remote_name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @remoteserver **=** ] **'***remoteserver***'**  
 Es el servidor remoto cuya información de inicio de sesión remoto se va a devolver. *remoteserver* es **sysname**, su valor predeterminado es null. Si *remoteserver* no es se especifica, se devuelve información sobre todos los servidores remotos definidos en el servidor local.  
  
 [ @remotename **=** ] **'***remote_name***'**  
 Es un inicio de sesión remoto específico en el servidor remoto. *remote_name* es **sysname**, su valor predeterminado es null. Si *remote_name* no se especifica, obtener información acerca de todos los usuarios remotos definidos para *remoteserver* se devuelve.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|servidores|**sysname**|Nombre de un servidor remoto definido en el servidor local.|  
|local_user_name|**sysname**|Inicio de sesión del servidor local al que está asociado el inicio de sesión remoto.|  
|remote_user_name|**sysname**|Inicio de sesión en el servidor remoto que se asigna a local_user_name.|  
|opciones|**sysname**|Trusted = El inicio de sesión remoto no necesita contraseña cuando se conecta con el servidor local desde el servidor remoto.<br /><br /> Untrusted (o en blanco) = El inicio de sesión remoto tiene que suministrar una contraseña cuando se conecta con el servidor local desde el servidor remoto.|  
  
## <a name="remarks"></a>Comentarios  
 Utilice sp_helpserver para presentar los nombres de servidores remotos definidos en el servidor local.  
  
## <a name="permissions"></a>Permissions  
 No se comprueba ningún permiso.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-reporting-help-on-a-single-server"></a>A. Presentar información acerca de un solo servidor  
 En el siguiente ejemplo se presenta información acerca de todos los usuarios remotos del servidor remoto `Accounts`.  
  
```  
EXEC sp_helpremotelogin 'Accounts';  
```  
  
### <a name="b-reporting-help-on-all-remote-users"></a>B. Presentar información acerca de todos los usuarios remotos  
 En el siguiente ejemplo se presenta información acerca de todos los usuarios remotos de todos los servidores remotos conocidos por el servidor local.  
  
```  
EXEC sp_helpremotelogin;  
```  
  
## <a name="see-also"></a>Vea también  
 [sp_addremotelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addremotelogin-transact-sql.md)   
 [sp_dropremotelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropremotelogin-transact-sql.md)   
 [sp_helpserver & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [sp_remoteoption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-remoteoption-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
