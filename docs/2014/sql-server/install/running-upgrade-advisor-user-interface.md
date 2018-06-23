---
title: Ejecutar el Asesor de actualizaciones (interfaz de usuario) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Upgrade Advisor Report Viewer
- Upgrade Advisor [SQL Server], running
- launching Upgrade Advisor
- Upgrade Advisor Analysis Wizard
- starting Upgrade Advisor
- SQL Server Upgrade Advisor, running
ms.assetid: 7f47c9b3-88d3-43d6-837e-f157b49a55ac
caps.latest.revision: 40
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 36a31e74e95b966137df96f5e3f2ab05fa7a991f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36103241"
---
# <a name="running-upgrade-advisor-user-interface"></a>Ejecutar el Asesor de actualizaciones (interfaz de usuario)
  Puede ejecutar el Asesor de actualizaciones para analizar componentes locales o remotos durante la planeación de la actualización. El Asesor de actualizaciones crea un informe para cada componente y la instancia que se analice.  
  
> [!IMPORTANT]  
>  El Asesor de actualizaciones no analiza instancias remotas de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Para analizar una instancia de [!INCLUDE[ssRS](../../includes/ssrs-md.md)], el Asesor de actualizaciones se debe instalar en el equipo donde esté instalado [!INCLUDE[ssRS](../../includes/ssrs-md.md)].  
>   
>  Para analizar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Integration Services, debe tener la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] instalado y [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] instalado en el mismo equipo.  
  
## <a name="running-the-upgrade-advisor-analysis-wizard"></a>Ejecutar al Asistente de análisis del Asesor de actualizaciones  
 La ejecución del Asistente para análisis del Asesor de actualizaciones consta de seis pasos:  
  
1.  Inicie el asistente desde la página de inicio del Asesor de actualizaciones.  
  
2.  Identifique el servidor y los componentes que desea analizar.  
  
3.  Recopile información de autenticación.  
  
4.  Recopile los parámetros adicionales según el tipo de componente.  
  
5.  Analice los componentes seleccionados.  
  
6.  Genere un informe de los problemas de la actualización.  
  
 Para obtener más información sobre el Asistente para análisis Asesor de actualizaciones, consulte [Cómo: ejecutar el Asistente de análisis del Asesor de actualizaciones](../../../2014/sql-server/install/how-to-run-the-upgrade-advisor-analysis-wizard.md).  
  
 Para obtener información específica que se requiere para cada paso, consulte [referencia actualizar de la interfaz de usuario de asistente](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md).  
  
## <a name="running-the-upgrade-advisor-report-viewer"></a>Ejecuta el Visor de informes del Asesor de actualizaciones  
 El Visor de informes del Asesor de actualizaciones se usa para visualizar informes generados por el Asistente para análisis del Asesor de actualizaciones. Cuando se cargue el informe, podrá filtrar los componentes del mismo según los siguientes criterios:  
  
-   Todos los problemas  
  
-   Todos los problemas de actualización  
  
-   Problemas anteriores a la actualización  
  
-   Todos los problemas de migración  
  
-   Problemas resueltos  
  
-   Problemas sin resolver  
  
 Para obtener instrucciones paso a paso relacionadas con el uso del visor de informes, vea los temas siguientes:  
  
-   [Cómo: ver un informe del Asesor de actualizaciones](../../../2014/sql-server/install/how-to-view-an-upgrade-advisor-report.md)  
  
-   [Cómo: filtrar informes](../../../2014/sql-server/install/how-to-filter-reports.md)  
  
-   [Cómo: exportar informes](../../../2014/sql-server/install/how-to-export-reports.md)  
  
## <a name="see-also"></a>Vea también  
 [Cómo: ejecutar el Asistente de análisis del Asesor de actualizaciones](../../../2014/sql-server/install/how-to-run-the-upgrade-advisor-analysis-wizard.md)   
 [Upgrade Advisor referencia de la interfaz de usuario](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md)   
 [Resolver problemas de actualización](../../../2014/sql-server/install/resolving-upgrade-issues.md)   
 [Trabajar con el Asesor de actualizaciones](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  