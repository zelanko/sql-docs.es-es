---
title: Funcionalidad del motor de base de datos no incluida en SQL Server 2016 | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 02/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 100
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 36ac9e8ad8a2eac7291ff87ce5c691ac79a0ea79
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="discontinued-database-engine-functionality-in-sql-server-2016"></a>Funcionalidad del motor de base de datos no incluida en SQL Server 2016
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  En este tema se describen las características del [!INCLUDE[ssDE](../includes/ssde-md.md)] que ya no están disponibles en [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].  
  
## <a name="discontinued-features-in-includesssql15includessssql15-mdmd"></a>Características no incluidas en [!INCLUDE[ssSQL15](../includes/sssql15-md.md)]  
  
-   [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] es una aplicación de 64 bits. La instalación de 32 bits está descontinuada, a pesar de que algunos de los elementos se ejecutan como componentes de 32 bits.  
  
-   El nivel de compatibilidad 90 se ha dejado de usar. Para obtener más información, vea [Nivel de compatibilidad de ALTER DATABASE &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  

-   No se incluye el subsistema Active X. En su lugar, use scripts de PowerShell o la línea de comandos.
  
## <a name="previous-versions"></a>Versiones anteriores  
  
-   [Funcionalidad del motor de base de datos no incluida en SQL Server 2014](https://msdn.microsoft.com/library/ms144262\(v=sql.120\))  
  
-   [Funcionalidad del motor de base de datos no incluida en SQL Server 2012](https://msdn.microsoft.com/library/ms144262\(v=sql.110\))  
  
-   [Funcionalidad del motor de base de datos no incluida en SQL Server 2008](https://msdn.microsoft.com/library/ms144262\(v=sql.100\))  
  
## <a name="see-also"></a>Vea también  
 [Características desusadas del motor de base de datos de SQL Server 2016](../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)   
 [Características que ya no se usan en la replicación de SQL Server](../relational-databases/replication/deprecated-features-in-sql-server-replication.md)  
  
 

