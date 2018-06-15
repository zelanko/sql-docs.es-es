---
title: Movimiento de archivos de base de datos | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: databases
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- disaster recovery [SQL Server], moving database files
- files [SQL Server], moving
- data files [SQL Server], moving
- file moving [SQL Server]
- moving full-text catalogs
- moving databases
- full-text catalogs [SQL Server], moving
- moving database files
- scheduled disk maintenance [SQL Server]
- moving files
- relocating database files
- planned database relocations [SQL Server]
- databases [SQL Server], moving
ms.assetid: 89f01b10-5fae-4ed8-b0fb-a4b9f540fd28
caps.latest.revision: 34
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a92b002e6590903ae90f584e7b87d565df7272fe
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32925020"
---
# <a name="move-database-files"></a>Mover archivos de base de datos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede mover bases de datos del sistema y del usuario especificando la nueva ubicación de los archivos en la cláusula FILENAME de la instrucción [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) . De este modo se pueden desplazar archivos de datos, registro y catálogo de texto completo. Esto puede resultar útil en las situaciones siguientes:  
  
-   Recuperación de un error. Por ejemplo, la base de datos se encuentra en modo sospechoso o se ha cerrado a causa de un error de hardware.  
  
-   Reubicación planeada.  
  
-   Reubicación para el mantenimiento planeado del disco.  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Description|  
|-----------|-----------------|  
|[Mover bases de datos de usuario](../../relational-databases/databases/move-user-databases.md)|Describe los procedimientos para mover archivos de base de datos de usuario y archivos del catálogo de texto completo a una nueva ubicación.|  
|[Mover bases de datos del sistema](../../relational-databases/databases/move-system-databases.md)|Describe el procedimiento para mover archivos de base de datos del sistema a una nueva ubicación.|  
  
## <a name="see-also"></a>Ver también  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [CREATE DATABASE &#40;Transact-SQL de SQL Server&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [Adjuntar y separar bases de datos &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)  
  
  
