---
title: Crear consultas de obtención de detalles usando DMX | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 42c896ee-e5ee-4017-b66e-31d1fe66d369
caps.latest.revision: 5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 72c540463b5bf2b1dff262731fddbc5d258a1de6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37151706"
---
# <a name="create-drillthrough-queries-using-dmx"></a>Crear consultas de obtención de detalles usando DMX
  Para todos los modelos que admitan la obtención de detalles, puede recuperar los datos de los casos y los datos de la estructura creando una consulta DMX en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o en cualquier otro cliente que soporte DMX.  
  
> [!WARNING]  
>  Para ver los datos, debe estar habilitada la obtención de detalles y es necesario tener los permisos necesarios.  
  
## <a name="specifying-drillthrough-options"></a>Especificar las opciones de la obtención de detalles  
 La sintaxis general para recuperar los casos de modelos y de estructuras es la siguiente:  
  
```  
SELECT <model column list>, StructureColumn('<structure column name') FROM <modelname>.CASES  
```  
  
 Para más información sobre el uso de consultas DMX para devolver datos de casos, vea [SELECT FROM &#60;model&#62;.CASES &#40;DMX&#41;](/sql/dmx/select-from-model-content-dmx) y [SELECT FROM &#60;estructura&#62;.CASES](/sql/dmx/select-from-structure-cases).  
  
## <a name="examples"></a>Ejemplos  
 La siguiente consulta DMX devuelve los datos de los casos para una serie de productos concreta de un modelo de serie temporal. La consulta también devuelve la columna `Amount`, que no se usó en el modelo pero que está disponible en la estructura de minería de datos.  
  
```  
SELECT [DateSeries], [Model Region], Quantity, StructureColumn('Amount') AS [M200 Pacific Amount]  
FROM Forecasting.CASES  
WHERE [Model Region] = 'M200 Pacific'  
```  
  
 Observe que en este ejemplo, se ha usado un alias para cambiar el nombre de la columna de estructura. Si no asigna un alias a la columna de estructura, la columna se devuelve con el nombre 'Expression'. Este es el comportamiento predeterminado para todas las columnas sin nombre.  
  
## <a name="see-also"></a>Vea también  
 [Las consultas de obtención de detalles &#40;minería de datos&#41;](drillthrough-queries-data-mining.md)   
 [Obtención de detalles en estructuras de minería de datos](drillthrough-on-mining-structures.md)  
  
  
