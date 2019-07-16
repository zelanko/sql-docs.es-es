---
title: Restaurar la base de datos master - Analytics Platform System | Microsoft Docs
description: Restaure la base de datos maestra en Analytics Platform System.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 7c9931ab6fb0946de83c3113a36de723a7a05cd0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960138"
---
# <a name="restore-the-master-database-in-analytics-platform-system"></a>Restaurar la base de datos maestra en Analytics Platform System
El **Restore Master** página de SQL Server PDW Configuration Manager le permite restaurar la base de datos maestra desde una copia de seguridad.  
  
## <a name="before-you-begin"></a>Antes de empezar  
  
> [!IMPORTANT]  
> Para llevar a cabo la restauración, SQL Server PDW debe eliminar la base de datos principal actual, que contiene información de seguridad de usuario y el catálogo de base de datos. Se recomienda realizar una copia de seguridad de la base de datos maestra actual antes de realizar la restauración.  
  
## <a name="to-restore-the-master-database"></a>Para restaurar la base de datos maestra  
  
1.  Inicie el Administrador de configuración. Para obtener más información, consulte [iniciar el Administrador de configuración &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md).  
  
2.  En el panel izquierdo del Administrador de configuración, haga clic en **Restore Master**.  
  
3.  Seleccione Restaurar la copia de seguridad principal.  
  
4.  Haga clic en **Aplicar**.  
  
5.  Para llevar a cabo la restauración, PDW de SQL Server se cierra correctamente todos los servicios de dispositivo y desconectar todos los usuarios. Una vez finalizada la restauración, SQL Server PDW reiniciará los servicios del dispositivo.  
  
![DWConfig dispositivo Restore master PDW](./media/restore-the-master-database/SQL_Server_PDW_DWConfig_ApplPDWRestore.png "SQL_Server_PDW_DWConfig_ApplPDWRestore")  
  
