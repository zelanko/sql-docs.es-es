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
manager: craigg
ms.openlocfilehash: 607ac55fe426cd086ce31ade33d3e772e7a3d9a9
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487158"
---
# <a name="permissions-hierarchy-database-engine"></a>Jerarquía de permisos (motor de base de datos)
  El [!INCLUDE[ssDE](../../../includes/ssde-md.md)] administra un conjunto jerárquico de entidades que se pueden proteger mediante permisos. Estas entidades se conocen como *elementos protegibles*. Los protegibles más prominentes son los servidores y las bases de datos, pero los permisos discretos se pueden establecer en un nivel mucho más específico. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] regula las acciones de las entidades de seguridad en los elementos protegibles comprobando que se les ha concedido los permisos adecuados.

 En la ilustración siguiente se muestran las relaciones entre las jerarquías de permisos del [!INCLUDE[ssDE](../../../includes/ssde-md.md)] .

 ![Diagrama de jerarquías de permisos del motor de base de datos](../../database-engine/media/wj-security-layers.gif "Diagrama de jerarquías de permisos del motor de base de datos")

## <a name="chart-of-sql-server-permissions"></a>Gráfico de los permisos de SQL Server
 Para obtener un gráfico [!INCLUDE[ssDE](../../../includes/ssde-md.md)] de tamaño póster [https://github.com/microsoft/sql-server-samples/blob/master/samples/features/security/permissions-posters/Microsoft_SQL_Server_2017_and_Azure_SQL_Database_permissions_infographic.pdf](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/security/permissions-posters/Microsoft_SQL_Server_2017_and_Azure_SQL_Database_permissions_infographic.pdf)de todos los permisos en formato pdf, consulte .

## <a name="working-with-permissions"></a>Trabajar con permisos
 Los permisos se pueden manipular con las conocidas consultas GRANT, DENY y REVOKE de [!INCLUDE[tsql](../../includes/tsql-md.md)] . La información sobre los permisos está visible en las vistas de catálogo [sys.server_permissions](/sql/relational-databases/system-catalog-views/sys-server-permissions-transact-sql) y [sys.database_permissions](/sql/relational-databases/system-catalog-views/sys-database-permissions-transact-sql) . También hay información sobre la compatibilidad con permisos para consultas mediante el uso de las funciones integradas.

## <a name="see-also"></a>Consulte también
 [Proteger](securing-sql-server.md) los permisos de SQL [Server&#40;Motor](permissions-database-engine.md) de base de datos Database&#41;Engine&#41;[Las entidades de seguridad protegibles &#40;Motor](authentication-access/principals-database-engine.md) de base de datos de motor de base de datos GRANT &#40;[Transact-SQLTransact-SQL&#41;](/sql/t-sql/statements/grant-transact-sql) REVOKE &#40;[Transact-SQLTransact-SQL&#41;](/sql/t-sql/statements/revoke-transact-sql) [DENY &#40;Transact-SQLTransact-SQL&#41;transact-SQLTransact-SQL HAS_PERMS_BY_NAME](/sql/t-sql/statements/deny-transact-sql) &#40;[Securables](securables.md) [Transact-SQLTransact-SQL&#41;](/sql/t-sql/functions/has-perms-by-name-transact-sql) [sys.fn_builtin_permissions &#40;Transact-SQLTransact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql) [sys.server_permissions &#40;Transact-SQLTransact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-permissions-transact-sql) [sys.database_permissions &#40;Transact-SQLTransact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-permissions-transact-sql)


