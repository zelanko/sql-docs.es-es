---
title: ALTER REMOTE SERVICE BINDING (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 5985acaca76b19a1a863ecc066f6a9da9b900008
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "33066052"
---
# <a name="alter-remote-service-binding-transact-sql"></a>ALTER REMOTE SERVICE BINDING (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
  
 WITH USER = \<*user_name>*  
 Especifica el usuario de base de datos que tiene el certificado asociado con el servicio remoto de este enlace. La clave pública de este certificado se utiliza para cifrar y autenticar mensajes intercambiados con el servicio remoto.  
  
 ANONYMOUS  
 Especifica si se va a utilizar la autenticación anónima en la comunicación con el servicio remoto. Si ANONYMOUS = ON, se utiliza la autenticación anónima y las credenciales del usuario local no se transfieren al servicio remoto. Si ANONYMOUS = OFF, las credenciales de usuario se transfieren. Si no se especifica esta cláusula, el valor predeterminado es OFF.  
  
## <a name="remarks"></a>Notas  
 La clave pública del certificado asociado a *user_name* se usa para autenticar mensajes enviados al servicio remoto y para cifrar una clave de sesión que se usará después para cifrar la conversación. El certificado de *user_name* debe corresponder al certificado de un inicio de sesión en la base de datos que hospede el servicio remoto.  
  
## <a name="permissions"></a>Permisos  
 De manera predeterminada, el permiso para modificar un enlace de servicio remoto corresponde al propietario del enlace de servicio remoto, a los miembros del rol fijo de base de datos **db_owner** y a los miembros del rol fijo de servidor **sysadmin**.  
  
 El usuario que ejecuta la instrucción ALTER REMOTE SERVICE BINDING debe tener permiso de suplantación del usuario especificado en la instrucción.  
  
 Para modificar AUTHORIZATION para un enlace de servicio remoto, utilice la instrucción ALTER AUTHORIZATION.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se cambia el enlace de servicio remoto `APBinding` para cifrar mensajes mediante los certificados de la cuenta `SecurityAccount`.  
  
```  
ALTER REMOTE SERVICE BINDING APBinding  
    WITH USER = SecurityAccount ;  
```  
  
## <a name="see-also"></a>Ver también  
 [CREATE REMOTE SERVICE BINDING &#40;Transact-SQL&#41;](../../t-sql/statements/create-remote-service-binding-transact-sql.md)   
 [DROP REMOTE SERVICE BINDING &#40;Transact-SQL&#41;](../../t-sql/statements/drop-remote-service-binding-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
