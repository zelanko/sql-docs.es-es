---
title: Cambios substanciales en las características del Motor de base de datos de SQL Server 2016 | Microsoft Docs
ms.custom: ''
ms.date: 11/27/2016
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
manager: jroth
ms.openlocfilehash: b2fda344839ee7d885a11313d088140738dfb640
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66803406"
---
# <a name="breaking-changes-to-database-engine-features-in-sql-server-2016"></a>Cambios substanciales en las características del Motor de base de datos de SQL Server 2016
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  En este tema se describen los cambios recientes en [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)][!INCLUDE[ssDE](../includes/ssde-md.md)] y versiones anteriores de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Estos cambios pueden provocar errores en las aplicaciones, en los scripts o en las funcionalidades basados en versiones anteriores de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Podría encontrar estos problemas al actualizar.  
  
##  <a name="SQL15"></a> Cambios recientes en [!INCLUDE[ssSQL15](../includes/sssql15-md.md)]  
  
-   La columna *sample_ms* de `sys.dm_io_virtual_file_stats` ha pasado de ser un tipo de datos **int** a **bigint**.  
  
-   La columna *TimeStamp* de `sys.fn_virtualfilestats` pasó de ser un tipo de datos **int** a un tipo de datos **bigint**.  

-   Por debajo del nivel de compatibilidad de base de datos 130, las conversiones implícitas de los tipos de datos **datetime** a **datetime2** muestran una mayor precisión al reflejar las fracciones de milisegundos, lo que se traduce en diferentes valores convertidos. Use una conversión explícita del tipo de datos datetime2 siempre que haya un escenario de comparación mixto entre tipos de datos datetime y datetime2. Para obtener más información, vea este [artículo de Soporte técnico de Microsoft](https://support.microsoft.com/help/4010261).

-   En el nivel de compatibilidad de la base de datos 130, las operaciones que realizan las conversiones implícitas entre determinados tipos de datos numéricos y de fecha y hora muestran una mayor precisión y pueden generar diferentes valores convertidos. Esto incluye el uso de funciones que requieren cálculos, como `DATEDIFF` y `ROUND`. Para obtener más información, vea este [artículo de Soporte técnico de Microsoft](https://support.microsoft.com/help/4010261).

## <a name="previous-versions"></a> Versiones anteriores  

Para obtener información sobre los cambios importantes en [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] y en algunas versiones anteriores, vea [Cambios recientes en las características del Motor de base de datos de SQL Server 2014](../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md?view=sql-server-2014).

#### <a name="archived-documentation-for-very-old-versions-of-sql-server"></a>Documentación archivada para las versiones muy antiguas de SQL Server

[!INCLUDE[Archived documentation for very old versions of SQL Server](../includes/paragraph-content/previous-versions-archive-documentation-sql-server.md)]

## <a name="see-also"></a>Consulte también  
 [Características desusadas del motor de base de datos de SQL Server 2016](../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)   
 [Funcionalidad del motor de base de datos no incluida en SQL Server 2016](../database-engine/discontinued-database-engine-functionality-in-sql-server-2016.md)   
 [Compatibilidad con versiones anteriores del Motor de base de datos de SQL Server](../database-engine/sql-server-database-engine-backward-compatibility.md)   
 [Nivel de compatibilidad de ALTER DATABASE &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-compatibility-level.md)   
 [Mejoras de SQL Server 2016 o 2017 en Windows en la manipulación de algunos tipos de datos y operaciones infrecuentes](https://support.microsoft.com/help/4010261)   
