---
title: Funcionalidad del motor de base de datos no incluida | Microsoft Docs
ms.custom: seo-lt-2019
ms.date: 12/13/2019
ms.prod: sql
ms.prod_service: high-availability
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
- SSL
- WITH APPEND
- sys.database_principal_aliases
- sp_dboption
- DATABASEPROPERTY
- FASTFIRSTROW hint
- SET DISABLE_DEF_CNST_CHK
ms.assetid: d686cdf0-d11d-4dba-9ec8-de1a5f189f25
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>= sql-server-linux-2017  || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: db10b57b5eda73cb2bb2105f4f99fb6e5cbed733
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/19/2019
ms.locfileid: "75258120"
---
# <a name="discontinued-database-engine-functionality-in-sql-server"></a>Funcionalidad del motor de base de datos no incluida en SQL Server
[!INCLUDE[tsql-appliesto-ss-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss-xxxx-xxxx-xxx-md.md)]

  En este tema se describen las características del [!INCLUDE[ssDE](../includes/ssde-md.md)] que ya no están disponibles en [!INCLUDE[ssCurrent](../includes/ssnoversion-md.md)].  

## <a name="discontinued-features-in-includesssqlv15includessssqlv15-mdmd"></a>Características no incluidas en [!INCLUDE[ssSQLv15](../includes/sssqlv15-md.md)]  

- Las siguientes opciones de configuración con ámbito de base de datos no se incluyen:

  - `DISABLE_BATCH_MODE_ADAPTIVE_JOIN`
  - `DISABLE_BATCH_MODE_MEMORY_GRANT_FEEDBACK`
  - `DISABLE_INTERLEAVED_EXECUTION_TVF`

Para obtener las opciones de configuración actuales, vea [ALTER DATABASE SCOPED CONFIGURATION (Transact-SQL)](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).

>[!NOTE]
>Ninguna característica se ha dejado de incluir en [!INCLUDE[ssSQLv14](../includes/sssqlv14-md.md)].

## <a name="discontinued-features-in-includesssql15includessssql15-mdmd"></a>Características no incluidas en [!INCLUDE[ssSQL15](../includes/sssql15-md.md)]

- [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] es una aplicación de 64 bits. La instalación de 32 bits está descontinuada, a pesar de que algunos de los elementos se ejecutan como componentes de 32 bits.  

- El nivel de compatibilidad 90 se ha dejado de usar. Para obtener más información, vea [Nivel de compatibilidad de ALTER DATABASE &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  

- No se incluye el subsistema Active X. En su lugar, use scripts de PowerShell o la línea de comandos.

- Parámetros de inicio **-h** y **-g**. Para más información, consulte [Opciones de inicio del servicio de motor de base de datos](https://docs.microsoft.com/sql/database-engine/configure-windows/database-engine-service-startup-options?view=sql-server-2014).

- Ya no se incluye el cifrado de Capa de sockets seguros (SSL). En su lugar use Seguridad de la capa de transporte (TLS). Para más información, vea [Habilitación de conexiones cifradas en el motor de base de datos](../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).

## <a name="previous-versions"></a>Versiones anteriores

- [Funcionalidad del motor de base de datos no incluida en SQL Server 2014](https://docs.microsoft.com/sql/database-engine/discontinued-database-engine-functionality-in-sql-server-2016?view=sql-server-2014)

### <a name="see-also"></a>Consulte también

- [Características en desuso del motor de base de datos de SQL Server 2019](deprecated-database-engine-features-in-sql-server-version-15.md)
- [Características en desuso del motor de base de datos de SQL Server 2017](deprecated-database-engine-features-in-sql-server-2017.md)
- [Características en desuso del motor de base de datos de SQL Server 2016](../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)
- [Cambios importantes en las características del motor de base de datos de SQL Server 2019](breaking-changes-to-database-engine-features-in-sql-server-version-15.md)
- [Cambios importantes en las características del motor de base de datos de SQL Server 2017](breaking-changes-to-database-engine-features-in-sql-server-2017.md)
- [Cambios importantes en las características del motor de base de datos de SQL Server 2016](breaking-changes-to-database-engine-features-in-sql-server-2016.md)
- [Características en desuso en la replicación de SQL Server](../relational-databases/replication/deprecated-features-in-sql-server-replication.md)