---
title: Realizar una copia de un modelo de minería de datos | Documentos de Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f78d5842ec0400afd51b8adce1bf1efc65a604b8
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="make-a-copy-of-a-mining-model"></a>Realizar una copia de un modelo de minería de datos
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  La creación de una copia de un modelo de minería de datos resulta útil para crear rápidamente varios modelos de minería de datos basados en los mismos datos. Una vez copiado el modelo, puede modificar la nueva copia de este si cambia los parámetros o agrega un filtro.  
  
 Por ejemplo, si tiene una tabla Customers que está vinculada a una tabla de compras, puede crear copias para generar modelos de minería de datos independientes para cada dato demográfico de los clientes, filtrando por atributos como la edad o la región.  
  
 Para más información sobre cómo copiar el contenido del modelo (como la representación gráfica o los patrones del modelo) en el Portapapeles para usarlo en otros programas, vea [Copiar una vista de un modelo de minería de datos](../../analysis-services/data-mining/copy-a-view-of-a-mining-model.md).  
  
### <a name="to-create-a-related-mining-model"></a>Para crear un modelo de minería relacionado  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], en el Explorador de soluciones, haga clic en la estructura de minería de datos que contiene el modelo de minería.  
  
2.  Haga clic en la pestaña **Modelos de minería de datos** .  
  
3.  Seleccione el modelo y haga clic con el botón secundario del mouse para abrir el menú contextual.  
  
     O bien  
  
     Seleccione el modelo. En el menú **Modelo de minería de datos** , seleccione **Nuevo modelo de minería de datos**.  
  
4.  Escriba un nombre para el nuevo modelo de minería de datos y seleccione un algoritmo. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-edit-the-filter-on-the-copied-mining-model"></a>Para modificar el filtro en el modelo de minería de datos copiado  
  
1.  Seleccione el modelo de minería de datos.  
  
2.  En la ventana **Propiedades** , haga clic en el cuadro de texto de la propiedad **Filter** y luego haga clic en el botón de generación **(…)** .  
  
3.  Cambiar las condiciones de los filtros.  
  
     Para más información sobre cómo usar los cuadros de diálogo del editor de filtros, vea [Aplicar un filtro a un modelo de minería de datos](../../analysis-services/data-mining/apply-a-filter-to-a-mining-model.md).  
  
4.  En la ventana **Propiedades** , en el cuadro de texto **AlgorithmParameters** , haga clic en **Establecer parámetros de algoritmo**y cambie los parámetros del algoritmo si eso es lo que quiere.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Filtros para modelos de minería de datos & #40; Analysis Services: minería de datos & #41;](../../analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md)   
 [Tareas y tareas de modelo de minería de datos](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)   
 [Eliminar un filtro de un modelo de minería de datos](../../analysis-services/data-mining/delete-a-filter-from-a-mining-model.md)  
  
  
