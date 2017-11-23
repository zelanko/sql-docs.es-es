---
title: sp_delete_firewall_rule (base de datos de SQL Azure) | Documentos de Microsoft
ms.custom: 
ms.date: 07/27/2016
ms.prod: 
ms.prod_service: sql-database, sql-data-warehouse
ms.reviewer: 
ms.service: sql-database
ms.component: system-stored-procedures
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_delete_firewall_rule_TSQL
- sp_delete_firewall_rule
- sys.sp_delete_firewall_rule
- sys.sp_delete_firewall_rule_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_delete_firewall_rule procedure
ms.assetid: cf93eed1-ba97-4850-9fcc-b9c5a9317908
caps.latest.revision: "14"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: aa2815c27668bc680ce5da72b6713e29b517f43b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="spdeletefirewallrule-azure-sql-database"></a>sp_delete_firewall_rule (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

  Quita la configuración del firewall de nivel de servidor del servidor [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. Este procedimiento almacenado solo está disponible en la base de datos maestra para el inicio de sesión principal de nivel de servidor.  

  
## <a name="syntax"></a>Sintaxis  
  
```  
sp_delete_firewall_rule [@name =] 'name' 
[ ; ] 
```  
  
## <a name="arguments"></a>Argumentos  
 El argumento del procedimiento almacenado es:  
  
 [@name =] '*nombre*'  
 El nombre de la configuración del firewall de nivel de servidor que se quitará. *nombre* es **nvarchar (128)** no tiene ningún valor predeterminado.  
  
## <a name="remarks"></a>Comentarios  
 En [!INCLUDE[ssSDS](../../includes/sssds-md.md)], datos de inicio de sesión necesitan para autenticar una conexión y las reglas de firewall de nivel de servidor se almacenan temporalmente en caché en cada base de datos. Esta caché se actualiza periódicamente. Para forzar una actualización de la caché de autenticación y asegúrese de que una base de datos tiene la versión más reciente de la tabla de inicios de sesión, ejecute [DBCC FLUSHAUTHCACHE &#40; Transact-SQL &#41; ](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 Solo el inicio de sesión principal de nivel de servidor creado por el proceso de aprovisionamiento puede eliminar reglas de firewall de nivel de servidor. El usuario debe estar conectado a la base de datos maestra para ejecutar sp_delete_firewall_rule.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se quita la configuración del firewall de nivel de servidor denominada 'Example setting 1'. Ejecute la instrucción en la base de datos maestra virtual.  
  
```   
EXEC sp_delete_firewall_rule N'Example setting 1';   
```  
  
## <a name="see-also"></a>Vea también  
 [Firewall de base de datos SQL Azure](https://azure.microsoft.com/documentation/articles/sql-database-firewall-configure/)   
 [Cómo: configurar el Firewall (base de datos SQL Azure)](https://azure.microsoft.com/documentation/articles/sql-database-configure-firewall-settings/)   
 [sp_set_firewall_rule &#40; Base de datos SQL Azure &#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)   
 [Sys.firewall_rules &#40; Base de datos SQL Azure &#41;](../../relational-databases/system-catalog-views/sys-firewall-rules-azure-sql-database.md)  
  
  


