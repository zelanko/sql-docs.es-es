---
title: Eliminar una vista del origen de datos (Analysis Services) | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3b3486aacb727f002b004d079f5e4a17f235ef9c
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34022382"
---
# <a name="delete-a-data-source-view-analysis-services"></a>Eliminar una vista del origen de datos (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Si ha dejado de usar una vista del origen de datos (DSV) en un proyecto de OLAP, puede eliminarla del proyecto en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 La eliminación de una DSV es permanente. No es posible restaurar una DSV eliminada en un proyecto o base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 No se pueden eliminar las DSV de las que dependen otros objetos desde una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] abierta por [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] en el modo en línea. Para eliminar una DSV desde un proyecto que está conectado a una base de datos que se ejecuta en un servidor, primero debe eliminar todos los objetos de la base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que dependen de esa DSV antes de eliminar la DSV.  
  
 Si elimina una DSV, invalidará otros objetos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que dependen de ella, de modo que, antes de eliminar la DSV, verá la lista de objetos que quedarían invalidados cuando se quite la DSV. Revise esta lista con atención para asegurarse de que no contiene objetos que todavía espera usar.  
  
 ![Eliminar objetos, cuadro de diálogo](../../analysis-services/multidimensional-models/media/ssas-olapdsv-deleteobjects.gif "cuadro de diálogo Eliminar objetos")  
  
## <a name="see-also"></a>Vea también  
 [Vistas del origen de datos en modelos multidimensionales](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)   
 [Cambiar las propiedades de una vista del origen de datos & #40; Analysis Services & #41;](../../analysis-services/multidimensional-models/change-properties-in-a-data-source-view-analysis-services.md)  
  
  
