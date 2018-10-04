---
title: Revisar las propiedades de dimensión de cubo y | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: dda922b8-6d75-4662-b09e-8a317c6a1c70
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b4db6133a486e77369630dc717fab02b3be7f8e2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48196275"
---
# <a name="reviewing-cube-and-dimension-properties"></a>Revisar las propiedades de cubo y dimensión
  Después de definir un cubo, se pueden revisar los resultados mediante el Diseñador de cubos. En la tarea siguiente, revisará la estructura del cubo del proyecto Tutorial de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
### <a name="to-review-cube-and-dimension-properties-in-cube-designer"></a>Para revisar las propiedades del cubo y de las dimensiones en el Diseñador de cubos  
  
1.  Para abrir el Diseñador de cubos, haga doble clic en el cubo **Tutorial de Analysis Services** en el nodo **Cubos** del Explorador de soluciones.  
  
2.  En el panel **Medidas** de la pestaña **Estructura de cubo** del Diseñador de cubos, expanda el grupo de medida **Internet Sales** para ver las medidas definidas.  
  
     Si desea cambiar el orden de dichas medidas, arrástrelas para obtener el orden que desee. El orden afectará al modo en que determinadas aplicaciones cliente ordenarán las medidas. El grupo de medida y cada una de sus medidas tienen propiedades que pueden modificarse en la ventana Propiedades.  
  
3.  En el panel **Dimensiones** de la pestaña **Estructura de cubo** del Diseñador de cubos, revise las dimensiones de cubo que se encuentran en el cubo Tutorial de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
     Observe que, si bien solo se crearon tres dimensiones en el nivel de base de datos, como se muestra en el Explorador de soluciones, hay cinco dimensiones de cubo en el cubo Tutorial de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . El cubo contiene más dimensiones que la base de datos porque la dimensión de base de datos Date se utiliza como base para tres dimensiones de cubo independientes relacionadas con fechas, basadas en los hechos relacionados con fechas de la tabla de hechos. Estas dimensiones relacionadas con fechas también se denominan *dimensiones realizadoras de roles*. Las tres dimensiones de cubo relacionadas con fechas permiten que los usuarios dimensionen el cubo mediante tres hechos independientes que están relacionados con cada venta de producto: la fecha de pedido del producto, la fecha de vencimiento de satisfacción del pedido y la fecha de envío del pedido. Si se reutiliza una única dimensión de base de datos para las dimensiones de cubo, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] simplifica la administración de las dimensiones, utiliza menos espacio en el disco y reduce el tiempo general de procesamiento.  
  
4.  En el panel **Dimensiones** de la pestaña **Estructura de cubo** , expanda **Customer**y, a continuación, haga clic en **Editar Customer** para abrir la dimensión en el Diseñador de dimensiones.  
  
     El Diseñador de dimensiones contiene estas pestañas: **Estructura de dimensión**, **Relaciones de atributo**, **Traducciones**y **Explorador**. Tenga en cuenta que la pestaña **Estructura de dimensión** incluye tres paneles: **Atributos**, **Jerarquías**y **Vista del origen de datos**. Los atributos que contiene la dimensión aparecen en el panel **Atributos** . Para obtener más información, consulte [Dimension Attribute Properties Reference](multidimensional-models/dimension-attribute-properties-reference.md), [jerarquías definidas por el usuario](multidimensional-models/user-defined-hierarchies-create.md).  
  
5.  Para cambiar al Diseñador de cubos, haga clic con el botón derecho en el cubo **Tutorial de Analysis Services** del nodo **Cubos** en el Explorador de soluciones y, después, haga clic en **Ver diseñador**.  
  
6.  En el Diseñador de cubos, haga clic en la pestaña **Uso de dimensiones** .  
  
     En esta vista del cubo Tutorial de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , puede ver las dimensiones de cubo que se utilizan en el grupo de medida Internet Sales. Asimismo, puede definir el tipo de relación entre cada dimensión y cada grupo de medida en el que se utiliza.  
  
7.  Haga clic en la pestaña **Particiones** .  
  
     El Diseñador de cubos define una única partición para el cubo, utilizando el modo de almacenamiento de procesamiento analítico en línea multidimensional (MOLAP) sin agregaciones. Con MOLAP, todos los datos de nivel hoja y todas las agregaciones se almacenan en el cubo para maximizar el rendimiento. Las agregaciones son resúmenes de datos precalculados que mejoran el tiempo de respuesta de las consultas ya que tienen las respuestas preparadas antes de que se planteen las preguntas. Puede definir particiones adicionales, parámetros de almacenamiento y parámetros de reescritura en la pestaña **Particiones** . Para obtener más información, consulte [Particiones &#40;Analysis Services - Datos multidimensionales&#41;](multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md), [Agregaciones y diseños de agregaciones](multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md).  
  
8.  Haga clic en la pestaña **Explorador** .  
  
     Observe que el cubo no puede examinarse porque todavía no se ha implementado en una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. En este punto, el cubo del proyecto Tutorial de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] es simplemente una definición de un cubo, que puede implementar en cualquier instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Cuando implementa y procesa un cubo, puede crear los objetos definidos en una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] y rellenar los objetos con datos de los orígenes de datos subyacentes.  
  
9. En el Explorador de soluciones, haga clic con el botón derecho en **Tutorial de Analysis Services** en el nodo **Cubos** y, luego, haga clic en **Ver código**. Es posible que tenga que esperar.  
  
     El código XML del cubo Tutorial de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] se muestra en la pestaña **[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial.cube [XML]** . Es el código real que se utiliza para crear el cubo en una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] durante la implementación. Para obtener más información, consulte [Ver el XML de un proyecto de Analysis Services &#40;SSDT&#41;](multidimensional-models/view-the-xml-for-an-analysis-services-project-ssdt.md).  
  
10. Cierre la pestaña Código XML.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Implementar un proyecto de Analysis Services](lesson-2-5-deploying-an-analysis-services-project.md)  
  
## <a name="see-also"></a>Vea también  
 [Examinar los datos de dimensiones en el Diseñador de dimensiones](multidimensional-models/database-dimensions-browse-dimension-data-in-dimension-designer.md)  
  
  
