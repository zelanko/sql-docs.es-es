---
title: Errores del sistema inesperados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 1679bf9e-a2ef-4f90-8907-a002f7341a7d
caps.latest.revision: 7
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 58ccdb66ad026f2a27594f58ea091c2cf0888e15
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37318345"
---
# <a name="unexpected-system-failures"></a>Errores del sistema inesperados
  Esta regla comprueba si el evento SYSTEM 6008 aparece en el registro de eventos del equipo. Este evento indica un cierre del sistema inesperado. El sistema podría ser inestable y no proporcionar la estabilidad e integridad que se exigen para hospedar una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="best-practices-recommendations"></a>Prácticas recomendadas  
 Trate inmediatamente la causa del reinicio inesperado del servidor o mueva la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a otro equipo.  
  
  
