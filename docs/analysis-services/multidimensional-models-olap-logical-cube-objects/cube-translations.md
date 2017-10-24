---
title: Traducciones de cubo | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- multiple language support [Analysis Services]
- international considerations [Analysis Services]
- global considerations [Analysis Services]
- cubes [Analysis Services], translations
- OLAP objects [Analysis Services], translations
- translations [Analysis Services], cubes
ms.assetid: 4e4fd6a4-d324-4508-b75a-2a57de9ab8ff
caps.latest.revision: 41
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ecd500f3b661f6f6d59746c907ed60a5a31ff495
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="cube-translations"></a>Traducciones de cubo
  Una traducción es un mecanismo simple para cambiar las etiquetas y títulos mostrados de un idioma a otro. Cada traducción se define como un par de valores: una cadena con el texto traducido y un número con el identificador de idioma. Todos los objetos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] disponen de traducción. Las dimensiones también pueden tener los valores de atributo traducidos. La aplicación cliente es responsable de localizar la configuración de idioma que el usuario ha definido y efectuar el cambio para mostrar todos los títulos y etiquetas en dicho idioma. Un objeto puede tener tantas traducciones como se desee.  
  
 Un objeto <xref:Microsoft.AnalysisServices.Translation> simple está compuesto por el número del identificador de idioma y el título traducido. El número de Id. de idioma es un **entero** con el identificador de idioma. El título traducido es el texto traducido.  
  
 En [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], una traducción de cubo es una representación específica del lenguaje del nombre de un objeto de cubo, como un título o una carpeta para mostrar. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] también admite traducciones de nombres de dimensión y de miembro.  
  
 Las traducciones ofrecen compatibilidad de servidor para aplicaciones cliente que admitan varios idiomas. Con frecuencia, usuarios de distintos países ven los datos de un cubo. Resulta útil poder traducir los distintos elementos de un cubo a diferentes idiomas para que los usuarios de estos idiomas puedan ver y comprender los metadatos del cubo. Por ejemplo, un usuario corporativo en Francia puede obtener acceso a un cubo desde una estación de trabajo con una configuración regional en francés y ver los valores de las propiedades del objeto en francés. Igualmente, un usuario corporativo en Alemania puede obtener acceso al mismo cubo desde una estación de trabajo con una configuración regional en alemán y ver los valores de las propiedades del objeto en alemán.  
  
 La información de intercalación e idioma para el equipo cliente se almacena con formato de identificador de configuración regional (LCID). Tras la conexión, el cliente pasa el LCID a la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. La instancia utiliza el LCID para determinar el conjunto de traducciones que se utiliza al proporcionar metadatos de objetos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] a cada usuario corporativo. Si un objeto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no contiene la traducción especificada, el idioma predeterminado se utiliza para devolver el contenido al cliente.  
  
## <a name="see-also"></a>Vea también  
 [Traducciones de dimensiones](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimension-translations.md)   
 [Compatibilidad con traducción en Analysis Services](../../analysis-services/translation-support-in-analysis-services.md)   
 [Sugerencias de globalización y mejores prácticas &#40; Analysis Services &#41;](../../analysis-services/globalization-tips-and-best-practices-analysis-services.md)  
  
  

