---
title: Hacer una copia de un modelo de minería de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models [Analysis Services], copying
- mining models [Analysis Services], creating
- mining models [Analysis Services], how-to topics
- copying mining models
ms.assetid: 7975bb02-f188-49a0-b7de-5b9b216254ad
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7464c7d780a420b0f95b59ebde02494bd40661e6
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66084219"
---
# <a name="make-a-copy-of-a-mining-model"></a>Realizar una copia de un modelo de minería de datos
  La creación de una copia de un modelo de minería de datos resulta útil para crear rápidamente varios modelos de minería de datos basados en los mismos datos. Una vez copiado el modelo, puede modificar la nueva copia de este si cambia los parámetros o agrega un filtro.  
  
 Por ejemplo, si tiene una tabla Customers que está vinculada a una tabla de compras, puede crear copias para generar modelos de minería de datos independientes para cada dato demográfico de los clientes, filtrando por atributos como la edad o la región.  
  
 Para más información sobre cómo copiar el contenido del modelo (como la representación gráfica o los patrones del modelo) en el Portapapeles para usarlo en otros programas, vea [Copiar una vista de un modelo de minería de datos](copy-a-view-of-a-mining-model.md).  
  
### <a name="to-create-a-related-mining-model"></a>Para crear un modelo de minería relacionado  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], en el Explorador de soluciones, haga clic en la estructura de minería de datos que contiene el modelo de minería.  
  
2.  Haga clic en la pestaña **Modelos de minería de datos** .  
  
3.  Seleccione el modelo y haga clic con el botón secundario del mouse para abrir el menú contextual.  
  
     o bien  
  
     Seleccione el modelo. En el menú **Modelo de minería de datos** , seleccione **Nuevo modelo de minería de datos**.  
  
4.  Escriba un nombre para el nuevo modelo de minería de datos y seleccione un algoritmo. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-edit-the-filter-on-the-copied-mining-model"></a>Para modificar el filtro en el modelo de minería de datos copiado  
  
1.  Seleccione el modelo de minería de datos.  
  
2.  En la ventana **propiedades** , haga clic en el cuadro de texto de la propiedad **filtro** y haga clic en el botón compilar **(...)** .  
  
3.  Cambiar las condiciones de los filtros.  
  
     Para más información sobre cómo usar los cuadros de diálogo del editor de filtros, vea [Aplicar un filtro a un modelo de minería de datos](apply-a-filter-to-a-mining-model.md).  
  
4.  En la ventana **propiedades** , en el `AlgorithmParameters` cuadro de texto, haga clic en **parámetros de establecer**y cambie los parámetros del algoritmo, si lo desea.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte también  
 [Filtros para modelos de minería de datos &#40;Analysis Services-minería de datos&#41;](mining-models-analysis-services-data-mining.md)   
 [Tareas y procedimientos del modelo de minería de datos](mining-model-tasks-and-how-tos.md)   
 [Eliminar un filtro de un modelo de minería de datos](delete-a-filter-from-a-mining-model.md)  
  
  
