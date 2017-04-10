---
title: "Errores del sistema inesperados | Microsoft Docs"
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
  - "Prácticas recomendadas [motor de base de datos]"
ms.assetid: 1679bf9e-a2ef-4f90-8907-a002f7341a7d
caps.latest.revision: 8
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 8
---
# Errores del sistema inesperados
  Esta regla comprueba si el evento SYSTEM 6008 aparece en el registro de eventos del equipo. Este evento indica un cierre del sistema inesperado. El sistema podría ser inestable y no proporcionar la estabilidad e integridad que se exigen para hospedar una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## Prácticas recomendadas  
 Trate inmediatamente la causa del reinicio inesperado del servidor o mueva la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a otro equipo.  
  
  