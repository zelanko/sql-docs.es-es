---
title: Sys.dm_os_server_diagnostics_log_configurations | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_os_server_diagnostics_log_configurations
- sys.dm_os_server_diagnostics_log_configurations_TSQL
- dm_os_server_diagnostics_log_configurations
- dm_os_server_diagnostics_log_configurations_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dm_os_server_diagnostics_log_configurations
- sys.dm_os_server_diagnostics_log_configurations
ms.assetid: c09ea433-d283-4f83-af69-d458aad59217
caps.latest.revision: 16
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 0d9c20dfd5c84d0fd0937cad26eb2d61a1cdc545
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2018
ms.locfileid: "39555035"
---
# <a name="sysdmosserverdiagnosticslogconfigurations"></a>sys.dm_os_server_diagnostics_log_configurations
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  Devuelve una fila con la configuración actual del registro de diagnóstico de clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Estos valores de propiedad determinan si el registro de diagnóstico está activado o desactivado, así como la ubicación, el número y el tamaño de los archivos de registro.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|is_enabled|**bit**|Indica si el registro está activado o desactivado.<br /><br /> 1 = El registro de diagnóstico está activado<br /><br /> 0 = El registro de diagnóstico está desactivado|  
|max_size|**int**|Tamaño máximo en megabytes que cada uno de los registros de diagnóstico puede alcanzar. El valor predeterminado es 100 MB.|  
|max_files|**int**|Número máximo de archivos de registro de diagnóstico que pueden almacenarse en el equipo antes de que se reciclen para nuevos registros de diagnóstico.|  
|path|**nvarchar(260)**|Ruta de acceso que indica la ubicación de los registros de diagnóstico. La ubicación predeterminada es \<\MSSQL\Log> en la carpeta de instalación de la instancia en clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
## <a name="permissions"></a>Permisos  
 Necesita permisos VIEW SERVER STATE en la instancia en clúster de conmutación por error de SQL Server.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se usa sys.dm_os_server_diagnostics_log_configurations para devolver los valores de propiedad para los registros de diagnóstico de conmutación por error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
SELECT <list of columns>  
FROM sys.dm_os_server_diagnostics_log_configurations;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|IS_ENABLED|PATH|MAX_SIZE|MAX_FILES|  
|-----------------|----------|---------------|----------------|  
|1|\<C:\Program Files\Microsoft SQL Server\MSSQL13\MSSQL\Log >|10|10|  
  
## <a name="see-also"></a>Vea también  
 [Ver y leer el registro de diagnósticos de la instancia de clúster de conmutación por error](../../sql-server/failover-clusters/windows/view-and-read-failover-cluster-instance-diagnostics-log.md)  
  
  
