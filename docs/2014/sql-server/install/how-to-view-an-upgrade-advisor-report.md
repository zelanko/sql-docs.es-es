---
title: 'Cómo: ver un informe del Asesor de actualizaciones | Documentos de Microsoft'
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
- displaying reports
- viewing reports
- Upgrade Advisor [SQL Server], reports
- SQL Server Upgrade Advisor, reports
- reports [Upgrade Advisor], viewing
ms.assetid: d13b38af-0ac3-4030-83cd-e7d7825dd09f
caps.latest.revision: 32
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: b3617edd1d79e258490c0cc44fc3b21e012c4573
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36108926"
---
# <a name="how-to-view-an-upgrade-advisor-report"></a>Cómo ver un informe del Asesor de actualizaciones
  El Asesor de actualizaciones crea informes de cada componente que haya seleccionado para su análisis. En este tema se describe cómo ver un informe del Asesor de actualizaciones desde la página de inicio de este último.  
  
> [!IMPORTANT]  
>  El visor de informes carga archivos basados en nombres de archivo estándar. Si se ha cambiado el nombre los archivos, el visor de informes no los cargará.  
  
### <a name="to-view-a-report"></a>Para ver un informe  
  
1.  Haga clic en **iniciar**, haga clic en **todos los programas**, haga clic en **[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** y, a continuación, haga clic en  **[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Asesor de actualizaciones**.  
  
2.  En la página de inicio del Asesor de actualizaciones, haga clic en **iniciar el Visor de informes de Asesor de actualizaciones**.  
  
3.  Para seleccionar un informe en la ubicación predeterminada en su equipo:  
  
    1.  En el **Server** lista, seleccione un servidor.  
  
    2.  En el **instancia o componente** , seleccione una combinación de componente o instancia del componente.  
  
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
  
    -   Para ver los objetos en la que se encontró este problema, haga clic en **mostrar objetos afectados**.  
  
    -   Para ver ayuda sobre el problema, haga clic en **más información acerca de este problema y cómo resolverlo**.  
  
    -   Para marcar el problema como resuelto, que oculta el problema al ver el informe de nuevo, seleccione **ha resuelto este problema**.  
  
> [!NOTE]  
>  Es posible que el informe contenga elementos correspondientes a problemas indetectables. Se trata de problemas que no se pueden detectar o que generarían demasiados resultados positivos falsos. Haga clic en el **más información acerca de este problema y cómo resolverlo** vínculo para ver una lista de problemas no detectables para el componente.  
  
## <a name="see-also"></a>Vea también  
 [Cómo: exportar informes](../../../2014/sql-server/install/how-to-export-reports.md)   
 [Cómo: ejecutar el Asistente de análisis del Asesor de actualizaciones](../../../2014/sql-server/install/how-to-run-the-upgrade-advisor-analysis-wizard.md)   
 [Resolver problemas de actualización](../../../2014/sql-server/install/resolving-upgrade-issues.md)   
 [Temas "Cómo..." asesor de actualización](../../../2014/sql-server/install/upgrade-advisor-how-to-topics.md)   
 [Trabajar con el Asesor de actualizaciones](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  