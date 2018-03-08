---
title: Eliminar relaciones | Documentos de Microsoft
ms.custom: 
ms.date: 02/22/2018
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: multidimensional-tabular
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d40e3f05-54e8-4c4b-807a-0b06f446079b
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 690224c1798494e75f6b26add07d51c3afa7134f
ms.sourcegitcommit: d8ab09ad99e9ec30875076acee2ed303d61049b7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/23/2018
---
# <a name="delete-relationships"></a>Eliminar relaciones 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
Puede eliminar las relaciones existentes utilizando el diseñador de modelos en la Vista de diagrama o utilizando el cuadro de diálogo Administrar relaciones. Para obtener información acerca de cómo se usan las relaciones en los modelos tabulares, vea [relaciones](../../analysis-services/tabular-models/relationships-ssas-tabular.md).  
  
## <a name="considerations-for-deleting-relationships"></a>Consideraciones para eliminar relaciones  
 Tenga en cuenta los siguientes problemas a la hora de decidir si va a eliminar una relación:  
  
-   No hay ninguna manera de deshacer la eliminación de una relación. Puede volver a crearla, pero esta acción requiere que se vuelvan a calcular completamente las fórmulas del modelo. Por consiguiente, compruebe siempre si una relación se usa en fórmulas antes de eliminarla.  
  
-   Eliminar una relación entre dos tablas puede provocar errores en las fórmulas que hacen referencia a estas tablas.  
  
-   La función RELATED de las Expresiones de análisis de datos (DAX) usa las relaciones entre tablas para buscar valores relacionados en otra tabla. Devolverá resultados diferentes una vez eliminada la relación. Para obtener más información, vea la función RELATED (DAX).  
  
-   Además de cambiar los resultados de las fórmulas y las tablas dinámicas, tanto la creación como la eliminación de relaciones harán que el libro se vuelva a calcular, lo que puede tardar algún tiempo.  
  
## <a name="delete-relationships"></a>Eliminar relaciones  
  
#### <a name="to-delete-a-relationship-by-using-diagram-view"></a>Para eliminar una relación utilizando la Vista de diagrama  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], haga clic en el menú **Modelo** , elija **Vista de modelo**y haga clic en **Vista de diagrama**.  
  
2.  Haga clic con el botón derecho en una línea de relación entre dos tablas y, después, haga clic en **Eliminar**.  
  
#### <a name="to-delete-a-relationship-by-using-the-manage-relationships-dialog-box"></a>Para eliminar una relación utilizando el cuadro de diálogo Administrar relaciones  
  
1.  En [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], haga clic en el menú **Tabla** y, a continuación, haga clic en **Administrar relaciones**.  
  
2.  En el cuadro de diálogo **Administrar relaciones** , seleccione una o más relaciones en la lista.  
  
     Para seleccionar varias relaciones, mantenga presionada la tecla CTRL mientras hace clic en cada una.  
  
3.  Haga clic en **Eliminar relación**.  
  
4.  En el cuadro de diálogo **Administrar las relaciones** , haga clic en **Cerrar**.  
  
## <a name="see-also"></a>Vea también  
 [Relaciones](../../analysis-services/tabular-models/relationships-ssas-tabular.md)   
 [Crear una relación](../../analysis-services/tabular-models/create-a-relationship-between-two-tables-ssas-tabular.md)  
  
  
