---
title: Idiomas e intercalaciones (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Windows collations [Analysis Services]
- default collations
- languages [Analysis Services]
- sort orders [Analysis Services]
- language identifiers [Analysis Services]
- default languages
- collations [Analysis Services]
ms.assetid: 666cf8a7-223b-4be5-86c0-7fe2bcca0d09
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 62956774e203b1438de1ea07708940d0711053ac
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66079378"
---
# <a name="languages-and-collations-analysis-services"></a>Idiomas e intercalaciones (Analysis Services)
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] admite los idiomas e intercalaciones que proporcionan los sistemas operativos [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows. Las propiedades de `Language` y `Collation` se establecen inicialmente en el nivel de instancia durante la instalación, pero se pueden cambiar más tarde en diferentes niveles de la jerarquía de objetos.  
  
 En un modelo multidimensional (solo), se pueden establecer estas propiedades en una base de datos o en un cubo; también se pueden establecer en traducciones que se crean para objetos dentro de un cubo.  
  
 Al configurar `Language` y `Collation`, está especificando la configuración que usará el modelo de datos durante el procesamiento y la ejecución de consultas, o (solo en el caso de los modelos multidimensionales) equipando un modelo con varias traducciones para que los hablantes de otros idiomas puedan trabajar con el modelo en su idioma nativo. Las propiedades `Language` y `Collation` de un objeto (una base de datos, un modelo o un cubo) se configuran de forma explícita en las situaciones en las que el servidor de producción y el entorno de desarrollo están configurados para diferentes configuraciones regionales y quiere asegurarse de que el idioma y la intercalación coinciden con los del entorno de destino.  
  
 En este tema se incluye las siguientes secciones:  
  
-   [Objetos que admiten propiedades de idioma e intercalación](#bkmk_object)  
  
-   [Compatibilidad con idiomas en Analysis Services](#bkmk_lang)  
  
-   [Compatibilidad con la intercalación en Analysis Services](#bkmk_collations)  
  
-   [Cambiar el idioma o la intercalación predeterminados de la instancia](#bkmk_defaultLang)  
  
-   [Cambiar el idioma o la intercalación en un cubo](#bkmk_cube)  
  
-   [Cambiar el idioma y la intercalación dentro de un modelo de datos mediante XMLA](#bkmk_XMLA)  
  
-   [Mejore el rendimiento de las configuraciones regionales en inglés a través de EnableFast1033Locale](#bkmk_enablefast1033)  
  
-   [Compatibilidad con GB18030 en Analysis Services](#bkmk_gb18030)  
  
##  <a name="objects-that-support-language-and-collation-properties"></a><a name="bkmk_object"></a>Objetos que admiten propiedades de idioma e intercalación  
 `Language`a `Collation` menudo, las propiedades y se exponen juntas `Language`: donde puede establecer, `Collation`también puede establecer.  
  
 Puede establecer `Language` y `Collation` en estos objetos:  
  
-   **Instancia**de. Todos los proyectos implementados en la instancia adoptarán la combinación de idioma e intercalación de la instancia, suponiendo que el idioma y la intercalación no se hayan definido. De forma predeterminada, un modelo multidimensional deja vacía la configuración de idioma e intercalación. Cuando se implementa el proyecto, la base de datos y los cubos resultantes obtienen la configuración de idioma e intercalación de la instancia.  
  
     Inicialmente, las propiedades de idioma e intercalación se establecen durante la instalación, pero un administrador puede invalidarlas en Management Studio. Para obtener información detallada, vea [Cambiar la configuración predeterminada de idioma o intercalación en la instancia](#bkmk_defaultLang) .  
  
-   **Base de datos**. Para interrumpir la herencia, puede establecer explícitamente la configuración de idioma e intercalación en el nivel de proyecto que se utiliza en todos los cubos de la base de datos. A menos que se indique lo contrario, todos los cubos de la base de datos obtendrán la configuración de idioma e intercalación que se especifique en este nivel. Si habitualmente codifica e implementa en distintas configuraciones regionales (por ejemplo, desarrolla la solución en un equipo chino, pero la implementa en un servidor que pertenece a una subsidiaria francesa), la configuración de idioma e intercalación en el nivel de base de datos es el primer paso, y el más importante, para garantizar que la solución funciona en el entorno de destino. El mejor lugar para establecer estas propiedades es dentro del proyecto (a través del comando **Editar base de datos** en el proyecto).  
  
-   **Dimensión de base de datos**. Aunque el diseñador exponga las propiedades `Language` y `Collation` en una dimensión de la base de datos, configurar las propiedades en este objeto no resulta útil. Las dimensiones de base de datos no se utilizan como objetos independientes, por lo que puede ser difícil, si no imposible, aprovechar las propiedades que defina. Cuando se encuentra en un cubo, una dimensión siempre hereda `Language` y `Collation` de su elemento primario de cubo. Los valores que se hayan establecido en el objeto de dimensión de base de datos independiente se omiten.  
  
-   **Cubo**. Como estructura de consulta primaria, la configuración de idioma e intercalación se puede establecer en el nivel del cubo. Por ejemplo, tal vez desee crear versiones de un cubo en varios idiomas, como versiones en inglés y chino, dentro del mismo proyecto, donde cada cubo tenga su propia configuración de idioma e intercalación.  
  
     Sea cual sea la combinación de idioma e intercalación que establezca en el cubo, se usa con todas las medidas y dimensiones contenidas en el cubo. La única forma de establecer propiedades de intercalación más depuradas se produce cuando se crean traducciones en un atributo de dimensión. De lo contrario, suponiendo que no haya ninguna traducción en el nivel de atributo, hay una intercalación por cubo.  
  
 Además, puede establecer `Language`, por sí mismo, en un objeto **Translation** .  
  
 Al agregar traducciones a un cubo o dimensión se crea un objeto de traducción. `Language`forma parte de la definición de la traducción. `Collation`, sin embargo, se configura en el cubo o en un nivel superior y todas las traducciones la comparten. Esto es evidente en el XMLA de un cubo que contiene traducciones, donde se verán varias propiedades de idioma (una para cada traducción), pero solo una intercalación. Tenga en cuenta que hay una excepción en el caso de traducciones de atributo de dimensión, donde puede reemplazar la intercalación de cubo para especificar una intercalación de atributo que coincida con la columna de origen (el motor de base de datos admite la configuración de intercalación en columnas individuales y se acostumbra a configurar traducciones individuales para obtener datos de miembro de diferentes columnas de origen). Pero, en caso contrario, para las demás traducciones, `Language` se usa por sí mismo, sin un corolario de `Collation`. Vea [Translations &#40;Analysis Services&#41; (Traducciones &#40;Analysis Services&#41;)](translations-analysis-services.md) para más información.  
  
##  <a name="language-support-in-analysis-services"></a><a name="bkmk_lang"></a> Compatibilidad con idiomas en Analysis Services  
 La propiedad `Language` establece la configuración regional de un objeto, que se utiliza durante el procesamiento, las consultas y con `Captions` y `Translations` para admitir escenarios multilingües. Las configuraciones regionales se basan en un identificador de idioma (por ejemplo, inglés) y un territorio (por ejemplo, Estados Unidos o Australia) que refina aún más las representaciones de fecha y hora.  
  
 En el nivel de instancia, la propiedad se establece durante la instalación y se basa en el idioma del sistema operativo de Windows Server (uno de 37 idiomas, dando por hecho que se ha instalado un paquete de idioma). No se puede cambiar el idioma en el programa de instalación.  
  
 Después de la instalación, puede invalidar `Language` en la página de propiedades del servidor de Management Studio o en el archivo de configuración msmdsrv.ini. Puede elegir entre muchos más idiomas, incluidos todos los que admite el cliente Windows. Cuando se establece en el nivel de instancia, en el servidor, `Language` determina la configuración regional de todas las bases de datos que se implementan posteriormente. Por ejemplo, si establece `Language` en alemán, todas las bases de datos que se implementan en la instancia tendrán una propiedad de idioma de 1031, el LCID de alemán.  
  
###  <a name="value-of-the-language-property-is-a-locale-identifier-lcid"></a><a name="bkmk_lcid"></a> El valor de la propiedad Language es un identificador de configuración regional (LCID)  
 Los valores válidos incluyen cualquier LCID que aparezca en la lista desplegable. En Management Studio y SQL Server Data Tools, los LCID se representan en equivalentes de cadena. Aparecen los mismos idiomas en todos los lugares donde se expone la propiedad `Language`, independientemente de la herramienta. Al contar con una lista idéntica de idiomas se garantiza que las traducciones se pueden implementar y probar de forma coherente en todo el modelo.  
  
 Aunque Analysis Services muestra los idiomas por nombre, el valor real almacenado para la propiedad es un LCID. Al establecer una propiedad de idioma mediante programación o mediante el archivo msmdsrv.ini, use el [identificador de configuración regional (LCID)](http://en.wikipedia.org/wiki/Locale) como valor. Un LCID es un valor de 32 bits que consta de un identificador de idioma, un identificador de ordenación y bits reservados que identifican un idioma determinado. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] utiliza los LCID para especificar el idioma seleccionado para instancias y objetos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
 Puede establecer el LCID con formatos hexadecimales o decimales. Algunos ejemplos de valores válidos para la `Language` propiedad son:  
  
-   0x0409 o 1033 para **inglés (Estados Unidos)**  
  
-   0x0411 o 1041 para **japonés**  
  
-   0x0407 o 1031 para **alemán (Alemania)**  
  
-   0x0416 o 1046 para **portugués (Brasil)**  
  
 Para obtener una lista más completa, vea [Identificadores de configuración regional asignados por Microsoft](https://msdn.microsoft.com/goglobal/bb964664.aspx). Para obtener más información, vea [páginas de códigos](/windows/desktop/Intl/code-pages).  
  
> [!NOTE]  
>  La propiedad `Language` no determina el idioma en el que se devuelven los mensajes del sistema ni qué cadenas aparecen en la interfaz de usuario. Los errores, las advertencias y los mensajes están localizados en todos los idiomas admitidos en Office y Office 365, y se usan automáticamente cuando la conexión de cliente especifica una de las configuraciones regionales admitidas.  
  
##  <a name="collation-support-in-analysis-services"></a><a name="bkmk_collations"></a> Compatibilidad con intercalaciones en Analysis Services  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] utiliza intercalaciones binarias y de Windows exclusivamente. No utiliza intercalaciones de SQL Server heredadas. Dentro de un cubo, se utiliza una única intercalación en su totalidad, a excepción de las traducciones en el nivel de atributo. Para más información sobre cómo definir traducciones de atributos, vea [Translations &#40;Analysis Services&#41; (Traducciones &#40;Analysis Services&#41;)](translations-analysis-services.md).  
  
 Las intercalaciones controlan la distinción de mayúsculas y minúsculas de todas las cadenas en un alfabeto bicameral del idioma, a excepción de los identificadores de objeto. Si utiliza mayúsculas y minúsculas en un identificador de objeto, tenga en cuenta que la distinción de mayúsculas y minúsculas de los identificadores de objeto no está determinada por la intercalación, sino por [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Para los identificadores de objeto compuestos en el alfabeto del inglés, los identificadores de objeto no distinguen nunca mayúsculas de minúsculas, independientemente de la intercalación. Los alfabetos bicamerales del cirílico y de otros idiomas hacen lo contrario (siempre distinguen mayúsculas de minúsculas). Para más información, vea [Sugerencias de globalización y procedimientos recomendados &#40;Analysis Services&#41;](globalization-tips-and-best-practices-analysis-services.md) .  
  
 La intercalación de Analysis Services es compatible con el motor de bases de datos relacionales de SQL Server, dando por hecho que se mantiene la paridad en las opciones de ordenación que seleccione para cada servicio. Por ejemplo, si la base de datos relacionales distingue acentos, debe configurar el cubo de la misma manera. Pueden producirse problemas cuando las configuraciones de intercalación difieren. Para obtener un ejemplo y soluciones alternativas, vea [Espacios en blanco en una cadena Unicode tienen distintos resultados de procesamiento en función de la intercalación](https://social.technet.microsoft.com/wiki/contents/articles/23979.ssas-processing-error-blanks-in-a-unicode-string-have-different-processing-outcomes-based-on-collation-and-character-set.aspx). Para obtener más información sobre la intercalación y el motor de base de datos, vea [Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md).  
  
###  <a name="collation-types"></a><a name="bkmk_collationtype"></a> Tipos de intercalación  
 Analysis Services admite dos tipos de intercalación:  
  
-   **Intercalaciones de Windows**  
  
     Las intercalaciones de Windows ordenan caracteres según las características lingüísticas y culturales del idioma. En Windows, las intercalaciones superan el numero de configuraciones regionales (o idiomas) que se usan con ellas, debido a que muchos idiomas comparten alfabetos y reglas comunes de ordenación y comparación de caracteres. Por ejemplo, 33 configuraciones regionales de Windows, incluidas las configuraciones regionales de Windows para portugués e inglés, utilizan la página de códigos Latin1 (1252) y siguen un conjunto común de reglas para ordenar y comparar caracteres.  
  
-   **Intercalaciones binarias (BIN o BIN2)**  
  
     La intercalaciones binarias se ordenan en puntos de código Unicode, no en valores lingüísticos. Por ejemplo, Latin1_General_BIN y Japanese_BIN generan resultados de ordenación idénticos en datos Unicode. Mientras que una ordenación lingüística podría producir resultados como aAbBcCdD, una ordenación binaria sería ABCDabcd porque el punto de código de todos los caracteres en mayúsculas es colectivamente superior a los puntos de código de los caracteres en minúsculas.  
  
###  <a name="sort-order-options"></a><a name="bkmk_sortorder"></a> Opciones de orden  
 Las opciones de ordenación se utilizan para refinar las reglas de ordenación y comparación por distinción de mayúsculas y minúsculas, de acentos, de caracteres kana y de ancho. Por ejemplo, el valor predeterminado de la propiedad de configuración `Collation` para [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] es Latin1_General_AS_CS, lo que especifica que se utiliza la intercalación Latin1_General con un orden que distingue acentos y mayúsculas y minúsculas.  
  
 Tenga en cuenta que BIN y BIN2 son mutuamente excluyentes de otras opciones de ordenación, si desea utilizar BIN o BIN2, desactive la opción de ordenación de distinción de acentos. De manera similar, si selecciona BIN2, no estarán disponibles las opciones de distinción de mayúsculas y minúsculas, sin distinción de mayúsculas y minúsculas, distinción de acentos, sin distinción de acentos, distinción de caracteres kana y distinción de ancho.  
  
 La siguiente tabla describe las opciones de orden de intercalación de Windows y los sufijos asociados para [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
|Orden (sufijo)|Descripción del orden|  
|---------------------------|----------------------------|  
|Binario (_BIN) o BIN2 (_BIN2)|Hay dos tipos de intercalaciones binarias en SQL Server; las intercalaciones BIN antiguas y las intercalaciones BIN2 nuevas. En una intercalación BIN2, todos los caracteres se ordenan en función de sus puntos de código. En una intercalación BIN, solo se ordena el primer carácter en función del punto de código, mientras que los demás caracteres se ordenan en función de sus valores de bytes (Dado que la plataforma de Intel tiene una arquitectura "litte endian", los caracteres de codificación Unicode siempre se intercambian por bytes).<br /><br /> En intercalaciones binarias de tipos de datos Unicode, la configuración regional no se tiene en cuenta a la hora de ordenar los datos. Por ejemplo, Latin_1_General_BIN y Japanese_BIN producen resultados de orden idénticos cuando se usan en datos Unicode.<br /><br /> El orden binario utiliza la distinción de mayúsculas y minúsculas, y de acentos. El orden binario es también el más rápido.|  
|Distinguir mayúsculas de minúsculas (_CS)|Distingue entre letras mayúsculas y minúsculas. Si se selecciona, las letras minúsculas se ordenan por delante de sus versiones en mayúsculas. Puede establecer explícitamente la opción sin distinción de mayúsculas y minúsculas especificando _CI. La configuración de mayúsculas y minúsculas específica de la intercalación no se aplica a identificadores de objeto, como el identificador de una dimensión, el cubo y otros objetos. Para más información, vea [Sugerencias de globalización y procedimientos recomendados &#40;Analysis Services&#41;](globalization-tips-and-best-practices-analysis-services.md) .|  
|Distinguir acentos (_AS)|Distingue entre caracteres acentuados y no acentuados. Por ejemplo, 'a' no es igual a 'ấ'. Si esta opción no se activa, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] considera que las letras acentuadas son idénticas a sus versiones no acentuadas en la ordenación. Puede establecer explícitamente la opción sin distinción de acentos especificando _AI.|  
|Distinguir kana (_KS)|Distingue entre los dos tipos de caracteres Kana japoneses: Hiragana y Katakana. Si esta opción no se activa, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] considera los caracteres Hiragana y Katakana como caracteres iguales en la ordenación. No existe ningún sufijo de orden para el tipo de orden que no distingue los tipos de Kana.|  
|Distinguir ancho (_WS)|Distingue entre un carácter de un solo byte y el mismo carácter representado como un carácter de doble byte. Si esta opción no se activa, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] considera que la representación de un solo byte y de doble byte del mismo carácter es idéntica en la ordenación. No existe ningún sufijo de orden para el tipo de orden que no distingue el ancho.|  
  
##  <a name="change-the-default-language-or-collation-on-the-instance"></a><a name="bkmk_defaultLang"></a> Cambiar la configuración predeterminada de idioma o intercalación en la instancia  
 La configuración de idioma e intercalación predeterminada se establece durante la instalación, pero se puede cambiar como parte de la configuración posterior a la instalación. El cambio de la intercalación en el nivel de instancia no es tarea sencilla e incluye estos requisitos:  
  
-   El reinicio del servicio.  
  
-   Actualizar la configuración de intercalación de los objetos existentes. La configuración de intercalación se hereda al crear el objeto. Los cambios posteriores en la intercalación deben realizarse manualmente. Para obtener información detallada, vea [Cambiar idioma e intercalación dentro de un modelo de datos mediante XMLA](#bkmk_XMLA) para obtener sugerencias sobre cómo se propagan los cambios de intercalación en todo el modelo.  
  
-   Volver a procesar las particiones y dimensiones después de actualizar la intercalación.  
  
 Puede usar SQL Server Management Studio o PowerShell AMO para cambiar la configuración de idioma o intercalación predeterminada en el nivel de servidor. Como alternativa, puede modificar la ** \<configuración de Language>** y ** \<CollationName>** en el archivo msmdsrv. ini, especificando el LCID del idioma.  
  
1.  En Management Studio, haga clic con el botón secundario en nombre del servidor | **Properties** | **Idioma o intercalación**de propiedades.  
  
2.  Elija las opciones de ordenación. Para seleccionar **Binario** o **Binario 2**, desactive primero la casilla **Distinguir acentos**.  
  
     Observe que la intercalación y el idioma son configuraciones completamente independientes. Si cambia uno, los valores del otro no se filtran para mostrar las combinaciones comunes.  
  
3.  Actualice el modelo de datos para usar la nueva intercalación (vea la siguiente sección).  
  
4.  Reinicie el servicio.  
  
##  <a name="change-the-language-or-collation-on-a-cube"></a><a name="bkmk_cube"></a> Cambiar idioma o intercalación en un cubo  
  
1.  En el Explorador de soluciones, haga doble clic en el cubo para abrirlo en el Diseñador de cubos.  
  
2.  En el panel Medidas o Dimensiones, seleccione el nodo superior. El objeto de nivel superior de cualquiera de los paneles es el cubo.  
  
3.  En Propiedades, establezca `Language` y `Collation`. Los valores que elija se utilizarán en todos los objetos de cubo, incluidas las dimensiones y medidas de cubo, y afectarán a las operaciones de procesamiento y consulta.  
  
     La única forma de incrustar propiedades alternativas de idioma e intercalación en objetos dentro del cubo es a través de las traducciones. Vea [Translations &#40;Analysis Services&#41; (Traducciones &#40;Analysis Services&#41;)](translations-analysis-services.md) para más información.  
  
##  <a name="change-language-and-collation-within-a-data-model-using-xmla"></a><a name="bkmk_XMLA"></a> Cambiar idioma e intercalación dentro de un modelo de datos mediante XMLA  
 La configuración de idioma e intercalación se hereda al crear el objeto. Los cambios posteriores en estas propiedades deben realizarse manualmente. Un método para cambiar rápidamente la intercalación de varios objetos es usar un comando ALTER en un script XMLA.  
  
 De forma predeterminada, la intercalación se establece una vez en el nivel de base de datos. La herencia está implícita en el resto de la jerarquía de objetos. Si se establece explícitamente `Collation` en los objetos de dentro del cubo, lo cual está permitido en los atributos de dimensión individuales, aparecerá en la definición de XMLA. De lo contrario, solo existe la propiedad de intercalación de nivel superior.  
  
 Antes de usar XMLA para modificar una base de datos existente, asegúrese de que no está incorporando discrepancias entre la base de datos y los archivos de origen utilizados para crearla. Por ejemplo, tal vez quiera usar XMLA para cambiar rápidamente el idioma o la intercalación para pruebas de prueba de concepto, pero seguir realizando cambios en el archivo de origen (vea [Cambiar idioma o intercalación en un cubo](#bkmk_cube)), volviendo a implementar la solución con los procedimientos operativos existentes ya en vigor.  
  
1.  En Management Studio, haga clic con el botón secundario en la base de datos | **Script de base de datos como** | **ALTER en** | **nueva ventana del editor de consultas**.  
  
2.  Busque y reemplace el idioma o la intercalación existente con otro valor.  
  
3.  Presione F5 para ejecutar el script.  
  
4.  Vuelva a procesar el cubo.  
  
##  <a name="boost-performance-for-english-locales-through-enablefast1033locale"></a><a name="bkmk_enablefast1033"></a> Aumente el rendimiento de las configuraciones regionales de inglés mediante EnableFast1033Locale  
 Si utiliza el identificador de idioma Inglés (Estados Unidos) (0x0409 o 1033) como idioma predeterminado para la instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], puede obtener ventajas de rendimiento adicionales si establece la propiedad de configuración `EnableFast1033Locale`, una propiedad de configuración avanzada disponible solo para este identificador de idioma. Al establecer el valor de esta propiedad en **true** , [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] puede utilizar un algoritmo más rápido en las comparaciones y los algoritmos hash de cadenas. Para más información sobre cómo establecer las propiedades de configuración, vea [Configurar las propiedades de servidor en Analysis Services](server-properties/server-properties-in-analysis-services.md).  
  
##  <a name="gb18030-support-in-analysis-services"></a><a name="bkmk_gb18030"></a> Compatibilidad con GB18030 en Analysis Services  
 GB18030 es un estándar independiente que se usa en la República Popular China para codificar caracteres chinos. En GB18030, los caracteres pueden tener una longitud de 1, 2 o 4 bytes. En Analysis Services, no se produce ninguna conversión de datos al procesar datos de orígenes externos. Los datos simplemente se almacenan como datos Unicode. En el momento de la consulta, se realiza una conversión de GB18030 a través de las bibliotecas de cliente de Analysis Services (específicamente, el proveedor OLE DB MSOLAP.dll) cuando se devuelven datos de texto en los resultados de la consulta, en función de la configuración del sistema operativo cliente. El motor de base de datos también es compatible con GB18030. Para obtener información detallada, vea [Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md).  
  
## <a name="see-also"></a>Consulte también  
 [Escenarios de globalización para Analysis Services multidimensional](globalization-scenarios-for-analysis-services-multiidimensional.md)   
 [Sugerencias de globalización y prácticas recomendadas &#40;Analysis Services&#41;](globalization-tips-and-best-practices-analysis-services.md)   
 [Compatibilidad con la intercalación y Unicode](../relational-databases/collations/collation-and-unicode-support.md)  
  
  
