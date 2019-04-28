---
title: Crear consultas de obtención de detalles usando DMX | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 42c896ee-e5ee-4017-b66e-31d1fe66d369
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2ff75840ba60d8ab93a3adeeeef949263e607b35
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62722707"
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
 [Consultas de obtención de detalles &#40;minería de datos&#41;](drillthrough-queries-data-mining.md)   
 [Obtención de detalles en estructuras de minería de datos](drillthrough-on-mining-structures.md)  
  
  
