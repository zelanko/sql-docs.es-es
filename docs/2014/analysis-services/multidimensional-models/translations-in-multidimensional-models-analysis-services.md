---
title: Traducciones en modelos multidimensionales | Documentos de Microsoft
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
- sql12.asvs.dimensiondesigner.deletelanguagefirm.f1
ms.assetid: 5521f8ef-b10a-4861-9df7-1e43e0a1fb3f
caps.latest.revision: 8
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: edb58addda246c716224b578aad3713812708476
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36113694"
---
# <a name="translations-in-multidimensional-models"></a>Traducciones en modelos multidimensionales
  Compatibilidad con varios idiomas en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] se lleva a cabo mediante las traducciones. Una traducción contiene un identificador de idioma y enlaces para las propiedades de los objetos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que se pueden presentar en varios idiomas. Por ejemplo, puede definir una traducción para una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que presente el título y la descripción de la base de datos en un idioma concreto. Para obtener más información acerca de las traducciones, vea [las traducciones de cubos](../multidimensional-models-olap-logical-cube-objects/cube-translations.md).  
  
## <a name="defining-translations"></a>Definir traducciones  
 Puede definir traducciones en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] utilizando el diseñador adecuado para el objeto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que se vaya a traducir. Definir una traducción se crea un `Translation` objeto asociado con el adecuado [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] objeto que tiene los valores literales explícitos especificados, en el idioma especificado, para las propiedades del asociado [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] objeto.  
  
 Los siguientes objetos y propiedades de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] pueden tener traducciones asociadas a ellos:  
  
|Objeto|Propiedades|Diseñador|  
|------------|----------------|--------------|  
|Base de datos|`Caption`, `Description`|[General &#40;Diseñador de la base de datos&#41; &#40;Analysis Services - datos multidimensionales&#41;](../general-database-designer-analysis-services-multidimensional-data.md)|  
|Cube|`Caption`, `Description`|[Traducciones &#40;Diseñador de cubos&#41; &#40;Analysis Services - datos multidimensionales&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|Grupo de medida|`Caption`|[Traducciones &#40;Diseñador de cubos&#41; &#40;Analysis Services - datos multidimensionales&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|Measure|`Caption`, `DisplayFolder`|[Traducciones &#40;Diseñador de cubos&#41; &#40;Analysis Services - datos multidimensionales&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|Dimensión de cubo|`Caption`|[Traducciones &#40;Diseñador de cubos&#41; &#40;Analysis Services - datos multidimensionales&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|Perspective|`Caption`|[Traducciones &#40;Diseñador de cubos&#41; &#40;Analysis Services - datos multidimensionales&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|Indicador clave de rendimiento (KPI)|`Caption`, `Description`, `DisplayFolder`|[Traducciones &#40;Diseñador de cubos&#41; &#40;Analysis Services - datos multidimensionales&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|Acción|`Caption`|[Traducciones &#40;Diseñador de cubos&#41; &#40;Analysis Services - datos multidimensionales&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|Conjunto con nombre|`Caption`|[Traducciones &#40;Diseñador de cubos&#41; &#40;Analysis Services - datos multidimensionales&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|miembro calculado|`Caption`|[Traducciones &#40;Diseñador de cubos&#41; &#40;Analysis Services - datos multidimensionales&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|Dimensión de base de datos|`Caption`, `AttributeAllMember`|[Traducciones &#40;Diseñador de dimensiones&#41; &#40;Analysis Services - datos multidimensionales&#41;](../translations-dimension-designer-analysis-services-multidimensional-data.md)|  
|Attribute|`Caption`, `CaptionColumn` <sup>1</sup>, `AttributeHierarchyDisplayFolder`, `NamingTemplate`, `MembersWithDataCaption`|[Traducciones &#40;Diseñador de dimensiones&#41; &#40;Analysis Services - datos multidimensionales&#41;](../translations-dimension-designer-analysis-services-multidimensional-data.md)|  
|Hierarchy|`Caption`, `AllMemberName`|[Traducciones &#40;Diseñador de dimensiones&#41; &#40;Analysis Services - datos multidimensionales&#41;](../translations-dimension-designer-analysis-services-multidimensional-data.md)|  
|Nivel|`Caption`|[Traducciones &#40;Diseñador de dimensiones&#41; &#40;Analysis Services - datos multidimensionales&#41;](../translations-dimension-designer-analysis-services-multidimensional-data.md)|  
  
 <sup>1</sup> el `CaptionColumn` propiedad de un atributo se puede enlazar a una columna en una vista del origen de datos y puede utilizar una intercalación de Windows distinto del especificado para la instancia, a diferencia de otras traducciones.  
  
### <a name="defining-attribute-translations"></a>Definir traducciones de atributos  
 Las traducciones asociadas con atributos en las dimensiones de base de datos se tratan de manera diferente a otras traducciones en los siguientes aspectos:  
  
-   Se puede asociar una columna de enlace, en vez de un valor literal explícito, con la propiedad `CaptionColumn` para que se puedan traducir los nombres de miembro del atributo.  
  
-   Se puede utilizar una intercalación de Windows diferente a la intercalación especificada para la instancia para que los miembros del atributo se puedan ordenar adecuadamente según el idioma especificado en la traducción.  
  
 Puede usar el **traducción de datos de atributo** cuadro de diálogo de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] para definir las traducciones de atributos en dimensiones de base de datos. Para obtener más información sobre la **traducción de datos de atributo** cuadro de diálogo, vea [cuadro de diálogo traducción de datos de atributo &#40;Analysis Services - datos multidimensionales&#41;](../attribute-data-translation-dialog-box-analysis-services-multidimensional-data.md).  
  
## <a name="resolving-translations"></a>Resolver traducciones  
 Si una aplicación cliente solicita información en un identificador de idioma concreto, la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] intenta resolver los datos y los metadatos  de los objetos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] con el identificador de idioma más cercano posible. Si la aplicación cliente no especifica un idioma predeterminado, especifica el identificador de configuración regional neutro (0) o procesa el identificador de idioma predeterminado (1024), [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usará el idioma predeterminado para que la instancia devuelva los datos y los metadatos de los objetos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 Si la aplicación cliente especifica un identificador de idioma diferente al identificador de idioma predeterminado, la instancia recorre en iteración todos las traducciones disponibles para todos los objetos disponibles. Si el identificador de idioma predeterminado coincide con el identificador de idioma de una traducción, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] devuelve esa traducción. Si no se encuentra ninguna coincidencia, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] intenta utilizar uno de los siguientes métodos para devolver traducciones con el identificador de idioma más cercano al identificador de idioma especificado:  
  
-   En los siguientes identificadores de idioma, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] intenta utilizar un identificador de idioma alternativo si no se ha definido una traducción para el identificador de idioma especificado:  
  
    |Identificador de idioma especificado|Identificador de idioma alternativo|  
    |-----------------------------------|-----------------------------------|  
    |3076 - Chino (RAE de Hong Kong, RPC)|1028 - Chino (Taiwán)|  
    |5124 - Chino (RAE de Macao)|1028 - Chino (Taiwán)|  
    |1028 - Chino (Taiwán)|Idioma predeterminado|  
    |4100 - Chino (Singapur)|2052 - Chino (RPC)|  
    |2074 - Croata|Idioma predeterminado|  
    |3098 - Croata (cirílico)|Idioma predeterminado|  
  
-   En los demás identificadores de idioma especificados, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] extrae el idioma principal del identificador de idioma especificado y recupera el identificador de idioma que indica Windows como el mejor resultado del idioma principal. Si no se puede encontrar una traducción para la mejor coincidencia de identificador de idioma, o si el identificador de idioma especificado es la mejor coincidencia para el idioma principal, se utiliza el idioma predeterminado.  
  
## <a name="deleting-translation-objects"></a>Eliminar objetos de traducción  
 Puede hacer clic con el botón secundario en un objeto de traducción en el diseñador de cubos o dimensiones para quitarlo de forma definitiva. No es posible restaurar ni reciclar un objeto eliminado, de modo que asegúrese de revisar la lista de objetos afectados antes de continuar.  
  
## <a name="see-also"></a>Vea también  
 [Escenarios de globalización para Analysis Services multidimensional](../globalization-scenarios-for-analysis-services-multiidimensional.md)   
 [Idiomas e intercalaciones &#40;Analysis Services&#41;](../languages-and-collations-analysis-services.md)  
  
  