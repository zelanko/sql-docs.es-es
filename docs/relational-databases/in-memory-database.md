---
title: Base de datos en memoria| Microsoft Docs
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- in-memory database
- feature, in-memory database
- in-memory
ms.assetid: 11f8017e-5bc3-4bab-8060-c16282cfbac1
author: briancarrig
ms.author: brcarrig
manager: amitban
ms.openlocfilehash: e4e0e6622a2a313b85dfa00df8c88044486f75f5
ms.sourcegitcommit: be09f0f3708f2e8eb9f6f44e632162709b4daff6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/21/2019
ms.locfileid: "65995003"
---
# <a name="in-memory-database"></a>Base de datos en memoria

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

“Base de datos en memoria” es un término genérico para las características de SQL Server que aprovechan las tecnologías basadas en memoria. A medida que se desarrollen nuevas características basadas en memoria, iremos actualizando esta página.

## <a name="hybrid-buffer-pool"></a>Grupo de búferes híbrido

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

El [grupo de búferes híbrido](../database-engine/configure-windows/hybrid-buffer-pool.md) permite al motor de base de datos acceder directamente a las páginas de datos de los archivos de base de datos almacenados en dispositivos de memoria persistente (PMEM).

## <a name="memory-optimized-tempdb-metadata"></a>Metadatos tempdb optimizados para memoria

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] introduce una nueva característica, [metadatos tempdb optimizados para memoria](./databases/tempdb-database.md#memory-optimized-tempdb-metadata), que quita de forma eficaz algunos cuellos de botella de contención y desbloquea un nuevo nivel de escalabilidad para cargas de trabajo intensivas de tempdb.

## <a name="in-memory-oltp"></a>OLTP en memoria

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[OLTP en memoria](./in-memory-oltp/in-memory-oltp-in-memory-optimization.md) es la tecnología principal disponible en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y [!INCLUDE[ssSDS](../includes/sssds-md.md)] para optimizar el rendimiento de escenarios de datos transitorios, carga de datos, ingesta de datos y procesamiento de transacciones.

**Se aplica a:** desde [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] hasta [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].

## <a name="persistent-memory-support-for-linux"></a>Compatibilidad con memoria persistente para Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

[!INCLUDE[sqlv15](../includes/sssqlv15-md.md)] agrega compatibilidad para dispositivos de memoria persistente (PMEM) para Linux, con lo que se proporciona el esclarecimiento total de los archivos de registro de transacciones y datos colocados en la [memoria persistente](../linux/sql-server-linux-configure-pmem.md).

**Se aplica a:** desde [!INCLUDE[sqlv15](../includes/sssqlv15-md.md)] hasta [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].
