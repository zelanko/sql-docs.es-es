---
title: Errores del sistema inesperados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 1679bf9e-a2ef-4f90-8907-a002f7341a7d
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 951b49c0356ae27cb58041af5186becfd12853bb
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52814938"
---
# <a name="unexpected-system-failures"></a>Errores del sistema inesperados
  Esta regla comprueba si el evento SYSTEM 6008 aparece en el registro de eventos del equipo. Este evento indica un cierre del sistema inesperado. El sistema podría ser inestable y no proporcionar la estabilidad e integridad que se exigen para hospedar una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="best-practices-recommendations"></a>Prácticas recomendadas  
 Trate inmediatamente la causa del reinicio inesperado del servidor o mueva la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a otro equipo.  
  
  
