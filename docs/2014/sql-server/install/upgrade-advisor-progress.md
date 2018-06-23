---
title: Progreso del Asesor de actualización | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Upgrade Advisor [SQL Server], analysis progress status
- analyzing system [Upgrade Advisor], progress information
- SQL Server Upgrade Advisor, analysis progress status
- monitoring analysis progress
- progress information [Upgrade Advisor]
- status information [Upgrade Advisor]
ms.assetid: a9e3d1c8-d492-4beb-93c7-f1bc40d4a910
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: e1b867360b773253ae22d24a76ce00b35c589d96
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36113507"
---
# <a name="upgrade-advisor-progress"></a>Progreso del Asesor de actualizaciones
  El análisis del Asesor de actualizaciones se inicia con un analizador dedicado que realiza un análisis de cada componente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que seleccionó. Cuando se analizan los componentes, se notifica el progreso en la **progreso** cuadro de diálogo.  
  
## <a name="options"></a>Opciones  
 **Acción**  
 Especifica el componente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] seleccionado para el análisis.  
  
 **Estado**  
 Muestra el valor de estado devuelto desde la interfaz de progreso del componente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **de mensaje**  
 Muestra el mensaje de error o de confirmación que devuelve cada analizador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Si el análisis se prolonga demasiado tiempo, puede detenerlo, salir del Asistente para análisis del Asesor de actualizaciones y, a continuación, volver a ejecutar el asistente. Para reducir el tiempo del análisis, seleccione menos componentes para analizar.  
  
 Cuando el análisis se haya completado, el informe se escribe en un archivo. Puede ver el informe, haga clic en **iniciar informe** para iniciar el Visor de informes desde esta página. Si desea ver el informe más adelante, puede abrir el **Visor de informes del Asesor de actualizaciones** desde la página de inicio del Asesor de actualizaciones.  
  
> [!NOTE]  
>  Los informes anteriores se guardan cada vez que se analice un servidor. Los informes se guardan con la marca de tiempo como nombre de archivo. El visor de informes muestra los cinco últimos informes guardados.  
  
## <a name="see-also"></a>Vea también  
 [Cómo: iniciar el Asesor de actualizaciones](../../../2014/sql-server/install/how-to-launch-upgrade-advisor.md)   
 [Cómo: ejecutar el Asistente de análisis del Asesor de actualizaciones](../../../2014/sql-server/install/how-to-run-the-upgrade-advisor-analysis-wizard.md)   
 [Componentes de SQL Server](../../../2014/sql-server/install/sql-server-components.md)   
 [Upgrade Advisor referencia de la interfaz de usuario](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md)   
 [Trabajar con el Asesor de actualizaciones](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  