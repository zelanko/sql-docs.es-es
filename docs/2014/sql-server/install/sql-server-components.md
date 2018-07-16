---
title: Componentes de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Upgrade Advisor, components
- listing components to analyze
- Upgrade Advisor [SQL Server], components
- component analysis [Upgrade Advisor]
- finding components to analyze
- locating components to analyze
- detecting components to analyze
- server names [Upgrade Advisor]
- analyzing system [Upgrade Advisor], component list
- identifying components to analyze
ms.assetid: 539b9525-ce3f-4950-9146-5527a5a297ee
caps.latest.revision: 41
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 99998b5b9e24de92f826a73941bf6b86e5ad4318
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37177128"
---
# <a name="sql-server-components"></a>Componentes de SQL Server
  Puede ejecutar el Asistente para actualización de análisis de Advisor en un equipo local o remoto que tenga [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] instalado. El primer paso en el análisis previo a la actualización es identificar el equipo y los componentes para el análisis.  
  
## <a name="options"></a>Opciones  
 **Nombre del equipo**  
 Especifica el nombre del equipo que se va a analizar. El Asesor de actualizaciones rellena el **nombre del servidor** cuadro con el nombre del equipo local. También puede utilizar "." y "localhost" para conectarse con el equipo local.  
  
 Para analizar un equipo diferente, utilice las instrucciones siguientes:  
  
-   Para examinar instancias que no estén en clúster, escriba el nombre del equipo.  
  
-   Para examinar las instancias clúster, escriba el nombre de la instancia en clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Para examinar componentes no organizados en clúster que están instalados en el nodo de un clúster, escriba el nombre del equipo del nodo de clúster de conmutación por error.  
  
    > [!IMPORTANT]  
    >  No incluya el nombre de instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 En lugar de especificar el nombre de equipo, puede especificar la dirección IP.  
  
 Si está examinando [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], debe especificar el nombre del equipo local. El Asesor de actualizaciones solo examina los servidores de informes locales.  
  
 **Detectar**  
 El **detectar** botón obtiene acceso al equipo especificado y detecta los componentes para analizar:  
  
-   Si se está analizando una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un equipo remoto, deberá habilitar los servicios de Registro remoto en dicho equipo.  
  
-   Se detectará [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si se encuentra una instancia de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], or [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] en el Registro del equipo.  
  
-   Se detectará [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] si se encuentra una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en el Registro del equipo.  
  
-   Se detectará [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] si se encuentra [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en el registro del equipo. No obstante, el Asesor de actualizaciones solo examina los servidores de informes locales.  
  
 **Components**  
 Seleccione los componentes que desea analizar. Puede hacer clic en el **detectar** para seleccionar todos los componentes instalados en el equipo. Aparecerá una marca de verificación junto a aquellos componentes que se han detectado como instalados en el equipo. También puede seleccionar manualmente los componentes a analizar activando o desactivando la casilla que se encuentra al lado de cada componente.  
  
## <a name="see-also"></a>Vea también  
 [Trabajar con el Asesor de actualizaciones](../../../2014/sql-server/install/working-with-upgrade-advisor.md)   
 [Actualización del Asistente para la referencia de la interfaz de usuario](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md)  
  
  
