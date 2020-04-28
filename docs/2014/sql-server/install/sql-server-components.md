---
title: Componentes de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
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
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 514524f063bf78ceb4862612dd8c78ce8cf78fc4
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68811088"
---
# <a name="sql-server-components"></a>Componentes de SQL Server
  Puede ejecutar el Asistente para análisis del Asesor de actualizaciones en un equipo local o remoto [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]que [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]tenga [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]instalado, [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] , o. El primer paso en el análisis previo a la actualización es identificar el equipo y los componentes para el análisis.  
  
## <a name="options"></a>Opciones  
 **Nombre del equipo**  
 Especifica el nombre del equipo que se va a analizar. El asesor de actualizaciones rellena el cuadro **nombre del servidor** con el nombre del equipo local. También puede utilizar "." y "localhost" para conectarse con el equipo local.  
  
 Para analizar un equipo diferente, utilice las instrucciones siguientes:  
  
-   Para examinar instancias no agrupadas, escriba el nombre del equipo.  
  
-   Para examinar las instancias clúster, escriba el nombre de la instancia en clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Para examinar los componentes no agrupados que están instalados en un nodo de un clúster, escriba el nombre de equipo del nodo de clúster de conmutación por error.  
  
    > [!IMPORTANT]  
    >  No incluya el nombre de instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 En lugar de especificar el nombre de equipo, puede especificar la dirección IP.  
  
 Si está examinando [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], debe especificar el nombre del equipo local. El Asesor de actualizaciones solo examina los servidores de informes locales.  
  
 **Detect**  
 El botón **detectar** accede al equipo especificado y detecta los componentes que se deben analizar:  
  
-   Si se está analizando una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un equipo remoto, deberá habilitar los servicios de Registro remoto en dicho equipo.  
  
-   Se detectará [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si se encuentra una instancia de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], or [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] en el Registro del equipo.  
  
-   Se detectará [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] si se encuentra una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en el Registro del equipo.  
  
-   Se detectará [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] si se encuentra [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en el registro del equipo. No obstante, el Asesor de actualizaciones solo examina los servidores de informes locales.  
  
 **Componentes**  
 Seleccione los componentes que desea analizar. Puede hacer clic en el botón **detectar** para seleccionar todos los componentes instalados en el equipo. Aparecerá una marca de verificación junto a aquellos componentes que se han detectado como instalados en el equipo. También puede seleccionar manualmente los componentes a analizar activando o desactivando la casilla que se encuentra al lado de cada componente.  
  
## <a name="see-also"></a>Consulte también  
 [Trabajar con el asesor de actualizaciones](../../../2014/sql-server/install/working-with-upgrade-advisor.md)   
 [Referencia de la interfaz de usuario del Asesor de actualizaciones](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md)  
  
  
