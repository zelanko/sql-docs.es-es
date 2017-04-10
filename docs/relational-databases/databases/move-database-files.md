---
title: "Mover archivos de base de datos | Microsoft Docs"
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
  - "recuperación ante desastres [SQL Server], movimiento de los archivos de base de datos"
  - "archivos [SQL Server], mover"
  - "archivos de datos [SQL Server], movimiento"
  - "movimiento de archivos [SQL Server]"
  - "mover catálogos de texto completo"
  - "mover bases de datos"
  - "catálogos de texto completo [SQL Server], mover"
  - "mover archivos de base de datos"
  - "mantenimiento de disco programado [SQL Server]"
  - "mover archivos"
  - "reubicar archivos de base de datos"
  - "reubicaciones de bases de datos planeadas [SQL Server]"
  - "bases de datos [SQL Server], movimiento"
ms.assetid: 89f01b10-5fae-4ed8-b0fb-a4b9f540fd28
caps.latest.revision: 34
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 34
---
# Mover archivos de base de datos
  En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede mover bases de datos del sistema y del usuario especificando la nueva ubicación de los archivos en la cláusula FILENAME de la instrucción [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) . De este modo se pueden desplazar archivos de datos, registro y catálogo de texto completo. Esto puede resultar útil en las situaciones siguientes:    
  
-   Recuperación de un error. Por ejemplo, la base de datos se encuentra en modo sospechoso o se ha cerrado a causa de un error de hardware.  
  
-   Reubicación planeada.  
  
-   Reubicación para el mantenimiento planeado del disco.  
  
## En esta sección  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Mover bases de datos de usuario](../../relational-databases/databases/move-user-databases.md)|Describe los procedimientos para mover archivos de base de datos de usuario y archivos del catálogo de texto completo a una nueva ubicación.|  
|[Mover bases de datos del sistema](../../relational-databases/databases/move-system-databases.md)|Describe el procedimiento para mover archivos de base de datos del sistema a una nueva ubicación.|  
  
## Vea también  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [CREATE DATABASE &#40;Transact-SQL de SQL Server&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [Adjuntar y separar bases de datos &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)  
  
  