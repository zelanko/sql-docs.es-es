---
title: "Funcionalidad del motor de base de datos no incluida en SQL Server 2016 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "02/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "protocolo VIA"
  - "características no admitidas [SQL Server]"
  - "SQL Mail"
  - "funcionalidad no incluida [SQL Server]"
  - "RESTORE WITH DBO_ONLY"
  - "BACKUP WITH PASSWORD"
  - "instancias de usuario habilitadas"
  - "BACKUP WITH MEDIAPASSWORD"
  - "AWE"
  - "SQL-DMO"
  - "*= y =*"
  - "80 niveles de compatibilidad"
  - "COMPUTE BY"
  - "tiempo de espera de instancia de usuario"
  - "sp_dropalias"
  - "COMPUTE"
  - "WITH APPEND"
  - "sys.database_principal_aliases"
  - "sp_dboption"
  - "DATABASEPROPERTY"
  - "Sugerencia FASTFIRSTROW"
  - "SET DISABLE_DEF_CNST_CHK"
ms.assetid: d686cdf0-d11d-4dba-9ec8-de1a5f189f25
caps.latest.revision: 100
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 100
---
# Funcionalidad del motor de base de datos no incluida en SQL Server 2016
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  En este tema se describen las características del [!INCLUDE[ssDE](../includes/ssde-md.md)] que ya no están disponibles en [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].  
  
## <a name="discontinued-features-in-includesssql15tokensssql15mdmd"></a>Características no incluidas en [!INCLUDE[ssSQL15](../includes/sssql15-md.md)]  
  
-   [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] es una aplicación de 64 bits. La instalación de 32 bits está descontinuada, a pesar de que algunos de los elementos se ejecutan como componentes de 32 bits.  
  
-   El nivel de compatibilidad 90 se ha dejado de usar. Para obtener más información, vea [Nivel de compatibilidad de ALTER DATABASE &#40;Transact-SQL&#41;](../Topic/ALTER%20DATABASE%20Compatibility%20Level%20\(Transact-SQL\).md).  

-   No se incluye el subsistema Active X. En su lugar, use scripts de PowerShell o la línea de comandos.
  
## <a name="previous-versions"></a>Versiones anteriores  
  
-   [Funcionalidad del motor de base de datos no incluida en SQL Server 2014](https://msdn.microsoft.com/library/ms144262\(v=sql.120\))  
  
-   [Funcionalidad del motor de base de datos no incluida en SQL Server 2012](https://msdn.microsoft.com/library/ms144262\(v=sql.110\))  
  
-   [Funcionalidad del motor de base de datos no incluida en SQL Server 2008](https://msdn.microsoft.com/library/ms144262\(v=sql.100\))  
  
## <a name="see-also"></a>Vea también  
 [Características desusadas del motor de base de datos de SQL Server 2016](../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)   
 [Características que ya no se usan en la replicación de SQL Server](../relational-databases/replication/deprecated-features-in-sql-server-replication.md)  
  
 