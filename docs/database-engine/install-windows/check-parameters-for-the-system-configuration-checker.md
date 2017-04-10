---
title: "Comprobar los par&#225;metros del Comprobador de configuraci&#243;n del sistema | Microsoft Docs"
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
  - "instalar SQL Server, comprobaciones de la configuración del sistema"
  - "comprobaciones de la configuración del sistema, errores [SQL Server]"
  - "comprobar configuración antes de la instalación"
  - "SCC [SQL Server]"
  - "comprobador de configuración del sistema"
  - "recorrer equipo antes de la instalación [SQL Server]"
  - "comprobar configuración antes de la instalación"
  - "información de estado [SQL Server], comprobador de configuración del sistema"
  - "parámetros [SQL Server], comprobador de configuración del sistema"
  - "comprobadores de configuración [SQL Server]"
  - "instalar [SQL Server], comprobador de configuración del sistema"
ms.assetid: 8e712c15-6bfa-4d71-b303-9526101e5594
caps.latest.revision: 46
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 46
---
# Comprobar los par&#225;metros del Comprobador de configuraci&#243;n del sistema
  Durante la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el Comprobador de configuración del sistema (SCC) examina el equipo en el que se instalará [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El SCC comprueba las condicione que impiden una instalación correcta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Antes de que el programa de instalación inicie el Asistente para la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , el SCC recupera el estado de cada elemento. A continuación, compara el resultado con las condiciones necesarias y proporciona instrucciones para evitar problemas de bloqueo.  
  
 El comprobador de la configuración del sistema genera un informe que contiene una descripción breve de cada regla ejecutada y el estado de ejecución. El informe de comprobación de la configuración del sistema se encuentra en %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\130\Setup Bootstrap\Log\\<AAAAMMDD_HHMM>\\.  
  
## Vea también  
 [Requisitos de hardware y software para instalar SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server-2016.md)   
 [Consideraciones de seguridad para una instalación de SQL Server](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)   
 [Actualizaciones de ediciones y versiones admitidas](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)  
  
  