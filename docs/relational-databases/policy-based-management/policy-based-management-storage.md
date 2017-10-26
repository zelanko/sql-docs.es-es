---
title: "Almacenamiento de la administración basada en directivas | Microsoft Docs"
ms.custom: 
ms.date: 08/09/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Policy-Based Management, storage
ms.assetid: d0cbf214-fc2e-4917-8d31-1d71c9ffa61d
caps.latest.revision: 11
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: e59b30393d9bb917fc48511d7e621c14e9a01c9c
ms.openlocfilehash: fa8ad7ecca05b2fe7b4ef6b955f5b24fadb0e23b
ms.contentlocale: es-es
ms.lasthandoff: 08/10/2017

---
# <a name="policy-based-management-storage"></a>Almacenamiento de la administración basada en directivas
  Las directivas se almacenan en la base de datos msdb. Después de cambiar una directiva o condición, se debería hacer una copia de seguridad de la base de datos msdb. Para obtener más información, vea [Realizar copias de seguridad y restaurar bases de datos del sistema &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md).  
  
## <a name="storing-policies"></a>Almacenar directivas  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] incluye directivas que se pueden utilizar para supervisar una sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Estas directivas no están instaladas en [!INCLUDE[ssDE](../../includes/ssde-md.md)] de forma predeterminada, pero se pueden importar desde la ubicación de instalación predeterminada C:\Archivos de programa (x86)\Microsoft SQL Server\140\Tools\Policies\DatabaseEngine\1033.  
  
 Puede crear directamente las directivas usando el menú **Archivo/Nuevo** y guardándolas después en un archivo. Esto le permite crear directivas cuando no esté conectado a una instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
 El historial de las directivas evaluadas en la instancia actual de [!INCLUDE[ssDE](../../includes/ssde-md.md)] se mantiene en las tablas del sistema de msdb. El historial de las directivas aplicadas a otras instancias de [!INCLUDE[ssDE](../../includes/ssde-md.md)] o a [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no se conserva.  
  
  

