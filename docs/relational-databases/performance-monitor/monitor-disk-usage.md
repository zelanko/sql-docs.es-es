---
title: "Supervisar el uso del disco | Microsoft Docs"
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
  - "supervisión de base de datos [SQL Server], uso del disco"
  - "discos [SQL Server]"
  - "supervisar rendimiento [SQL Server], uso de la CPU"
  - "rendimiento de servidor [SQL Server], uso de la CPU"
  - "supervisar [SQL Server], actividad de disco"
  - "paginación excesiva [SQL Server]"
  - "optimizar bases de datos [SQL Server] , uso del disco"
  - "E/S [SQL Server], supervisar"
  - "discos [SQL Server], supervisar actividad"
  - "aislar la actividad del disco [SQL Server]"
  - "rendimiento de base de datos [SQL Server], uso de disco"
  - "supervisar el rendimiento del servidor [SQL Server], uso del disco"
ms.assetid: 1525449c-ea7d-4222-b294-1ba1fe99c9ac
caps.latest.revision: 23
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 23
---
# Supervisar el uso del disco
  Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa llamadas de entrada/salida (E/S) del sistema operativo Microsoft Windows para realizar las operaciones de lectura y escritura en el disco. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] administra el momento y el modo en que se realizan las operaciones de E/S de disco, pero el sistema operativo Windows realiza las operaciones de E/S subyacentes. El subsistema de E/S incluye el bus del sistema, tarjetas controladoras de disco, discos, unidades de cinta, la unidad de CD-ROM y muchos otros dispositivos de E/S. La E/S del disco es una causa frecuente de los atascos en un sistema.  
  
 La supervisión de la actividad del disco implica dos aspectos básicos:  
  
-   Supervisar la E/S del disco y detectar la paginación excesiva  
  
-   Aislar la actividad del disco que crea [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
 Para obtener más información, vea [Supervisar el uso del disco](http://social.technet.microsoft.com/wiki/contents/articles/monitoring-disk-usage.aspx).  
  
  