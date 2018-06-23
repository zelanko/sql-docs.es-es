---
title: Monitor de actividad de trabajo (Configuración del filtro) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.jobactivitymon.filter.f1
ms.assetid: 89cb0055-5262-447f-8464-7203d4caba78
caps.latest.revision: 12
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 732e20f57170f18bfc3b1d441bc7c0e7a4fc5a88
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36201804"
---
# <a name="job-activity-monitor-filter-settings"></a>Monitor de actividad de trabajo (Configuración del filtro)
  Utilice esta página para reducir el número de filas visibles en el Monitor de actividad de trabajo. Inserte criterios en uno o varios de los cuadros disponibles, para mostrar solo las filas que coinciden con los valores especificados. Algunos cuadros, como **Estado** o **Tipo de bloqueo** ofrecen un número determinado de valores posibles, en una lista desplegable. Otros, como **Aplicación** , permiten indicar un número indeterminado de valores, como una lista separada por comas. Los iconos de barra de herramientas permiten ordenar los cuadros disponibles alfabéticamente o por categoría. Haga clic en los criterios para consultar una descripción breve.  
  
 Para filtrar el Monitor de actividad de trabajo, proporcione los criterios de filtro que desee, haga clic en **Aplicar filtro**y, a continuación, haga clic en **Aceptar**.  
  
## <a name="all-jobs"></a>Todos los trabajos  
 Este grupo de criterios de filtro está disponible cuando se filtra el Monitor de actividad de trabajo.  
  
 **Nombre**  
 Filtra trabajos por nombre.  
  
 **Siguiente ejecución**  
 Filtra por la fecha de la siguiente ejecución.  
  
 **Ejecutable**  
 Muestra trabajos que se pueden ejecutar o trabajos que no se pueden ejecutar. Seleccione **Sí** para ver solo los trabajos que se pueden ejecutar, seleccione **No** para ver únicamente los trabajos que no se pueden ejecutar, o bien seleccione **Todos** para ver los dos tipos de trabajo.  
  
 **Última ejecución**  
 Filtra por la fecha de la última ejecución.  
  
 **Resultado de la última ejecución**  
 Filtra trabajos por el estado de la última ejecución.  
  
 **Enabled**  
 Muestra solo trabajos habilitados o no habilitados.  
  
 **Categoría**  
 Filtra trabajos por su categoría.  
  
 **Programado**  
 Muestra todos los trabajos con o sin programaciones.  
  
 **Estado**  
 Filtra trabajos por el estado.  
  
## <a name="description-area"></a>Descripción (área)  
 **Descripción (cuadro)**  
 Este cuadro sin nombre proporciona una descripción breve de los criterios a medida que se seleccionan.  
  
 **Aplicar filtro**  
 Para aplicar el filtro, haga clic en **Aplicar****filtro** y, después, en **Aceptar**. Para conservar los parámetros de filtro en el cuadro de diálogo **Configuración****del filtro** , pero no aplicarlos, desactive la casilla **Aplicar****filtro**y haga clic en **Aceptar**para mostrar todas las filas.  
  
 **Desactivar**  
 Recupera la configuración predeterminada del filtro.  
  
## <a name="see-also"></a>Vea también  
 [Actividad de trabajos de monitor](../../ssms/agent/monitor-job-activity.md)  
  
  