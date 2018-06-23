---
title: Especificar clave de dimensión y el tipo (Asistente para dimensiones) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.dimensionwizard.dimensionkeyandtype.f1
ms.assetid: d7d5db55-36c3-45f6-ade3-29aa516589c1
caps.latest.revision: 22
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 1ce08115251beee6dc71509bc4d3a53420ecd678
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36196312"
---
# <a name="specify-dimension-key-and-type-dimension-wizard"></a>Especificar clave y tipo de dimensión (Asistente para dimensiones)
  Use la página **Especificar clave y tipo de dimensión** para definir el atributo clave de la dimensión y para indicar si es una dimensión variable lenta (SCD).  
  
> [!NOTE]  
>  Esta página se muestra solo si ha seleccionado **Generar la dimensión sin un origen de datos** en la página **Seleccionar método de generación** y si ha seleccionado **Dimensión estándar** en la página **Seleccionar el tipo de dimensión** .  
  
## <a name="options"></a>Opciones  
 **Atributo clave**  
 Seleccione el atributo que será el atributo clave para la dimensión.  
  
> [!NOTE]  
>  Si no se ha definido ningún atributo para la dimensión, el único valor disponible para esta opción es **Crear atributo clave automáticamente.** Este valor no está disponible si se define algún atributo para la dimensión.  
  
 **Se trata de una dimensión variable**  
 Seleccione para indicar que la dimensión es una dimensión variable lenta. Al seleccionar esta opción se crean columnas y atributos adicionales que se pueden utilizar para realizar un seguimiento del movimiento de los miembros dentro de las jerarquías de la dimensión a lo largo del tiempo.  
  
## <a name="see-also"></a>Vea también  
 [Asistente de dimensiones (Ayuda F1)](dimension-wizard-f1-help.md)   
 [Dimensiones &#40;Analysis Services - datos multidimensionales&#41;](multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)   
 [Dimensiones en modelos multidimensionales](multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  