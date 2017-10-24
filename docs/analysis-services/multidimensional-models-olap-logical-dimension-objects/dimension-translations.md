---
title: Traducciones de dimensiones | Documentos de Microsoft
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
- dimensions [Analysis Services], translations
- multiple language support [Analysis Services]
- international considerations [Analysis Services]
- global considerations [Analysis Services]
- LCIDs
- translations [Analysis Services], dimensions
ms.assetid: 38fc1e05-2ac9-4816-b52b-dfd19c3a43a2
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 16291e847c84e884d4308d8c67fa512fbb821cdf
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="dimension-translations"></a>Traducciones de dimensiones
  Una traducción es un mecanismo simple para cambiar las etiquetas y títulos mostrados de un idioma a otro. Cada traducción se define como un par de valores: una cadena con el texto traducido y un número con el identificador de idioma. Todos los objetos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] disponen de traducción. Las dimensiones también pueden tener los valores de atributo traducidos. La aplicación cliente es responsable de localizar la configuración de idioma que el usuario ha definido y efectuar el cambio para mostrar todos los títulos y etiquetas en dicho idioma. Un objeto puede tener tantas traducciones como se desee.  
  
 Un objeto <xref:Microsoft.AnalysisServices.Translation> simple está compuesto por el número del identificador de idioma y el título traducido. El número de Id. de idioma es un **entero** con el identificador de idioma. El título traducido es el texto traducido.  
  
 En [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], una traducción de dimensiones es una representación específica del lenguaje del nombre de una dimensión, el nombre de un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] objeto o uno de sus miembros, como el nivel de un título, un miembro o jerarquía. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] también admite traducciones de objetos de cubo.  
  
 Las traducciones ofrecen compatibilidad de servidor para aplicaciones cliente que admitan varios idiomas. Con frecuencia, los usuarios de distintos países ven un mismo cubo y sus dimensiones. Resulta útil poder traducir varios elementos de un cubo y sus dimensiones a distintos idiomas, de forma que estos usuarios puedan ver y comprender el cubo. Por ejemplo, un usuario corporativo en Francia puede obtener acceso a un cubo desde una estación de trabajo con una configuración regional en francés y ver los valores de propiedad del objeto en francés. Sin embargo, un usuario corporativo en Alemania que obtiene acceso al mismo cubo desde una estación de trabajo con una configuración regional en alemán puede ver los mismos valores de las propiedades del objeto en alemán.  
  
 La información de intercalación e idioma para el equipo cliente se almacena con formato de identificador de configuración regional (LCID). Tras la conexión, el cliente pasa el LCID a la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. La instancia utiliza el LCID para determinar qué conjunto de traducciones debe usarse para proporcionar los metadatos a los objetos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Si un objeto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no contiene la traducción especificada, el idioma predeterminado se utiliza para devolver el contenido al cliente.  
  
## <a name="see-also"></a>Vea también  
 [Traducciones de cubos](../../analysis-services/multidimensional-models-olap-logical-cube-objects/cube-translations.md)   
 [Compatibilidad con traducción en Analysis Services](../../analysis-services/translation-support-in-analysis-services.md)   
 [Sugerencias de globalización y mejores prácticas &#40; Analysis Services &#41;](../../analysis-services/globalization-tips-and-best-practices-analysis-services.md)  
  
  

