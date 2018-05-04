---
title: Habilitar obtención de detalles para un modelo de minería de datos | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data mining [Analysis Services], how-to topics
- drillthrough [Analysis Services]
ms.assetid: 4fa44f60-ef9a-4b59-98c0-c0baf1195c8e
caps.latest.revision: 28
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 516fff1c886a0ae22a3449e513107d9a8e6366b5
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="enable-drillthrough-for-a-mining-model"></a>Habilitar la obtención de detalles para un modelo de minería
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Si ha habilitado la obtención de detalles para un modelo de minería de datos, al examinar el modelo, puede recuperar información detallada sobre los casos que se usaron para crear el modelo. Para ver esta información, debe tener los permisos necesarios y se debe de haber procesado la estructura.  
  
 **Permisos** : para que un usuario obtenga detalles de los datos del modelo o de los datos de la estructura, el usuario debe ser miembro de un rol con permisos [AllowDrillThrough](../../analysis-services/scripting/properties/allowdrillthrough-element-assl.md) en el modelo o en la estructura de minería de datos. Los permisos de obtención de detalles se establecen por separado en la estructura y en el modelo.  
  
-   Los permisos de obtención de detalles en el modelo permiten obtener detalles del modelo, incluso si no se dispone de permisos en la estructura.  
  
-   Los permisos de obtención de detalles en la estructura ofrecen la posibilidad adicional de incluir columnas de la estructura en las consultas de obtención de detalles del modelo, mediante la función [StructureColumn &#40;DMX&#41;](../../dmx/structurecolumn-dmx.md). También puede consultar los casos de prueba y entrenamiento de la estructura mediante la sintaxis SELECT… DESDE \<estructura >. Sintaxis de los casos.  
  
 **Almacenamiento en caché de casos de entrenamiento** : la obtención de detalles funciona recuperando información sobre los casos de entrenamiento de la estructura de minería de datos. Esta información se almacena en la caché cuando se procesa la estructura. Por consiguiente, si decide borrar todos los datos de la caché cambiando la propiedad <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> a **ClearAfterProcessing**, la obtención de detalles no funcionará.  
  
> [!NOTE]  
>  Si los casos de entrenamiento no se han almacenado en la caché, deberá cambiar la propiedad <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> a **KeepTrainingCases** y, después, deberá volver a procesar el modelo antes de ver los datos de los casos.  
  
 Para más información, vea [Consultas de obtención de detalles &#40;minería de datos&#41;](../../analysis-services/data-mining/drillthrough-queries-data-mining.md).  
  
### <a name="to-enable-drillthrough-on-a-mining-model"></a>Para habilitar la obtención de detalles en un modelo de minería de datos  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], en la pestaña **Modelos de minería de datos** del Diseñador de minería de datos, haga clic con el botón derecho en el nombre del modelo de minería de datos del que quiere habilitar la obtención de detalles y seleccione **Propiedades**.  
  
2.  En las ventanas **Propiedades** , haga clic en **AllowDrillThrough**y seleccione **True**.  
  
3.  En la pestaña **Modelos de minería de datos** , haga clic con el botón derecho en el modelo y seleccione **Procesar modelo**.  
  
### <a name="to-enable-caching-for-a-mining-structure"></a>Para habilitar el almacenamiento en caché para una estructura de minería de datos  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], en la pestaña **Estructura de minería de datos** del Diseñador de minería de datos, haga clic con el botón derecho en el nombre de la estructura de minería de datos.  
  
2.  Abra la ventana **Propiedades** .  
  
3.  En la ventana **Propiedades** , busque la propiedad **CacheMode** y seleccione **KeepTrainingCases** en la lista.  
  
4.  En el menú **Base de datos** , seleccione **Procesar**.  
  
## <a name="see-also"></a>Vea también  
 [Las consultas de obtención de detalles & #40; minería de datos & #41;](../../analysis-services/data-mining/drillthrough-queries-data-mining.md)  
  
  
