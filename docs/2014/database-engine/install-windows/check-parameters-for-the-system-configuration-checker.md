---
title: Comprobar los parámetros del Comprobador de configuración del sistema | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- installing SQL Server, system configuration checks
- failed system configuration checks [SQL Server]
- verifying configuration before installation
- SCC [SQL Server]
- system configuration checker
- scanning computer before installation [SQL Server]
- checking configuration before installation
- status information [SQL Server], system configuration checker
- parameters [SQL Server], system configuration checker
- configuration checkers [SQL Server]
- Setup [SQL Server], system configuration checker
ms.assetid: 8e712c15-6bfa-4d71-b303-9526101e5594
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2a1d08730c8fd4ec5a750c0cf2c70e0498be602e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62779448"
---
# <a name="check-parameters-for-the-system-configuration-checker"></a>Comprobar los parámetros del Comprobador de configuración del sistema
  Durante la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , el Comprobador de configuración del sistema (SCC) examina el equipo en el que se instalará [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . El SCC comprueba las condicione que impiden una instalación correcta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Antes de que el programa de instalación inicie el Asistente para la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , el SCC recupera el estado de cada elemento. A continuación, compara el resultado con las condiciones necesarias y proporciona instrucciones para evitar problemas de bloqueo.  
  
 El comprobador de la configuración del sistema genera un informe que contiene una descripción breve de cada regla ejecutada y el estado de ejecución. El informe de comprobación de la configuración del sistema se encuentra\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]en%\\ ProgramFiles% \120\Setup \\Bootstrap\Log<YYYYMMDD_HHMM>.  
  
## <a name="see-also"></a>Consulte también  
 [Requisitos de hardware y software para la instalación de SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)   
 [Consideraciones de seguridad para una instalación de SQL Server](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)   
 [Actualizaciones de ediciones y versiones admitidas](supported-version-and-edition-upgrades.md)  
  
  
