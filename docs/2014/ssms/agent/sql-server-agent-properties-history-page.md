---
title: Propiedades de Agente SQL Server (página Historial) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.ag.agent.history.f1
ms.assetid: dc73734c-b3c3-407f-bbd1-8714b4fa47b0
caps.latest.revision: 19
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 46a62984a55b5141f66fb459b42274fe3ca94c1d
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2018
ms.locfileid: "43818191"
---
# <a name="sql-server-agent-properties-history-page"></a>Propiedades de Agente SQL Server (página Historial)
  Utilice esta página para ver y modificar los valores de configuración para administrar el registro del historial de servicios del Agente [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="options"></a>Opciones  
 **Limitar tamaño del registro de historial de trabajos**  
 Establece los límites para la cantidad de información del historial de trabajos que el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conserva en el registro.  
  
 **Tamaño máximo del registro de historial de trabajos (filas)**  
 Establece el número máximo de filas que conserva el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Cuando el registro crece para contener este número de filas, el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] elimina las filas más antiguas del registro a medida que se van incluyendo filas nuevas.  
  
 **Máximo de filas de historial de trabajos por trabajo**  
 Establece el número máximo de filas que el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conserva por trabajo. Cuando el historial para un trabajo determinado crece para contener este número de filas, el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] quita las filas más antiguas del registro a medida que se van incluyendo filas nuevas.  
  
 **Quitar historial del agente**  
 Especifica que el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] quitará las entradas que han permanecido en el registro más tiempo que el especificado. Es una ejecución única para quitar el historial. Si es necesaria la repetición de un trabajo, cree y programe un plan de mantenimiento con un trabajo de limpieza.  
  
 **Anterior a**  
 Establece el tiempo que el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conservará las entradas.  
  
## <a name="see-also"></a>Vea también  
 [Registro de errores del Agente SQL Server](sql-server-agent-error-log.md)  
  
  
