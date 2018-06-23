---
title: Definir períodos de tiempo (Asistente para dimensiones) | Documentos de Microsoft
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
- sql12.asvs.dimensionwizard.timefrequency.f1
ms.assetid: 6bda6b7e-d306-4e68-9acb-84de8f44d1b4
caps.latest.revision: 21
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 6d0eaa7b29e84be26032618fe7470652adc1a7b6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36196851"
---
# <a name="define-time-periods-dimension-wizard"></a>Definir períodos de tiempo (Asistente para dimensiones)
  Use la página **Definir períodos de tiempo** para definir la información del año natural y las frecuencias de tiempo que se deben incluir en la dimensión de tiempo o en la dimensión de tiempo de servidor.  
  
> [!NOTE]  
>  Esta página se muestra solo si se ha seleccionado la opción **Dimensión de tiempo de servidor** en la página **Seleccionar el tipo de dimensión** , o si se ha seleccionado la opción **Build the dimension without using a data source** (Generar la dimensión sin un origen de datos) en la página **Select Build Method** (Seleccionar método de generación) y se ha seleccionado **Dimensión de tiempo** en la página **Seleccionar el tipo de dimensión** .  
  
> [!IMPORTANT]  
>  Esta página se usa para definir el año natural de una dimensión de tiempo. Para definir un año fiscal, de fabricación, de informe u 8601 ISO (Organización Internacional de Normalización) para la dimensión de tiempo, use la página **Seleccionar calendarios** .  
  
## <a name="options"></a>Opciones  
 **Primer día natural**  
 Escriba o seleccione el día en el que se inicia el año actual.  
  
 **Último día natural**  
 Escriba o seleccione el día en el que finaliza el año actual.  
  
 **Primer día de la semana**  
 Seleccione el día en el que se inicia una semana.  
  
 **Períodos de tiempo**  
 Seleccione los períodos de tiempo para el año natural de la dimensión de tiempo.  
  
> [!NOTE]  
>  El período de tiempo `Date` es obligatorio.  
  
 **Idioma para los nombres de miembro de hora**  
 Seleccione el idioma de los miembros de dimensión de tiempo.  
  
## <a name="see-also"></a>Vea también  
 [Asistente de dimensiones (Ayuda F1)](dimension-wizard-f1-help.md)   
 [Dimensiones &#40;Analysis Services - datos multidimensionales&#41;](multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)   
 [Dimensiones en modelos multidimensionales](multidimensional-models/dimensions-in-multidimensional-models.md)   
 [Seleccionar calendarios &#40;Asistente para dimensiones&#41;](select-calendars-dimension-wizard.md)  
  
  