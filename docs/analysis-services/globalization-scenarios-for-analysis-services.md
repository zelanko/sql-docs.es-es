---
title: Escenarios de globalización para Analysis Services | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5d708a2e3daca372bc336e91886889b79909627a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65357402"
---
# <a name="globalization-scenarios-for-analysis-services"></a>Escenarios de globalización para Analysis Services
[!INCLUDE[ssas-appliesto-sqlas-aas](../includes/ssas-appliesto-sqlas-aas.md)]

  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] almacena y manipula datos y metadatos multilingües en modelos de datos tabulares y multidimensionales. El almacenamiento de datos es Unicode (UTF-16), en los juegos de caracteres que utilizan la codificación Unicode. Si carga datos ANSI en un modelo de datos, los caracteres se almacenan con puntos de código equivalentes de Unicode.  
  
 Con la compatibilidad con Unicode, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] puede almacenar datos en cualquiera de los idiomas admitidos por los sistemas operativos de servidor y cliente Windows, y permite la lectura, escritura, ordenación y comparación de datos en todos los juegos de caracteres que se usan en un equipo Windows. Las aplicaciones cliente de BI que consumen datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] pueden representar datos en el idioma que elija el usuario, siempre que haya datos en ese idioma dentro del modelo.  
  
 La compatibilidad de idiomas puede tener diferentes implicaciones para cada persona. En la siguiente lista se tratan algunas cuestiones comunes relacionadas con la forma en que Analysis Services es compatible con idiomas.  
  
-   Los datos, como ya se indicó, se almacenan en cualquier conjunto de caracteres con codificación Unicode de un sistema operativo de cliente Windows.  
  
-   Se pueden traducir los metadatos, como los nombres de objeto. Aunque la compatibilidad varía según el tipo de modelo, tanto los modelos multidimensionales como los tabulares admiten la inserción de cadenas traducidas dentro del modelo. Puede definir varias traducciones y, luego, usar un identificador de configuración regional para determinar qué traducción se devolverá al cliente. Consulte [Características](#bkmk_features) , más adelante, para obtener más detalles.  
  
-   Los mensajes de error, advertencia e información que devuelve el motor de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] (msmdsrv) están localizados a los 43 idiomas que admiten Office y Office 365. No es necesaria ninguna configuración para obtener los mensajes en un idioma determinado. La configuración regional de la aplicación cliente determina las cadenas que se devuelven.  
  
-   El archivo de configuración (msmdsrv.ini) y PowerShell AMO solo están disponibles en inglés.  
  
-   Los archivos de registro contienen una mezcla de mensajes en inglés y localizados, si instaló un paquete de idioma en el servidor Windows Server en el que se ejecuta Analysis Services.  
  
-   Documentación y las herramientas, como [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] y [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], se traducen en estos idiomas: Chino simplificado, chino tradicional, francés, alemán, italiano, japonés, coreano, portugués (Brasil), ruso y español. La referencia cultural se especifica durante la instalación.  
  
 En el caso de los modelos multidimensionales, Analysis Services le permite definir el idioma, la intercalación y las traducciones de forma independiente en toda la jerarquía de objetos.  En el caso de los modelos tabulares, solo puede agregar las traducciones, porque el sistema operativo hereda el idioma y la intercalación.  
  
 Los escenarios habilitados a través de las características de globalización de Analysis Services incluyen:  
  
-   Un mismo modelo de datos proporciona diversos títulos traducidos para que los valores y los nombres de campos aparezcan en el idioma que elija el usuario. Para empresas que operen en países bilingües como Canadá, Bélgica y Suiza, la compatibilidad con varios idiomas en todas las aplicaciones de cliente y servidor es un requisito de codificación estándar. Este escenario se habilita con las traducciones y conversiones de divisa. Consulte [Características](#bkmk_features) , más adelante, para ver información detallada y vínculos.  
  
-   Los entornos de desarrollo y producción están ubicados geográficamente en distintos países. Cada vez es más común que una solución se desarrolle en un país y, luego, se implemente en otro. Saber cómo configurar las propiedades de idioma e intercalación es fundamental si tiene que preparar una solución desarrollada en un idioma para su implementación en un servidor que utiliza otro paquete de idioma. Configurar estas propiedades le permite invalidar los valores predeterminados heredados que obtiene del sistema host original. Consulte [Idiomas e intercalaciones &#40;Analysis Services&#41;](../analysis-services/languages-and-collations-analysis-services.md) para obtener más información sobre la configuración de propiedades.  
  
##  <a name="bkmk_features"></a> Características para crear una solución multilingüe globalizada  
 En el nivel de cliente, las aplicaciones globalizadas que consumen o manipular datos multidimensionales de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] pueden usar las características multilingües y multiculturales de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 Puede recuperar datos y metadatos de los objetos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] en los que se han definido las traducciones automáticamente proporcionando un identificador de configuración regional cuando se conecte con una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
 Vea [Sugerencias de globalización y procedimientos recomendados &#40;Analysis Services&#41;](../analysis-services/globalization-tips-and-best-practices-analysis-services.md) para conocer las prácticas de diseño y codificación que pueden ayudarle a evitar problemas relacionados con los datos en diversos idiomas.  
  
||||  
|-|-|-|  
|**Capacidad**|**Tabular**|**Multidimensional**|  
|[Idiomas e intercalaciones &#40;Analysis Services&#41;](../analysis-services/languages-and-collations-analysis-services.md)|Heredado del sistema operativo.|Heredado, pero con la capacidad de reemplazar el idioma y la intercalación de objetos importantes en la jerarquía de modelo.|  
|Ámbito de compatibilidad con la traducción|Leyendas y descripciones.|Las traducciones se pueden crear para nombres de objeto, leyendas, identificadores y descripciones. También pueden estar en cualquier script y lenguaje Unicode. Es así aunque las herramientas y el entorno estén en otro idioma. Por ejemplo, en un entorno de desarrollo en el que se usen el idioma inglés y una intercalación latina en toda la pila, puede incluir en el modelo un objeto que utilice caracteres cirílicos en su nombre.|  
|Implementación de compatibilidad con la traducción|Creación con [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para generar archivos de traducción que rellenará y, luego, importará de vuelta en el modelo.<br /><br /> Vea [Traducciones en modelos tabulares &#40;Analysis Services&#41;](../analysis-services/tabular-models/translations-in-tabular-models-analysis-services.md) para obtener más información.|Creación con[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para definir las traducciones del título, la descripción y los tipos de cuenta de cubos y medidas, dimensiones y atributos.<br /><br /> Vea [Traducciones en modelos multidimensionales &#40;Analysis Services&#41;](../analysis-services/multidimensional-models/translations-in-multidimensional-models-analysis-services.md) para obtener más información. |  
|Conversión de moneda|No disponible.|La conversión de moneda convierte las medidas que contienen datos de divisas con scripts MDX especializados. Puede usar el Asistente de Business Intelligence de [!INCLUDE[ss_dtbi](../includes/ss-dtbi-md.md)] para generar un script MDX que utilice una combinación de datos y metadatos de dimensiones, atributos y grupos de medida para convertir las medidas que contienen datos de divisas. Vea [Conversiones de moneda &#40;Analysis Services&#41;](../analysis-services/currency-conversions-analysis-services.md).|  
  
## <a name="see-also"></a>Vea también  
 [Compatibilidad con traducción en Analysis Services](../analysis-services/translation-support-in-analysis-services.md)   
 [Internacionalización para aplicaciones para Windows](http://msdn.microsoft.com/library/windows/desktop/dd318661%28v=vs.85%29.aspx)   
 [Globalización](/globalization/)   
 [Creación de aplicaciones de la Tienda Windows con diseño adaptable basado en la configuración regional](https://blogs.windows.com/buildingapps/2014/03/06/writing-windows-store-apps-with-locale-based-adaptive-design/)   
 [Desarrollo de aplicaciones universales de Windows con C# y XAML](http://www.microsoftvirtualacademy.com/training-courses/developing-universal-windows-apps-with-c-and-xaml)  
  
  
