---
title: Quitar columnas de una estructura de minería de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining structures [Analysis Services], columns
- removing columns
- deleting columns
- columns [data mining], mining structure columns
ms.assetid: 41073ffe-9351-416b-9f0c-62634bc213f9
author: minewiskan
ms.author: owend
ms.openlocfilehash: 8b2377aa37747a1e6e58f4494129afd2b2adcd78
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/08/2020
ms.locfileid: "84520463"
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
  
## <a name="see-also"></a>Consulte también  
 [Tareas y procedimientos de las estructuras de minería de datos](mining-structure-tasks-and-how-tos.md)  
  
  
