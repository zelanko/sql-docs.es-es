---
title: "Quitar columnas de una estructura de minería de datos | Documentos de Microsoft"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mining structures [Analysis Services], columns
- removing columns
- deleting columns
- columns [data mining], mining structure columns
ms.assetid: 41073ffe-9351-416b-9f0c-62634bc213f9
caps.latest.revision: "27"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: d7dc82033994b08f45283bf03bcae11d441c1b60
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="remove-columns-from-a-mining-structure"></a>Quitar columnas de una estructura de minería de datos
  Puede usar el Diseñador de minería de datos para quitar columnas de la estructura de minería de datos después de que haya sido creada. Algunos ejemplos de razones para quitar una columna de la estructura de minería de datos son:  
  
-   La estructura de minería de datos contiene varias copias de una columna y quiere evitar el uso de datos duplicados en un modelo.  
  
-   Los datos deberían estar protegidos, pero se ha habilitado la obtención de detalles.  
  
-   Los datos no se usan en el modelado y no deben procesarse.  
  
 Eliminar una columna de la estructura de minería de datos no cambia la columna en la vista del origen de datos o en los datos externos; solamente se suprimen los metadatos. Sin embargo, cuando cambia las columnas usadas en la estructura de minería de datos, debe volver a procesar la estructura y cualquier modelo basado en ella.  
  
### <a name="to-remove-a-column-from-the-mining-structure"></a>Para quitar una columna de la estructura de minería de datos  
  
1.  Seleccione la pestaña **Estructura de minería de datos** en el Diseñador de minería de datos.  
  
2.  Expanda el árbol de la estructura de minería de datos para mostrar todas las columnas.  
  
3.  Haga clic con el botón derecho en la columna que quiera eliminar y, después, seleccione **Eliminar**.  
  
4.  En el cuadro de diálogo **Eliminar objetos** , haga clic en **Aceptar**.  
  
## <a name="see-also"></a>Vea también  
 [Tareas y procedimientos de las estructuras de minería de datos](../../analysis-services/data-mining/mining-structure-tasks-and-how-tos.md)  
  
  
