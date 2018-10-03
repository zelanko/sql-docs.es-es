---
title: Ejecute el Asesor de actualizaciones (interfaz de usuario) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Upgrade Advisor Report Viewer
- Upgrade Advisor [SQL Server], running
- launching Upgrade Advisor
- Upgrade Advisor Analysis Wizard
- starting Upgrade Advisor
- SQL Server Upgrade Advisor, running
ms.assetid: 7f47c9b3-88d3-43d6-837e-f157b49a55ac
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c402516980f5cf3e1790f8a5fa6d594c93b0e500
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48176115"
---
# <a name="running-upgrade-advisor-user-interface"></a>Ejecutar el Asesor de actualizaciones (interfaz de usuario)
  Puede ejecutar el Asesor de actualizaciones para analizar componentes locales o remotos durante la planeación de la actualización. El Asesor de actualizaciones genera un informe para cada componente y la instancia que se está analizando.  
  
> [!IMPORTANT]  
>  El Asesor de actualizaciones no analiza instancias remotas de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Para analizar una instancia de [!INCLUDE[ssRS](../../includes/ssrs.md)], el Asesor de actualizaciones se debe instalar en el equipo donde esté instalado [!INCLUDE[ssRS](../../includes/ssrs.md)].  
>   
>  Para analizar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Integration Services, debe tener la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] instalado y [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] instalado en el mismo equipo.  
  
## <a name="running-the-upgrade-advisor-analysis-wizard"></a>Ejecute al Asistente para análisis del Asesor  
 La ejecución del Asistente para análisis del Asesor de actualizaciones consta de seis pasos:  
  
1.  Inicie el asistente desde la página de inicio del Asesor de actualizaciones.  
  
2.  Identifique el servidor y los componentes que desea analizar.  
  
3.  Recopile información de autenticación.  
  
4.  Recopile los parámetros adicionales según el tipo de componente.  
  
5.  Analice los componentes seleccionados.  
  
6.  Genere un informe de los problemas de la actualización.  
  
 Para obtener más información sobre el Asistente para actualización de análisis de Advisor, consulte [Cómo: ejecutar el Asistente para actualizar Analysis Advisor](../../../2014/sql-server/install/how-to-run-the-upgrade-advisor-analysis-wizard.md).  
  
 Para obtener información específica que se requiere para cada paso, consulte [Actualizar referencia de interfaz de usuario del Asistente para](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md).  
  
## <a name="running-the-upgrade-advisor-report-viewer"></a>Ejecuta el Visor de informes del Asesor de actualizaciones  
 El Visor de informes del Asesor de actualizaciones se usa para visualizar informes generados por el Asistente para análisis del Asesor de actualizaciones. Cuando se cargue el informe, podrá filtrar los componentes del mismo según los siguientes criterios:  
  
-   Todos los problemas  
  
-   Todos los problemas de actualización  
  
-   Problemas anteriores a la actualización  
  
-   Todos los problemas de migración  
  
-   Problemas resueltos  
  
-   Problemas sin resolver  
  
 Para obtener instrucciones paso a paso relacionadas con el uso del visor de informes, vea los temas siguientes:  
  
-   [Cómo ver un informe del Asesor de actualizaciones](../../../2014/sql-server/install/how-to-view-an-upgrade-advisor-report.md)  
  
-   [Cómo filtrar informes](../../../2014/sql-server/install/how-to-filter-reports.md)  
  
-   [Cómo exportar informes](../../../2014/sql-server/install/how-to-export-reports.md)  
  
## <a name="see-also"></a>Vea también  
 [Cómo: ejecutar el Asistente para análisis del Asesor](../../../2014/sql-server/install/how-to-run-the-upgrade-advisor-analysis-wizard.md)   
 [Actualización del Asistente para la referencia de la interfaz de usuario](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md)   
 [Resolver problemas de actualización](../../../2014/sql-server/install/resolving-upgrade-issues.md)   
 [Trabajar con el Asesor de actualizaciones](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
