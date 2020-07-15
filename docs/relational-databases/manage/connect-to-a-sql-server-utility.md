---
title: Conexión a una utilidad de SQL Server | Microsoft Docs
description: Obtenga información sobre cómo conectarse a una utilidad de SQL Server para poder administrar el mantenimiento de recursos de SQL Server. Puede conectarse mediante SQL Server Management Studio (SSMS).
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: b9b90b8d-241f-4b74-ac14-de7b10ea1821
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 1d2ea96cc97f84a342c12ea841a263c8bf06adc0
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85776017"
---
# <a name="connect-to-a-sql-server-utility"></a>Conectarse a una utilidad de SQL Server
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Antes de poder conectarse a una utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , debe crear un punto de control de la utilidad (UCP). Para obtener más información, vea [Características y tareas de la utilidad de SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md).  
  
 Para ver y administrar el mantenimiento de los recursos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , use [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) para conectar a una utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Para conectarse a una utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a través de SSMS:  
  
1.  Inicie SSMS.  
  
2.  En SSMS, conéctese a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
3.  Haga clic en **Ver** y, a continuación, en **Explorador de la utilidad**.  
  
4.  En el panel de navegación del Explorador de la utilidad, haga clic en ![](../../relational-databases/manage/media/connect-to-utility.gif "Connect_to_Utility")**Conectar con la utilidad**.  
  
5.  En el cuadro de diálogo **Conectar con el servidor** , especifique el nombre de instancia del UCP y, a continuación, haga clic en **Conectar**.  
  
6.  Vea el panel de navegación del explorador de la utilidad para obtener una vista de árbol de los recursos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el UCP.  
  
 Cuando cree un UCP nuevo, también se conectará a la utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obtener más información, vea [Crear un punto de control de la Utilidad de SQL Server &#40;Utilidad de SQL Server&#41;](../../relational-databases/manage/create-a-sql-server-utility-control-point-sql-server-utility.md).  
  
## <a name="see-also"></a>Consulte también  
 [Características y tareas de la utilidad de SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [Ver los resultados de la directiva de mantenimiento de recursos &#40;Utilidad de SQL Server&#41;](../../relational-databases/manage/view-resource-health-policy-results-sql-server-utility.md)  
  
  
