---
title: Errores del sistema inesperados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 1679bf9e-a2ef-4f90-8907-a002f7341a7d
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 4451b3103281038d383d3e2dda2ab0353ff1b90d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48207215"
---
# <a name="unexpected-system-failures"></a>Errores del sistema inesperados
  Esta regla comprueba si el evento SYSTEM 6008 aparece en el registro de eventos del equipo. Este evento indica un cierre del sistema inesperado. El sistema podría ser inestable y no proporcionar la estabilidad e integridad que se exigen para hospedar una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="best-practices-recommendations"></a>Prácticas recomendadas  
 Trate inmediatamente la causa del reinicio inesperado del servidor o mueva la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a otro equipo.  
  
  
