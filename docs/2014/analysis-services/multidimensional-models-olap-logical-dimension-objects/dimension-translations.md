---
title: Traducciones de dimensiones | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- dimensions [Analysis Services], translations
- multiple language support [Analysis Services]
- international considerations [Analysis Services]
- global considerations [Analysis Services]
- LCIDs
- translations [Analysis Services], dimensions
ms.assetid: 38fc1e05-2ac9-4816-b52b-dfd19c3a43a2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 81e0ecacaa185b9fe520513af57ced3b382a343c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62728531"
---
# <a name="dimension-translations"></a>Traducciones de dimensiones
  Una traducción es un mecanismo simple para cambiar las etiquetas y títulos mostrados de un idioma a otro. Cada traducción se define como un par de valores: una cadena con el texto traducido y un número con el identificador de idioma. Todos los objetos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] disponen de traducción. Las dimensiones también pueden tener los valores de atributo traducidos. La aplicación cliente es responsable de localizar la configuración de idioma que el usuario ha definido y efectuar el cambio para mostrar todos los títulos y etiquetas en dicho idioma. Un objeto puede tener tantas traducciones como se desee.  
  
 Un objeto <xref:Microsoft.AnalysisServices.Translation> simple está compuesto por el número del identificador de idioma y el título traducido. El número del identificador de idioma es un valor `Integer` con el identificador de idioma. El título traducido es el texto traducido.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] En [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], una traducción de dimensiones es una representación específica del idioma del nombre de una dimensión, el nombre de un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] objeto o uno de sus miembros, como un título, un miembro o un nivel de jerarquía. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] también admite traducciones de objetos de cubo.  
  
 Las traducciones ofrecen compatibilidad de servidor para aplicaciones cliente que admitan varios idiomas. Con frecuencia, los usuarios de distintos países ven un mismo cubo y sus dimensiones. Resulta útil poder traducir varios elementos de un cubo y sus dimensiones a distintos idiomas, de forma que estos usuarios puedan ver y comprender el cubo. Por ejemplo, un usuario empresarial en Francia puede tener acceso a un cubo desde una estación de trabajo con una configuración regional en francés y ver los valores de las propiedades del objeto en francés. Sin embargo, un usuario corporativo en Alemania que obtiene acceso al mismo cubo desde una estación de trabajo con una configuración regional en alemán puede ver los mismos valores de las propiedades del objeto en alemán.  
  
 La información de intercalación e idioma para el equipo cliente se almacena con formato de identificador de configuración regional (LCID). Tras la conexión, el cliente pasa el LCID a la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. La instancia utiliza el LCID para determinar qué conjunto de traducciones debe usarse para proporcionar los metadatos a los objetos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Si un objeto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no contiene la traducción especificada, el idioma predeterminado se utiliza para devolver el contenido al cliente.  
  
## <a name="see-also"></a>Consulte también  
 [Traducciones de cubo](../multidimensional-models-olap-logical-cube-objects/cube-translations.md)   
 [Traducciones &#40;Analysis Services&#41;](../translations-analysis-services.md)   
 [Sugerencias de globalización y prácticas recomendadas &#40;Analysis Services&#41;](../globalization-tips-and-best-practices-analysis-services.md)  
  
  
