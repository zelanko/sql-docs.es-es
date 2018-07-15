---
title: Definir un nuevo atributo automáticamente | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- automatic attribute creation
- attributes [Analysis Services], creating
ms.assetid: 208a050a-5e2f-470c-b645-8d835e123db7
caps.latest.revision: 33
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 74b4e1950e6a31675994b7cae1562ff92a56de4a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37299195"
---
# <a name="define-a-new-attribute-automatically"></a>Definir un nuevo atributo automáticamente
  Puede crear un atributo nuevo en una dimensión con la edición de tipo arrastrar y colocar del Diseñador de dimensiones.  
  
### <a name="to-create-a-new-attribute-automatically"></a>Para crear un nuevo atributo automáticamente  
  
1.  En el Diseñador de dimensiones, abra la dimensión en la que desea crear el atributo.  
  
2.  En la pestaña **Estructura de dimensión** , en el panel **Vista del origen de datos** , seleccione la columna dentro de la tabla a la que desee enlazar el atributo y arrástrela al panel **Atributos** .  
  
     [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] crea el nuevo atributo con el mismo nombre que la columna con la que está enlazado. Si hay varios atributos que utilizan la misma columna, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] anexará un número al nombre de atributo.  
  
## <a name="see-also"></a>Vea también  
 [Dimensiones en modelos multidimensionales](dimensions-in-multidimensional-models.md)   
 [Referencia de las propiedades de los atributos de dimensión](dimension-attribute-properties-reference.md)  
  
  
