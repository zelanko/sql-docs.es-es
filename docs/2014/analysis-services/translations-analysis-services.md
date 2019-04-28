---
title: Traducciones (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Business Intelligence Development Studio, translations [Analysis Services]
- translations [Analysis Services], about translations
- object translations [Analysis Services]
- language identifiers [Analysis Services]
- attribute translations [Analysis Services]
- translations [Analysis Services]
ms.assetid: 018471e0-3c82-49ec-aa16-467fb58a6d5f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e85f6ca82f11b9f19c14a020d879afb65a6d1775
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62794486"
---
# <a name="translations-analysis-services"></a>Traducciones (Analysis Services)
  **[!INCLUDE[applies](../includes/applies-md.md)]**  solo a modelos multidimensionales  
  
 En un modelo de datos multidimensional de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , puede incrustar varias traducciones de un título para proporcionar cadenas específicas de la configuración regional que coincidan con cada LCID. Se pueden agregar traducciones del nombre de la base de datos, los objetos del cubo y los objetos de dimensión de la base de datos.  
  
 Definir una traducción crea los metadatos y el título traducido dentro del modelo, pero para representar cadenas localizadas en una aplicación cliente, deberá establecer la propiedad de `Language` en el objeto o pasar un parámetro de `Locale Identifier` en la cadena de conexión (por ejemplo, estableciendo `LocaleIdentifier=1036` para que devuelva cadenas en francés). Le recomendamos que utilice `Locale Identifier` si desea admitir varias traducciones simultáneas del mismo objeto en diferentes idiomas. Si configura la propiedad `Language`, funcionará, pero esto afectará también al procesamiento y a las consultas, lo cual podría tener consecuencias no deseadas. Configurar `Locale Identifier` es la mejor opción, porque solo se utiliza para devolver las cadenas traducidas.  
  
 Una traducción está formada por un identificador de configuración regional (LCID), un título traducido del objeto (por ejemplo, el nombre de la dimensión o el atributo) y, si se quiere, un enlace a una columna que proporciona los valores de los datos en el idioma de destino. Puede tener varias traducciones, pero solo puede utilizar una para cada una de las conexiones. No hay ningún límite teórico en la cantidad de traducciones que puede incrustar en el modelo, pero cada traducción agrega complejidad a las pruebas y todas las traducciones deben compartir la misma intercalación. Por lo tanto, al diseñar la solución, tenga en cuenta estas restricciones naturales.  
  
> [!TIP]  
>  Puede usar aplicaciones cliente como Excel, Management Studio y [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] para devolver las cadenas traducidas. Para obtener información detallada, vea [Globalization Tips and Best Practices &#40;Analysis Services&#41;](globalization-tips-and-best-practices-analysis-services.md) .  
  
## <a name="setting-up-a-model-to-support-translated-members"></a>Configuración de un modelo para admitir los miembros traducidos  
 Un modelo de datos que se use en una solución multilingüe no solo necesitará las etiquetas traducidas (los nombres de campo y las descripciones). También debe proporcionar los valores de los datos que se articulan en los diferentes alfabetos de los idiomas. Para conseguir una solución multilingüe, necesita atributos individuales, enlazados a las columnas de una base de datos externa que devuelva los datos.  
  
 Las bases de datos de muestra de Adventure Works (almacenamiento de datos relacional y multidimensional) muestran la característica de traducción. El modelo de muestra incluye descripciones y títulos traducidos. El almacenamiento de datos relacional de muestra contiene columnas de valores traducidos que proporcionan los miembros de atributos localizados del modelo.  
  
 Para ver los valores de datos traducidos de los que dispone el modelo:  
  
1.  Abra el modelo multidimensional de Adventure Works en el diseñador.  
  
2.  En el Explorador de soluciones, abra vistas del origen de datos y haga doble clic en Adventure Works DW\<versión > .dsv.  
  
3.  Busque dimDate, dimProduct, dimProductCategory o dimProductSubcategory. Todas estas dimensiones contienen atributos de miembros traducidos de mes, día de la semana, nombre de producto, nombre de categoría, etc.  
  
4.  Haga clic con el botón derecho en cualquier campo y seleccione **Explorar datos**. Verá las traducciones de inglés, español y francés de cada miembro.  
  
 Los formatos de fecha, hora y moneda no se implementan con traducciones. Para proporcionar dinámicamente formatos específicos de cada cultura en función de la configuración regional del cliente, utilice el Asistente de conversión de moneda y la propiedad `FormatString`. Para más información, vea [Conversiones de moneda &#40;Analysis Services&#41;](currency-conversions-analysis-services.md) y [Elemento FormatString &#40;ASSL&#41;](https://docs.microsoft.com/bi-reference/assl/properties/formatstring-element-assl).  
  
 [Lección 9: Definir perspectivas y traducciones](lesson-9-defining-perspectives-and-translations.md) en el Tutorial de Analysis Services le guiará por los pasos para crear y probar las traducciones.  
  
## <a name="defining-translations"></a>Definir traducciones  
 Al definir una traducción se crea un objeto `Translation` como un elemento secundario de la base de datos, de la dimensión o del objeto de cubo [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Utilice [!INCLUDE[ss_dtbi](../includes/ss-dtbi-md.md)] para abrir la solución y definir las traducciones.  
  
### <a name="add-translations-to-a-cube"></a>Agregar traducciones a un cubo  
 Puede agregar traducciones al cubo, grupos de medidas, medidas, dimensión del cubo, perspectivas, KPI, acciones, conjuntos con nombre y miembros calculados.  
  
1.  En el Explorador de soluciones, haga doble clic en el nombre del cubo para abrir el Diseñador de cubos.  
  
2.  Haga clic en la pestaña **Traducciones** . Todos los objetos que admitan traducciones se mostrarán en esta página.  
  
3.  Para cada objeto, especifique el idioma de destino (se resuelve internamente en un LCID), el título traducido y la descripción traducida. La lista de idiomas es coherente en todo Analysis Services, tanto si configura el idioma del servidor en Management Studio como si agrega una invalidación de traducción en un solo atributo.  
  
     Recuerde que no puede cambiar la intercalación. Un cubo utiliza básicamente una intercalación, incluso si admite varios idiomas mediante títulos traducidos (hay una excepción para los atributos de dimensión que se describe a continuación). Si los idiomas no se ordenan correctamente en la intercalación compartida, tendrá que hacer copias del cubo para adaptarse a los requisitos de intercalación.  
  
4.  Compile e implemente el proyecto.  
  
5.  Conéctese a la base de datos con una aplicación cliente, como Excel, y modifique la cadena de conexión para usar el identificador de configuración regional. Para más información, vea [Sugerencias de globalización y procedimientos recomendados &#40;Analysis Services&#41;](globalization-tips-and-best-practices-analysis-services.md) .  
  
### <a name="add-translations-to-a-dimension-and-attributes"></a>Agregar traducciones a una dimensión y atributos  
 Puede agregar traducciones a dimensiones de una base de datos, atributos, jerarquías y niveles de una jerarquía.  
  
 Los títulos traducidos se agregan al modelo manualmente con el teclado o con copiar y pegar, pero en el caso de los miembros de atributos de dimensión, puede obtener valores traducidos de una base de datos externa. En concreto, la propiedad `CaptionColumn` de un atributo se puede enlazar a una columna de una vista de un origen de datos.  
  
 En el nivel del atributo, puede invalidar la configuración de intercalación: por ejemplo, puede ajustar la distinción de ancho o usar una ordenación binaria para un atributo concreto. En [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], la intercalación se expone donde se definen los enlaces de datos. Dado que va a enlazar una traducción de atributo de dimensión con una columna de un origen diferente en la vista del origen de datos (DSV), hay una configuración de intercalación disponible para que pueda especificar la intercalación que utiliza la columna de origen. Consulte [Set or Change the Column Collation](../relational-databases/collations/set-or-change-the-column-collation.md) para ver más detalles sobre la intercalación de columnas en la base de datos relacional.  
  
1.  En el Explorador de soluciones, haga doble clic en el nombre de la dimensión para abrir el Diseñador de dimensiones.  
  
2.  Haga clic en la pestaña **Traducciones** . Todos los objetos de dimensión que admitan traducciones se mostrarán en esta página.  
  
     Para cada objeto, especifique el idioma de destino (se resuelve en un LCID), el título traducido y la descripción traducida. La lista de idiomas es coherente en todo Analysis Services, tanto si configura el idioma del servidor en Management Studio como si agrega una invalidación de traducción en un solo atributo.  
  
3.  Para enlazar un atributo con una columna que proporciona valores traducidos:  
  
    1.  Aún en el Diseñador de dimensiones | **Traducciones**, agregue una nueva traducción. Elija el idioma. Aparecerá una nueva columna en la página para aceptar los valores traducidos.  
  
    2.  Coloque el cursor en una celda vacía situada junto a uno de los atributos. El atributo no puede ser la clave, pero todos los demás atributos son opciones viables. Debería ver un pequeño botón con un punto dentro de él. Haga clic en el botón para abrir el **cuadro de diálogo Traducción de datos de atributos**.  
  
    3.  Escriba una traducción para el título. Se usará como etiqueta de datos en el idioma de destino: por ejemplo, como nombre de campo en una lista de campos de tabla dinámica.  
  
    4.  Elija la columna de origen que proporciona los valores traducidos de los miembros del atributo. Solo están disponibles las columnas ya existentes en la tabla o la consulta enlazada a la dimensión. Si la columna no existe, deberá modificar la vista del origen de datos, la dimensión y el cubo para elegir la columna.  
  
    5.  Elija la intercalación y el criterio de ordenación, si procede.  
  
4.  Compile e implemente el proyecto.  
  
5.  Conéctese a la base de datos con una aplicación cliente, como Excel, y modifique la cadena de conexión para usar el identificador de configuración regional. Para más información, vea [Sugerencias de globalización y procedimientos recomendados &#40;Analysis Services&#41;](globalization-tips-and-best-practices-analysis-services.md).  
  
### <a name="add-a-translation-of-the-database-name"></a>Agregar una traducción del nombre de la base de datos  
 En el nivel de la base de datos, puede agregar traducciones del nombre y la descripción de la base de datos. El nombre traducido de la base de datos puede verse en las conexiones de cliente que especifican el LCID del idioma, pero depende de la herramienta. Por ejemplo, al ver la base de datos en Management Studio, no se mostrará el nombre traducido, aunque especifique el identificador de configuración regional en la conexión. La API que utiliza Management Studio para conectarse a Analysis Services no lee la propiedad `Language`.  
  
1.  En el Explorador de soluciones, haga clic con el botón derecho en el nombre del proyecto | **Editar base de datos** para abrir el Diseñador de bases de datos.  
  
2.  En Traducciones, especifique el idioma de destino (se resuelve en un LCID), el título traducido y la descripción traducida. La lista de idiomas es coherente en todo Analysis Services, tanto si configura el idioma del servidor en Management Studio como si agrega una invalidación de traducción en un solo atributo.  
  
3.  En la página de propiedades de la base de datos, configure `Language` con el mismo LCID que especificó para la traducción. Si quiere, configure también `Collation` si el valor predeterminado no es adecuado.  
  
4.  Compile e implemente la base de datos.  
  
## <a name="resolving-translations"></a>Resolver traducciones  
 Si una aplicación cliente solicita un identificador de configuración regional, la instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] tratará de resolver los datos y metadatos de los objetos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] en el LCID que mejor coincida. Si la aplicación cliente no especifica un idioma predeterminado, especifica el identificador de configuración regional neutro (0) o procesa el identificador de idioma predeterminado (1024), [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] usará el idioma predeterminado para que la instancia devuelva los datos y los metadatos de los objetos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
## <a name="see-also"></a>Vea también  
 [Escenarios de globalización para Analysis Services multidimensional](globalization-scenarios-for-analysis-services-multiidimensional.md)   
 [Idiomas e intercalaciones &#40;Analysis Services&#41;](languages-and-collations-analysis-services.md)   
 [Establecer o cambiar la intercalación de columnas](../relational-databases/collations/set-or-change-the-column-collation.md)   
 [Sugerencias de globalización y procedimientos recomendados &#40;Analysis Services&#41;](globalization-tips-and-best-practices-analysis-services.md)  
  
  
