---
title: Cambios substanciales en las características del Motor de base de datos de SQL Server 2016 | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: release-landing
ms.topic: conceptual
helpviewer_keywords:
- Database Engine [SQL Server], what's new
- breaking changes [SQL Server]
ms.assetid: 47edefbd-a09b-4087-937a-453cd5c6e061
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c2680ee81bbf2f4b49eb3835bb18a3d4b712f8c5
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/13/2018
ms.locfileid: "51602695"
---
# <a name="breaking-changes-to-database-engine-features-in-sql-server-2016"></a>Cambios substanciales en las características del Motor de base de datos de SQL Server 2016
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  En este tema se describen los cambios recientes en [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)][!INCLUDE[ssDE](../includes/ssde-md.md)] y versiones anteriores de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Estos cambios pueden provocar errores en las aplicaciones, en los scripts o en las funcionalidades basados en versiones anteriores de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Podría encontrar estos problemas al actualizar.  
  
##  <a name="SQL15"></a> Cambios recientes en [!INCLUDE[ssSQL15](../includes/sssql15-md.md)]  
  
-   La columna sample_ms de sys.dm_io_virtual_file_stats ha pasado de ser un tipo de datos **int** a **bigint** .  
  
-   La columna TimeStamp de sys.fn_virtualfilestats pasó de ser un tipo de datos **int** a un tipo de datos **bigint** .  

-   El empleo de los algoritmos de hash MD2, MD4, MD5, SHA o SHA1 (no recomendado) exige establecer el nivel de compatibilidad de base de datos en anterior a 130.  

-   Por debajo del nivel de compatibilidad de base de datos 130, las conversiones implícitas de los tipos de datos **datetime** a **datetime2** muestran una mayor precisión al reflejar las fracciones de milisegundos, lo que se traduce en diferentes valores convertidos. Use una conversión explícita del tipo de datos datetime2 siempre que haya un escenario de comparación mixto entre tipos de datos datetime y datetime2. Para obtener más información, consulte este [artículo del servicio de soporte técnico de Microsoft](https://support.microsoft.com/help/4010261).
  
## <a name="previous-versions"></a>Versiones anteriores  
  
-   [Cambios recientes en las características del Motor de base de datos de SQL Server 2014](breaking-changes-to-database-engine-features-in-sql-server-2016.md)  
  
-   [Cambios recientes en las características del Motor de base de datos de SQL Server 2012](breaking-changes-to-database-engine-features-in-sql-server-2016.md)  
  
-   [Cambios recientes en las características del Motor de base de datos de SQL Server 2008](breaking-changes-to-database-engine-features-in-sql-server-2016.md)  
  
## <a name="see-also"></a>Ver también  
 [Características desusadas del motor de base de datos de SQL Server 2016](../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)   
 [Funcionalidad del motor de base de datos no incluida en SQL Server 2016](../database-engine/discontinued-database-engine-functionality-in-sql-server-2016.md)   
 [Compatibilidad con versiones anteriores del Motor de base de datos de SQL Server](../database-engine/sql-server-database-engine-backward-compatibility.md)   
 [Nivel de compatibilidad de ALTER DATABASE &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-compatibility-level.md)   
 [Mejoras de SQL Server 2016 o 2017 en Windows en la manipulación de algunos tipos de datos y operaciones infrecuentes](https://support.microsoft.com/help/4010261)
  
  
