---
title: Iniciar el Monitor de replicación | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Replication Monitor, starting
ms.assetid: e037bd27-cc87-4ee9-9e5f-83f6d717cfa4
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: cff23206923825d0e86e47ad6921c19f45e68b35
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85068628"
---
# <a name="start-the-replication-monitor"></a>Iniciar el Monitor de replicación
  El Monitor de replicación se puede iniciar desde [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] en cualquier instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], o desde el símbolo del sistema. Tras iniciar el Monitor de replicación, agregue uno o más publicadores para supervisión. Para obtener más información, vea [Agregar y quitar publicadores del Monitor de replicación](add-and-remove-publishers-from-replication-monitor.md).  
  
### <a name="to-start-replication-monitor-from-sql-server-management-studio"></a>Para iniciar el Monitor de replicación desde SQL Server Management Studio  
  
1.  Conéctese a una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]y expanda el nodo de servidor.  
  
2.  Haga clic con el botón secundario en la carpeta **Replicación** o en cualquiera de sus subcarpetas y, a continuación, haga clic en **Iniciar Monitor de replicación**.  
  
### <a name="to-start-replication-monitor-from-the-command-prompt"></a>Para iniciar el Monitor de replicación desde el símbolo del sistema  
  
1.  Desde el símbolo del sistema, navegue al directorio de instalación de herramientas. La ruta de acceso predeterminada es [!INCLUDE[ssInstallPath](../../../includes/ssinstallpath-md.md)]Tools\Binn\.  
  
2.  Ejecute sqlmonitor.exe.  
  
## <a name="see-also"></a>Consulte también  
 [Supervisar la replicación](../monitoring-replication.md)  
  
  
