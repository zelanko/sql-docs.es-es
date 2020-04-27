---
title: Funcionalidad de Motor de base de datos no incluida en SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: release-landing
ms.topic: conceptual
helpviewer_keywords:
- VIA protocol
- unsupported features [SQL Server]
- SQL Mail
- discontinued functionality [SQL Server]
- RESTORE WITH DBO_ONLY
- BACKUP WITH PASSWORD
- user instances enabled
- BACKUP WITH MEDIAPASSWORD
- AWE
- SQL-DMO
- '*= and =*'
- 80 compatibility levels
- COMPUTE BY
- user instance timeout
- sp_dropalias
- COMPUTE
- WITH APPEND
- sys.database_principal_aliases
- sp_dboption
- DATABASEPROPERTY
- FASTFIRSTROW hint
- SET DISABLE_DEF_CNST_CHK
ms.assetid: d686cdf0-d11d-4dba-9ec8-de1a5f189f25
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 2ebb9b4e3db7cf8f7a19fd582dceb0b19f5c47d0
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "67463470"
---
# <a name="discontinued-database-engine-functionality-in-sql-server-2014"></a>Funcionalidad del motor de base de datos no incluida en SQL Server 2014
  En este tema se describen las características del [!INCLUDE[ssDE](../includes/ssde-md.md)] que ya no están disponibles en [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].  
  
## <a name="discontinued-features-in-sssql14"></a><a name="SQL14"></a>Características no incluidas en[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 En la tabla siguiente se enumeran las características que se quitaron en [!INCLUDE[ssSQL14](../includes/sssql14-md.md)].  
  
|Categoría|Característica no incluida|Sustituta|  
|--------------|--------------------------|-----------------|  
|Nivel de compatibilidad|Nivel de compatibilidad 90|Las bases de datos se deben establecer en el nivel de compatibilidad 100 como mínimo. Cuando se actualiza una base de datos con un nivel de compatibilidad inferior a 100 a [!INCLUDE[ssSQL14](../includes/sssql14-md.md)], el nivel de compatibilidad de la base de datos se establece en 100 durante la operación de actualización.|  
  
## <a name="discontinued-features-in-sssql11"></a><a name="Denali"></a>Características no incluidas en[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
 En la tabla siguiente se enumeran las características que se quitaron en [!INCLUDE[ssSQL11](../includes/sssql11-md.md)].  
  
|Categoría|Característica no incluida|Sustituta|  
|--------------|--------------------------|-----------------|  
|Copias de seguridad y restauración|La **copia de seguridad {database &#124; log} con la contraseña** y la copia de **seguridad {Database &#124; log} con MEDIAPASSWORD** no se incluyen. **RESTORE {DATABASE &#124; log} con la contraseña de [media]** sigue en desuso.|None|  
|Copias de seguridad y restauración|**RESTORE {DATABASE &#124; LOG}... CON DBO_ONLY**|**RESTORE {DATABASE &#124; LOG}...... CON RESTRICTED_USER**|  
|Nivel de compatibilidad|Nivel de compatibilidad 80|Las bases de datos se deben establecer en el nivel de compatibilidad 90 como mínimo.|  
|Opciones de configuración|`sp_configure 'user instance timeout'` y `'user instances enabled'`|Utilice la característica Local Database. Para obtener más información, consulte [utilidad SqlLocalDB](../tools/sqllocaldb-utility.md)|  
|Protocolos de conexión|Se suspende la compatibilidad para el protocolo VIA.|Utilice TCP en su lugar.|  
|Objetos de base de datos|Cláusula `WITH APPEND` en desencadenadores|Volver a crear todo desencadenador.|  
|Opciones de base de datos|`sp_dboption`|`ALTER DATABASE`|  
|Correo|SQL Mail|Usar Database Mail. Para obtener más información, vea [correo electrónico de base de datos](../relational-databases/database-mail/database-mail.md) y [usar correo electrónico de base de datos en lugar de SQL Mail](../relational-databases/policy-based-management/use-database-mail-instead-of-sql-mail.md).|  
|Administración de la memoria|Compatibilidad para Extensiones de ventana de dirección (AWE) de 32 bits y para agregar memoria sin interrupciones de 32 bits.|Use un sistema operativo de 64 bits.|  
|Metadatos|`DATABASEPROPERTY`|`DATABASEPROPERTYEX`|  
|Capacidad de programación|Objetos de administración distribuida de SQL Server (SQL-DMO)|Objetos de administración de SQL Server (SMO)|  
|Sugerencias de consulta|Sugerencia `FASTFIRSTROW`|`OPTION (FAST`*n* `)`.|  
|Servidores remotos|Ya no se incluye la capacidad para que los usuarios creen nuevos servidores remotos con `sp_addserver`. Solamente sigue estando disponible `sp_addserver` con la opción 'local'. Los servidores remotos conservados durante la actualización o creados por la replicación se pueden utilizar.|Reemplace los servidores remotos con servidores vinculados.|  
|Seguridad|`sp_dropalias`|Reemplace los alias por una combinación de cuentas de usuario y roles de la base de datos. Use `sp_dropalias` para quitar los alias de las bases de datos actualizadas.|  
|Seguridad|El parámetro de versión de **PWDCOMPARE** que representa un valor de un inicio [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] de sesión anterior a 2000 es discontinuo.|None|  
|Programación de Service Broker en SMO|La clase **Microsoft. SqlServer. Management. SMO. Broker. BrokerPriority** ya no implementa la interfaz **Microsoft. SqlServer. Management. SMO. IObjectPermission** .||  
|Opciones de Set|`SET DISABLE_DEF_CNST_CHK`|Ninguno.|  
|Tablas del sistema|sys.database_principal_aliases|Utilice roles en lugar de alias.|  
|Transact-SQL|Ya no se incluye `RAISERROR` en el formato `RAISERROR integer 'string'`.|Vuelva a escribir la instrucción con la sintaxis de **RAISERROR (...)** actual.|  
|Sintaxis de Transact-SQL|`COMPUTE / COMPUTE BY`|Use `ROLLUP`|  
|Sintaxis de Transact-SQL|Uso de ** \* ** y **=&#42;**|Utilice la sintaxis de unión de ANSI. Para obtener más información, vea [from (Transact-SQL).](https://msdn.microsoft.com/library/ms177634\(SQL.105\).aspx)|  
|XEvents|databases_data_file_size_changed, databases_log_file_size_changed<br /><br /> eventdatabases_log_file_used_size_changed<br /><br /> locks_lock_timeouts_greater_than_0<br /><br /> locks_lock_timeouts|Se han reemplazado por evento de database_file_size_change, database_file_size_change<br /><br /> evento de database_file_size_change<br /><br /> lock_timeout_greater_than_0<br /><br /> lock_timeout|  
  
 **Cambios adicionales de XEvent**  
  
 **resource_monitor_ring_buffer_record**:  
  
-   Campos que se han quitado: single_pages_kb, multiple_pages_kb  
  
-   Campos agregados: target_kb, pages_kb  
  
 **memory_node_oom_ring_buffer_recorded**:  
  
-   Campos que se han quitado: single_pages_kb, multiple_pages_kb  
  
-   Campos agregados: target_kb, pages_kb  
  
## <a name="see-also"></a>Consulte también  
 [Características desusadas del motor de base de datos de SQL Server 2014](deprecated-database-engine-features-in-sql-server-2016.md?view=sql-server-2014)  
  
  
