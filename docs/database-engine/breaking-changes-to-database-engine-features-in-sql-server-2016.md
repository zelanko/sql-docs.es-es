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
manager: craigg
ms.openlocfilehash: 83725ee74e17a91465356b426b13afc0c265f851
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52536385"
---
# <a name="breaking-changes-to-database-engine-features-in-sql-server-2016"></a>Cambios substanciales en las características del Motor de base de datos de SQL Server 2016
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  En este tema se describen los principales cambios en [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)] y versiones anteriores de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Estos cambios pueden provocar errores en las aplicaciones, en los scripts o en las funcionalidades basados en versiones anteriores de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Podría encontrar estos problemas al actualizar.  
  
##  <a name="SQL15"></a> Cambios recientes en [!INCLUDE[ssSQL15](../includes/sssql15-md.md)]  
  
-   La columna sample_ms de sys.dm_io_virtual_file_stats ha pasado de ser un tipo de datos **int** a **bigint** .  
  
-   La columna TimeStamp de sys.fn_virtualfilestats pasó de ser un tipo de datos **int** a un tipo de datos **bigint** .  

-   El empleo de los algoritmos de hash MD2, MD4, MD5, SHA o SHA1 (no recomendado) exige establecer el nivel de compatibilidad de base de datos en anterior a 130.  

-   Por debajo del nivel de compatibilidad de base de datos 130, las conversiones implícitas de los tipos de datos **datetime** a **datetime2** muestran una mayor precisión al reflejar las fracciones de milisegundos, lo que se traduce en diferentes valores convertidos. Use una conversión explícita del tipo de datos datetime2 siempre que haya un escenario de comparación mixto entre tipos de datos datetime y datetime2. Para obtener más información, consulte este [artículo del servicio de soporte técnico de Microsoft](https://support.microsoft.com/help/4010261).

## <a name="previous-versions"></a> Versiones anteriores  

Para obtener información sobre los cambios importantes en SQL Server versión 2014 y en algunas versiones anteriores, vea [Cambios recientes en las características del Motor de base de datos de SQL Server 2014](https://docs.microsoft.com/sql/database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016?view=sql-server-2014#SQL14).

#### <a name="archived-documentation-for-very-old-versions-of-sql-server"></a>Documentación archivada para las versiones muy antiguas de SQL Server

[!INCLUDE[Archived documentation for very old versions of SQL Server](../includes/paragraph-content/previous-versions-archive-documentation-sql-server.md)]

## <a name="see-also"></a>Ver también  
 [Características desusadas del motor de base de datos de SQL Server 2016](../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)   
 [Funcionalidad del motor de base de datos no incluida en SQL Server 2016](../database-engine/discontinued-database-engine-functionality-in-sql-server-2016.md)   
 [Compatibilidad con versiones anteriores del Motor de base de datos de SQL Server](../database-engine/sql-server-database-engine-backward-compatibility.md)   
 [Nivel de compatibilidad de ALTER DATABASE &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-compatibility-level.md)   
 [Mejoras de SQL Server 2016 o 2017 en Windows en la manipulación de algunos tipos de datos y operaciones infrecuentes](https://support.microsoft.com/help/4010261)
  
  
