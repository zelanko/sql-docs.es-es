---
title: Restaurar la base de datos maestra (Analytics Platform System)
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7870021a-0d89-422e-b8ea-1cc95b45c139
caps.latest.revision: "11"
ms.openlocfilehash: b82ef65734b6953c085436d5322e7bf42ef979b4
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="restore-the-master-database"></a>Restaurar la base de datos maestra
El **Restore Master** página de SQL Server PDW Configuration Manager le permite restaurar la base de datos maestra desde una copia de seguridad.  
  
## <a name="before-you-begin"></a>Antes de comenzar  
  
> [!IMPORTANT]  
> Para llevar a cabo la restauración, SQL Server PDW debe eliminar la base de datos principal actual, que contiene información de seguridad de usuario y el catálogo de base de datos. Se recomienda realizar una copia de seguridad de la base de datos maestra actual antes de realizar la restauración.  
  
## <a name="to-restore-the-master-database"></a>Para restaurar la base de datos maestra  
  
1.  Inicie el Administrador de configuración. Para obtener más información, vea [iniciar el Administrador de configuración &#40; Sistema de la plataforma de análisis &#41; ](launch-the-configuration-manager.md).  
  
2.  En el panel izquierdo del Administrador de configuración, haga clic en **Restore Master**.  
  
3.  Seleccione la copia de seguridad principal para restaurar.  
  
4.  Haga clic en **Aplicar**.  
  
5.  Para llevar a cabo la restauración, SQL Server PDW se apagará todos los servicios del dispositivo y desconectar todos los usuarios. Una vez finalizada la restauración, SQL Server PDW reiniciará los servicios del dispositivo.  
  
![DWConfig dispositivo Restore master PDW](./media/restore-the-master-database/SQL_Server_PDW_DWConfig_ApplPDWRestore.png "SQL_Server_PDW_DWConfig_ApplPDWRestore")  
  
