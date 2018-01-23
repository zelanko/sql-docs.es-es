---
title: "Compatibilidad con traducción en Analysis Services | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Business Intelligence Development Studio, translations [Analysis Services]
- translations [Analysis Services], about translations
- object translations [Analysis Services]
- language identifiers [Analysis Services]
- attribute translations [Analysis Services]
- translations [Analysis Services]
ms.assetid: 018471e0-3c82-49ec-aa16-467fb58a6d5f
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: fc97336300fef2dd621f1f151ff39a04cc3fbfe6
ms.sourcegitcommit: 82c9868b5bf95e5b0c68137ba434ddd37fc61072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/22/2018
---
# <a name="translation-support-in-analysis-services"></a>Compatibilidad con traducción en Analysis Services
[!INCLUDE[ssas-appliesto-sqlas-aas](../includes/ssas-appliesto-sqlas-aas.md)]

  En un modelo de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , puede incrustar varias traducciones de un título o descripción para proporcionar cadenas específicas de la configuración regional que coincidan con cada LCID. En el caso de los modelos multidimensionales, se pueden agregar traducciones del nombre de la base de datos, los objetos del cubo y los objetos de dimensión de la base de datos. En el caso de los modelos tabulares, puede traducir las descripciones y títulos de tabla y columna.  
  
 Al definir una traducción, se crean los metadatos y el título traducido dentro del modelo, pero para que se representen cadenas localizadas en una aplicación cliente, deberá configurar la propiedad **Language** en el objeto o pasar un parámetro **Culture** o **Locale Identifier** en la cadena de conexión (por ejemplo, estableciendo `LocaleIdentifier=1036` para devolver cadenas en francés).  
  
 Utilice **Locale Identifier** si quiere admitir varias traducciones simultáneas del mismo objeto en diferentes idiomas. Si configura la propiedad **Language** , funcionará, pero esto afectará también al procesamiento y a las consultas, lo cual podría tener consecuencias no deseadas. Configurar **Locale Identifier** es la mejor opción, porque solo se utiliza para devolver las cadenas traducidas.  
  
 Una traducción está formada por un identificador de configuración regional (LCID), un título traducido del objeto (por ejemplo, el nombre de la dimensión o el atributo) y, si se quiere, un enlace a una columna que proporciona los valores de los datos en el idioma de destino. Puede tener varias traducciones, pero solo puede utilizar una para cada una de las conexiones. No hay ningún límite teórico en la cantidad de traducciones que puede incrustar en el modelo, pero cada traducción agrega complejidad a las pruebas y todas las traducciones deben compartir la misma intercalación. Por lo tanto, al diseñar la solución, tenga en cuenta estas restricciones naturales.  
  
> [!TIP]  
>  Puede utilizar aplicaciones cliente como Excel, Management Studio y SQL Server Profiler para devolver las cadenas traducidas. Para más información, vea [Sugerencias de globalización y procedimientos recomendados &#40;Analysis Services&#41;](../analysis-services/globalization-tips-and-best-practices-analysis-services.md) .  
  
## <a name="how-to-add-translated-metadata-to-model-in-analysis-services"></a>Incorporación de metadatos traducidos al modelo de Analysis Services  
 Visite estos vínculos para obtener instrucciones paso a paso:  
  
-   [Traducciones en modelos tabulares &#40;Analysis Services&#41;](../analysis-services/tabular-models/translations-in-tabular-models-analysis-services.md)  
  
-   [Traducciones en modelos multidimensionales &#40;Analysis Services&#41;](../analysis-services/multidimensional-models/translations-in-multidimensional-models-analysis-services.md)  
  
## <a name="see-also"></a>Vea también  
 [Escenarios de globalización para Analysis Services](../analysis-services/globalization-scenarios-for-analysis-services.md)   
 [Idiomas e intercalaciones &#40; Analysis Services &#41;](../analysis-services/languages-and-collations-analysis-services.md)   
 [Establecer o cambiar la intercalación de columnas](../relational-databases/collations/set-or-change-the-column-collation.md)   
 [Sugerencias de globalización y mejores prácticas &#40; Analysis Services &#41;](../analysis-services/globalization-tips-and-best-practices-analysis-services.md)  
  
  
