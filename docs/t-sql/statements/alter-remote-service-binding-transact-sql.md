---
title: Modificar enlace de servicio remoto (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER REMOTE SERVICE BINDING
- ALTER_REMOTE_SERVICE_BINDING_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- remote service bindings [Service Broker], modifying
- ALTER REMOTE SERVICE BINDING statement
- modifying remote service bindings
ms.assetid: ee620b4a-9375-4eaa-a016-69916c9e1e68
caps.latest.revision: 37
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5352750b43775b53a508b42de17d33a792a40b1b
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="alter-remote-service-binding-transact-sql"></a>ALTER REMOTE SERVICE BINDING (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cambia el usuario asociado a un enlace de servicio remoto o cambia el parámetro de autenticación anónima del enlace.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
ALTER REMOTE SERVICE BINDING binding_name   
   WITH [ USER = <user_name> ] [ , ANONYMOUS = { ON | OFF } ]   
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *binding_name*  
 Nombre del enlace de servicio remoto que se va a cambiar. No se pueden especificar nombres de servidor, base de datos o esquema.  
  
 CON usuario = \< *nombre_usuario >*  
 Especifica el usuario de base de datos que tiene el certificado asociado con el servicio remoto de este enlace. La clave pública de este certificado se utiliza para cifrar y autenticar mensajes intercambiados con el servicio remoto.  
  
 ANONYMOUS  
 Especifica si se va a utilizar la autenticación anónima en la comunicación con el servicio remoto. Si ANONYMOUS = ON, se utiliza la autenticación anónima y las credenciales del usuario local no se transfieren al servicio remoto. Si ANONYMOUS = OFF, las credenciales de usuario se transfieren. Si no se especifica esta cláusula, el valor predeterminado es OFF.  
  
## <a name="remarks"></a>Comentarios  
 La clave pública del certificado asociado con *nombre_usuario* se utiliza para autenticar los mensajes enviados al servicio remoto y para cifrar una clave de sesión que, a continuación, se utiliza para cifrar la conversación. El certificado para *nombre_usuario* debe corresponder al certificado de un inicio de sesión en la base de datos que hospeda el servicio remoto.  
  
## <a name="permissions"></a>Permissions  
 Permiso para modificar un enlace de servicio remoto predeterminado es el propietario del servicio remoto de enlace, los miembros de la **db_owner** fijo de rol de base de datos y los miembros de la **sysadmin** rol fijo de servidor.  
  
 El usuario que ejecuta la instrucción ALTER REMOTE SERVICE BINDING debe tener permiso de suplantación del usuario especificado en la instrucción.  
  
 Para modificar AUTHORIZATION para un enlace de servicio remoto, utilice la instrucción ALTER AUTHORIZATION.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se cambia el enlace de servicio remoto `APBinding` para cifrar mensajes mediante los certificados de la cuenta `SecurityAccount`.  
  
```  
ALTER REMOTE SERVICE BINDING APBinding  
    WITH USER = SecurityAccount ;  
```  
  
## <a name="see-also"></a>Vea también  
 [CREATE REMOTE SERVICE BINDING &#40;Transact-SQL&#41;](../../t-sql/statements/create-remote-service-binding-transact-sql.md)   
 [QUITAR el enlace de servicio remoto &#40; Transact-SQL &#41;](../../t-sql/statements/drop-remote-service-binding-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
