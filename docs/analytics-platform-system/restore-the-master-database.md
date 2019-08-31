---
title: 'Restaurar base de datos maestra: Analytics Platform System (APS) | Microsoft Docs'
description: Restaure la base de datos maestra en Analytics Platform System (APS).
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 624e1199fb953945ae6476a1f935dded48508bab
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/30/2019
ms.locfileid: "70176137"
---
# <a name="restore-the-master-database-in-analytics-platform-system-aps"></a>Restauración de la base de datos maestra en Analytics Platform System (APS)
La página **restaurar maestro** del PDW de SQL Server Configuration Manager le permite restaurar la base de datos maestra a partir de una copia de seguridad.  
  
## <a name="before-you-begin"></a>Antes de empezar  
  
> [!IMPORTANT]  
> Para realizar la restauración, PDW de SQL Server debe eliminar la base de datos maestra actual, que contiene información de seguridad del usuario y el catálogo de la base de datos. Se recomienda hacer una copia de seguridad de la base de datos maestra actual antes de realizar la restauración.  
  
## <a name="to-restore-the-master-database"></a>Para restaurar la base de datos maestra  
  
1.  Inicie el Configuration Manager. Para obtener más información, consulte [Inicio de &#40;Configuration Manager Analytics Platform System&#41;](launch-the-configuration-manager.md).  
  
2.  En el panel izquierdo del Configuration Manager, haga clic en **restaurar maestro**.  
  
3.  Seleccione la copia de seguridad maestra que se va a restaurar.  
  
4.  Haga clic en **Aplicar**.  
  
5.  Para realizar la restauración, PDW de SQL Server cerrará todos los servicios del dispositivo y desconectará a todos los usuarios. Una vez finalizada la restauración, PDW de SQL Server reiniciará los servicios de la aplicación.  
  
![Dispositivo DWCONFIG PDW restore Master](./media/restore-the-master-database/SQL_Server_PDW_DWConfig_ApplPDWRestore.png "SQL_Server_PDW_DWConfig_ApplPDWRestore")  
  
