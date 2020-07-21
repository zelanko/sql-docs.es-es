---
title: Jerarquía de permisos (motor de base de datos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql12.swb.server.permissions.f1--May use common.permissions
helpviewer_keywords:
- security [SQL Server], denying access
- hierarchies [SQL Server], permissions
- securables [SQL Server]
- security [SQL Server], permissions
- permissions [SQL Server], hierarchy
- security [SQL Server], granting access
ms.assetid: f6d20a55-ef03-4e14-85f9-009902889866
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 9a04e5595e509de63b362b31b240e113e635581d
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85063168"
---
# <a name="permissions-hierarchy-database-engine"></a>Jerarquía de permisos (motor de base de datos)
  El [!INCLUDE[ssDE](../../../includes/ssde-md.md)] administra un conjunto jerárquico de entidades que se pueden proteger mediante permisos. Estas entidades se conocen como *elementos protegibles*. Los protegibles más prominentes son los servidores y las bases de datos, pero los permisos discretos se pueden establecer en un nivel mucho más específico. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] regula las acciones de las entidades de seguridad en los elementos protegibles comprobando que se les ha concedido los permisos adecuados.

 En la ilustración siguiente se muestran las relaciones entre las jerarquías de permisos del [!INCLUDE[ssDE](../../../includes/ssde-md.md)] .

 ![Diagrama de jerarquías de permisos del motor de base de datos](../../database-engine/media/wj-security-layers.gif "Diagrama de jerarquías de permisos del motor de base de datos")

## <a name="chart-of-sql-server-permissions"></a>Gráfico de los permisos de SQL Server
 Para obtener un gráfico con el tamaño de un póster de todos los [!INCLUDE[ssDE](../../../includes/ssde-md.md)] permisos en formato PDF, vea [https://github.com/microsoft/sql-server-samples/blob/master/samples/features/security/permissions-posters/Microsoft_SQL_Server_2017_and_Azure_SQL_Database_permissions_infographic.pdf](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/security/permissions-posters/Microsoft_SQL_Server_2017_and_Azure_SQL_Database_permissions_infographic.pdf) .

## <a name="working-with-permissions"></a>Trabajar con permisos
 Los permisos se pueden manipular con las conocidas consultas GRANT, DENY y REVOKE de [!INCLUDE[tsql](../../includes/tsql-md.md)] . La información sobre los permisos está visible en las vistas de catálogo [sys.server_permissions](/sql/relational-databases/system-catalog-views/sys-server-permissions-transact-sql) y [sys.database_permissions](/sql/relational-databases/system-catalog-views/sys-database-permissions-transact-sql) . También hay información sobre la compatibilidad con permisos para consultas mediante el uso de las funciones integradas.

## <a name="see-also"></a>Consulte también
 [Proteger SQL Server](securing-sql-server.md) [permisos &#40;motor de base de datos&#41;entidades](permissions-database-engine.md) [protegibles](securables.md) [&#40;](authentication-access/principals-database-engine.md) motor de base de datos&#41;[Grant &#40;TRANSACT-](/sql/t-sql/statements/grant-transact-sql) sql&#41;[revocación &#40;Transact-SQL&#41;](/sql/t-sql/statements/revoke-transact-sql) [Deny &#40;transact-SQL&#41;](/sql/t-sql/statements/deny-transact-sql) [HAS_PERMS_BY_NAME &#40;transact-SQL&#41;](/sql/t-sql/functions/has-perms-by-name-transact-sql) [Sys. fn_builtin_permissions &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql) [Sys. server_permissions &#40;Transact-](/sql/relational-databases/system-catalog-views/sys-server-permissions-transact-sql) SQL&#41;[Sys. database_permissions &#40;Transact-](/sql/relational-databases/system-catalog-views/sys-database-permissions-transact-sql) SQL&#41;


