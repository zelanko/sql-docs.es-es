---
title: Introducción del Asistente para actualización | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Upgrade Advisor Report Viewer
- SQL Server Upgrade Advisor, components
- tools [Upgrade Advisor]
- Upgrade Advisor [SQL Server], components
- components [Upgrade Advisor]
- Upgrade Advisor Analysis Wizard
- limitations [Upgrade Advisor]
- analyzing system [Upgrade Advisor]
- analyzing system [Upgrade Advisor], about analysis
ms.assetid: f5c56f63-4478-40af-abb9-642f58a0026c
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9fba325ab05844388ceceb1e53b6d4a8cf618468
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48208405"
---
# <a name="upgrade-advisor-overview"></a>Información general sobre el Asesor de actualizaciones
  El Asesor de actualizaciones proporciona una consola central para analizar los componentes de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] y [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] así como para ver informes que contienen información sobre los resultados del análisis.  
  
## <a name="how-upgrade-advisor-works"></a>Cómo funciona el Asesor de actualizaciones  
 Al ejecutar el Asesor de actualizaciones, se mostrará la página de inicio del mismo. La página de inicio del Asesor de actualizaciones es el punto de lanzamiento para:  
  
-   Asistente para análisis del Asesor de actualizaciones  
  
-   Visor de informes del Asesor de actualizaciones  
  
-   Ayuda del Asesor de actualizaciones  
  
 La primera vez que utilice el Asesor de actualizaciones, ejecute el Asistente para análisis del Asesor de actualizaciones para analizar un servidor. Cuando el análisis complete el asistente, haga clic en **iniciar informe** desde el asistente o vuelva a la página de inicio del Asesor de actualizaciones. Desde allí, ejecute el Visor de informes del Asesor de actualizaciones para ver el informe. El informe proporciona vínculos a temas de información que le ayudarán a resolver los problemas conocidos.  
  
## <a name="upgrade-advisor-analysis-wizard"></a>Asistente para análisis del Asesor de actualizaciones  
 Para llevar a cabo un análisis, haga clic en **iniciar Asistente de análisis del Asistente para actualización** en la página de inicio del Asesor de actualizaciones. El Asistente para análisis del Asesor de actualizaciones recopilará información sobre el equipo, las instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], los componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y los archivos de seguimiento que desea analizar. Una vez recopilada y confirmada toda la información, el Asistente para análisis del Asesor de actualizaciones analizará los componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Cada vez que ejecute el Asistente para análisis del Asesor de actualizaciones, se generará un informe independiente y no se sobrescribirá los informes existentes relativos a los componentes seleccionados. No obstante, el visor de informes solo muestra los cinco últimos informes.  
  
 Cuando el Asistente para análisis del Asesor de actualizaciones finalice el análisis, creará un archivo XML para cada componente que se haya incluido en el análisis. Los elementos y problemas detectados en cada componente se incluirán en los archivos XML.  
  
### <a name="what-upgrade-advisor-analyzes"></a>Elementos analizados por el Asesor de actualizaciones  
 Un analizador dedicado se ejecuta en el contexto del Asesor de actualizaciones para cada componente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La salida de cada analizador es un informe XML sobre dicho componente.  
  
 El Asesor de actualizaciones consulta los siguientes componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   Servidor de bases de datos (también conocido como [!INCLUDE[ssDE](../../includes/ssde-md.md)] en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]), que incluye Replicación, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Búsqueda de texto completo y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
> [!NOTE]  
>  Durante el análisis, cada analizador crea un archivo de registro. Puede utilizar estos archivos de registro para solucionar los problemas del análisis. Por ejemplo, si el Asesor de actualizaciones se está ejecutando con lentitud, puede ver los archivos de registro para determinar la causa del retraso.  
  
### <a name="upgrade-advisor-limitations"></a>Limitaciones del Asesor de actualizaciones  
 El Asesor de actualizaciones no puede detectar todos los problemas que podrían afectar a una actualización. Por ejemplo, si ha incrustado código SQL en una aplicación cliente que se ejecuta en los equipos de escritorio de los usuarios finales, no será posible que el Asesor de actualizaciones analice dichas aplicaciones. Para estos elementos, deberá tener en cuenta los problemas y actualizar, migrar o modificar la información según lo requiera la instalación.  
  
 El Asesor de actualizaciones no analiza procedimientos almacenados cifrados, código escrito en procedimientos almacenados extendidos ni código fuente escrito en un lenguaje que no sea [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
## <a name="upgrade-advisor-report-viewer"></a>Visor de informes del Asesor de actualizaciones  
 Para ver un informe del Asesor de actualizaciones, haga clic en **iniciar Visor de informes de Asesor de actualizaciones** en la página de inicio del Asesor de actualizaciones. Cuando se inicie el Visor de informes del Asesor de actualizaciones, se cargarán los informes ubicados en el directorio predeterminado. No se muestran los informes si el Visor de informes del Asesor de actualizaciones no encuentra ningún informe en el directorio predeterminado. Si no hay ningún informe en el directorio predeterminado, puede ejecutar el Asistente para análisis del Asesor de actualizaciones para crear un informe o cargar un informe existente de otro servidor o de un subdirectorio.  
  
 El Asesor de actualizaciones de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] no sobrescribe informes existentes. No obstante, el visor de informes solo muestra los cinco últimos informes. Para ver un informe anterior, seleccione el informe desde el **informe** cuadro de lista desplegable. La marca de tiempo indica la fecha y la hora en que se generó el informe.  
  
 Cuando los archivos XML del Asistente para análisis del Asesor de actualizaciones se cargan en el Visor de informes del Asesor de actualizaciones, aparecerá un informe por cada componente. El informe contiene todos los problemas conocidos, tanto detectables como no detectables, que deben solucionarse. Para cada problema existe un icono que indica la importancia, una etiqueta que informa de cuándo debe corregirse el problema y una breve descripción. Cuando expanda un problema, verá una descripción más extensa, un vínculo a los detalles del problema y otro vínculo al archivo de Ayuda. La información de cada problema está diseñada para proporcionar la información necesaria para corregir el problema.  
  
 La mayoría de los componentes tienen problemas que no se pueden detectar. Para ver estos problemas, expanda el **otros problemas de actualización** elemento para el componente y, a continuación, haga clic en el vínculo para ver información adicional sobre los problemas en la documentación. Para obtener más información sobre los problemas de compatibilidad con versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [Trabajar con el Asesor de actualizaciones](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
