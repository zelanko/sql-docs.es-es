---
title: Validar una instalación de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- validating installations [SQL Server]
ms.assetid: 1689af50-d2b8-4aa6-8f27-cc7127157fc8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 34e4c29cb28f76c930f1f04152528ca1a8a89dfc
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62775238"
---
# <a name="validate-a-sql-server-installation"></a>Validar una instalación de SQL Server
  El informe de detección de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se puede utilizar para comprobar la versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y las características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instaladas en el equipo. El **instalado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] informe de detección de características** muestra un informe de todos los [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], y [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] productos y características que se instalan en el servidor local. El informe de detección de características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está disponible en la página **Herramientas** del Centro de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Para ejecutar el informe de detección de características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :**  
  
 Inicie el centro de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; para ello, en el menú **Inicio**, seleccione **Todos los programas**, **[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \<nombre de la versión>**, **Herramientas de configuración** y haga clic en **Centro de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**. Para ejecutar el informe de detección de características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], haga clic en **Herramientas** en el área de navegación izquierda del **Centro de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** y haga clic en **Informe de detección de características instaladas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] informe de detección se guarda en % ProgramFiles %\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\120\Setup Bootstrap\Log\\< última sesión de instalación\>.  
  
 También puede generar el informe de detección a través de la línea de comandos. Ejecute "Setup.exe/Action = RunDiscovery" desde un símbolo del sistema, si agrega "/ q" a la línea de comandos anterior no se mostrará ninguna interfaz de usuario, pero el informe se creará igualmente en % ProgramFiles %\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\120\Setup Bootstrap\Log\\< última sesión de instalación\>.  
  
## <a name="see-also"></a>Vea también  
 [Ver y leer los archivos de registro de instalación de SQL Server](view-and-read-sql-server-setup-log-files.md)  
  
  
