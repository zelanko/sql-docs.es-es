---
title: Quitar columnas de una estructura de minería de datos | Documentos de Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: bd8691d8ec0cc1546e27e8195e7d0bbc20709f59
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34015882"
---
# <a name="remove-columns-from-a-mining-structure"></a>Quitar columnas de una estructura de minería de datos
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
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
 [Tareas de estructura de minería de datos y procedimientos](../../analysis-services/data-mining/mining-structure-tasks-and-how-tos.md)  
  
  
