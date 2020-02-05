---
title: Ejecutar Monitor de sistema | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- System Monitor [SQL Server], running
- Windows System Monitor [SQL Server], running
- remote procedure calls [SQL Server]
- starting Windows NT System Monitor
- RPC
ms.assetid: 05297984-bc8d-43df-829c-032387f7ea61
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 015570319e537199f13bd1d3783c508e22ab49ed
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "67987372"
---
# <a name="run-system-monitor"></a>Ejecutar Monitor de sistema
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  El Monitor del sistema utiliza llamadas a procedimiento remoto (RPC) para recopilar información de Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Cualquier usuario que disponga de permisos de Microsoft Windows para ejecutar el Monitor del sistema puede utilizarlo para supervisar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Cuando utilice el Monitor del sistema o el Monitor de rendimiento, no podrá conectarse a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se ejecute en Windows 98.  
  
 Al igual que con todas las herramientas para la supervisión del rendimiento, es normal que se produzca una disminución del rendimiento al supervisar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]con el Monitor del sistema. La sobrecarga real en una instancia específica dependerá de la plataforma de hardware, el número de contadores y el intervalo de actualización seleccionado. No obstante, la integración del Monitor del sistema con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está diseñada para que la disminución del rendimiento sea la mínima.  
  
> [!NOTE]  
>  Si ha seleccionado los contadores de rendimiento de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para la supervisión en el complemento Monitor del sistema, los contadores estarán presentes aunque no se ejecute [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Para obtener información sobre cómo iniciar el Monitor del sistema, vea [Iniciar el Monitor de sistema &#40;Windows&#41;](../../relational-databases/performance/start-system-monitor-windows.md).  
  
  
