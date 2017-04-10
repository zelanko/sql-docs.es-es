---
title: "Cambiar la seguridad de las transacciones en una sesi&#243;n de creaci&#243;n de reflejo de la base de datos (Transact-SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "seguridad de transacciones [creación reflejo base de datos SQL Server]"
ms.assetid: 8b03bb82-8589-4558-8545-9942fe008391
caps.latest.revision: 38
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 38
---
# Cambiar la seguridad de las transacciones en una sesi&#243;n de creaci&#243;n de reflejo de la base de datos (Transact-SQL)
  La seguridad de las transacciones es el atributo que controla el modo operativo de la sesión. No obstante, el propietario de la base de datos puede cambiar la seguridad de las transacciones en cualquier momento. De forma predeterminada, el nivel de seguridad de las transacciones está establecido en FULL (modo operativo sincrónico).  
  
 Si se desactiva la seguridad de las transacciones, la sesión cambia al modo operativo asincrónico, lo que maximiza el rendimiento. Si la base de datos principal no está disponible, la base de datos reflejada se detiene pero está disponible como base de datos en espera semiactiva (la conmutación por error requiere forzar el servicio, con una posible pérdida de datos).  
  
### Para activar la seguridad de las transacciones  
  
1.  Conéctese al servidor principal.  
  
2.  Escriba la instrucción Transact-SQL siguiente:  
  
    ```  
    ALTER DATABASE <database> SET PARTNER SAFETY FULL  
    ```  
  
     donde *\<nombre_base_de_datos>* es el nombre de la base de datos reflejada.  
  
### Para desactivar la seguridad de las transacciones  
  
1.  Conéctese al servidor principal.  
  
2.  Emita la instrucción siguiente:  
  
    ```  
    ALTER DATABASE <database> SET PARTNER SAFETY OFF  
    ```  
  
     donde *\<nombre_base_de_datos>* es la base de datos reflejada.  
  
## Vea también  
 [Reflejo de la base de datos ALTER DATABASE &#40;Transact-SQL&#41;](../Topic/ALTER%20DATABASE%20Database%20Mirroring%20\(Transact-SQL\).md)   
 [Modos de funcionamiento de la creación de reflejo de la base de datos](../../database-engine/database-mirroring/database-mirroring-operating-modes.md)  
  
  