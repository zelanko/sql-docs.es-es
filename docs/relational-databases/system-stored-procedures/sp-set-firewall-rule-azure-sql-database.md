---
title: sp_set_firewall_rule (Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 07/28/2016
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sp_set_firewall_rule
- sp_set_firewall_rule_TSQL
- sys.sp_set_firewall_rule
- sys.sp_set_firewall_rule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_set_firewall_rule
- firewall_rules, setting server rules
ms.assetid: a974a561-5382-4039-8499-3a56767bcefe
author: VanMSFT
ms.author: vanto
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 9bc37626879b743eb3a5d0864490dc3543a8d8a9
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2019
ms.locfileid: "70152062"
---
# <a name="sp_set_firewall_rule-azure-sql-database"></a>sp_set_firewall_rule (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

  Crea o actualiza la configuración del firewall de nivel de servidor para el servidor [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. Este procedimiento almacenado solo está disponible en la base de datos maestra para el inicio de sesión principal de nivel de servidor o asignado Azure Active Directory entidad de seguridad.  
  
  
## <a name="syntax"></a>Sintaxis  
  
```
sp_set_firewall_rule [@name =] 'name', 
    [@start_ip_address =] 'start_ip_address', 
    [@end_ip_address =] 'end_ip_address'
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 En la tabla siguiente se muestran los argumentos y las opciones admitidos en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
|NOMBRE|Datatype|Descripción|  
|----------|--------------|-----------------|  
|[@name =] Name|**NVARCHAR (128)**|El nombre utilizado para describir y distinguir la configuración del firewall de nivel de servidor.|  
|[@start_ip_address =] ' start_ip_address '|**VARCHAR (50)**|La dirección IP más baja en el intervalo de la configuración del firewall de nivel de servidor. Las direcciones IP iguales o superiores a esta pueden intentar conectarse con el servidor [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. La dirección IP más baja posible es `0.0.0.0`.|  
|[@end_ip_address =] ' end_ip_address '|**VARCHAR (50)**|La dirección IP más alta en el intervalo de la configuración del firewall de nivel de servidor. Las direcciones IP iguales o inferiores a esta pueden intentar conectarse con el servidor [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. La dirección IP más alta posible es `255.255.255.255`.<br /><br /> Nota: los intentos de conexión de Azure se permiten cuando este campo y el campo *start_ip_address* es igual a `0.0.0.0`.|  
  
## <a name="remarks"></a>Remarks  
 Los nombres de la configuración del firewall de nivel de servidor deben ser únicos. Si el nombre del valor proporcionado para el procedimiento almacenado ya existe en la tabla de configuración del firewall, las direcciones IP inicial y final se actualizarán. De lo contrario, se creará una nueva configuración del firewall de nivel de servidor.  
  
 Cuando se agrega una configuración de Firewall de nivel de servidor en la que las direcciones IP inicial y final son iguales a `0.0.0.0`, se habilita el acceso a su servidor [!INCLUDE[ssSDS](../../includes/sssds-md.md)] desde Azure. Proporcione un valor al parámetro *Name* que le ayude a recordar para qué sirve la configuración de Firewall de nivel de servidor.  
  
 En [!INCLUDE[ssSDS](../../includes/sssds-md.md)], los datos de inicio de sesión necesarios para autenticar una conexión y reglas de firewall de nivel de servidor se almacenan temporalmente en caché en cada base de datos. Esta caché se actualiza regularmente. Para forzar una actualización de la caché de autenticación y garantizar que una base de datos tenga la versión más reciente de la tabla de inicios de sesión, ejecute [DBCC FLUSHAUTHCACHE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md).  
  
## <a name="permissions"></a>Permisos  
 Solo el inicio de sesión principal de nivel de servidor creado por el proceso de aprovisionamiento o una entidad de seguridad Azure Active Directory asignada como administrador puede crear o modificar reglas de Firewall de nivel de servidor. El usuario debe estar conectado a la base de datos maestra para ejecutar sp_set_firewall_rule.  
  
## <a name="examples"></a>Ejemplos  
 En el código siguiente se crea una configuración de Firewall de nivel de servidor denominada `Allow Azure` que permite el acceso desde Azure. Ejecute lo siguiente en la base de datos maestra virtual.  
  
```  
-- Enable Azure connections.  
exec sp_set_firewall_rule N'Allow Azure', '0.0.0.0', '0.0.0.0';  
  
```  
  
 El código siguiente crea una configuración del firewall de nivel de servidor denominada `Example setting 1` solo para la dirección IP `0.0.0.2`. A continuación, se llama de nuevo al procedimiento almacenado `sp_set_firewall_rule` para actualizar la dirección IP final a `0.0.0.4`, en esa configuración de Firewall. Esto crea un intervalo que permite que las direcciones IP `0.0.0.2`, `0.0.0.3`y `0.0.0.4` tengan acceso al servidor.  
  
```  
-- Create server-level firewall setting for only IP 0.0.0.2  
exec sp_set_firewall_rule N'Example setting 1', '0.0.0.2', '0.0.0.2';  
  
-- Update server-level firewall setting to create a range of allowed IP addresses
exec sp_set_firewall_rule N'Example setting 1', '0.0.0.2', '0.0.0.4';  
  
```  
  
## <a name="see-also"></a>Vea también  
 [Azure SQL Database Firewall](https://azure.microsoft.com/documentation/articles/sql-database-firewall-configure/)   
 [Cómo configurar los valores del firewall (Azure SQL Database)](https://azure.microsoft.com/documentation/articles/sql-database-configure-firewall-settings/)   
 [Sys. firewall_rules &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-firewall-rules-azure-sql-database.md)
