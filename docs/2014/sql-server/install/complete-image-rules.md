---
title: Reglas de completar imagen | Documentos de Microsoft
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 45d7ecbc-9fc0-4365-8051-c2a525374280
caps.latest.revision: 14
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 50575384cf2d10d52eeb78666f6829046f64935a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36103463"
---
# <a name="complete-image-rules"></a>Reglas de completar imagen
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Valida la configuración del equipo antes de que finalice la operación de instalación. Durante la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , el Comprobador de configuración del sistema (SCC) examina el equipo en el que se instalará [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . El SCC comprueba las condiciones que impiden una operación de instalación correcta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Antes de que el programa de instalación inicie el Asistente para la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , el SCC recupera el estado de cada elemento. A continuación, compara el resultado con las condiciones necesarias y proporciona instrucciones para evitar problemas de bloqueo.  
  
 La comprobación de la configuración del sistema genera un informe que contiene una descripción breve de cada regla ejecutada y el estado de ejecución. El informe de comprobación de configuración de sistema se encuentra en % programfiles %\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\120\Setup Bootstrap\Log\\< aaaammdd_hhmm >\\.  
  
 Antes de ejecutar la operación de instalación, revise los temas siguientes:  
  
1.  [Requisitos de hardware y Software para instalar SQL Server 2014](hardware-and-software-requirements-for-installing-sql-server.md)  
  
2.  [Características compatibles con las ediciones de SQL Server 2014](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)  
  
3.  [Consideraciones de seguridad para una instalación de SQL Server](../../../2014/sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
4.  [Versiones en idioma local en SQL Server](../../../2014/sql-server/install/local-language-versions-in-sql-server.md)  
  
 Otras referencias:  
  
1.  [Actualizaciones de ediciones y versiones admitidas](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)  
  
2.  [Antes de instalar los clústeres de conmutación por error](../failover-clusters/install/before-installing-failover-clustering.md)  
  
  