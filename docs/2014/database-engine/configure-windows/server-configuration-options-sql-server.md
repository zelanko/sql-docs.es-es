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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62809573"
---
# <a name="server-configuration-options-sql-server"></a>Opciones de configuración de servidor (SQL Server)
  Puede administrar y optimizar los recursos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante opciones de configuración con [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o el procedimiento almacenado del sistema sp_configure. Las opciones de configuración de servidores más utilizadas están disponibles mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]; es posible el acceso a todas las opciones de configuración mediante sp_configure. Antes de establecer estas opciones, debe considerar detenidamente los efectos en el sistema. Para obtener más información, vea [Ver o cambiar las propiedades del servidor &#40;SQL Server&#41;](view-or-change-server-properties-sql-server.md).  
  
> [!IMPORTANT]  
>  Solo un administrador de la base de datos con experiencia o un técnico de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con la titulación apropiada debe cambiar las opciones avanzadas.  
  
## <a name="categories-of-configuration-options"></a>Categorías de las opciones de configuración  
 Las opciones de configuración tienen efecto en uno de estos dos momentos:  
  
-   Inmediatamente después de establecer la opción y ejecutar la instrucción RECONFIGURE (o, en algunos casos, RECONFIGURE WITH OVERRIDE).  
  
     O bien  
  
-   Después de realizar las acciones anteriores y reiniciar la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Las opciones que necesitan que se reinicie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solo mostrarán inicialmente el valor modificado en la columna value. Después de reiniciar, el nuevo valor aparecerá tanto en la columna value como en la columna value_in_use.  
  
 Para algunas opciones, es necesario reiniciar el servidor para que el valor de la nueva configuración surta efecto. Si establece el nuevo valor y ejecuta sp_configure antes de reiniciar el servidor, el nuevo valor aparecerá en la columna value de las opciones de configuración, pero no en la columna value_in_use. Después de reiniciar el servidor, el nuevo valor aparecerá en la columna value_in_use.  
  
 Las opciones de configuración automática son aquellas que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ajusta según las necesidades del sistema. En la mayoría de los casos, esto elimina la necesidad de establecer los valores manualmente. Como ejemplo se pueden citar las opciones min server memory y max server memory, así como la opción user connections.  
  
## <a name="configuration-options-table"></a>Tabla de opciones de configuración  
 La siguiente tabla contiene todas las opciones de configuración disponibles, la gama de valores posibles y los valores predeterminados. Las opciones de configuración están marcadas con códigos de letras de la forma siguiente:  
  
-   A = Opciones avanzadas, que solo deben ser cambiadas por un administrador de base de datos con experiencia o un técnico de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con la titulación apropiada, y que requieren el valor 1 para show advanced options.  
  
-   RR = Opciones que requieren el reinicio del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
-   SC = Opciones de configuración automática.  
  
    |Opción de configuración|Valor mínimo|Valor máximo|Valor predeterminado|  
    |--------------------------|-------------------|-------------------|-------------|  
    |[comprobar el número de depósitos de caché](access-check-cache-server-configuration-options.md) (a)|0|16384|0|  
    |[comprobar la cuota de caché](access-check-cache-server-configuration-options.md) (a)|0|2147483647|0|  
    |[consultas distribuidas ad hoc](ad-hoc-distributed-queries-server-configuration-option.md) (A)|0|1|0|  
    |[affinity I/o Mask](affinity-input-output-mask-server-configuration-option.md) (A, RR)|-2147483648|2147483647|0|  
    |[affinity64 I/o Mask](affinity64-input-output-mask-server-configuration-option.md) (a, solo disponible en la versión de 64 bits [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]de)|-2147483648|2147483647|0|  
    |[máscara de afinidad](affinity-mask-server-configuration-option.md) (A)|-2147483648|2147483647|0|  
    |[affinity64 Mask](affinity64-mask-server-configuration-option.md) (A, RR), disponible solo en la versión de 64 bits de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|-2147483648|2147483647|0|  
    |[Agent XPS](agent-xps-server-configuration-option.md) (A)|0|1|0<br /><br /> Cambia a 1 cuando se inicia el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El valor predeterminado es 0 si el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se establece para que se inicie automáticamente durante la instalación.|  
    |[permitir actualizaciones](allow-updates-server-configuration-option.md) (obsoleto. No debe usarse. Generará un error durante la reconfiguración).|0|1|0|  
    |[Valor predeterminado de la suma de comprobación de copia de seguridad](../backup-checksum-default.md)|0|1|0|  
    |[compresión de copia de seguridad predeterminada](view-or-configure-the-backup-compression-default-server-configuration-option.md)|0|1|0|  
    |[umbral de proceso bloqueado](blocked-process-threshold-server-configuration-option.md) (A)|0|86400|0|  
    |[modo auditoría C2](c2-audit-mode-server-configuration-option.md) (A, RR)|0|1|0|  
    |[clr enabled](clr-enabled-server-configuration-option.md)|0|1|0|  
    |[compatibilidad con criterio común habilitada](common-criteria-compliance-enabled-server-configuration-option.md) (A, RR)|0|1|0|  
    |[autenticación de la base de datos independiente (A)](contained-database-authentication-server-configuration-option.md)|0||0|  
    |[umbral de costo para paralelismo](configure-the-cost-threshold-for-parallelism-server-configuration-option.md) (A)|0|32767|5|  
    |[cross db ownership chaining](cross-db-ownership-chaining-server-configuration-option.md)|0|1|0|  
    |[umbral de cursor](configure-the-cursor-threshold-server-configuration-option.md) (A)|-1|2147483647|-1|  
    |[Correo electrónico de base de datos XPS](database-mail-xps-server-configuration-option.md) (A)|0|1|0|  
    |[idioma de texto completo predeterminado](configure-the-default-full-text-language-server-configuration-option.md) (A)|0|2147483647|1033|  
    |[idioma predeterminado](configure-the-default-language-server-configuration-option.md)|0|9.999|0|  
    |[seguimiento predeterminado habilitado](default-trace-enabled-server-configuration-option.md) (A)|0|1|1|  
    |no [permitir resultados de desencadenadores](disallow-results-from-triggers-server-configuration-option.md) (A)|0|1|0|  
    |[EKM provider enabled](ekm-provider-enabled-server-configuration-option.md)|0|1|0|  
    |[filestream_access_level](filestream-access-level-server-configuration-option.md)|0|2|0|  
    |[factor de relleno](configure-the-fill-factor-server-configuration-option.md) (A, RR)|0|100|0|  
    |ft crawl bandwidth (max); vea [ft crawl bandwidth](ft-crawl-bandwidth-server-configuration-option.md)(A)|0|32767|100|  
    |ft crawl bandwidth (min); vea [ft crawl bandwidth](ft-crawl-bandwidth-server-configuration-option.md)(A)|0|32767|0|  
    |ft notify bandwidth (max); vea [ft notify bandwidth](ft-notify-bandwidth-server-configuration-option.md)(A)|0|32767|100|  
    |ft notify bandwidth (min); vea [ft notify bandwidth](ft-notify-bandwidth-server-configuration-option.md)(A)|0|32767|0|  
    |[memoria para creación de índices](configure-the-index-create-memory-server-configuration-option.md) (A, SC)|704|2147483647|0|  
    |[resolución de xACT dudosa](in-doubt-xact-resolution-server-configuration-option.md) (A)|0|2|0|  
    |[agrupación ligera](lightweight-pooling-server-configuration-option.md) (A, RR)|0|1|0|  
    |[bloqueos](configure-the-locks-server-configuration-option.md) (A, RR, SC)|5000|2147483647|0|  
    |[grado máximo de paralelismo](configure-the-max-degree-of-parallelism-server-configuration-option.md) (A)|0|32767|0|  
    |[intervalo máximo de rastreo de texto completo](max-full-text-crawl-range-server-configuration-option.md) (A)|0|256|4|  
    |[Max Server Memory](server-memory-server-configuration-options.md) (A, SC)|16|2147483647|2147483647|  
    |[max text repl size](configure-the-max-text-repl-size-server-configuration-option.md)|0|2147483647|65536|  
    |[número máximo de subprocesos de trabajo](configure-the-max-worker-threads-server-configuration-option.md) (A)|128|32767<br /><br /> 1024 es el máximo recomendado para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de 32 bits, y 2048 para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de 64 bits.|0<br /><br /> Cero configura automáticamente el número máximo de subprocesos de trabajo en función del número de procesadores, usando la fórmula (256 + (*\<procesadores>* -4) * 8) para 32 bits [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y dos veces la misma para 64 bits [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
    |[retención de medios](configure-the-media-retention-server-configuration-option.md) (A, RR)|0|365|0|  
    |[memoria mínima por consulta](configure-the-min-memory-per-query-server-configuration-option.md) (A)|512|2147483647|1024|  
    |[memoria de servidor mínima](server-memory-server-configuration-options.md) (A, SC)|0|2147483647|0|  
    |[desencadenadores anidados](configure-the-nested-triggers-server-configuration-option.md)|0|1|1|  
    |[tamaño de paquete de red](configure-the-network-packet-size-server-configuration-option.md) (A)|512|32767|4096|  
    |[Procedimientos de automatización OLE](ole-automation-procedures-server-configuration-option.md) (A)|0|1|0|  
    |[Open Objects](open-objects-server-configuration-option.md) (A, RR, obsoleto)|0|2147483647|0|  
    |[optimizar para cargas de trabajo ad hoc](optimize-for-ad-hoc-workloads-server-configuration-option.md) (A)|0|1|0|  
    |[PH_timeout](ph-timeout-server-configuration-option.md) (A)|1|3600|60|  
    |[calcular rango previamente](precompute-rank-server-configuration-option.md) (A)|0|1|0|  
    |[aumento de prioridad](configure-the-priority-boost-server-configuration-option.md) (A, RR)|0|1|0|  
    |[límite de costo del regulador de consultas](configure-the-query-governor-cost-limit-server-configuration-option.md) (A)|0|2147483647|0|  
    |[espera de consulta](configure-the-query-wait-server-configuration-option.md) (A)|-1|2147483647|-1|  
    |[Recovery Interval](configure-the-recovery-interval-server-configuration-option.md) (A, SC)|0|32767|0|  
    |[acceso remoto](configure-the-remote-access-server-configuration-option.md) (RR)|0|1|1|  
    |[remote admin connections](remote-admin-connections-server-configuration-option.md)|0|1|0|  
    |[tiempo de espera de inicio de sesión remoto](configure-the-remote-login-timeout-server-configuration-option.md)|0|2147483647|10|  
    |[transacciones de procedimientos remotos](configure-the-remote-proc-trans-server-configuration-option.md)|0|1|0|  
    |[remote query timeout](configure-the-remote-query-timeout-server-configuration-option.md)|0|2147483647|600|  
    |[Opción Replication XPS](replication-xps-server-configuration-option.md) (A)|0|1|0|  
    |[Buscar procedimientos de inicio](configure-the-scan-for-startup-procs-server-configuration-option.md) (A, RR)|0|1|0|  
    |[server trigger recursion](server-trigger-recursion-server-configuration-option.md)|0|1|1|  
    |[establecer el tamaño del espacio de trabajo](set-working-set-size-server-configuration-option.md) (A, RR, obsoleto)|0|1|0|  
    |[show advanced options](show-advanced-options-server-configuration-option.md)|0|1|0|  
    |[SMO y DMO XPS](smo-and-dmo-xps-server-configuration-option.md) (A)|0|1|1|  
    |[transformar palabras irrelevantes](transform-noise-words-server-configuration-option.md) (A)|0|1|0|  
    |[fecha límite de año de dos dígitos](configure-the-two-digit-year-cutoff-server-configuration-option.md) (A)|1753|9.999|2049|  
    |[conexiones de usuario](configure-the-user-connections-server-configuration-option.md) (A, RR, SC)|0|32767|0|  
    |[user options](configure-the-user-options-server-configuration-option.md)|0|32767|0|  
    |[xp_cmdshell](xp-cmdshell-server-configuration-option.md) (A)|0|1|0|  
  
## <a name="see-also"></a>Consulte también  
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)  
  
  
