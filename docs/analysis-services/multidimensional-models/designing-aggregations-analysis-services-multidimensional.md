---
title: Diseñar agregaciones (Analysis Services - Multidimensional) | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c720b45a0ac674282ad78bafd5dcd67bba8b60cc
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="designing-aggregations-analysis-services---multidimensional"></a>Diseñar agregaciones (Analysis Services - Multidimensional)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
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
 [Las agregaciones y diseños de agregaciones](../../analysis-services/multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md)  
  
  
