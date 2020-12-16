---
description: Características que ya no se utilizan en la replicación de SQL Server
title: Características obsoletas en la replicación de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 01/22/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- deprecated features [SQL Server replication]
ms.assetid: 46bd3edd-d6de-40a6-a015-21cce8321feb
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: 3a81ec710ed3d0927d7839309de371066ff81445
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97461876"
---
# <a name="deprecated-features-in-sql-server-replication"></a>Características que ya no se utilizan en la replicación de SQL Server
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  Este tema describe las características de replicación desusadas que siguen estando disponibles en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Está previsto quitar estas características en una futura versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Las características en desuso no se deben usar en nuevas aplicaciones.  
  
## <a name="items-deprecated-in-sssql15"></a>Elementos desusados en [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]  
  
|Característica|Descripción|  
|-------------|-----------------|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|Se admite la replicación si cada extremo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está en dos versiones principales de la versión actual de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por tanto, [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] no admite la replicación a o desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)].|  
|[!INCLUDE[ssEW](../../includes/ssew-md.md)]|Se admite la replicación si cada extremo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está en dos versiones principales de la versión actual de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por tanto, [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] no admite la replicación a o desde [!INCLUDE[ssEW](../../includes/ssew-md.md)].|  
  
## <a name="see-also"></a>Consulte también  
 [Compatibilidad con versiones anteriores de replicación](../../relational-databases/replication/replication-backward-compatibility.md)  
  
  
