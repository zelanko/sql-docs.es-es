---
title: Destino de procesamiento de dimensiones | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.dimensionprocessingdest.f1
helpviewer_keywords:
- Dimension Processing destination
- loading dimensions
- destinations [Integration Services], Dimension Processing
- dimensions [Analysis Services], processing
ms.assetid: 4c49bb95-7259-42f4-a785-bb6aaf5f8566
caps.latest.revision: 39
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 139058c982315f12141d55c315a18554d4babd4a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37217725"
---
# <a name="dimension-processing-destination"></a>procesamiento de dimensiones, destino
  El destino de Procesamiento de dimensiones carga y procesa una dimensión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Para más información sobre las dimensiones, vea [Dimensiones &#40;Analysis Services - Datos multidimensionales&#41;](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md).  
  
 El destino de Procesamiento de dimensiones incluye las siguientes características:  
  
-   Opciones para ejecutar procesamiento incremental, completo o de actualización.  
  
-   Configuración de errores, para especificar si el procesamiento de dimensiones debe pasar por alto los errores o detenerse después de una cantidad de errores especificada.  
  
-   Asignación de las columnas de entrada a columnas en tablas de dimensiones.  
  
 Para más información sobre el procesamiento de objetos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], vea [Opciones y valores de procesamiento &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md).  
  
## <a name="configuration-of-the-dimension-processing-destination"></a>Configuración del destino de Procesamiento de dimensiones  
 El destino de Procesamiento de dimensiones usa un administrador de conexiones de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para conectarse al proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que contiene las dimensiones que procesa el destino. Para más información, consulte [Analysis Services Connection Manager](../connection-manager/analysis-services-connection-manager.md).  
  
 Este destino tiene una entrada. No admite una salida de error.  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información sobre las propiedades que se pueden establecer en el cuadro de diálogo **Editor de destino de procesamiento de dimensiones** , haga clic en uno de los siguientes temas:  
  
-   [Editor de destino de procesamiento de dimensiones &#40;página Administrador de conexiones&#41;](../dimension-processing-destination-editor-connection-manager-page.md)  
  
-   [Editor de destino de procesamiento de dimensiones &#40;página asignaciones&#41;](../dimension-processing-destination-editor-mappings-page.md)  
  
-   [Editor de destino de procesamiento de dimensiones &#40;página Opciones avanzadas&#41;](../dimension-processing-destination-editor-advanced-page.md)  
  
 El cuadro de diálogo **Editor avanzado** indica las propiedades que se pueden establecer mediante programación. Para obtener más información acerca de las propiedades que puede establecer a través del cuadro de diálogo **Editor avanzado** o mediante programación, haga clic en uno de los temas siguientes:  
  
-   [Common Properties](../common-properties.md)  
  
 Para más información sobre cómo establecer las propiedades, vea [Establecer las propiedades de un componente de flujo de datos](set-the-properties-of-a-data-flow-component.md).  
  
## <a name="see-also"></a>Vea también  
 [Flujo de datos](data-flow.md)   
 [Transformaciones de Integration Services](transformations/integration-services-transformations.md)  
  
  
