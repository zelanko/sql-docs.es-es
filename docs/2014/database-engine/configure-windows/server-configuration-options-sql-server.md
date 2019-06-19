---
title: Opciones de configuración de servidor (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 02/29/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- surface area configuration [SQL Server], sp_configure
- configuration options [SQL Server], when take effect
- server management [SQL Server], configuration options
- SQL Server Management Studio [SQL Server], servers
- servers [SQL Server], configuring
- configuration options [SQL Server], setting
- options [SQL Server], configuration
- RECONFIGURE statement
- performance [SQL Server], servers
- configuration options [SQL Server]
- RECONFIGURE WITH OVERRIDE statement
- SQL Server, configuring
- sp_configure
- stored procedures [SQL Server], configuration options
- server configuration [SQL Server]
- administering SQL Server, configuration options
ms.assetid: 9f38eba6-39b1-4f1d-ba24-ee4f7e2bc969
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 645aee1374f7dbf3c290500bb35ca47115983670
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62809573"
---
# <a name="server-configuration-options-sql-server"></a>Opciones de configuración de servidor (SQL Server)
  Puede administrar y optimizar los recursos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante opciones de configuración con [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o el procedimiento almacenado del sistema sp_configure. Las opciones de configuración de servidores más utilizadas están disponibles mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]; es posible el acceso a todas las opciones de configuración mediante sp_configure. Antes de establecer estas opciones, debe considerar detenidamente los efectos en el sistema. Para obtener más información, vea [Ver o cambiar las propiedades del servidor &#40;SQL Server&#41;](view-or-change-server-properties-sql-server.md).  
  
> [!IMPORTANT]  
>  Solo un administrador de la base de datos con experiencia o un técnico de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con la titulación apropiada debe cambiar las opciones avanzadas.  
  
## <a name="categories-of-configuration-options"></a>Categorías de las opciones de configuración  
 Las opciones de configuración tienen efecto en uno de estos dos momentos:  
  
-   Inmediatamente después de establecer la opción y ejecutar la instrucción RECONFIGURE (o, en algunos casos, RECONFIGURE WITH OVERRIDE).  
  
     -o bien-  
  
-   Después de realizar las acciones anteriores y reiniciar la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Las opciones que necesitan que se reinicie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solo mostrarán inicialmente el valor modificado en la columna value. Después de reiniciar, el nuevo valor aparecerá tanto en la columna value como en la columna value_in_use.  
  
 Para algunas opciones, es necesario reiniciar el servidor para que el valor de la nueva configuración surta efecto. Si establece el nuevo valor y ejecuta sp_configure antes de reiniciar el servidor, el nuevo valor aparecerá en la columna value de las opciones de configuración, pero no en la columna value_in_use. Después de reiniciar el servidor, el nuevo valor aparecerá en la columna value_in_use.  
  
 Las opciones de configuración automática son aquellas que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ajusta según las necesidades del sistema. En la mayoría de los casos, esto elimina la necesidad de establecer los valores manualmente. Como ejemplo se pueden citar las opciones min server memory y max server memory, así como la opción user connections.  
  
## <a name="configuration-options-table"></a>Tabla de opciones de configuración  
 La siguiente tabla contiene todas las opciones de configuración disponibles, la gama de valores posibles y los valores predeterminados. Las opciones de configuración están marcadas con códigos de letras de la forma siguiente:  
  
-   A = Opciones avanzadas, que solo deben ser cambiadas por un administrador de base de datos con experiencia o un técnico de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con la titulación apropiada, y que requieren el valor 1 para show advanced options.  
  
-   RR = Opciones que requieren el reinicio del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
-   SC = Opciones de configuración automática.  
  
    |Opción de configuración|Valor mínimo|Valor máximo|Default|  
    |--------------------------|-------------------|-------------------|-------------|  
    |[access check cache bucket count](access-check-cache-server-configuration-options.md) (A)|0|16384|0|  
    |[access check cache quota](access-check-cache-server-configuration-options.md) (A)|0|2147483647|0|  
    |[ad hoc distributed queries](ad-hoc-distributed-queries-server-configuration-option.md) (A)|0|1|0|  
    |[affinity I/O mask](affinity-input-output-mask-server-configuration-option.md) (A, RR)|-2147483648|2147483647|0|  
    |[affinity64 I/O mask](affinity64-input-output-mask-server-configuration-option.md) (A, disponible solo en la versión de 64 bits de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])|-2147483648|2147483647|0|  
    |[affinity mask](affinity-mask-server-configuration-option.md) (A)|-2147483648|2147483647|0|  
    |[affinity64 mask](affinity64-mask-server-configuration-option.md) (A, RR), disponible solo en la versión de 64 bits de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|-2147483648|2147483647|0|  
    |[Agent XPs](agent-xps-server-configuration-option.md) (A)|0|1|0<br /><br /> Cambia a 1 cuando se inicia el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . El valor predeterminado es 0 si el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se establece para que se inicie automáticamente durante la instalación.|  
    |[allow updates](allow-updates-server-configuration-option.md) (obsoleto. No debe usarse. Generará un error durante la reconfiguración).|0|1|0|  
    |[Valor predeterminado de la suma de comprobación de copia de seguridad](../backup-checksum-default.md)|0|1|0|  
    |[compresión de copia de seguridad predeterminada](view-or-configure-the-backup-compression-default-server-configuration-option.md)|0|1|0|  
    |[blocked process threshold](blocked-process-threshold-server-configuration-option.md) (A)|0|86400|0|  
    |[c2 audit mode](c2-audit-mode-server-configuration-option.md) (A, RR)|0|1|0|  
    |[clr enabled](clr-enabled-server-configuration-option.md)|0|1|0|  
    |[common criteria compliance enabled](common-criteria-compliance-enabled-server-configuration-option.md) (A, RR)|0|1|0|  
    |[autenticación de la base de datos independiente (A)](contained-database-authentication-server-configuration-option.md)|0||0|  
    |[cost threshold for parallelism](configure-the-cost-threshold-for-parallelism-server-configuration-option.md) (A)|0|32767|5|  
    |[cross db ownership chaining](cross-db-ownership-chaining-server-configuration-option.md)|0|1|0|  
    |[cursor threshold](configure-the-cursor-threshold-server-configuration-option.md) (A)|-1|2147483647|-1|  
    |[Database Mail XPs](database-mail-xps-server-configuration-option.md) (A)|0|1|0|  
    |[default full-text language](configure-the-default-full-text-language-server-configuration-option.md) (A)|0|2147483647|3082|  
    |[default language](configure-the-default-language-server-configuration-option.md)|0|9999|0|  
    |[default trace enabled](default-trace-enabled-server-configuration-option.md) (A)|0|1|1|  
    |[disallow results from triggers](disallow-results-from-triggers-server-configuration-option.md) (A)|0|1|0|  
    |[EKM provider enabled](ekm-provider-enabled-server-configuration-option.md)|0|1|0|  
    |[filestream_access_level](filestream-access-level-server-configuration-option.md)|0|2|0|  
    |[fill factor](configure-the-fill-factor-server-configuration-option.md) (A, RR)|0|100|0|  
    |ft crawl bandwidth (max); vea [ft crawl bandwidth](ft-crawl-bandwidth-server-configuration-option.md)(A)|0|32767|100|  
    |ft crawl bandwidth (min); vea [ft crawl bandwidth](ft-crawl-bandwidth-server-configuration-option.md)(A)|0|32767|0|  
    |ft notify bandwidth (max); vea [ft notify bandwidth](ft-notify-bandwidth-server-configuration-option.md)(A)|0|32767|100|  
    |ft notify bandwidth (min); vea [ft notify bandwidth](ft-notify-bandwidth-server-configuration-option.md)(A)|0|32767|0|  
    |[index create memory](configure-the-index-create-memory-server-configuration-option.md) (A, SC)|704|2147483647|0|  
    |[in-doubt xact resolution](in-doubt-xact-resolution-server-configuration-option.md) (A)|0|2|0|  
    |[lightweight pooling](lightweight-pooling-server-configuration-option.md) (A, RR)|0|1|0|  
    |[locks](configure-the-locks-server-configuration-option.md) (A, RR, SC)|5000|2147483647|0|  
    |[max degree of parallelism](configure-the-max-degree-of-parallelism-server-configuration-option.md) (A)|0|32767|0|  
    |[max full-text crawl range](max-full-text-crawl-range-server-configuration-option.md) (A)|0|256|4|  
    |[max server memory](server-memory-server-configuration-options.md) (A, SC)|16|2147483647|2147483647|  
    |[max text repl size](configure-the-max-text-repl-size-server-configuration-option.md)|0|2147483647|65536|  
    |[max worker threads](configure-the-max-worker-threads-server-configuration-option.md) (A)|128|32767<br /><br /> 1024 es el máximo recomendado para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de 32 bits, y 2048 para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de 64 bits.|0<br /><br /> Cero configura automáticamente el número máximo de subprocesos de trabajo dependientes del número de procesadores mediante la fórmula (256 + ( *\<procesadores>* -4) * 8) para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de 32 bits, y dos veces la misma fórmula para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de 64 bits.|  
    |[media retention](configure-the-media-retention-server-configuration-option.md) (A, RR)|0|365|0|  
    |[min memory per query](configure-the-min-memory-per-query-server-configuration-option.md) (A)|512|2147483647|1024|  
    |[min server memory](server-memory-server-configuration-options.md) (A, SC)|0|2147483647|0|  
    |[desencadenadores anidados](configure-the-nested-triggers-server-configuration-option.md)|0|1|1|  
    |[network packet size](configure-the-network-packet-size-server-configuration-option.md) (A)|512|32767|4096|  
    |[Ole Automation Procedures](ole-automation-procedures-server-configuration-option.md) (A)|0|1|0|  
    |[open objects](open-objects-server-configuration-option.md) (A, RR, obsoleto)|0|2147483647|0|  
    |[optimize for ad hoc workloads](optimize-for-ad-hoc-workloads-server-configuration-option.md) (A)|0|1|0|  
    |[PH_timeout](ph-timeout-server-configuration-option.md) (A)|1|3600|60|  
    |[precompute rank](precompute-rank-server-configuration-option.md) (A)|0|1|0|  
    |[priority boost](configure-the-priority-boost-server-configuration-option.md) (A, RR)|0|1|0|  
    |[query governor cost limit](configure-the-query-governor-cost-limit-server-configuration-option.md) (A)|0|2147483647|0|  
    |[query wait](configure-the-query-wait-server-configuration-option.md) (A)|-1|2147483647|-1|  
    |[recovery interval](configure-the-recovery-interval-server-configuration-option.md) (A, SC)|0|32767|0|  
    |[remote access](configure-the-remote-access-server-configuration-option.md) (RR)|0|1|1|  
    |[remote admin connections](remote-admin-connections-server-configuration-option.md)|0|1|0|  
    |[remote login timeout](configure-the-remote-login-timeout-server-configuration-option.md)|0|2147483647|10|  
    |[remote proc trans](configure-the-remote-proc-trans-server-configuration-option.md)|0|1|0|  
    |[remote query timeout](configure-the-remote-query-timeout-server-configuration-option.md)|0|2147483647|600|  
    |[Opción Replication XPs](replication-xps-server-configuration-option.md) (A)|0|1|0|  
    |[scan for startup procs](configure-the-scan-for-startup-procs-server-configuration-option.md) (A, RR)|0|1|0|  
    |[server trigger recursion](server-trigger-recursion-server-configuration-option.md)|0|1|1|  
    |[set working set size](set-working-set-size-server-configuration-option.md) (A, RR, obsoleto)|0|1|0|  
    |[show advanced options](show-advanced-options-server-configuration-option.md)|0|1|0|  
    |[SMO y DMO XPs](smo-and-dmo-xps-server-configuration-option.md) (A)|0|1|1|  
    |[transform noise words](transform-noise-words-server-configuration-option.md) (A)|0|1|0|  
    |[two digit year cutoff](configure-the-two-digit-year-cutoff-server-configuration-option.md) (A)|1753|9999|2049|  
    |[user connections](configure-the-user-connections-server-configuration-option.md) (A, RR, SC)|0|32767|0|  
    |[user options](configure-the-user-options-server-configuration-option.md)|0|32767|0|  
    |[xp_cmdshell](xp-cmdshell-server-configuration-option.md) (A)|0|1|0|  
  
## <a name="see-also"></a>Vea también  
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)  
  
  
