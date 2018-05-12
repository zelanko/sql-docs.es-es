---
title: Definir una relación normal y las propiedades de relación normal | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9ee79742f919d7f47ae73968666d96622e3429bc
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="define-a-regular-relationship-and-regular-relationship-properties"></a>Definir relaciones normales y propiedades de las relaciones normales
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Al definir una nueva dimensión de cubo o un nuevo grupo de medida, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] intentará detectar si existe una relación normal y, a continuación, establecerá la configuración de uso de la dimensión en **Normal**. Puede ver o modificar una relación de dimensión normal en la pestaña **Uso de dimensiones** del Diseñador de cubos.  
  
 Al definir la relación de una dimensión de cubo con un grupo de medida, también se especifica el atributo de granularidad de esa relación. El atributo de granularidad define el nivel mínimo de detalle disponible en el cubo para dicha dimensión, que suele ser el atributo clave de la dimensión. Sin embargo, en algunos casos, quizás desee establecer la granularidad de determinada dimensión de cubo de determinado grupo de medida en otra granularidad. Por ejemplo, si utiliza un grupo de medida Sales Quotas o Budget, quizás desee establecer el atributo de granularidad de la dimensión Time en el atributo Month, no en el atributo Day. Al especificar que el atributo de granularidad sea distinto del atributo clave, se debe garantizar que los demás atributos de la dimensión estén directa o indirectamente vinculados a este otro atributo por medio de relaciones de atributo. De lo contrario, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no podrá agregar los datos correctamente.  
  
  
