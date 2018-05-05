---
title: Eliminar una columna | Documentos de Microsoft
ms.custom: ''
ms.date: 02/22/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 703db83b-e554-450e-813e-23ad08c1cdad
caps.latest.revision: 5
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: b8980d2b49fde78ef09c8215186b4a0ae17d0bdd
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="delete-a-column"></a>Eliminar una columna 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  En este artículo se describe cómo eliminar una columna de una tabla de modelo tabular.  
  
## <a name="delete-a-model-table-column"></a>Eliminar una columna de tabla modelo  
  
> [!NOTE]  
>  Al eliminar una columna de una tabla de modelo no se elimina la columna de una definición de consulta de partición. Si la columna que va a eliminar forma parte de una partición, debe eliminar manualmente la columna de la definición de consulta de partición. Si no se elimina la columna de la definición de consulta de partición, se consultará la columna y se devolverán datos, pero no se rellenan en la tabla de modelo, durante las operaciones de procesamiento. Para obtener más información, consulte [particiones](../../analysis-services/tabular-models/partitions-ssas-tabular.md).  
  
#### <a name="to-delete-a-model-table-column"></a>Para eliminar una columna de tabla de modelo  
  
-   En el diseñador de modelos, en la tabla que contiene la columna que quiere eliminar, haga clic con el botón derecho en la columna y, después, haga clic en **Eliminar**.  
  
#### <a name="to-delete-a-model-table-column-by-using-the-table-properties-dialog-box"></a>Para eliminar una columna de tabla de modelo mediante el cuadro de diálogo Propiedades de tabla  
  
1.  En el diseñador de modelos, haga clic en la tabla que contiene la columna que desea eliminar, y, a continuación, haga clic en el menú **Tabla** y, a continuación, en  **Propiedades de tabla**.  
  
2.  En **Nombres de columna de**, seleccione **Modelo** (*para usar los nombres de columna de tabla de modelo, si son distintos del origen*).  
  
3.  En el cuadro de diálogo **Editar propiedades de tabla** , en la ventana de vista previa de la tabla, desactive la columna de origen que desee eliminar y haga clic en **Aceptar**.  
  
## <a name="see-also"></a>Vea también  
 [Agregar columnas a una tabla](../../analysis-services/tabular-models/add-columns-to-a-table-ssas-tabular.md)   
 [Particiones](../../analysis-services/tabular-models/partitions-ssas-tabular.md)  
  
  
