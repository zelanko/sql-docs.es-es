---
title: Cómo ver un informe del Asesor de actualizaciones | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- displaying reports
- viewing reports
- Upgrade Advisor [SQL Server], reports
- SQL Server Upgrade Advisor, reports
- reports [Upgrade Advisor], viewing
ms.assetid: d13b38af-0ac3-4030-83cd-e7d7825dd09f
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c0ae231e380530f11d4c97a917927ed62e99fb47
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66094795"
---
# <a name="how-to-view-an-upgrade-advisor-report"></a>Cómo ver un informe del Asesor de actualizaciones
  El Asesor de actualizaciones crea informes de cada componente que haya seleccionado para su análisis. En este tema se describe cómo ver un informe del Asesor de actualizaciones desde la página de inicio de este último.  
  
> [!IMPORTANT]  
>  El visor de informes carga archivos basados en nombres de archivo estándar. Si se ha cambiado el nombre los archivos, el visor de informes no los cargará.  
  
### <a name="to-view-a-report"></a>Para ver un informe  
  
1.  Haga clic en **Inicio**, **todos los programas**, **[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** y, a continuación, haga clic en ** [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Asesor de actualizaciones**.  
  
2.  En la página de inicio del Asesor de actualizaciones, haga clic en **iniciar el visor de informes del Asesor de actualizaciones**.  
  
3.  Para seleccionar un informe en la ubicación predeterminada en su equipo:  
  
    1.  En la lista **servidor** , seleccione un servidor.  
  
    2.  En la lista **instancia o componente** , seleccione una combinación componente o componente/instancia.  
  
     Para seleccionar un informe en otra ubicación:  
  
    1.  Haga clic en el vínculo **abrir Informe** .  
  
    2.  Vaya a la ubicación del informe y haga doble clic en el archivo XML.  
  
     El Asesor de actualizaciones almacena hasta cinco informes del análisis anterior como historial. Para ver estos informes, haga clic en el cuadro de lista desplegable **Informe** y seleccione un informe. Los informes se enumeran según la marca de tiempo establecida durante su generación.  
  
     El informe contiene los detalles siguientes para todos los problemas detectados:  
  
    -   **Importancia**, que indica la importancia de corregir el problema.  
  
    -   **Cuándo solucionarlo**, que indica si se debe corregir el problema antes o después de actualizar a, antes o después [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]de migrar la aplicación o los datos, o en cualquier momento.  
  
    -   Breve descripción del problema.  
  
4.  Si el informe contiene más de 20 elementos, haga clic en la flecha verde hacia la derecha situada en la parte superior o en parte inferior del informe para ver el conjunto siguiente de elementos. Haga clic en la flecha verde hacia la izquierda para ver los 20 elementos anteriores.  
  
5.  Para ordenar el informe, haga clic en uno de los encabezados de columna.  
  
6.  Para ver los detalles de un elemento en particular, haga clic en dicho elemento. Aparecerá una descripción del problema, junto con una serie de opciones adicionales:  
  
    -   Para ver los objetos en los que se encontró este problema, haga clic en **Mostrar objetos afectados**.  
  
    -   Para ver la ayuda del problema, haga clic en **más información sobre este problema y cómo resolverlo**.  
  
    -   Para marcar el problema como resuelto, lo que oculta el problema al volver a ver el informe, seleccione **este problema**se ha resuelto.  
  
> [!NOTE]  
>  Es posible que el informe contenga elementos correspondientes a problemas indetectables. Se trata de problemas que no se pueden detectar o que generarían demasiados resultados positivos falsos. Haga clic en el vínculo **más información sobre este problema y cómo resolverlo** para ver una lista de problemas no detectables del componente.  
  
## <a name="see-also"></a>Consulte también  
 [Cómo: exportar informes](../../../2014/sql-server/install/how-to-export-reports.md)   
 [Cómo: ejecutar el Asistente para análisis del Asesor de actualizaciones](../../../2014/sql-server/install/how-to-run-the-upgrade-advisor-analysis-wizard.md)   
 [Resolver problemas de actualización](../../../2014/sql-server/install/resolving-upgrade-issues.md)   
 [Temas de procedimientos del Asesor de actualizaciones](../../../2014/sql-server/install/upgrade-advisor-how-to-topics.md)   
 [Trabajar con el Asesor de actualizaciones](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
