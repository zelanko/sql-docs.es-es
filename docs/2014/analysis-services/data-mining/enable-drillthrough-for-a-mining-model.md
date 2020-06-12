---
title: Habilitar la obtención de detalles para un modelo de minería de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining [Analysis Services], how-to topics
- drillthrough [Analysis Services]
ms.assetid: 4fa44f60-ef9a-4b59-98c0-c0baf1195c8e
author: minewiskan
ms.author: owend
ms.openlocfilehash: 0a6adfc389776f91132e527130f50f61c9783d9f
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/08/2020
ms.locfileid: "84522491"
---
# <a name="enable-drillthrough-for-a-mining-model"></a>Habilitar la obtención de detalles para un modelo de minería
  Si ha habilitado la obtención de detalles para un modelo de minería de datos, al examinar el modelo, puede recuperar información detallada sobre los casos que se usaron para crear el modelo. Para ver esta información, debe tener los permisos necesarios y se debe de haber procesado la estructura.  
  
 **Permisos** : para que un usuario obtenga detalles de los datos del modelo o de los datos de la estructura, el usuario debe ser miembro de un rol con permisos [AllowDrillThrough](https://docs.microsoft.com/bi-reference/assl/properties/allowdrillthrough-element-assl) en el modelo o en la estructura de minería de datos. Los permisos de obtención de detalles se establecen por separado en la estructura y en el modelo.  
  
-   Los permisos de obtención de detalles en el modelo permiten obtener detalles del modelo, incluso si no se dispone de permisos en la estructura.  
  
-   Los permisos de obtención de detalles en la estructura ofrecen la posibilidad adicional de incluir columnas de la estructura en las consultas de obtención de detalles del modelo, mediante la función [StructureColumn &#40;DMX&#41;](/sql/dmx/structurecolumn-dmx). También puede consultar los casos de prueba y entrenamiento de la estructura mediante el uso de la instrucción SELECT... DESDE \<structure> . Sintaxis de CASEs.  
  
 **Almacenamiento en caché de casos de entrenamiento** : la obtención de detalles funciona recuperando información sobre los casos de entrenamiento de la estructura de minería de datos. Esta información se almacena en la caché cuando se procesa la estructura. Por consiguiente, si decide borrar todos los datos de la caché cambiando la propiedad <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> a `ClearAfterProcessing`, la obtención de detalles no funcionará.  
  
> [!NOTE]  
>  Si los casos de entrenamiento no se han almacenado en la caché, deberá cambiar la propiedad <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> a **KeepTrainingCases** y, después, deberá volver a procesar el modelo antes de ver los datos de los casos.  
  
 Para obtener más información, vea [Consultas de obtención de detalles &#40;minería de datos&#41;](drillthrough-queries-data-mining.md).  
  
### <a name="to-enable-drillthrough-on-a-mining-model"></a>Para habilitar la obtención de detalles en un modelo de minería de datos  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], en la pestaña **Modelos de minería de datos** del Diseñador de minería de datos, haga clic con el botón derecho en el nombre del modelo de minería de datos del que quiere habilitar la obtención de detalles y seleccione **Propiedades**.  
  
2.  En las ventanas **propiedades** , haga clic en **AllowDrillthrough**y seleccione **true**.  
  
3.  En la pestaña **modelos de minería de datos** , haga clic con el botón secundario en el modelo y seleccione **procesar modelo**.  
  
### <a name="to-enable-caching-for-a-mining-structure"></a>Para habilitar el almacenamiento en caché para una estructura de minería de datos  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], en la pestaña **Estructura de minería de datos** del Diseñador de minería de datos, haga clic con el botón derecho en el nombre de la estructura de minería de datos.  
  
2.  Abra la ventana **Propiedades** .  
  
3.  En la ventana **Propiedades** , busque la propiedad **CacheMode** y seleccione **KeepTrainingCases** en la lista.  
  
4.  En el menú **Base de datos** , seleccione **Procesar**.  
  
## <a name="see-also"></a>Consulte también  
 [Consultas de obtención de detalles &#40;minería de datos&#41;](drillthrough-queries-data-mining.md)  
  
  
