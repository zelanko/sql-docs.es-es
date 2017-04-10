---
title: "Validar una instalaci&#243;n de SQL Server | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "setup-install"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "validar instalaciones [SQL Server]"
ms.assetid: 1689af50-d2b8-4aa6-8f27-cc7127157fc8
caps.latest.revision: 31
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 31
---
# Validar una instalaci&#243;n de SQL Server
  El informe de detección de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se puede utilizar para comprobar la versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y las características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instaladas en el equipo. El **Informe de detección de características instaladas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** muestra un informe de todos los productos y características de [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] que están instalados en el servidor local. El informe de detección de características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está disponible en la página **Herramientas** del Centro de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Para ejecutar el informe de detección de características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:**  
  
 Inicie el centro de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; para ello, en el menú **Inicio**, seleccione **Todos los programas**, **[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \<nombre de la versión>**, **Herramientas de configuración** y haga clic en **Centro de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**. Para ejecutar el informe de detección de características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], haga clic en **Herramientas** en el área de navegación izquierda del **Centro de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** y haga clic en **Informe de detección de características instaladas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**.  
  
 El informe de detección de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se guarda en %ProgramFiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\130\Setup Bootstrap\Log\\<última sesión de instalación\>.  
  
 También puede generar el informe de detección a través de la línea de comandos. Ejecute "Setup.exe /Action=RunDiscovery" desde un símbolo del sistema. Si agrega "/q" a la línea de comandos anterior, no se mostrará ninguna IU, pero el informe se creará igualmente en %ProgramFiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\130\Setup Bootstrap\Log\\<última sesión de instalación\>.  
  
## Vea también  
 [Ver y leer los archivos de registro de instalación de SQL Server](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
  