---
title: Sys. change_tracking_databases (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/08/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- change_tracking_databases
- sys.change_tracking_databases_TSQL
- sys.change_tracking_databases
- change_tracking_databases_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.change_tracking_databases
- change tracking [SQL Server], sys.change_tracking_databases
ms.assetid: bb233baa-2991-4904-a0eb-3772b81121a4
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 414286c06884721fad81ea25dd100fa5a7cd13b2
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85753012"
---
# <a name="change-tracking-catalog-views---syschange_tracking_databases"></a>Change Tracking vistas de catálogo: sys. change_tracking_databases
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Devuelve una fila por cada base de datos que tenga habilitada el seguimiento de cambios.  

|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|database_id|**int**|Identificador de la base de datos. Es único dentro de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|is_auto_cleanup_on|**bit**|Indica si los datos del seguimiento de cambios se limpian automáticamente después del período de retención configurado:<br /><br /> 0 = Off (desactivado)<br /><br /> 1 = Habilitado|  
|retention_period|**int**|Si se utiliza la limpieza automática, el período de la retención especifica el tiempo que se mantienen los datos del seguimiento de cambios en la base de datos.|  
|retention_period_units_desc|**nvarchar(60)**|Especifica la descripción del período de retención:<br /><br /> Minutos<br /><br /> Horas<br /><br /> Días|  
|retention_period_units|**tinyint**|Unidad de tiempo del período de retención:<br /><br /> 1 = Minutos<br /><br /> 2 = Horas<br /><br /> 3 = Días|  
  
## <a name="permissions"></a>Permisos  
 Se realizan las mismas comprobaciones del permiso para sys.change_tracking_databases que para sys.databases. Si el autor de la llamada de sys.change_tracking_databases no es el propietario de la base de datos, los permisos mínimos necesarios para ver la fila correspondiente son ALTER ANY DATABASE o VIEW ANY DATABASE de nivel de servidor, o el permiso CREATE DATABASE en la base de datos actual o maestra.  
  
## <a name="see-also"></a>Consulte también  
 [Change Tracking vistas de catálogo &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/6e8fd949-5560-4b34-879f-4e25aa24b183)   
 [Seguimiento de cambios de datos &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)  
  
  
