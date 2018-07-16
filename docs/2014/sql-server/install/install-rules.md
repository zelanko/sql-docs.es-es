---
title: Reglas de instalación | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- SCC
- System Configuration Check, Setup
helpviewer_keywords:
- System Configuration Check page [SQL Server Installation Wizard]
- SQL Server Installation Wizard, System Configuration Check page
- SCC [SQL Server]
ms.assetid: 168c0445-5651-42fc-91f4-d9f27d9e2281
caps.latest.revision: 49
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: df13e2ac5e6caf247f633e7f59ac397b2c5d22c7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37251497"
---
# <a name="install-rules"></a>Reglas de instalación
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Programa de instalación valida la configuración del equipo antes de que finalice la operación de instalación. Durante la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , el Comprobador de configuración del sistema (SCC) examina el equipo en el que se instalará [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . El SCC comprueba las condiciones que impiden una operación de instalación correcta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Antes de que el programa de instalación inicie el Asistente para la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , el SCC recupera el estado de cada elemento. A continuación, compara el resultado con las condiciones necesarias y proporciona instrucciones para evitar problemas de bloqueo.  
  
 La comprobación de la configuración del sistema genera un informe que contiene una descripción breve de cada regla ejecutada y el estado de ejecución. El informe de comprobación de configuración del sistema se encuentra en % programfiles %\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\120\Setup Bootstrap\Log\\< aaaammdd_hhmm >\\.  
  
 Antes de ejecutar la operación de instalación, revise los temas siguientes:  
  
1.  [Requisitos de hardware y software para instalar SQL Server 2014](hardware-and-software-requirements-for-installing-sql-server.md)  
  
2.  [Características compatibles con las ediciones de SQL Server 2014](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)  
  
3.  [Consideraciones de seguridad para una instalación de SQL Server](../../../2014/sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
4.  [Versiones en idioma local en SQL Server](../../../2014/sql-server/install/local-language-versions-in-sql-server.md)  
  
 Otras referencias:  
  
1.  [Actualizaciones de ediciones y versiones admitidas](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)  
  
2.  [Antes de instalar los clústeres de conmutación por error](../failover-clusters/install/before-installing-failover-clustering.md)  
  
## <a name="additional-rule-topics"></a>Temas adicionales sobre reglas  
 Vea los siguientes temas sobre reglas de instalación específicas para cada escenario:  
  
-   [Reglas de instalación](../../../2014/sql-server/install/installation-rules.md)  
  
-   [Las reglas de características &#40;actualizar&#41;](../../../2014/sql-server/install/feature-rules-upgrade.md)  
  
-   [Reglas de actualización de edición](../../../2014/sql-server/install/edition-upgrade-rules.md)  
  
-   [Página de desinstalación](../../../2014/sql-server/install/uninstallation-rules.md)  
  
-   [Reglas para preparar la imagen](../../../2014/sql-server/install/prepare-image-rules.md)  
  
-   [Reglas de completar imagen](../../../2014/sql-server/install/complete-image-rules.md)  
  
  
