---
title: Sys.dm_os_cluster_properties (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_os_cluster_properties_TSQL
- sys.dm_os_cluster_properties
- dm_os_cluster_properties_TSQL
- dm_os_cluster_properties
dev_langs:
- TSQL
helpviewer_keywords:
- dm_os_cluster_properties
- sys.dm_os_cluster_properties
ms.assetid: 6d82e770-fba7-49e0-9a0c-3b34b393e4a7
caps.latest.revision: 17
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 617f40a71074c8480d38e2eb5f59e108ee2d6ff7
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2018
ms.locfileid: "34464601"
---
# <a name="sysdmosclusterproperties-transact-sql"></a>sys.dm_os_cluster_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila con los valores actuales de las propiedades de recurso de clúster de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] identificadas en este tema. No se devolverá ningún dato si esta vista se ejecuta en una instancia independiente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Estas propiedades se usan para establecer los valores que afectan a la detección de errores, el tiempo de respuesta de errores y el registro para supervisar el estado de mantenimiento de la instancia en clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  

|Nombre de la columna|Propiedad|Description|  
|-----------------|--------------|-----------------|  
|VerboseLogging|bigint|Nivel de registro para el clúster de conmutación por error de SQL Server. Se puede activar el registro detallado para proporcionar detalles adicionales en los registros de errores para solucionar problemas. Los valores pueden ser los siguientes:<br /><br /> 0: el registro está desactivado (valor predeterminado)<br /><br /> 1: solo errores<br /><br /> 2: errores y advertencias<br /><br /> Para obtener más información, consulte [ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-configuration-transact-sql.md).|  
|SqlDumperDumpFlags|bigint|Las marcas de volcado de SQLDumper determinan el tipo de archivos de volcado generados por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El valor predeterminado es 0.|  
|SqlDumperDumpPath|nvarchar(260)|Ubicación donde la utilidad SQLDumper genera los archivos de volcado.|  
|SqlDumperDumpTimeOut|bigint|Valor de tiempo de espera en milisegundos para que la utilidad SQLDumper genere un volcado en caso de un error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El valor predeterminado es 0.|  
|FailureConditionLevel|bigint|Establece las condiciones en que el clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe producir la conmutación por error o reiniciarse. El valor predeterminado es 3. Para obtener una explicación detallada o para cambiar los valores de propiedad, vea [configurar los valores de propiedad FailureConditionLevel](../../sql-server/failover-clusters/windows/configure-failureconditionlevel-property-settings.md).|  
|HealthCheckTimeout|bigint|Valor de tiempo de espera que establece cuánto tiempo debe la DLL del recurso del motor de base de datos de SQL Server esperar la información de estado del servidor antes de considerar que la instancia de SQL Server no responde. El valor de tiempo de espera se expresa en milisegundos. Valor predeterminado es 60000. Para obtener más información o para cambiar el valor de esta propiedad, vea [Configure HealthCheckTimeout Property Settings](../../sql-server/failover-clusters/windows/configure-healthchecktimeout-property-settings.md).|  
  
## <a name="permissions"></a>Permissions  
 Necesita permisos VIEW SERVER STATE en la instancia en clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se usa sys.dm_os_cluster_properties para devolver los valores de propiedad para el recurso de clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
SELECT VerboseLogging, SqlDumperDumpFlags, SqlDumperDumpPath, SqlDumperDumpTimeOut, FailureConditionLevel, HealthCheckTimeout  
FROM sys.dm_os_cluster_properties;  
```  
  
 A continuación se muestra un conjunto de resultados de ejemplo.  
  
|VerboseLogging|SqlDumperDumpFlags|SqlDumperDumpPath|SqlDumperDumpTimeOut|FailureConditionLevel|HealthCheckTimeout|  
|--------------------|------------------------|-----------------------|--------------------------|---------------------------|------------------------|  
|0|0|NULL|0|3|60000|  
  
  
