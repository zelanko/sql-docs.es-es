---
title: Especificar clave y tipo de dimensión (Asistente para dimensiones) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensionwizard.dimensionkeyandtype.f1
ms.assetid: d7d5db55-36c3-45f6-ade3-29aa516589c1
author: minewiskan
ms.author: owend
ms.openlocfilehash: 019c4ea2744ec27aa7dc24d5065c176551e8cbeb
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84940396"
---
# <a name="specify-dimension-key-and-type-dimension-wizard"></a>Especificar clave y tipo de dimensión (Asistente para dimensiones)
  Use la página **Especificar clave y tipo de dimensión** para definir el atributo clave de la dimensión y para indicar si es una dimensión variable lenta (SCD).  
  
> [!NOTE]  
>   Esta página se muestra solo si ha seleccionado **Generar la dimensión sin un origen de datos** en la página **Seleccionar método de generación** y si ha seleccionado **Dimensión estándar** en la página **Seleccionar el tipo de dimensión** .  
  
## <a name="options"></a>Opciones  
 **Atributo clave**  
 Seleccione el atributo que será el atributo clave para la dimensión.  
  
> [!NOTE]  
>  Si no se ha definido ningún atributo para la dimensión, el único valor disponible para esta opción es **Crear atributo clave automáticamente.** Este valor no está disponible si se define algún atributo para la dimensión.  
  
 **Es una dimensión variable**  
 Seleccione para indicar que la dimensión es una dimensión variable lenta. Al seleccionar esta opción se crean columnas y atributos adicionales que se pueden utilizar para realizar un seguimiento del movimiento de los miembros dentro de las jerarquías de la dimensión a lo largo del tiempo.  
  
## <a name="see-also"></a>Consulte también  
 [Asistente para dimensiones (ayuda F1)](dimension-wizard-f1-help.md)   
 [Dimensiones &#40;Analysis Services de datos multidimensionales&#41;](multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)   
 [Dimensiones en modelos multidimensionales](multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  
