---
title: "Lección 8: Definir acciones | Documentos de Microsoft"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tutorial
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to: SQL Server 2016
ms.assetid: 15459396-83c9-48a0-b10a-99ae38768c79
caps.latest.revision: "16"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 556766b328f7af4086643235f126ea3c5a459332
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="lesson-8-defining-actions"></a>Lección 8: definir acciones
En esta lección, aprenderá a definir acciones en el proyecto de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Una acción es solo una instrucción de Expresiones multidimensionales (MDX) que se almacena en [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] y que se puede incorporar en las aplicaciones cliente e iniciarse por el usuario.  
  
> [!NOTE]  
> Los proyectos completos para todas las lecciones de este tutorial están disponibles en línea. Puede saltar a continuación a cualquier lección con el proyecto completado de la lección anterior como punto de partida. [Haga clic aquí](http://go.microsoft.com/fwlink/?LinkID=221866) para descargar los proyectos de ejemplo que tienen que ver con este tutorial.  
  
[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] admite los tipos de acciones descritos en la siguiente tabla.  
  
|||  
|-|-|  
|CommandLine|Ejecuta un comando en el símbolo del sistema.|  
|Conjunto de datos|Devuelve un conjunto de datos a una aplicación cliente.|  
|Obtención de detalles|Devuelve una instrucción de obtención de detalles como una expresión, que el cliente ejecuta para devolver un conjunto de filas.|  
|Html|Ejecuta un script HTML en un explorador de Internet.|  
|Propietario|Ejecuta una operación con una interfaz que no aparece en esta tabla.|  
|Informe|Envía una solicitud parametrizada basada en una dirección URL a un servidor de informes y devuelve un informe a una aplicación cliente.|  
|Conjunto de filas|Devuelve un conjunto de filas a una aplicación cliente.|  
|.|Ejecuta un comando OLE DB.|  
|Dirección URL|Muestra una página web dinámica en un explorador de Internet.|  
  
Las acciones permiten a los usuarios iniciar una aplicación o realizar otros pasos en el contexto de un elemento seleccionado. Para obtener más información, vea [Acciones &#40;Analysis Services - Datos multidimensionales&#41;](../analysis-services/multidimensional-models/actions-analysis-services-multidimensional-data.md), [Acciones en modelos multidimensionales](../analysis-services/multidimensional-models/actions-in-multidimensional-models.md)  
  
> [!NOTE]  
> Para obtener ejemplos de acciones, vea los ejemplos de acciones en la pestaña Plantillas del panel Herramientas de cálculo o en los ejemplos del almacenamiento de datos de ejemplo [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] DW. Para obtener más información sobre cómo instalar esta base de datos, vea [Instalar los datos y proyectos de ejemplo para el tutorial de modelado multidimensional de Analysis Services](../analysis-services/install-sample-data-and-projects.md).  
  
Esta lección incluye la tarea siguiente:  
  
[Definir y utilizar una acción de obtención de detalles](../analysis-services/lesson-8-1-defining-and-using-a-drillthrough-action.md)  
En esta tarea, se define, utiliza y modifica una acción de obtención de detalles a través de la relación de dimensión de hecho definida anteriormente en este tutorial.  
  
## <a name="next-lesson"></a>Lección siguiente  
[Lección 9: Definir perspectivas y traducciones](../analysis-services/lesson-9-defining-perspectives-and-translations.md)  
  
## <a name="see-also"></a>Vea también  
[Escenario de Tutorial de Analysis Services](../analysis-services/analysis-services-tutorial-scenario.md)  
[Creación de modelos multidimensionales &#40;tutorial de Adventure Works&#41;](../analysis-services/multidimensional-modeling-adventure-works-tutorial.md)  
[Acciones &#40;Analysis Services - Datos multidimensionales&#41;](../analysis-services/multidimensional-models/actions-analysis-services-multidimensional-data.md)  
[Acciones en modelos multidimensionales](../analysis-services/multidimensional-models/actions-in-multidimensional-models.md)  
  
  
  
