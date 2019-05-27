---
title: Obtener detalles de los datos de casos de un modelo de minería de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- drillthrough [Analysis Services]
ms.assetid: b4d3f350-e543-4ea9-b3a2-b4f7c0a9ae27
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6d683c9dc9a201b1f4351ee00d718ad0d7917606
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66084612"
---
# <a name="drill-through-to-case-data-from-a-mining-model"></a>Obtener detalles de datos de caso a partir de un modelo de minería de datos
  Si un modelo de minería de datos se ha configurado para obtener detalles de los casos de modelos, al examinar el modelo, puede recuperar información detallada sobre los casos que se usaron para crear el modelo. Además, si la estructura de minería de datos subyacente se ha configurado para permitir la obtención de detalles de la estructura de casos, y tiene los permisos adecuados, puede devolver información de la estructura de minería de datos. Puede incluir columnas que no se incluían en el modelo de minería de datos.  
  
 Si la estructura de minería de datos no permite la obtención de detalles de los datos subyacentes, pero sí lo hace el modelo de minería de datos, puede ver la información de los casos de modelo pero no de la estructura de minería de datos.  
  
> [!NOTE]  
>  Puede agregar la capacidad de obtener detalles de un modelo de minería de datos existente estableciendo la propiedad `AllowDrillthrough` en `True`. Sin embargo, después de habilitar la obtención de detalles, para ver los datos del caso, se debe volver a procesar el modelo. Para obtener más información, vea [Habilitar la obtención de detalles para un modelo de minería](enable-drillthrough-for-a-mining-model.md).  
  
 En función del tipo de visor que use, podrá seleccionar el nodo para la obtención de detalles de las maneras siguientes:  
  
|Nombre del visor|Nombre de la pestaña o del panel|Seleccionar nodo|  
|-----------------|----------------------|-----------------|  
|**Visor de árboles de Microsoft**|Pestaña**Árbol de decisión** |Haga clic en un nodo de árbol.<br /><br /> **Tenga en cuenta** evite usar la obtención de detalles en el `All` nodo, porque puede llevar mucho tiempo devolver resultados.|  
|**Visor de clústeres de Microsoft**|**Diagrama del clúster**|Haga clic en un nodo de clúster.|  
|**Visor de clústeres de Microsoft**|**Perfiles del clúster**|Haga clic en cualquier lugar de la columna de clúster.|  
|**Visor de asociación de Microsoft**|Pestaña**Reglas** |Haga clic en una fila que contenga un conjunto de reglas.|  
|**Visor de asociación de Microsoft**|Pestaña**Conjuntos de elementos** |Haga clic en una fila que contenga un conjunto de elementos.|  
|**Visor de agrupación en clústeres de secuencia de Microsoft**|Pestaña**Reglas** |Haga clic en una fila que contenga un conjunto de reglas.|  
|**Visor de agrupación en clústeres de secuencia de Microsoft**|Pestaña**Conjuntos de elementos** |Haga clic en una fila que contenga un conjunto de elementos.|  
  
> [!NOTE]  
>  Algunos modelos no pueden usar la obtención de detalles. La capacidad de usar la obtención de detalles depende del algoritmo usado para crear el modelo. Para obtener una lista de los tipos de modelo de minería de datos que admiten la obtención de detalles, vea [Drillthrough Queries &#40;Data Mining&#41;](drillthrough-queries-data-mining.md).  
  
### <a name="to-view-drillthrough-data-from-a-mining-model"></a>Para ver los datos de obtención de detalles de un modelo de minería de datos  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra la estructura de minería de datos que contiene el modelo de minería de datos que desea.  
  
2.  En el Diseñador de minería de datos, haga clic en la pestaña **Visor de modelo de minería de datos** .  
  
3.  Seleccione el modelo en la lista desplegable **Modelo de minería de datos** .  
  
4.  Seleccione un visor en la lista desplegable **Visor** y haga clic con el botón derecho en el nodo específico.  
  
5.  Seleccione **Obtener detalles**y, a continuación, seleccione **Solo columnas de modelos**o **Columnas de modelo y estructura** para abrir la ventana **Obtener detalles** .  
  
6.  Para copiar los datos en el Portapapeles, haga clic con el botón derecho en cualquier fila de la tabla y seleccione **Copiar todo**.  
  
## <a name="see-also"></a>Vea también  
 [Consultas de obtención de detalles &#40;minería de datos&#41;](drillthrough-queries-data-mining.md)  
  
  
