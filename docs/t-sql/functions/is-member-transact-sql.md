---
title: IS_MEMBER (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- IS_MEMBER
- IS_MEMBER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- database roles [SQL Server], members
- current member status
- roles [SQL Server], members
- testing member status
- members [SQL Server]
- checking member status
- IS_MEMBER function
- verifying member status
- groups [SQL Server], members
- members [SQL Server], verifying
ms.assetid: 77cb68a0-19b7-4fe1-ab17-e5587699631b
caps.latest.revision: 25
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 472d8f1cc258fdc57ef454fbb35f51e3f83b288d
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="ismember-transact-sql"></a>IS_MEMBER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Indica si el usuario actual es miembro del grupo de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows o del rol de base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especificados.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
IS_MEMBER ( { 'group' | 'role' } )  
```  
  
## <a name="arguments"></a>Argumentos  
 **'** *grupo* **'**  
**Se aplica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Es el nombre del grupo de Windows que se está comprobando; debe tener el formato *dominio*\\*grupo*. *grupo* es **sysname**.  
  
 **'** *rol* **'**  
 Es el nombre de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rol que se está comprobando. *rol* es **sysname** y pueden incluir la base de datos fija roles o funciones definidas por el usuario, pero no los roles de servidor.  
  
## <a name="return-types"></a>Tipos devueltos  
 **int**  
  
## <a name="remarks"></a>Comentarios  
 IS_MEMBER devuelve los siguientes valores.  
  
|Valor devuelto|Description|  
|------------------|-----------------|  
|0|Usuario actual no es un miembro de *grupo* o *rol*.|  
|1|Usuario actual es un miembro de *grupo* o *rol*.|  
|NULL|Cualquier *grupo* o *rol* no es válido. Cuando se consulta en un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o en un inicio de sesión que usa un rol de aplicación, devuelve NULL para un grupo de Windows.|  
  
 IS_MEMBER determina la pertenencia al grupo de Windows examinando un token de acceso creado por Windows. El token de acceso no refleja los cambios en la pertenencia a grupos que se realizan después de que un usuario se conecte a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La pertenencia a un grupo de Windows no se puede consultar en un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ni en un rol de aplicación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para agregar y quitar miembros de un rol de base de datos, utilice [ALTER ROLE &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-role-transact-sql.md). Para agregar y quitar miembros de un rol de servidor, utilice [ALTER SERVER ROLE &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-server-role-transact-sql.md).  
  
 Esta función evalúa la pertenencia al rol, no el permiso subyacente. Por ejemplo, el **db_owner** rol fijo de base de datos tiene la **CONTROL DATABASE** permiso. Si el usuario tiene la **CONTROL DATABASE** permiso pero no es un miembro del rol, esta función informará correctamente que el usuario no es un miembro de la **db_owner** rol, aunque el usuario tiene el mismo permisos.  
  
 Los miembros de la **sysadmin** rol fijo de servidor escriba cada base de datos como el **dbo** usuario. Comprobación de permisos para el miembro de la **sysadmin** rol fijo de servidor, comprueba los permisos para **dbo**, no el inicio de sesión original. Puesto que **dbo** no se puede agregar a un rol de base de datos y no existe en los grupos de Windows, **dbo** siempre devolverá 0 (o NULL si no existe el rol).  
  
## <a name="related-functions"></a>Funciones relacionadas  
 Para determinar si otro [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicio de sesión es un miembro de un rol de base de datos, use [IS_ROLEMEMBER &#40; Transact-SQL &#41; ](../../t-sql/functions/is-rolemember-transact-sql.md). Para determinar si un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicio de sesión es miembro de un rol de servidor, use [IS_SRVROLEMEMBER &#40; Transact-SQL &#41; ](../../t-sql/functions/is-srvrolemember-transact-sql.md).  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se comprueba si el usuario actual es miembro de un rol de base de datos o de un grupo de dominio de Windows.  
  
```  
-- Test membership in db_owner and print appropriate message.  
IF IS_MEMBER ('db_owner') = 1  
   PRINT 'Current user is a member of the db_owner role'  
ELSE IF IS_MEMBER ('db_owner') = 0  
   PRINT 'Current user is NOT a member of the db_owner role'  
ELSE IF IS_MEMBER ('db_owner') IS NULL  
   PRINT 'ERROR: Invalid group / role specified';  
GO  
  
-- Execute SELECT if user is a member of ADVWORKS\Shipping.  
IF IS_MEMBER ('ADVWORKS\Shipping') = 1  
   SELECT 'User ' + USER + ' is a member of ADVWORKS\Shipping.';   
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [IS_SRVROLEMEMBER &#40; Transact-SQL &#41;](../../t-sql/functions/is-srvrolemember-transact-sql.md)   
 [Entidades de seguridad &#40;motor de base de datos&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [Vistas de catálogo de seguridad &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Funciones de seguridad &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
  
  

