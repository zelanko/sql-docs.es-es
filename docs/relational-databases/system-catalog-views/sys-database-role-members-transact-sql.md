---
title: Sys.database_role_members (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/31/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.database_role_members_TSQL
- sys.database_role_members
- database_role_members_TSQL
- database_role_members
dev_langs:
- TSQL
helpviewer_keywords:
- sys.database_role_members catalog view
ms.assetid: ed1b019d-ca48-4db3-85df-cf6d2db591cf
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 50c617d4dd3467d30cfac1d4628f8bee50edc3a7
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2018
ms.locfileid: "39537835"
---
# <a name="sysdatabaserolemembers-transact-sql"></a>sys.database_role_members (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve una fila por cada miembro de cada rol de base de datos.  Los usuarios de base de datos, roles de aplicación y otros roles de base de datos pueden ser miembros de un rol de base de datos. Para agregar miembros a un rol, use la [ALTER ROLE](../../t-sql/statements/alter-role-transact-sql.md) instrucción con el `ADD MEMBER` opción. Unir con [sys.database_principals](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md) para devolver los nombres de los `principal_id` valores.
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**role_principal_id**|**int**|Identificador de entidad de seguridad de base de datos del rol.|  
|**member_principal_id**|**int**|Identificador de entidad de seguridad de base de datos del miembro.|  
  
## <a name="permissions"></a>Permisos  
 Cualquier usuario puede ver su propia pertenencia a roles. Para ver otro rol requiere la pertenencia a las pertenencias a la `db_securityadmin` rol fijo de base de datos o `VIEW DEFINITION` en la base de datos.  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="example"></a>Ejemplo  
 La siguiente consulta devuelve a los miembros de los roles de base de datos.  
  
```  
SELECT DP1.name AS DatabaseRoleName,   
   isnull (DP2.name, 'No members') AS DatabaseUserName   
 FROM sys.database_role_members AS DRM  
 RIGHT OUTER JOIN sys.database_principals AS DP1  
   ON DRM.role_principal_id = DP1.principal_id  
 LEFT OUTER JOIN sys.database_principals AS DP2  
   ON DRM.member_principal_id = DP2.principal_id  
WHERE DP1.type = 'R'
ORDER BY DP1.name;  
```  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo de seguridad &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Entidades de seguridad &#40;motor de base de datos&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
[MODIFICAR rol (Transact-SQLL)](../../t-sql/statements/alter-role-transact-sql.md)      
[Sys.server_role_members (Transact-SQL)](../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)   
  


