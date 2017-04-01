---
title: "Bit de confianza | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Prácticas recomendadas [motor de base de datos]"
ms.assetid: 3198188a-2b59-4865-9560-10f760934b8e
caps.latest.revision: 9
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 9
---
# Bit de confianza
  Esta regla determina si el rol dbo para una base de datos está asignado al rol fijo de servidor sysadmin y la base de datos tiene su bit de confianza establecido en ON.  
  
 Si se cumplen estas condiciones, un usuario privilegiado de la base de datos puede elevar los privilegios al rol sysadmin. En este rol, el usuario puede crear y ejecutar ensamblados no seguros que ponen en peligro el sistema.  
  
## Prácticas recomendadas  
 Desactive el bit de confianza o revoque los permisos sysadmin del rol de la base de datos dbo.  
  
## Para obtener más información  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
  
## Vea también  
 [Supervisar y aplicar las prácticas recomendadas usando la administración basada en directivas](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  