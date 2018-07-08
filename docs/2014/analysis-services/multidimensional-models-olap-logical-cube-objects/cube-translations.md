---
title: Traducciones de cubo | Microsoft Docs
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
- multiple language support [Analysis Services]
- international considerations [Analysis Services]
- global considerations [Analysis Services]
- cubes [Analysis Services], translations
- OLAP objects [Analysis Services], translations
- translations [Analysis Services], cubes
ms.assetid: 4e4fd6a4-d324-4508-b75a-2a57de9ab8ff
caps.latest.revision: 41
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f894d45dffbf1c6eb746e3674127c75c4e59a81e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37163316"
---
# <a name="cube-translations"></a>Traducciones de cubo
  Una traducción es un mecanismo simple para cambiar las etiquetas y títulos mostrados de un idioma a otro. Cada traducción se define como un par de valores: una cadena con el texto traducido y un número con el identificador de idioma. Todos los objetos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] disponen de traducción. Las dimensiones también pueden tener los valores de atributo traducidos. La aplicación cliente es responsable de localizar la configuración de idioma que el usuario ha definido y efectuar el cambio para mostrar todos los títulos y etiquetas en dicho idioma. Un objeto puede tener tantas traducciones como se desee.  
  
 Un objeto <xref:Microsoft.AnalysisServices.Translation> simple está compuesto por el número del identificador de idioma y el título traducido. El número del identificador de idioma es un valor `Integer` con el identificador de idioma. El título traducido es el texto traducido.  
  
 En [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], una traducción de cubo es una representación específica del lenguaje del nombre de un objeto de cubo, como un título o una carpeta para mostrar. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] también admite traducciones de nombres de dimensión y de miembro.  
  
 Las traducciones ofrecen compatibilidad de servidor para aplicaciones cliente que admitan varios idiomas. Con frecuencia, usuarios de distintos países ven los datos de un cubo. Resulta útil poder traducir los distintos elementos de un cubo a diferentes idiomas para que los usuarios de estos idiomas puedan ver y comprender los metadatos del cubo. Por ejemplo, un usuario corporativo en Francia puede obtener acceso a un cubo desde una estación de trabajo con una configuración regional en francés y ver los valores de las propiedades del objeto en francés. Igualmente, un usuario corporativo en Alemania puede obtener acceso al mismo cubo desde una estación de trabajo con una configuración regional en alemán y ver los valores de las propiedades del objeto en alemán.  
  
 La información de intercalación e idioma para el equipo cliente se almacena con formato de identificador de configuración regional (LCID). Tras la conexión, el cliente pasa el LCID a la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. La instancia utiliza el LCID para determinar el conjunto de traducciones que se utiliza al proporcionar metadatos de objetos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] a cada usuario corporativo. Si un objeto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no contiene la traducción especificada, el idioma predeterminado se utiliza para devolver el contenido al cliente.  
  
## <a name="see-also"></a>Vea también  
 [Traducciones de dimensiones](../multidimensional-models-olap-logical-dimension-objects/dimension-translations.md)   
 [Traducciones &#40;Analysis Services&#41;](../translations-analysis-services.md)   
 [Sugerencias de globalización y procedimientos recomendados &#40;Analysis Services&#41;](../globalization-tips-and-best-practices-analysis-services.md)  
  
  
