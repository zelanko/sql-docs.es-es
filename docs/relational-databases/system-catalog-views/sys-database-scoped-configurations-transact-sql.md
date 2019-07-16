---
title: Sys.database_scoped_configurations (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- database_scoped_configurations
- database_scoped_configurations_TSQL
- sys.database_scoped_configurations
- sys.database_scoped_configurations_TSQL
helpviewer_keywords:
- sys.database_scoped_configurations catalog view
ms.assetid: 8899310a-3464-4d38-9f2f-88396c4e7dc2
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3439419bd3877b8ab7a951df58585703f169ee4f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68079447"
---
# <a name="sysdatabasescopedconfigurations-transact-sql"></a>sys.database_scoped_configurations (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Contiene una fila por cada configuración. 
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**configuration_id**|**int**|Id. de la opción de configuración.|  
|**name**|**nvarchar(60)**|El nombre de la opción de configuración. Para obtener información acerca de las configuraciones posibles, vea [ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).|  
|**value**|**sqlvariant**|El valor establecido para esta opción de configuración para la réplica principal.|  
|**value_for_secondary**|**sqlvariant**|El valor establecido para esta opción de configuración para las réplicas secundarias.|  
|**is_value_default**|**bit** |Especifica si el valor establecido es el valor predeterminado.|
  
##  <a name="Permissions"></a> Permisos  
Debe pertenecer al rol **public** .  
  
## <a name="remarks"></a>Comentarios  
Cuando se devuelve NULL como el valor de **value_for_secondary**, esto significa que se establece la base de datos secundaria a principal.  
 
Las opciones de configuración con ámbito de base de datos se transfieren con la base de datos. Esto significa que cuando se restaura o adjunta una base de datos, se conservan las opciones de configuración existentes.
  
## <a name="see-also"></a>Vea también  
 [ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)  
  
  
