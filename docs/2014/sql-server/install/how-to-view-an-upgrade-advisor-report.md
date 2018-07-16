---
title: 'Cómo: ver un informe del Asesor de actualizaciones | Microsoft Docs'
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
- displaying reports
- viewing reports
- Upgrade Advisor [SQL Server], reports
- SQL Server Upgrade Advisor, reports
- reports [Upgrade Advisor], viewing
ms.assetid: d13b38af-0ac3-4030-83cd-e7d7825dd09f
caps.latest.revision: 32
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: df6d91d700182c7d3828d9e35ac61cfaa0b3959d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37303585"
---
# <a name="how-to-view-an-upgrade-advisor-report"></a>Cómo ver un informe del Asesor de actualizaciones
  El Asesor de actualizaciones crea informes de cada componente que haya seleccionado para su análisis. En este tema se describe cómo ver un informe del Asesor de actualizaciones desde la página de inicio de este último.  
  
> [!IMPORTANT]  
>  El visor de informes carga archivos basados en nombres de archivo estándar. Si se ha cambiado el nombre los archivos, el visor de informes no los cargará.  
  
### <a name="to-view-a-report"></a>Para ver un informe  
  
1.  Haga clic en **iniciar**, haga clic en **todos los programas**, haga clic en **[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** y, a continuación, haga clic en  **[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Upgrade Advisor**.  
  
2.  En la página de inicio del Asesor de actualizaciones, haga clic en **iniciar Visor de informes de Asesor de actualizaciones**.  
  
3.  Para seleccionar un informe en la ubicación predeterminada en su equipo:  
  
    1.  En el **Server** lista, seleccione un servidor.  
  
    2.  En el **instancia o componente** lista, seleccione una combinación componente/instancia o componente.  
  
     Para seleccionar un informe en otra ubicación:  
  
    1.  Haga clic en el **abrir informe** vínculo.  
  
    2.  Vaya a la ubicación del informe y haga doble clic en el archivo XML.  
  
     El Asesor de actualizaciones almacena hasta cinco informes del análisis anterior como historial. Para ver estos informes, haga clic en el **informe** cuadro de lista desplegable y seleccione un informe. Los informes se enumeran según la marca de tiempo establecida durante su generación.  
  
     El informe contiene los detalles siguientes para todos los problemas detectados:  
  
    -   **Importancia**, lo que indica la importancia que tiene corregir el problema.  
  
    -   **Cuándo solucionarlo**, lo que indica si se debería (o debe) solucionar el problema antes o después de actualizar a [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], antes o después de migrar la aplicación o sus datos, o en cualquier momento.  
  
    -   Breve descripción del problema.  
  
4.  Si el informe contiene más de 20 elementos, haga clic en la flecha verde hacia la derecha situada en la parte superior o en parte inferior del informe para ver el conjunto siguiente de elementos. Haga clic en la flecha verde hacia la izquierda para ver los 20 elementos anteriores.  
  
5.  Para ordenar el informe, haga clic en uno de los encabezados de columna.  
  
6.  Para ver los detalles de un elemento en particular, haga clic en dicho elemento. Aparecerá una descripción del problema, junto con una serie de opciones adicionales:  
  
    -   Para ver los objetos que se ha detectado este problema, haga clic en **mostrar objetos afectados**.  
  
    -   Para ver la ayuda sobre el problema, haga clic en **más información sobre este problema y cómo resolverlo**.  
  
    -   Para marcar el problema como resuelto, que oculta el problema al ver el informe nuevo, seleccione **se ha resuelto este problema**.  
  
> [!NOTE]  
>  Es posible que el informe contenga elementos correspondientes a problemas indetectables. Se trata de problemas que no se pueden detectar o que generarían demasiados resultados positivos falsos. Haga clic en el **más información sobre este problema y cómo resolverlo** vínculo para ver una lista de problemas no detectables para el componente.  
  
## <a name="see-also"></a>Vea también  
 [Cómo: exportar informes](../../../2014/sql-server/install/how-to-export-reports.md)   
 [Cómo: ejecutar el Asistente para análisis del Asesor](../../../2014/sql-server/install/how-to-run-the-upgrade-advisor-analysis-wizard.md)   
 [Resolver problemas de actualización](../../../2014/sql-server/install/resolving-upgrade-issues.md)   
 [Actualizar temas de procedimientos del Asesor de actualizaciones](../../../2014/sql-server/install/upgrade-advisor-how-to-topics.md)   
 [Trabajar con el Asesor de actualizaciones](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
