---
title: Ejecutar el asesor de actualizaciones (interfaz de usuario) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
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
ms.openlocfilehash: 5aecaea9bef359ad24aebbd20dd5e9547497043b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66092445"
---
# <a name="running-upgrade-advisor-user-interface"></a>Ejecutar el Asesor de actualizaciones (interfaz de usuario)
  Puede ejecutar el Asesor de actualizaciones para analizar componentes locales o remotos durante la planeación de la actualización. El asesor de actualizaciones genera un informe para cada componente e instancia que se analiza.  
  
> [!IMPORTANT]  
>  El Asesor de actualizaciones no analiza instancias remotas de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Para analizar una instancia de [!INCLUDE[ssRS](../../includes/ssrs.md)], el Asesor de actualizaciones se debe instalar en el equipo donde esté instalado [!INCLUDE[ssRS](../../includes/ssrs.md)].  
>   
>  Para analizar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Integration Services, debe tener [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] instalado e [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] instalado en el mismo equipo.  
  
## <a name="running-the-upgrade-advisor-analysis-wizard"></a>Ejecutar el Asistente para análisis del Asesor de actualizaciones  
 La ejecución del Asistente para análisis del Asesor de actualizaciones consta de seis pasos:  
  
1.  Inicie el asistente desde la página de inicio del Asesor de actualizaciones.  
  
2.  Identifique el servidor y los componentes que desea analizar.  
  
3.  Recopile información de autenticación.  
  
4.  Recopile los parámetros adicionales según el tipo de componente.  
  
5.  Analice los componentes seleccionados.  
  
6.  Genere un informe de los problemas de la actualización.  
  
 Para obtener más información acerca del Asistente para análisis del Asesor de actualizaciones, vea [Cómo: ejecutar el Asistente para análisis del Asesor de actualizaciones](../../../2014/sql-server/install/how-to-run-the-upgrade-advisor-analysis-wizard.md).  
  
 Para obtener información específica necesaria para cada paso, consulte referencia de la [interfaz de usuario del Asesor de actualizaciones](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md).  
  
## <a name="running-the-upgrade-advisor-report-viewer"></a>Ejecutar el visor de informes del Asesor de actualizaciones  
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
  
## <a name="see-also"></a>Consulte también  
 [Cómo: ejecutar el Asistente para análisis del Asesor de actualizaciones](../../../2014/sql-server/install/how-to-run-the-upgrade-advisor-analysis-wizard.md)   
 [Referencia de la interfaz de usuario del Asesor de actualizaciones](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md)   
 [Resolver problemas de actualización](../../../2014/sql-server/install/resolving-upgrade-issues.md)   
 [Trabajar con el Asesor de actualizaciones](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
