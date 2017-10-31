---
title: Crear enlace de servicio remoto (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE REMOTE SERVICE BINDING
- SERVICE_BINDING_TSQL
- CREATE REMOTE SERVICE
- REMOTE_TSQL
- CREATE_REMOTE_SERVICE_BINDING_TSQL
- CREATE_REMOTE_SERVICE_TSQL
- BINDING
- SERVICE BINDING
- BINDING_TSQL
- CREATE_REMOTE_TSQL
- REMOTE_SERVICE_TSQL
- CREATE REMOTE
- REMOTE SERVICE
- REMOTE_SERVICE_BINDING_TSQL
- REMOTE
- REMOTE SERVICE BINDING
dev_langs:
- TSQL
helpviewer_keywords:
- binding remote service [Service Broker]
- dialog security [Service Broker]
- end-to-end security [Service Broker]
- security [Service Broker], remote service bindings
- CREATE REMOTE SERVICE BINDING statement
- conversation security [Service Broker]
- remote service bindings [Service Broker], creating
ms.assetid: 4165c404-4d50-4063-9a6e-6e267d309376
caps.latest.revision: 46
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a4083cb617d76084719450a6abc49fd76345cc7a
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="create-remote-service-binding-transact-sql"></a>CREATE REMOTE SERVICE BINDING (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea un enlace que define las credenciales de seguridad que se utilizarán para iniciar una conversación con un servicio remoto.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
CREATE REMOTE SERVICE BINDING binding_name   
   [ AUTHORIZATION owner_name ]   
   TO SERVICE 'service_name'   
   WITH  USER = user_name [ , ANONYMOUS = { ON | OFF } ]  
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *binding_name*  
 Es el nombre del enlace de servicio remoto que se va a crear. No se pueden especificar nombres de servidor, base de datos o esquema. El *binding_name* debe ser válido **sysname**.  
  
 AUTORIZACIÓN *owner_name*  
 Establece el propietario del enlace en el usuario o el rol de base de datos que se ha especificado. Cuando el usuario actual es **dbo** o **sa**, *owner_name* puede ser el nombre de cualquier usuario o rol válidos. En caso contrario, *owner_name* debe ser el nombre del usuario actual, el nombre de un usuario que el usuario actual tiene permisos IMPERSONATE o el nombre de un rol al que pertenece el usuario actual.  
  
 AL servicio '*service_name*'  
 Especifica el servicio remoto que se enlazará al usuario identificado en la cláusula WITH USER.  
  
 USUARIO = *user_name*  
 Especifica la entidad de seguridad de base de datos que posee el certificado asociado con el servicio remoto identificado por la cláusula TO SERVICE. Este certificado se utiliza para el cifrado y la autenticación de los mensajes que se intercambian con el servicio remoto.  
  
 ANONYMOUS  
 Especifica si se va a utilizar la autenticación anónima en la comunicación con el servicio remoto. Si ANONYMOUS = ON, se utiliza la autenticación anónima y se producen operaciones en la base de datos remoto como un miembro de la **público** rol fijo de base de datos. Si ANONYMOUS = OFF, las operaciones en la base de datos remota se realizan como un usuario específico de esa base de datos. Si no se especifica esta cláusula, el valor predeterminado es OFF.  
  
## <a name="remarks"></a>Comentarios  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] usa un enlace de servicio remoto para encontrar el certificado que se utilizará en una nueva conversación. La clave pública del certificado asociado con *nombre_usuario* se utiliza para autenticar los mensajes enviados al servicio remoto y para cifrar una clave de sesión que, a continuación, se utiliza para cifrar la conversación. El certificado para *nombre_usuario* debe corresponder al certificado de un usuario en la base de datos que hospeda el servicio remoto.  
  
 Un enlace de servicio remoto solo es necesario para servicios iniciadores que se comunican con servicios de destino que están fuera de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Una base de datos que hospeda un servicio iniciador debe contener enlaces de servicio remoto para todos los servicios de destino que están fuera de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La base de datos que hospeda un servicio de destino no necesita contener enlaces de servicio remoto para los servicios iniciadores que se comunican con el servicio de destino. Cuando los servicios iniciador y de destino están en la misma instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], no es necesario ningún enlace de servicio remoto. Sin embargo, si un enlace de servicio remoto es aquella en que presente la *service_name* especificado para TO SERVICE coincide con el nombre del servicio local, [!INCLUDE[ssSB](../../includes/sssb-md.md)] utilizará el enlace.  
  
 Cuando ANONYMOUS = ON, el servicio iniciador se conecta al servicio de destino como miembro de la **público** rol fijo de base de datos. De manera predeterminada, los miembros de este rol no tienen permiso para conectarse a una base de datos. Para enviar correctamente un mensaje, la base de datos de destino debe conceder el **público** rol permiso CONNECT para la base de datos y permiso SEND para el servicio de destino.  
  
 Cuando un usuario posee más de un certificado, [!INCLUDE[ssSB](../../includes/sssb-md.md)] selecciona, entre todos los certificados válidos y marcados como AVAILABLE FOR BEGIN_DIALOG, el que tenga la fecha de vencimiento más tardía.  
  
## <a name="permissions"></a>Permissions  
 Permisos para crear un control remoto del servicio de enlace predeterminada para el usuario mencionado en la cláusula de usuario, los miembros de la **db_owner** rol fijo de base de datos, los miembros de la **db_ddladmin** fijo de rol de base de datos y los miembros de la **sysadmin** rol fijo de servidor.  
  
 El usuario que ejecuta la instrucción CREATE REMOTE SERVICE BINDING debe tener permiso de suplantación para la entidad de seguridad especificada en la instrucción.  
  
 Un enlace de servicio remoto no puede ser un objeto temporal. Nombres de enlace de servicio remoto que empiecen por  **#**  se permiten, pero son objetos permanentes.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-creating-a-remote-service-binding"></a>A. Crear un enlace de servicio remoto  
 En el ejemplo siguiente se crea un enlace para el servicio `//Adventure-Works.com/services/AccountsPayable`. [!INCLUDE[ssSB](../../includes/sssb-md.md)] utiliza el certificado de la entidad de seguridad de base de datos `APUser` para autenticarse en el servicio remoto e intercambiar la clave de cifrado de sesión con el servicio remoto.  
  
```  
CREATE REMOTE SERVICE BINDING APBinding  
    TO SERVICE '//Adventure-Works.com/services/AccountsPayable'  
    WITH USER = APUser ;  
```  
  
### <a name="b-creating-a-remote-service-binding-using-anonymous-authentication"></a>B. Crear un enlace de servicio remoto con autenticación anónima  
 En el ejemplo siguiente se crea un enlace para el servicio `//Adventure-Works.com/services/AccountsPayable`. [!INCLUDE[ssSB](../../includes/sssb-md.md)] utiliza el certificado de la entidad de seguridad de base de datos `APUser` para intercambiar la clave de cifrado de sesión con el servicio remoto. Service Broker no se autentica en el servicio remoto. En la base de datos que hospeda el servicio remoto, los mensajes se entregan como el **invitado** usuario.  
  
```  
CREATE REMOTE SERVICE BINDING APBinding  
    TO SERVICE '//Adventure-Works.com/services/AccountsPayable'  
    WITH USER = APUser, ANONYMOUS=ON ;  
```  
  
## <a name="see-also"></a>Vea también  
 [Modificar enlace de servicio remoto &#40; Transact-SQL &#41;](../../t-sql/statements/alter-remote-service-binding-transact-sql.md)   
 [QUITAR el enlace de servicio remoto &#40; Transact-SQL &#41;](../../t-sql/statements/drop-remote-service-binding-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  

