---
title: Restaurar base de datos maestra
description: Restaure la base de datos maestra en Analytics Platform System (APS).
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 6d122881f5283da86f66494ee2f049756d151551
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400452"
---
# <a name="restore-the-master-database-in-analytics-platform-system-aps"></a>Restauración de la base de datos maestra en Analytics Platform System (APS)
La página **restaurar maestro** del PDW de SQL Server Configuration Manager le permite restaurar la base de datos maestra a partir de una copia de seguridad.  
  
## <a name="before-you-begin"></a>Antes de empezar  
  
> [!IMPORTANT]  
> Para realizar la restauración, PDW de SQL Server debe eliminar la base de datos maestra actual, que contiene información de seguridad del usuario y el catálogo de la base de datos. Se recomienda hacer una copia de seguridad de la base de datos maestra actual antes de realizar la restauración.  
  
## <a name="to-restore-the-master-database"></a>Para restaurar la base de datos maestra  
  
1.  Inicie el Configuration Manager. Para obtener más información, consulte [Inicio del&#41;de &#40;de Configuration Manager de la plataforma de análisis ](launch-the-configuration-manager.md).  
  
2.  En el panel izquierdo del Configuration Manager, haga clic en **restaurar maestro**.  
  
3.  Seleccione la copia de seguridad maestra que se va a restaurar.  
  
4.  Haga clic en **Aplicar**.  
  
5.  Para realizar la restauración, PDW de SQL Server cerrará todos los servicios del dispositivo y desconectará a todos los usuarios. Una vez finalizada la restauración, PDW de SQL Server reiniciará los servicios de la aplicación.  
  
![Restore master PDW del dispositivo de DWConfig](./media/restore-the-master-database/SQL_Server_PDW_DWConfig_ApplPDWRestore.png "SQL_Server_PDW_DWConfig_ApplPDWRestore")  
  
