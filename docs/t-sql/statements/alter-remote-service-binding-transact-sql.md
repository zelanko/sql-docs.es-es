---
title: ALTER REMOTE SERVICE BINDING (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 50d11dd143e4cb90a48100e6275aa0c3d8eb02ab
ms.sourcegitcommit: b2ab989264dd9d23c184f43fff2ec8966793a727
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/14/2020
ms.locfileid: "86381169"
---
# <a name="alter-remote-service-binding-transact-sql"></a>ALTER REMOTE SERVICE BINDING (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Cambia el usuario asociado a un enlace de servicio remoto o cambia el parámetro de autenticación anónima del enlace.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```syntaxsql
  
ALTER REMOTE SERVICE BINDING binding_name   
   WITH [ USER = <user_name> ] [ , ANONYMOUS = { ON | OFF } ]   
[ ; ]  
```  
  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *binding_name*  
 Nombre del enlace de servicio remoto que se va a cambiar. No se pueden especificar nombres de servidor, base de datos o esquema.  
  
 WITH USER = \<*user_name>*  
 Especifica el usuario de base de datos que tiene el certificado asociado con el servicio remoto de este enlace. La clave pública de este certificado se utiliza para cifrar y autenticar mensajes intercambiados con el servicio remoto.  
  
 ANONYMOUS  
 Especifica si se va a utilizar la autenticación anónima en la comunicación con el servicio remoto. Si ANONYMOUS = ON, se utiliza la autenticación anónima y las credenciales del usuario local no se transfieren al servicio remoto. Si ANONYMOUS = OFF, las credenciales de usuario se transfieren. Si no se especifica esta cláusula, el valor predeterminado es OFF.  
  
## <a name="remarks"></a>Observaciones  
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
  
## <a name="see-also"></a>Consulte también  
 [CREATE REMOTE SERVICE BINDING &#40;Transact-SQL&#41;](../../t-sql/statements/create-remote-service-binding-transact-sql.md)   
 [DROP REMOTE SERVICE BINDING &#40;Transact-SQL&#41;](../../t-sql/statements/drop-remote-service-binding-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
