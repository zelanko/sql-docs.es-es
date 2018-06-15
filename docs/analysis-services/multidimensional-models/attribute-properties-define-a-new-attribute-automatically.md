---
title: Definir un nuevo atributo automáticamente | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5368288930526435682723ba8f50d878ff029ce1
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34021712"
---
# <a name="attribute-properties---define-a-new-attribute-automatically"></a>Propiedades de atributo: definir un nuevo atributo automáticamente
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Puede crear un atributo nuevo en una dimensión con la edición de tipo arrastrar y colocar del Diseñador de dimensiones.  
  
### <a name="to-create-a-new-attribute-automatically"></a>Para crear un nuevo atributo automáticamente  
  
1.  En el Diseñador de dimensiones, abra la dimensión en la que desea crear el atributo.  
  
2.  En la pestaña **Estructura de dimensión** , en el panel **Vista del origen de datos** , seleccione la columna dentro de la tabla a la que desee enlazar el atributo y arrástrela al panel **Atributos** .  
  
     [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]crea el nuevo atributo con el mismo nombre que la columna con la que está enlazado. Si hay varios atributos que utilizan la misma columna, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] anexará un número al nombre de atributo.  
  
## <a name="see-also"></a>Vea también  
 [Dimensiones en modelos multidimensionales](../../analysis-services/multidimensional-models/dimensions-in-multidimensional-models.md)   
 [Referencia de propiedades de atributos de dimensión](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)  
  
  
