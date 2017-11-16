---
title: "Diseñar agregaciones (Analysis Services - Multidimensional) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- aggregations [Analysis Services], partitions
- partitions [Analysis Services], aggregations
ms.assetid: 3072b7e0-6961-42ad-a287-16f391f2cec4
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 7fef45841f28152dfed66aa95f670e8a21a3d903
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="designing-aggregations-analysis-services---multidimensional"></a>Diseñar agregaciones (Analysis Services - Multidimensional)
  Las agregaciones son resúmenes precalculados de datos de cubo que permiten a [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] proporcionar respuestas de consulta rápidas.  
  
 Utilice el Asistente para diseñar agregaciones para establecer las opciones de almacenamiento y para diseñar agregaciones en una partición. El asistente funciona en una sola partición de un grupo de medida cada vez, de manera que se pueden seleccionar distintas opciones y diseños para cada partición. El asistente le guía por los pasos necesarios para configurar el almacenamiento y el diseño de agregaciones para una partición. Para obtener más información acerca de cómo configurar el almacenamiento, vea.  
  
 Seleccione un método para controlar el número de agregaciones que diseñará el asistente y, después, deje que el asistente diseñe las agregaciones.  
  
 El objetivo es diseñar el número óptimo de agregaciones. Este número no solo proporcionará tiempos de respuesta satisfactorios, sino que también evitará que el tamaño de la partición sea excesivo. Cuanto mayor sea el número de agregaciones, menores serán los tiempos de respuesta, aunque también se necesitará más espacio de almacenamiento y más tiempo para realizar el cálculo. Además, a medida que el asistente diseña más agregaciones, las primeras agregaciones consiguen mejoras de rendimiento considerablemente mayores que las agregaciones más recientes. La reducción en las agregaciones menos útiles también aumenta el rendimiento. Puede controlar el número de agregaciones diseñadas por el asistente por medio de uno de los métodos disponibles que se indican a continuación:  
  
-   Especifique un límite de espacio de almacenamiento para las agregaciones.  
  
-   Especifique un límite de ganancia de rendimiento.  
  
-   Detenga manualmente el asistente cuando la curva de rendimiento frente a tamaño comience a mostrar una ganancia aceptable de rendimiento.  
  
-   Elija no diseñar agregaciones.  
  
 Para diseñar el almacenamiento, el asistente debe poder conectarse con [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en el servidor de destino. El asistente mostrará un mensaje de error si [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no se está ejecutando en el servidor de destino o si el proceso de diseño del almacenamiento no ha podido conectarse con el servidor de destino.  
  
 El paso final del asistente le permitirá realizar el procesamiento o aplazarlo. El procesamiento crea las agregaciones que se han diseñado con el asistente, mientras que el aplazamiento guarda las agregaciones diseñadas para procesarlas en el futuro, permitiendo de esta manera que continúen las actividades de diseño sin tener que realizar el procesamiento. En función del tamaño de la partición, el procesamiento podría prolongarse considerablemente. Si lo elige, puede interrumpir el procesamiento de una partición.  
  
## <a name="see-also"></a>Vea también  
 [Agregaciones y diseños de agregaciones](../../analysis-services/multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md)  
  
  

