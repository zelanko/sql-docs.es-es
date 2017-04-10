---
title: "Almacenamiento de la administraci&#243;n basada en directivas | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "administración basada en directivas, almacenamiento"
ms.assetid: d0cbf214-fc2e-4917-8d31-1d71c9ffa61d
caps.latest.revision: 11
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 11
---
# Almacenamiento de la administraci&#243;n basada en directivas
  Las directivas se almacenan en la base de datos msdb. Después de cambiar una directiva o condición, se debería hacer una copia de seguridad de la base de datos msdb. Para obtener más información, vea [Realizar copias de seguridad y restaurar bases de datos del sistema &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md).  
  
## Almacenar directivas  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] incluye directivas que se pueden utilizar para supervisar una sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Estas directivas no están instaladas en [!INCLUDE[ssDE](../../includes/ssde-md.md)] de forma predeterminada, pero se pueden importar desde la ubicación de instalación predeterminada C:\Archivos de programa\Microsoft SQL Server\130\Tools\Policies\DatabaseEngine\1033.  
  
 Puede crear directamente las directivas usando el menú **Archivo/Nuevo** y guardándolas después en un archivo. Esto le permite crear directivas cuando no esté conectado a una instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
 El historial de las directivas evaluadas en la instancia actual de [!INCLUDE[ssDE](../../includes/ssde-md.md)] se mantiene en las tablas del sistema de msdb. El historial de las directivas aplicadas a otras instancias de [!INCLUDE[ssDE](../../includes/ssde-md.md)] o a [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no se conserva.  
  
  