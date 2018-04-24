---
title: 'Restaurar base de datos maestra: Analytics Platform System | Documentos de Microsoft'
description: Restaure la base de datos maestra en el sistema de la plataforma de análisis.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 184184f332225e76e152c2d909cfff788b4fea91
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/19/2018
---
# <a name="restore-the-master-database-in-analytics-platform-system"></a>Restaurar la base de datos maestra en el sistema de la plataforma de análisis
El **Restore Master** página de SQL Server PDW Configuration Manager le permite restaurar la base de datos maestra desde una copia de seguridad.  
  
## <a name="before-you-begin"></a>Antes de comenzar  
  
> [!IMPORTANT]  
> Para llevar a cabo la restauración, SQL Server PDW debe eliminar la base de datos principal actual, que contiene información de seguridad de usuario y el catálogo de base de datos. Se recomienda realizar una copia de seguridad de la base de datos maestra actual antes de realizar la restauración.  
  
## <a name="to-restore-the-master-database"></a>Para restaurar la base de datos maestra  
  
1.  Inicie el Administrador de configuración. Para obtener más información, consulte [iniciar el Administrador de configuración &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md).  
  
2.  En el panel izquierdo del Administrador de configuración, haga clic en **Restore Master**.  
  
3.  Seleccione la copia de seguridad principal para restaurar.  
  
4.  Haga clic en **Aplicar**.  
  
5.  Para llevar a cabo la restauración, SQL Server PDW se apagará todos los servicios del dispositivo y desconectar todos los usuarios. Una vez finalizada la restauración, SQL Server PDW reiniciará los servicios del dispositivo.  
  
![DWConfig dispositivo Restore master PDW](./media/restore-the-master-database/SQL_Server_PDW_DWConfig_ApplPDWRestore.png "SQL_Server_PDW_DWConfig_ApplPDWRestore")  
  
