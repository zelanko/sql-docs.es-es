---
title: sp_setapprole (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_setapprole
- sp_setapprole_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_setapprole
ms.assetid: cf0901c0-5f90-42d4-9d5b-8772c904062d
caps.latest.revision: 42
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: ac733afa3f8afef74a9d6affb16e0f9dbcd5b4a9
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
ms.locfileid: "33259062"
---
# <a name="spsetapprole-transact-sql"></a>sp_setapprole (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Activa los permisos asociados a un rol de aplicación en la base de datos actual.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_setapprole [ @rolename = ] 'role',  
    [ @password = ] { encrypt N'password' }   
      |  
        'password' [ , [ @encrypt = ] { 'none' | 'odbc' } ]  
        [ , [ @fCreateCookie = ] true | false ]  
    [ , [ @cookie = ] @cookie OUTPUT ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@rolename =** ] **'***rol***'**  
 Es el nombre del rol de aplicación definido en la base de datos actual. *rol* es **sysname**, no tiene ningún valor predeterminado. *rol* debe existir en la base de datos actual.  
  
 [  **@password =** ] **{cifrar N'***contraseña***'}**  
 Es la contraseña necesaria para activar el rol de aplicación. *contraseña* es **sysname**, no tiene ningún valor predeterminado. *contraseña* puede estar protegido mediante el uso de ODBC **cifrar** función. Cuando se usa el **cifrar** función, la contraseña debe convertirse en una cadena Unicode mediante la colocación de **N** antes de la primera comilla.  
  
 La opción de cifrado no se admite en las conexiones que usan **SqlClient**.  
  
> [!IMPORTANT]  
>  ODBC **cifrar** función no proporciona cifrado. No debe confiar a esta función la protección de las contraseñas que se transmiten en una red. Si la información se va a transmitir en una red, utilice SSL o IPSec.  
  
 **@encrypt = 'none'**  
 Especifica que no se utiliza ofuscación. La contraseña se pasa a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como texto simple. Ésta es la opción predeterminada.  
  
 **@encrypt= "odbc"**  
 Especifica que ODBC ofuscará la contraseña utilizando ODBC **cifrar** función antes de enviar la contraseña para el [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Solo se puede especificar cuando se utiliza un cliente ODBC o el Proveedor OLE DB para SQL Server.  
  
 [  **@fCreateCookie =** ] **true** | **false**  
 Especifica si se va a crear una cookie. **True** se convierte implícitamente a 1. **false** se convierte implícitamente a 0.  
  
 [  **@cookie =** ]  **@cookie SALIDA**  
 Especifica un parámetro de salida que contendrá la cookie. Se generará la cookie solo si el valor de **@fCreateCookie** es **true**. **varbinary(8000)**  
  
> [!NOTE]  
>  El parámetro **OUTPUT** de la cookie para **sp_setapprole** está documentado actualmente como **varbinary(8000)** , que es la longitud máxima correcta. Pero la implementación actual devuelve **varbinary(50)**. Las aplicaciones deben seguir reservando **varbinary (8000)** para que la aplicación siga funcionando correctamente si la cookie de tamaño devuelto aumenta en una versión futura.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) y 1 (error)  
  
## <a name="remarks"></a>Comentarios  
 Después de una aplicación se activa la función mediante **sp_setapprole**, el rol permanece activo hasta que el usuario se desconecta del servidor o ejecuta **sp_unsetapprole**. **sp_setapprole** puede ser ejecutado solo por direct [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucciones. **sp_setapprole** no se puede ejecutar dentro de otro procedimiento almacenado o una transacción definida por el usuario.  
  
 Para obtener información general de las funciones de aplicación, consulte [Roles de aplicación](../../relational-databases/security/authentication-access/application-roles.md).  
  
> [!IMPORTANT]  
>  Para proteger la contraseña del rol de aplicación cuando se transmite a través de una red, siempre debe usar una conexión cifrada al habilitar un rol de aplicación.  
>   
>  El [!INCLUDE[msCoName](../../includes/msconame-md.md)] ODBC **cifrar** opción no es compatible con **SqlClient**. Si debe almacenar las credenciales, cífrelas con las funciones de la API de cifrado. El parámetro *contraseña* se almacena como un hash unidireccional. Para conservar la compatibilidad con versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], no se aplica la directiva de complejidad de contraseña **sp_addapprole**. Para aplicar la directiva de complejidad de contraseña, utilice [CREATE APPLICATION ROLE](../../t-sql/statements/create-application-role-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 Requiere la pertenencia a **público** y conocimiento de la contraseña para el rol.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-activating-an-application-role-without-the-encrypt-option"></a>A. Activar un rol de aplicación sin la opción de cifrado  
 En este ejemplo se habilita un rol de aplicación denominado `SalesAppRole`, con la contraseña de texto simple `AsDeF00MbXX`, creado con permisos específicamente diseñados para la aplicación que utiliza el usuario actual.  
  
```  
EXEC sp_setapprole 'SalesApprole', 'AsDeF00MbXX';  
GO  
```  
  
### <a name="b-activating-an-application-role-with-a-cookie-and-then-reverting-to-the-original-context"></a>B. Activar un rol de aplicación con una cookie y revertir al contexto original  
 En el siguiente ejemplo se habilita el rol de aplicación `Sales11` con la contraseña `fdsd896#gfdbfdkjgh700mM` y se crea una cookie. En el ejemplo se devuelve el nombre del usuario actual y se revierte al contexto original ejecutando `sp_unsetapprole`.  
  
```  
DECLARE @cookie varbinary(8000);  
EXEC sp_setapprole 'Sales11', 'fdsd896#gfdbfdkjgh700mM'  
    , @fCreateCookie = true, @cookie = @cookie OUTPUT;  
-- The application role is now active.  
SELECT USER_NAME();  
-- This will return the name of the application role, Sales11.  
EXEC sp_unsetapprole @cookie;  
-- The application role is no longer active.  
-- The original context has now been restored.  
GO  
SELECT USER_NAME();  
-- This will return the name of the original user.   
GO   
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Procedimientos almacenados de seguridad &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [CREATE APPLICATION ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [DROP APPLICATION ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-application-role-transact-sql.md)   
 [sp_unsetapprole &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unsetapprole-transact-sql.md)  
  
  
