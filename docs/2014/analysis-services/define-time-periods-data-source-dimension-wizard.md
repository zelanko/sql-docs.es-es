---
title: Definir períodos de tiempo (origen de datos) (Asistente para dimensiones) | Documentos de Microsoft
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
- sql12.asvs.dimensionwizard.timeperioddefinition.f1
ms.assetid: a5e6b9ff-69fa-4896-a840-de2b3e063ca9
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 2c20dc34617590c5e4d1ab7134378afb2b7cfb93
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36105275"
---
# <a name="define-time-periods-data-source-dimension-wizard"></a>Definir períodos de tiempo (Origen de datos, Asistente para dimensiones)
  Use la página **Definir períodos de tiempo** para definir los atributos que representan los períodos de tiempo en la dimensión de tiempo con columnas en la tabla especificada en la página **Seleccionar el tipo de dimensión** .  
  
> [!NOTE]  
>  Solo se mostrará esta página si ha seleccionado **Build the dimension using a data source** (Generar la dimensión con un origen de datos) en la página **Dimension Definition** (Definición de dimensión) y **Dimensión de tiempo** en la página **Seleccionar el tipo de dimensión** .  
  
## <a name="options"></a>Opciones  
 **Nombre de la propiedad de tiempo**  
 Muestra los tipos de atributos utilizados para indicar períodos de tiempo con dimensiones de tiempo. Para más información sobre tipos de atributo, vea [Elemento Type &#40;DimensionAttribute&#41; &#40;ASSL&#41;](scripting/properties/type-element-dimensionattribute-assl.md).  
  
> [!NOTE]  
>  El tipo de atributo `Date` solo debe utilizarse para las columnas con un tipo de datos DateTime.  
  
 **Columnas de la tabla de tiempo**  
 Muestra las columnas en las que se basarán los tipos de atributos correspondientes.  
  
 Para cambiar la columna, haga clic en la columna y, a continuación, seleccione otra columna de la lista.  
  
## <a name="see-also"></a>Vea también  
 [Asistente de dimensiones (Ayuda F1)](dimension-wizard-f1-help.md)   
 [Dimensiones &#40;Analysis Services - datos multidimensionales&#41;](multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)   
 [Dimensiones en modelos multidimensionales](multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  