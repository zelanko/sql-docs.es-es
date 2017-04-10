---
title: "Permisos de invitado en bases de datos de usuario | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Prácticas recomendadas [motor de base de datos]"
ms.assetid: 540f1c6d-df51-497e-958a-3a0f429d2920
caps.latest.revision: 8
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 8
---
# Permisos de invitado en bases de datos de usuario
  Esta regla determina si el usuario invitado tiene permiso de acceso a la base de datos. Esta regla solo se aplica a las bases de datos de usuario.  
  
## Prácticas recomendadas  
 Revoque el permiso del usuario invitado para tener acceso a la base de datos si no se requiere.  
  
 El usuario guest no puede quitarse, pero puede deshabilitarse si revoca su permiso CONNECT; para ello, ejecute REVOKE CONNECT FROM GUEST en cualquier base de datos que no sea master, tempdb ni msdb.  
  
## Para obtener más información  
 [Proteger SQL Server](../../relational-databases/security/securing-sql-server.md)  
  
## Vea también  
 [Supervisar y aplicar las prácticas recomendadas usando la administración basada en directivas](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  