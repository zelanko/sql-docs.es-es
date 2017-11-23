---
title: sp_set_database_firewall_rule (base de datos de SQL Azure) | Documentos de Microsoft
ms.custom: 
ms.date: 08/04/2017
ms.prod: 
ms.prod_service: sql-database
ms.reviewer: 
ms.service: sql-database
ms.component: system-stored-procedures
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_set_database_firewall_rule
- sp_set_database_firewall_rule_TSQL
- sys.sp_set_database_firewall_rule
- sys.sp_set_database_firewall_rule_TSQL
dev_langs: TSQL
helpviewer_keywords:
- sp_set_database_firewall_rule
- firewall_rules, setting database rules
ms.assetid: 8f0506b6-a4ac-4e4d-91db-8077c40cb17a
caps.latest.revision: "15"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: c83057218c015eb9d3488ea730e507ab795ddade
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="spsetdatabasefirewallrule-azure-sql-database"></a>sp_set_database_firewall_rule (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Crea o actualiza las reglas de firewall de nivel de base de datos para su [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. Las reglas de firewall de base de datos pueden configurarse para la **maestro** base de datos y para las bases de datos de usuario en [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. Las reglas de firewall de base de datos son especialmente útiles cuando se usan usuarios de base de datos independiente. Para obtener más información, vea [Usuarios de base de datos independiente: hacer que la base de datos sea portátil](../../relational-databases/security/contained-database-users-making-your-database-portable.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_set_database_firewall_rule [@name = ] [N]'name'  
, [@start_ip_address =] 'start_ip_address'  
, [@end_ip_address =] 'end_ip_address'
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 **[@name**  =] [N]'*nombre*'  
 El nombre utilizado para describir y distinguir la configuración del firewall de nivel de base de datos. *nombre* es **nvarchar (128)** con ningún valor predeterminado. El identificador de Unicode `N` es opcional para [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]. 
  
 **[@start_ip_address**  =] '*start_ip_address*'  
 La dirección IP más baja en el intervalo de la configuración del firewall de nivel de base de datos. Las direcciones IP iguales o superiores a esta pueden intentar conectarse con la instancia de [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. La dirección IP más baja posible es `0.0.0.0`. *start_ip_address* es **varchar (50)** con ningún valor predeterminado.  
  
 [ **@end_ip_address**  =] '*end_ip_address*'  
 La dirección IP más alta en el intervalo de la configuración del firewall de nivel de base de datos. Las direcciones IP iguales o inferiores a esta pueden intentar conectarse con la instancia de [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. La dirección IP más alta posible es `255.255.255.255`. *end_ip_address* es **varchar (50)** con ningún valor predeterminado.  
  
 En la tabla siguiente se muestran los argumentos compatibles y opciones en [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
> [!NOTE]  
>  Se permiten los intentos de conexión de Azure cuando este campo y el *start_ip_address* campo es igual a `0.0.0.0`.  
  
## <a name="remarks"></a>Comentarios  
 Los nombres de la configuración del firewall de nivel de base de datos para una base de datos deben ser únicos. Si el nombre de la configuración del firewall de nivel de base de datos proporcionado para el procedimiento almacenado ya existe en la tabla de configuración del firewall de nivel de base de datos, las direcciones IP inicial y final se actualizarán. De lo contrario, se creará una nueva configuración del firewall de nivel de base de datos.  
  
 Cuando se agrega una configuración de firewall de nivel de base de datos donde el principio y final de las direcciones IP son iguales a `0.0.0.0`, permitir el acceso a la base de datos en el [!INCLUDE[ssSDS](../../includes/sssds-md.md)] servidor desde cualquier recurso de Azure. Proporcione un valor para el *nombre* parámetro que le ayudará a recordar qué es la configuración del firewall.  
  
## <a name="permissions"></a>Permissions  
 Requiere **CONTROL** permiso en la base de datos.  
  
## <a name="examples"></a>Ejemplos  
 El siguiente código crea un nivel de base de datos de configuración de firewall denominada `Allow Azure` que habilita el acceso a la base de datos de Azure.  
  
```  
-- Enable Azure connections.  
EXECUTE sp_set_database_firewall_rule N'Allow Azure', '0.0.0.0', '0.0.0.0';  
  
```  
  
 El código siguiente crea una configuración del firewall de nivel de base de datos denominada `Example DB Setting 1` solo para la dirección IP `0.0.0.4`. A continuación, la `sp_set_database firewall_rule` procedimiento almacenado se llama de nuevo para actualizar la dirección IP final `0.0.0.6`, ya que la configuración de firewall. Esto crea un intervalo que permite que las direcciones IP `0.0.0.4`, `0.0.0.5`, y `0.0.0.6` para tener acceso a la base de datos.
  
```  
-- Create database-level firewall setting for only IP 0.0.0.4  
EXECUTE sp_set_database_firewall_rule N'Example DB Setting 1', '0.0.0.4', '0.0.0.4';  
  
-- Update database-level firewall setting to create a range of allowed IP addresses
EXECUTE sp_set_database_firewall_rule N'Example DB Setting 1', '0.0.0.4', '0.0.0.6';  
  
```  
  
## <a name="see-also"></a>Vea también  
 [Firewall de base de datos SQL Azure](https://azure.microsoft.com/documentation/articles/sql-database-firewall-configure/)   
 [Cómo: configurar el Firewall (base de datos SQL Azure)](https://azure.microsoft.com/documentation/articles/sql-database-configure-firewall-settings/)   
 [sp_set_firewall_rule &#40; Base de datos SQL Azure &#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)   
 [sp_delete_database_firewall_rule &#40; Base de datos SQL Azure &#41;](../../relational-databases/system-stored-procedures/sp-delete-database-firewall-rule-azure-sql-database.md)   
 [Sys.database_firewall_rules &#40; Base de datos SQL Azure &#41;](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md)  
  
  
