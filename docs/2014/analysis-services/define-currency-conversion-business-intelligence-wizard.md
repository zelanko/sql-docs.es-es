---
title: Definir la conversión de moneda (Asistente de Business Intelligence) | Documentos de Microsoft
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
- sql12.asvs.biwizard.currencyconversion.existingscriptpage.f1
ms.assetid: 37dd65b7-9d8d-44ad-b316-96a92c622472
caps.latest.revision: 21
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: ec54aa4e66cbcd9872dbce03bdb3e7c601c84980
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36198305"
---
# <a name="define-currency-conversion-business-intelligence-wizard"></a>Definir la conversión de moneda (Asistente de Business Intelligence)
  Use la página **Definir la conversión de moneda** para revisar el script MDX (Expresiones multidimensionales) que contiene la funcionalidad de conversión de moneda generada por el Asistente de Business Intelligence. A continuación, puede utilizar el script MDX generado por este asistente para sobrescribir o agregar la funcionalidad de conversión de moneda definida previamente en el script MDX del cubo.  
  
> [!NOTE]  
>  Esta página solo aparecerá si el Asistente de Business Intelligence detecta como mínimo una conversión de moneda definida previamente en el script MDX del cubo. En el script MDX del cubo, las conversiones de moneda se encuadran con los siguientes comentarios:  
>   
>  `//<Currency conversion>`  
>   
>  `...`  
>   
>  `[MDX statements for the currency conversion]`  
>   
>  `...`  
>   
>  `//</Currency conversion>`  
>   
>  Si cambia o quita estos comentarios, el Asistente de Business Intelligence quizás no pueda detectar una conversión de moneda definida previamente.  
  
## <a name="options"></a>Opciones  
 **Nuevo script de conversión de moneda**  
 Muestra el script MDX generado por la sesión actual del Asistente de Business Intelligence.  
  
 **Sobrescribir el script de conversión de moneda existente**  
 Seleccione esta opción para sobrescribir el script MDX mostrado en **Script de conversión de moneda existente** con el script MDX mostrado en **Nuevo script de conversión de moneda**.  
  
 **Anexar después de**  
 Seleccione esta opción para anexar el script MDX mostrado en **Nuevo script de conversión de moneda** al final del script MDX mostrado en **Script de conversión de moneda existente**. El script anexado aparece como una sección nueva.  
  
 **Script de conversión de moneda existente**  
 Seleccione la sección del script MDX existente que contiene la funcionalidad de conversión de moneda definida previamente que se sobrescribirá o anexará.  
  
## <a name="see-also"></a>Vea también  
 [Ayuda de F1 de Asistente de Business Intelligence](business-intelligence-wizard-f1-help.md)   
 [Diseñador de cubos &#40;Analysis Services - datos multidimensionales&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [Diseñador de dimensiones &#40;Analysis Services - datos multidimensionales&#41;](dimension-designer-analysis-services-multidimensional-data.md)  
  
  