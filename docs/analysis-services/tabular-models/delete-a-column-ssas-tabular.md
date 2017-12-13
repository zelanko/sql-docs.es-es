---
title: Eliminar una columna (SSAS Tabular) | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 703db83b-e554-450e-813e-23ad08c1cdad
caps.latest.revision: "5"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: e8b03c05cb27cdd2e736ad8bc57225408334827e
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="delete-a-column-ssas-tabular"></a>Eliminar una columna (SSAS tabular)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]En este tema se describe cómo eliminar una columna de una tabla de modelo tabular.  
  
## <a name="delete-a-model-table-column"></a>Eliminar una columna de tabla modelo  
  
> [!NOTE]  
>  Al eliminar una columna de una tabla de modelo no se elimina la columna de una definición de consulta de partición. Si la columna que va a eliminar forma parte de una partición, debe eliminar manualmente la columna de la definición de consulta de partición. Si no se elimina la columna de la definición de consulta de partición, se consultará la columna y se devolverán datos, pero no se rellenan en la tabla de modelo, durante las operaciones de procesamiento. Para obtener más información, vea [Particiones &#40;SSAS tabular&#41;](../../analysis-services/tabular-models/partitions-ssas-tabular.md).  
  
#### <a name="to-delete-a-model-table-column"></a>Para eliminar una columna de tabla de modelo  
  
-   En el diseñador de modelos, en la tabla que contiene la columna que quiere eliminar, haga clic con el botón derecho en la columna y, después, haga clic en **Eliminar**.  
  
#### <a name="to-delete-a-model-table-column-by-using-the-table-properties-dialog-box"></a>Para eliminar una columna de tabla de modelo mediante el cuadro de diálogo Propiedades de tabla  
  
1.  En el diseñador de modelos, haga clic en la tabla que contiene la columna que desea eliminar, y, a continuación, haga clic en el menú **Tabla** y, a continuación, en  **Propiedades de tabla**.  
  
2.  En **Nombres de columna de**, seleccione **Modelo** (*para usar los nombres de columna de tabla de modelo, si son distintos del origen*).  
  
3.  En el cuadro de diálogo **Editar propiedades de tabla** , en la ventana de vista previa de la tabla, desactive la columna de origen que desee eliminar y haga clic en **Aceptar**.  
  
## <a name="see-also"></a>Vea también  
 [Agregar columnas a una tabla &#40;SSAS tabular&#41;](../../analysis-services/tabular-models/add-columns-to-a-table-ssas-tabular.md)   
 [Particiones &#40;SSAS tabular&#41;](../../analysis-services/tabular-models/partitions-ssas-tabular.md)  
  
  
