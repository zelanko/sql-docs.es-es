---
title: Almacenamiento de la administración basada en directivas | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, storage
ms.assetid: d0cbf214-fc2e-4917-8d31-1d71c9ffa61d
caps.latest.revision: 11
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: be23dc08c05af648feb1fa20c1a512af6dc811d3
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2018
ms.locfileid: "43807691"
---
# <a name="policy-based-management-storage"></a>Almacenamiento de la administración basada en directivas
  Las directivas se almacenan en la base de datos msdb. Después de cambiar una directiva o condición, se debería hacer una copia de seguridad de la base de datos msdb. Para obtener más información, vea [Realizar copias de seguridad y restaurar bases de datos del sistema &#40;SQL Server&#41;](../backup-restore/back-up-and-restore-of-system-databases-sql-server.md).  
  
## <a name="storing-policies"></a>Almacenar directivas  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] incluye directivas que se pueden utilizar para supervisar una sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. De forma predeterminada, estas directivas no están instaladas en el [!INCLUDE[ssDE](../../includes/ssde-md.md)]; sin embargo, se puede importar desde la ubicación de instalación predeterminada de C:\Program Files (x86) \Microsoft SQL Server\120\Tools\Policies\DatabaseEngine\1033.  
  
 Puede crear directamente las directivas usando el menú **Archivo/Nuevo** y guardándolas después en un archivo. Esto le permite crear directivas cuando no esté conectado a una instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
 El historial de las directivas evaluadas en la instancia actual de [!INCLUDE[ssDE](../../includes/ssde-md.md)] se mantiene en las tablas del sistema de msdb. El historial de las directivas aplicadas a otras instancias de [!INCLUDE[ssDE](../../includes/ssde-md.md)] o a [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no se conserva.  
  
  
