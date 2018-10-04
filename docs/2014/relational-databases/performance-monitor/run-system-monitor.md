---
title: Ejecutar Monitor de sistema | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- System Monitor [SQL Server], running
- Windows System Monitor [SQL Server], running
- remote procedure calls [SQL Server]
- starting Windows NT System Monitor
- RPC
ms.assetid: 05297984-bc8d-43df-829c-032387f7ea61
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: de0da660823bafbb93943059f8e986008dabe70c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48137100"
---
# <a name="run-system-monitor"></a>Ejecutar Monitor de sistema
  El Monitor del sistema utiliza llamadas a procedimiento remoto (RPC) para recopilar información de Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Cualquier usuario que disponga de permisos de Microsoft Windows para ejecutar el Monitor del sistema puede utilizarlo para supervisar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Cuando utilice el Monitor del sistema o el Monitor de rendimiento, no podrá conectarse a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se ejecute en Windows 98.  
  
 Al igual que con todas las herramientas para la supervisión del rendimiento, es normal que se produzca una disminución del rendimiento al supervisar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]con el Monitor del sistema. La sobrecarga real en una instancia específica dependerá de la plataforma de hardware, el número de contadores y el intervalo de actualización seleccionado. No obstante, la integración del Monitor del sistema con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está diseñada para que la disminución del rendimiento sea la mínima.  
  
> [!NOTE]  
>  Si ha seleccionado los contadores de rendimiento de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para la supervisión en el complemento Monitor del sistema, los contadores estarán presentes aunque no se ejecute [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para obtener información sobre cómo iniciar el Monitor del sistema, vea [Iniciar el Monitor de sistema &#40;Windows&#41;](../performance/start-system-monitor-windows.md).  
  
  
