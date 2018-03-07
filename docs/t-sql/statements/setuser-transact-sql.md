---
title: SETUSER (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SETUSER_TSQL
- SETUSER
dev_langs:
- TSQL
helpviewer_keywords:
- delegation [SQL Server]
- impersonation [SQL Server]
- SETUSER statement
- user impersonation [SQL Server]
ms.assetid: 7acfac5c-9ad6-4226-b874-7add36c4ea43
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: a511e0337201c9b4501b5274fa8270fbebf7da50
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="setuser-transact-sql"></a>SETUSER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Permite a un miembro de la **sysadmin** rol fijo de servidor o el propietario de una base de datos para suplantar a otro usuario.  
  
> [!IMPORTANT]  
>  SETUSER se incluye únicamente por motivos de compatibilidad con versiones anteriores. Es posible que SETUSER deje de admitirse en versiones futuras de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se recomienda que use [EXECUTE AS](../../t-sql/statements/execute-as-transact-sql.md) en su lugar.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SETUSER [ 'username' [ WITH NORESET ] ]   
```  
  
## <a name="arguments"></a>Argumentos  
 **'** *nombre de usuario* **'**  
 Es el nombre de un usuario de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o de Windows en la base de datos actual al que se suplanta. Cuando *nombre de usuario* no se especifica, se restablece la identidad original del administrador del sistema o propietario de base de datos al suplantar al usuario.  
  
 WITH NORESET  
 Especifica que las siguientes instrucciones SETUSER (no especificada *nombre de usuario*) no se debe restablecer la identidad del usuario al administrador del sistema o propietario de la base de datos.  
  
## <a name="remarks"></a>Comentarios  
 Pueden utilizar SETUSER por un miembro de la **sysadmin** rol fijo de servidor o el propietario de una base de datos para adoptar la identidad de otro usuario para probar los permisos de ese usuario. No es suficiente la pertenencia al rol fijo de base de datos db_owner.  
  
 Solo se debe utilizar SETUSER con usuarios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. SETUSER no se admite con usuarios de Windows. Cuando se ha utilizado SETUSER para asumir la identidad de otro usuario, los objetos que crea el usuario que realiza la suplantación serán propiedad del usuario suplantado. Por ejemplo, si el propietario de la base de datos asume la identidad de usuario **Margaret** y crea una tabla denominada **pedidos**, **pedidos** es propiedad de tabla **Margaret** , no el administrador del sistema.  
  
 SETUSER sigue teniendo efecto hasta que se ejecute otra instrucción SETUSER o hasta que se cambie la base de datos actual con la instrucción USE.  
  
> [!NOTE]  
>  Si se utiliza SETUSER WITH NORESET, la única forma de que el administrador del sistema o el propietario de la base de datos pueda restablecer sus propios derechos es cerrar la sesión e iniciar otra.  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer a la **sysadmin** rol fijo de servidor o debe ser el propietario de la base de datos. Pertenencia en el **db_owner** rol fijo de base de datos no es suficiente  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente muestra cómo el propietario de la base de datos puede adoptar la identidad de otro usuario. La usuaria `mary` ha creado una tabla llamada `computer_types`. Mediante SETUSER, el propietario de la base de datos suplanta a `mary` para garantizar al usuario `joe` el acceso a la tabla `computer_types` y, a continuación, restablece su propia identidad.  
  
```  
SETUSER 'mary';  
GO  
GRANT SELECT ON computer_types TO joe;  
GO  
--To revert to the original user  
SETUSER;  
```  
  
## <a name="see-also"></a>Vea también  
 [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [USE &#40;Transact-SQL&#41;](../../t-sql/language-elements/use-transact-sql.md)  
  
  
