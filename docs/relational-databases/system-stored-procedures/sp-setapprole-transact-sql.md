---
title: sp_setapprole (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/12/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_setapprole
- sp_setapprole_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_setapprole
ms.assetid: cf0901c0-5f90-42d4-9d5b-8772c904062d
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 44e7b670ef5f16b6df861e939f9b8b2d9ace8dd5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68104430"
---
# <a name="spsetapprole-transact-sql"></a>sp_setapprole (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Activa los permisos asociados a un rol de aplicación en la base de datos actual.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  

```sql
sp_setapprole [ @rolename = ] 'role',  
    [ @password = ] { encrypt N'password' }
      |  
        'password' [ , [ @encrypt = ] { 'none' | 'odbc' } ]  
        [ , [ @fCreateCookie = ] true | false ]  
    [ , [ @cookie = ] @cookie OUTPUT ]  
```

## <a name="arguments"></a>Argumentos

`[ @rolename = ] 'role'` Es el nombre del rol de aplicación definido en la base de datos actual. *rol* es **sysname**, no tiene ningún valor predeterminado. *rol* debe existir en la base de datos actual.  
  
`[ @password = ] { encrypt N'password' }` Es la contraseña necesaria para activar el rol de aplicación. *contraseña* es **sysname**, no tiene ningún valor predeterminado. *contraseña* puede ofuscarse mediante ODBC **cifrar** función. Cuando se usa el **cifrar** función, la contraseña se debe convertir en una cadena Unicode mediante la colocación de **N** antes de la primera comilla.  
  
 No se admite la opción de cifrado en las conexiones que usan **SqlClient**.  
  
> [!IMPORTANT]  
> ODBC **cifrar** función no proporciona cifrado. No debe confiar a esta función la protección de las contraseñas que se transmiten en una red. Si la información se va a transmitir en una red, utilice SSL o IPSec.
  
 **@encrypt = 'none'**  
 Especifica que no se utiliza ofuscación. La contraseña se pasa a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como texto simple. Ésta es la opción predeterminada.  
  
 **@encrypt= 'odbc'**  
 Especifica que ODBC ofuscará la contraseña mediante el uso de ODBC **cifrar** función antes de enviar la contraseña para el [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Solo se puede especificar cuando se utiliza un cliente ODBC o el Proveedor OLE DB para SQL Server.  
  
`[ @fCreateCookie = ] true | false` Especifica si se puede crear una cookie. **True** se convierte implícitamente a 1. **false** se convierte implícitamente a 0.  
  
`[ @cookie = ] @cookie OUTPUT` Especifica un parámetro de salida que contendrá la cookie. La cookie solo se genera si el valor de **@fCreateCookie** es **true**. **varbinary(8000)**  
  
> [!NOTE]  
> El parámetro **OUTPUT** de la cookie para **sp_setapprole** está documentado actualmente como **varbinary(8000)** , que es la longitud máxima correcta. Pero la implementación actual devuelve **varbinary(50)** . Las aplicaciones deben seguir reservando **varbinary (8000)** para que la aplicación siga funcionando correctamente si la cookie devuelto tamaño aumenta en una versión futura.
  
## <a name="return-code-values"></a>Valores de código de retorno

 0 (correcto) y 1 (error)  
  
## <a name="remarks"></a>Comentarios

 Después de una aplicación de función se activa mediante **sp_setapprole**, el rol permanece activo hasta que el usuario se desconecta del servidor o ejecuta **sp_unsetapprole**. **sp_setapprole** sólo puede ejecutar direct [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucciones. **sp_setapprole** no se puede ejecutar dentro de otro procedimiento almacenado o una transacción definida por el usuario.  
  
 Para obtener información general de las funciones de aplicación, consulte [Roles de aplicación](../../relational-databases/security/authentication-access/application-roles.md).  
  
> [!IMPORTANT]  
> Para proteger la contraseña del rol de aplicación cuando se transmite a través de una red, siempre debe usar una conexión cifrada al habilitar un rol de aplicación.
> El [!INCLUDE[msCoName](../../includes/msconame-md.md)] ODBC **cifrar** opción no es compatible con **SqlClient**. Si debe almacenar las credenciales, cífrelas con las funciones de la API de cifrado. El parámetro *contraseña* se almacena como un hash unidireccional. Para mantener la compatibilidad con versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], no se aplica la directiva de complejidad de contraseña mediante **sp_addapprole**. Para aplicar la directiva de complejidad de contraseña, utilice [CREATE APPLICATION ROLE](../../t-sql/statements/create-application-role-transact-sql.md).  
  
## <a name="permissions"></a>Permisos

Requiere la pertenencia a **pública** y conocer la contraseña para el rol.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-activating-an-application-role-without-the-encrypt-option"></a>A. Activar un rol de aplicación sin la opción de cifrado

 En este ejemplo se habilita un rol de aplicación denominado `SalesAppRole`, con la contraseña de texto simple `AsDeF00MbXX`, creado con permisos específicamente diseñados para la aplicación que utiliza el usuario actual.

```sql
EXEC sys.sp_setapprole 'SalesApprole', 'AsDeF00MbXX';  
GO
```

### <a name="b-activating-an-application-role-with-a-cookie-and-then-reverting-to-the-original-context"></a>b. Activar un rol de aplicación con una cookie y revertir al contexto original

 En el siguiente ejemplo se habilita el rol de aplicación `Sales11` con la contraseña `fdsd896#gfdbfdkjgh700mM` y se crea una cookie. En el ejemplo se devuelve el nombre del usuario actual y se revierte al contexto original ejecutando `sp_unsetapprole`.  

```sql
DECLARE @cookie varbinary(8000);  
EXEC sys.sp_setapprole 'Sales11', 'fdsd896#gfdbfdkjgh700mM'  
    , @fCreateCookie = true, @cookie = @cookie OUTPUT;  
-- The application role is now active.  
SELECT USER_NAME();  
-- This will return the name of the application role, Sales11.  
EXEC sys.sp_unsetapprole @cookie;  
-- The application role is no longer active.  
-- The original context has now been restored.  
GO  
SELECT USER_NAME();  
-- This will return the name of the original user.
GO
```

## <a name="see-also"></a>Vea también

 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md) [procedimientos almacenados de seguridad &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md) [CREATE APPLICATION ROLE &#40;Transact-SQL&#41; ](../../t-sql/statements/create-application-role-transact-sql.md) [DROP APPLICATION ROLE &#40;Transact-SQL&#41; ](../../t-sql/statements/drop-application-role-transact-sql.md) [sp_unsetapprole &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unsetapprole-transact-sql.md)
