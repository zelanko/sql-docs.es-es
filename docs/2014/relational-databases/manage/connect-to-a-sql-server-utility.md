---
title: Conexión a una utilidad de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: b9b90b8d-241f-4b74-ac14-de7b10ea1821
caps.latest.revision: 6
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 9ffe9178af91046fa8a1e0b23928a235e9946b2e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37199195"
---
# <a name="connect-to-a-sql-server-utility"></a>Conectarse a una utilidad de SQL Server
  Antes de poder conectarse a una utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , debe crear un punto de control de la utilidad (UCP). Para obtener más información, vea [Características y tareas de la utilidad de SQL Server](sql-server-utility-features-and-tasks.md).  
  
 Para ver y administrar el mantenimiento de los recursos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , use [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) para conectar a una utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Para conectarse a una utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a través de SSMS:  
  
1.  Inicie SSMS.  
  
2.  En SSMS, conéctese a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
3.  Haga clic en **Ver** y, a continuación, en **Explorador de la utilidad**.  
  
4.  En el panel de navegación del Explorador de la utilidad, haga clic en ![](../../database-engine/media/connect-to-utility.gif "Connect_to_Utility")**Conectar con la utilidad**.  
  
5.  En el cuadro de diálogo **Conectar con el servidor** , especifique el nombre de instancia del UCP y, a continuación, haga clic en **Conectar**.  
  
6.  Vea el panel de navegación del explorador de la utilidad para obtener una vista de árbol de los recursos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el UCP.  
  
 Cuando cree un UCP nuevo, también se conectará a la utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obtener más información, vea [Crear un punto de control de la Utilidad de SQL Server &#40;Utilidad de SQL Server&#41;](create-a-sql-server-utility-control-point-sql-server-utility.md).  
  
## <a name="see-also"></a>Vea también  
 [Características y tareas de la utilidad de SQL Server](sql-server-utility-features-and-tasks.md)   
 [Ver los resultados de la directiva de mantenimiento de recursos &#40;Utilidad de SQL Server&#41;](view-resource-health-policy-results-sql-server-utility.md)  
  
  
