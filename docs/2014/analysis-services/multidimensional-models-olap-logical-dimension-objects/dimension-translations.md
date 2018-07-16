---
title: Traducciones de dimensiones | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- dimensions [Analysis Services], translations
- multiple language support [Analysis Services]
- international considerations [Analysis Services]
- global considerations [Analysis Services]
- LCIDs
- translations [Analysis Services], dimensions
ms.assetid: 38fc1e05-2ac9-4816-b52b-dfd19c3a43a2
caps.latest.revision: 19
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6ad366e146a52eacbad63e5fb3eac71418fd5d34
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37243455"
---
# <a name="dimension-translations"></a>Traducciones de dimensiones
  Una traducción es un mecanismo simple para cambiar las etiquetas y títulos mostrados de un idioma a otro. Cada traducción se define como un par de valores: una cadena con el texto traducido y un número con el identificador de idioma. Todos los objetos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] disponen de traducción. Las dimensiones también pueden tener los valores de atributo traducidos. La aplicación cliente es responsable de localizar la configuración de idioma que el usuario ha definido y efectuar el cambio para mostrar todos los títulos y etiquetas en dicho idioma. Un objeto puede tener tantas traducciones como se desee.  
  
 Un objeto <xref:Microsoft.AnalysisServices.Translation> simple está compuesto por el número del identificador de idioma y el título traducido. El número del identificador de idioma es un valor `Integer` con el identificador de idioma. El título traducido es el texto traducido.  
  
 En [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], una traducción de dimensiones es una representación específica del lenguaje del nombre de una dimensión, el nombre de un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] objeto o una de sus miembros, como el nivel de un título, un miembro o jerarquía. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] también admite traducciones de objetos de cubo.  
  
 Las traducciones ofrecen compatibilidad de servidor para aplicaciones cliente que admitan varios idiomas. Con frecuencia, los usuarios de distintos países ven un mismo cubo y sus dimensiones. Resulta útil poder traducir varios elementos de un cubo y sus dimensiones a distintos idiomas, de forma que estos usuarios puedan ver y comprender el cubo. Por ejemplo, un usuario corporativo en Francia puede obtener acceso a un cubo desde una estación de trabajo con una configuración regional en francés y ver los valores de propiedad del objeto en francés. Sin embargo, un usuario corporativo en Alemania que obtiene acceso al mismo cubo desde una estación de trabajo con una configuración regional en alemán puede ver los mismos valores de las propiedades del objeto en alemán.  
  
 La información de intercalación e idioma para el equipo cliente se almacena con formato de identificador de configuración regional (LCID). Tras la conexión, el cliente pasa el LCID a la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. La instancia utiliza el LCID para determinar qué conjunto de traducciones debe usarse para proporcionar los metadatos a los objetos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Si un objeto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no contiene la traducción especificada, el idioma predeterminado se utiliza para devolver el contenido al cliente.  
  
## <a name="see-also"></a>Vea también  
 [Traducciones de cubo](../multidimensional-models-olap-logical-cube-objects/cube-translations.md)   
 [Traducciones &#40;Analysis Services&#41;](../translations-analysis-services.md)   
 [Sugerencias de globalización y procedimientos recomendados &#40;Analysis Services&#41;](../globalization-tips-and-best-practices-analysis-services.md)  
  
  
