---
title: Monitor de actividad de trabajo (Configuración del filtro) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: maintenance-plans
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.jobactivitymon.filter.f1
ms.assetid: 89cb0055-5262-447f-8464-7203d4caba78
caps.latest.revision: 13
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 76e11f1afb39cb8ddd82f99d74e2d2a21c776664
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="job-activity-monitor-filter-settings"></a>Monitor de actividad de trabajo (Configuración del filtro)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
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
  
## <a name="see-also"></a>Ver también  
 [Actividad de trabajos de monitor](http://msdn.microsoft.com/library/71cb432b-631d-4b8b-9965-e731b3d8266d)  
  
  
