---
title: Crear una solución y un origen de datos (tutorial intermedio de minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 0488b231-1045-4169-aabb-c1005d86ca30
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 21bedc825f5890e3eb6551818dc5dc10724d2bf8
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68891436"
---
# <a name="creating-a-solution-and-data-source-intermediate-data-mining-tutorial"></a>Crear una solución y un origen de datos (tutorial intermedio de minería de datos)
  Para trabajar con minería de datos, primero debe crear un proyecto en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] mediante la plantilla, **Proyecto multidimensional y de minería de datos de Analysis Services**. Cuando se abre la plantilla, esta carga en el diseñador todos los esquemas que podría necesitar para minería de datos: orígenes de datos, estructuras y modelos de minería de datos, e incluso cubos si su estructura de minería de datos usa datos multidimensionales.  
  
 Cuando se crea el proyecto, la solución se almacena como un archivo local hasta que se implementa la solución. Cuando se implementa la solución, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] busca el servidor de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] especificado en las propiedades del proyecto, y crea una nueva base de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] con el mismo nombre que el proyecto. De forma predeterminada, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] usa la instancia **localhost** para los proyectos nuevos. Si usa una instancia con nombre o especifica un nombre diferente para la instancia predeterminada, debe cambiar la propiedad de la base de datos de implementación del proyecto a la ubicación donde desea crear los objetos de minería de datos.  
  
 Para obtener más información [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] acerca de los proyectos, vea [crear un proyecto de Analysis Services &#40;SSDT&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/create-an-analysis-services-project-ssdt).  
  
### <a name="to-create-a-new-analysis-services-project-for-this-tutorial"></a>Para crear un nuevo proyecto de Analysis Services en este tutorial  
  
1.  Abra [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
2.  En el menú **Archivo** , seleccione **Nuevo**y haga clic en **Proyecto**.  
  
3.  En el panel **Plantillas instaladas** , seleccione **Proyecto multidimensional y de minería de datos de Analysis Services** .  
  
4.  En el cuadro **Nombre** , asigne al nuevo proyecto el nombre **Minería de datos intermedia**.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-change-the-instance-where-data-mining-objects-are-stored-optional"></a>Para cambiar la instancia donde se almacenan los objetos de minería de datos (opcional)  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], en el menú **Proyecto** , haga clic en **Propiedades**.  
  
2.  En el lado izquierdo del panel **Páginas de propiedades** , haga clic en **Implementación**.  
  
3.  Compruebe que el nombre del **servidor** es **localhost**. Si usa una instancia diferente, escriba el nombre de la instancia. Si va a utilizar una instancia con nombre de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], escriba el nombre de equipo y, a continuación, el nombre de instancia. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-change-the-deployment-properties-for-a-project-optional"></a>Para cambiar las propiedades de implementación de un proyecto (opcional)  
  
1.  En el Explorador de soluciones, haga clic con el botón secundario en el proyecto y seleccione **Propiedades**.  
  
     -- o --  
  
     En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], en el menú **Proyecto** , seleccione **Propiedades**.  
  
2.  En el lado izquierdo del panel **Páginas de propiedades** , haga clic en **Implementación**.  
  
     En el panel **Opciones** , seleccione **Modo de implementación**y establezca las opciones en **Implementar todo** para sobrescribir o en **Implementar solo cambios** para actualizar los objetos o agregar objetos.  
  
## <a name="creating-a-data-source"></a>Crear un origen de datos  
 En el tutorial básico de minería de datos, creó un *origen de datos* con información de conexión para la base de datos [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] . Siga los mismos pasos para crear el origen de datos [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] en esta solución.  
  
#### <a name="to-create-a-data-source"></a>Para crear un origen de datos  
  
-   [Crear un origen de datos &#40;tutorial básico de minería de datos&#41;](../../2014/tutorials/creating-a-data-source-basic-data-mining-tutorial.md)  
  
 Un solo origen de datos puede admitir varias vistas del origen de datos, y cada vista del origen de datos puede tener varias tablas. Sin embargo, dado que el origen de datos y la vista del origen [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] de datos se implementan en la base de datos junto con los modelos de minería de datos que se crean, se recomienda incluir en cada vista del origen de datos solo las tablas necesarias para cada modelo de minería de datos o grupo de modelos.  
  
 En las lecciones siguientes, agregará vistas del origen de datos para admitir cada uno de los nuevos escenarios. Solo las lecciones de cesta de la compra y agrupación en clústeres de secuencia utilizan la misma vista del origen de datos; por el contrario, cada escenario utiliza una vista del origen de datos distinta, de forma que las lecciones son independientes y se pueden realizar por separado.  
  
|Escenario|Datos incluidos en la vista del origen de datos|  
|--------------|-------------------------------------------|  
|[Lección 2: generar un escenario de previsión &#40;tutorial intermedio de minería de datos&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)|Los informes de ventas mensuales para los modelos de bicicleta en distintas regiones, recopilados como una vista única.|  
|[Lección 3: Generar un escenario de cesta de la compra &#40;Tutorial intermedio de minería de datos&#41;](../../2014/tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md)|Una tabla que contiene una lista de pedidos de cliente, y una tabla anidada que muestra las compras individuales para cada cliente.|  
|[Lección 4: generar un escenario de agrupación en clústeres de secuencia &#40;tutorial intermedio de minería de datos&#41;](../../2014/tutorials/lesson-4-build-sequence-clustering-scenario-intermediate-data-mining.md)|Los mismos datos que se utilizan para el análisis de la cesta de la compra, además de un identificador que muestra el orden en que los elementos se compraron.|  
|[Lección 5: Generar modelos de red neuronal y de regresión logística &#40;Tutorial intermedio de minería de datos&#41;](../../2014/tutorials/lesson-5-build-models-intermediate-data-mining-tutorial.md)|Una única tabla que contiene algunos datos preliminares de seguimiento del rendimiento procedentes de un centro de llamadas.|  
  
## <a name="next-lesson"></a>Lección siguiente  
 [Lección 2: generar un escenario de previsión &#40;tutorial intermedio de minería de datos&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte también  
 [Proyectos de minería de datos](../../2014/analysis-services/data-mining/data-mining-projects.md)   
 [Vistas del origen de datos en modelos multidimensionales](https://docs.microsoft.com/analysis-services/multidimensional-models/data-source-views-in-multidimensional-models)  
  
  
