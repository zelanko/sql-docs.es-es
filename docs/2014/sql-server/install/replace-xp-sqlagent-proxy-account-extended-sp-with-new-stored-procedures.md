---
title: Reemplace el uso del procedimiento almacenado extendido con nuevos procedimientos almacenados xp_sqlagent_proxy_account | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- xp_sqlagent_proxy_account
ms.assetid: 0e3cc931-6237-41dd-bf0d-0c03f4d8fff2
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4faff8420e318f7250cfc67dda173197d8028f0b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66092759"
---
# <a name="replace-usage-of-the-xpsqlagentproxyaccount-extended-stored-procedure-with-new-stored-procedures"></a>Reemplazar el uso del procedimiento almacenado extendido xp_sqlagent_proxy_account con nuevos procedimientos almacenados
  El Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite varios servidores proxy. Puede definir estos servidores proxy utilizando un nuevo conjunto de procedimientos almacenados. Para obtener más información sobre los nuevos procedimientos almacenados del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea los temas siguientes en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   "sp_add_proxy ([!INCLUDE[tsql](../../includes/tsql-md.md)])"  
  
-   "sp_delete_proxy ([!INCLUDE[tsql](../../includes/tsql-md.md)])"  
  
-   "sp_enum_login_for_proxy ([!INCLUDE[tsql](../../includes/tsql-md.md)])"  
  
-   "sp_enum_proxy_for_subsystem ([!INCLUDE[tsql](../../includes/tsql-md.md)])"  
  
-   "sp_enum_sqlagent_subsystems ([!INCLUDE[tsql](../../includes/tsql-md.md)])"  
  
-   "sp_grant_proxy_to_subsystem ([!INCLUDE[tsql](../../includes/tsql-md.md)])"  
  
-   "sp_grant_login_to_proxy ([!INCLUDE[tsql](../../includes/tsql-md.md)])"  
  
-   "sp_help_proxy" ([!INCLUDE[tsql](../../includes/tsql-md.md)])"  
  
-   "sp_revoke_login_from_proxy ([!INCLUDE[tsql](../../includes/tsql-md.md)])"  
  
-   "sp_revoke_proxy_from_subsystem ([!INCLUDE[tsql](../../includes/tsql-md.md)])"  
  
-   "sp_update_proxy ([!INCLUDE[tsql](../../includes/tsql-md.md)])"  
  
> [!NOTE]  
>  Después de actualizar a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], cualquier instrucción que utilice el **xp_sqlagent_proxy_account** procedimiento almacenado extendido no funcionará. Use **sp_xp_cmdshell_proxy_account** en lugar de **xp_sqlagent_proxy_account** para establecer el proxy para **xp_cmdshell**.  
  
## <a name="component"></a>Componente  
 e[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización del Agente SQL Server](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)  
  
  
