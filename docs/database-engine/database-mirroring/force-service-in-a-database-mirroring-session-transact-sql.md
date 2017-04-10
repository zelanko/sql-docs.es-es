---
title: "Forzar el servicio en una sesi&#243;n de creaci&#243;n de reflejo de la base de datos (Transact-SQL) | Microsoft Docs"
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
  - "servicio forzado [SQL Server]"
  - "creación de reflejo de la base de datos [SQL Server], forzar servicio"
ms.assetid: 8b6ffe77-35f3-4e2a-a658-8a38a8e1c794
caps.latest.revision: 40
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 40
---
# Forzar el servicio en una sesi&#243;n de creaci&#243;n de reflejo de la base de datos (Transact-SQL)
  En los modos de alto rendimiento y de alta seguridad sin conmutación automática por error, si se produce un error en el servidor principal mientras el servidor reflejado está disponible, el propietario de la base de datos puede hacer que ésta esté disponible forzando la conmutación por error del servicio (con una posible pérdida de datos) para la base de datos reflejada. Esta opción está disponible solamente si se cumplen todas las condiciones siguientes:  
  
-   El servidor principal está inactivo.  
  
-   WITNESS está establecido en OFF o está conectado al servidor reflejado.  
  
> [!CAUTION]  
>  El servicio forzado es estrictamente un método de recuperación de desastres. Si se fuerza el servicio, pueden perderse datos. Por consiguiente, fuerce el servicio solo si es aceptable el riesgo de perder datos para restaurar el servicio en la base de datos inmediatamente. Si forzar el servicio supone una posible pérdida de un gran volumen de datos, se recomienda detener la creación del reflejo y sincronizar manualmente las bases de datos. Para obtener más información acerca de los riesgos que supone forzar el servicio, vea [Database Mirroring Operating Modes](../../database-engine/database-mirroring/database-mirroring-operating-modes.md).  
  
 Al forzar el servicio se suspende la sesión y se inicia un nuevo punto de bifurcación de recuperación. El efecto de forzar el servicio es parecido al de quitar la creación del reflejo y recuperar la base de datos principal anterior. No obstante, forzar el servicio facilita la resincronización de las bases de datos (con posible pérdida de datos) cuando se reanuda la creación del reflejo.  
  
### Para forzar el servicio en una sesión de creación de reflejo de la base de datos  
  
1.  Conéctese al servidor reflejado.  
  
2.  Emita la instrucción siguiente:  
  
     ALTER DATABASE *<database_name>* SET PARTNER FORCE_SERVICE_ALLOW_DATA_LOSS  
  
     Donde *<database_name>* es la base de datos reflejada.  
  
     El servidor reflejado pasa inmediatamente al servidor principal y la creación del reflejo se suspende.  
  
## Vea también  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [Modos de funcionamiento de la creación de reflejo de la base de datos](../../database-engine/database-mirroring/database-mirroring-operating-modes.md)  
  
  