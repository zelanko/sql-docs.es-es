---
title: Información general de arquitectura lógica (Analysis Services - datos multidimensionales) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- cubes [Analysis Services], examples
- cubes [Analysis Services], about cubes
ms.assetid: 1a547bce-dacf-4d32-bc0f-3829f4b026e1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 27095834c7f3b863bbc1a4f330898790cf467ec6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62699205"
---
# <a name="logical-architecture-overview-analysis-services---multidimensional-data"></a>Información general de arquitectura lógica (Analysis Services - Datos multidimensionales)
  Analysis Services funciona en un modo de implementación de servidor que determina la arquitectura de memoria y el entorno en tiempo de ejecución utilizados por diferentes tipos de modelos de Analysis Services. Determina el modo de servidor durante la instalación. **Modo multidimensional y minería de datos** admite OLAP tradicional y minería de datos. **Modo tabular** admite modelos tabulares. **El modo integrado de SharePoint** hace referencia a una instancia de Analysis Services que se instaló como PowerPivot para SharePoint y se usa para cargar y consultar modelos de datos de Excel o PowerPivot dentro de un libro.  
  
 En este tema se explica la arquitectura básica de Analysis Services cuando se usa en modo Multidimensional y Minería de datos. Para obtener más información acerca de los otros modos, consulte [de modelos tabulares &#40;Tabular de SSAS&#41; ](../../tabular-models/tabular-models-ssas.md) y [comparar tabulares y las soluciones multidimensionales &#40;SSAS&#41;](../../../analysis-services/comparing-tabular-and-multidimensional-solutions-ssas.md).  
  
## <a name="basic-architecture"></a>Arquitectura básica  
 Una instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] puede contener varias bases de datos y una base de datos puede tener al mismo tiempo objetos OLAP y objetos de minería de datos. Las aplicaciones conectan una instancia especificada de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] y una base de datos especificada. Un equipo servidor puede hospedar varias instancias de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Las instancias de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] se denominan "\<ServerName >\\< InstanceName\>". La ilustración siguiente muestra todas las relaciones indicadas entre [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] objetos.  
  
 ![Relaciones de objetos de ejecución de AMO](../../../analysis-services/dev-guide/media/amo-runningobjects.gif "relaciones de objetos de ejecución de AMO")  
  
 Las clases básicas son el conjunto mínimo de objetos necesario para generar un cubo. Este conjunto mínimo de objetos incluye una dimensión, un grupo de medida y una partición. La agregación es opcional.  
  
 Las dimensiones se crean a partir de atributos y jerarquías. Las jerarquías están formadas por un conjunto ordenado de atributos, donde cada atributo del conjunto corresponde a un nivel de la jerarquía.  
  
 Los cubos se crean a partir de dimensiones y grupos de medida. Las dimensiones de la colección de dimensiones de un cubo pertenecen a la colección de dimensiones de la base de datos. Los grupos de medida son colecciones de medidas que tienen la misma vista del origen de datos y el mismo subconjunto de dimensiones del cubo. Un grupo de medida incluye una o más particiones para administrar los datos físicos. El grupo de medida puede tener un diseño de agregaciones predeterminado. Todas las particiones del grupo de medida pueden usar el diseño de agregaciones predeterminado; asimismo, cada partición puede tener su propio diseño de agregaciones.  
  
 Objetos Server  
 Cada instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] se considera un objeto de servidor diferente en AMO; cada instancia distinta se conecta a un objeto <xref:Microsoft.AnalysisServices.Server> con una conexión diferente. Cada objeto de servidor contiene uno o más orígenes de datos, vistas del origen de datos y objetos de base de datos, así como ensamblados y roles de seguridad.  
  
 Objetos Dimension  
 Cada objeto de base de datos contiene varios objetos de dimensión. Cada objeto de dimensión contiene uno o más atributos, que se organizan en jerarquías.  
  
 Objetos de cubo  
 Cada objeto de base de datos contiene uno o más objetos de cubo. Un cubo se define por medio de sus medidas y dimensiones. Las medidas y dimensiones de un cubo se derivan de las tablas y vistas de la vista del origen de datos en la que se basa el cubo, o que se genera a partir de las definiciones de medidas y dimensiones.  
  
## <a name="object-inheritance"></a>Herencia de objetos  
 El modelo de objetos ASSL contiene varios grupos de elementos repetidos. Por ejemplo, el grupo de elementos "`Dimensions` contienen `Hierarchies`," define la jerarquía de dimensión de un elemento. Tanto los objetos `Cubes` como `MeasureGroups` contienen el grupo de elementos "`Dimensions` contain `Hierarchies`".  
  
 A menos que se invalide explícitamente, un elemento hereda los detalles de estos grupos de elementos repetidos del nivel superior. Por ejemplo, el valor de `Translations` de un objeto `CubeDimension` es el mismo que el valor de `Translations` de su elemento antecesor, `Cube`.  
  
 Para invalidar explícitamente propiedades heredadas de un objeto de nivel superior, un objeto no necesita repetir explícitamente la estructura completa y las propiedades del objeto de nivel superior. Las únicas propiedades que un objeto necesita indicar explícitamente son las propiedades que el objeto desea invalidar. Por ejemplo, un objeto `CubeDimension` puede incluir únicamente los elementos `Hierarchies` que se deben deshabilitar en el objeto `Cube`, los elementos para los que la visibilidad se debe cambiar o los elementos para los que no se han indicado algunos detalles de `Level` en el nivel `Dimension`.  
  
 Algunas propiedades especificadas en un objeto proporcionan valores predeterminados para la misma propiedad en un objeto secundario o descendiente. Por ejemplo, `Cube.StorageMode` proporciona el valor predeterminado de `Partition.StorageMode`. Para los valores predeterminados heredados, ASSL aplica estas reglas para los valores predeterminados heredados:  
  
-   Cuando la propiedad del objeto secundario tiene el valor NULL en XML, el valor de la propiedad tiene como valor predeterminado el valor heredado. Sin embargo, si consulta el valor en el servidor, éste devuelve el valor NULL del elemento XML.  
  
-   No es posible determinar mediante programación si la propiedad de un objeto secundario se ha establecido directamente en el objeto secundario o se ha heredado.  
  
## <a name="example"></a>Ejemplo  
 El cubo Imports contiene dos medidas, Packages y Last, y tres dimensiones relacionadas, Route, Source y Time.  
  
 ![Ejemplo de cubo 1](../../../analysis-services/dev-guide/media/cubeintro1.gif "ejemplo 1 de cubo")  
  
 Los valores alfanuméricos más pequeños que están alrededor del cubo son los miembros de las dimensiones. Los miembros de ejemplo son ground (miembro de la dimensión Route), Africa (miembro de la dimensión Source) y 1st quarter (miembro de la dimensión Time).  
  
### <a name="measures"></a>medidas  
 Los valores de las celdas del cubo representan las dos medidas, Packages y Last. La medida Packages representa el número de paquetes importados y la función `Sum` se utiliza para agregar los hechos. La medida Last representa la fecha de recepción y la función `Max` se utiliza para agregar los hechos.  
  
### <a name="dimensions"></a>Dimensions  
 La dimensión Route representa los medios por los que las importaciones llegan a su destino. Los miembros de esta dimensión son ground, nonground, air, sea, road o rail. La dimensión Source representa las ubicaciones en las que se producen las importaciones, caso de África o Asia. La dimensión Time representa los trimestres y semestres de un único año.  
  
### <a name="aggregates"></a>Agregados  
 Los usuarios corporativos de un cubo pueden determinar el valor de cualquier medida para los miembros de cada dimensión, con independencia del nivel del miembro de la dimensión, ya que [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] agrega valores a los niveles superiores según sea necesario. Por ejemplo, los valores de medida en la ilustración anterior se pueden agregar según una jerarquía de calendario estándar mediante el uso de la jerarquía de tiempo de calendario en la dimensión de tiempo como se muestra en el diagrama siguiente.  
  
 ![Diagrama de medidas organizadas en una dimensión de tiempo](../../../analysis-services/dev-guide/media/cubeintro2.gif "diagrama de medidas organizadas en una dimensión de tiempo")  
  
 Además de agregar medidas mediante una sola dimensión, se pueden agregar medidas mediante combinaciones de miembros de dimensión diferentes. Esto permite a los usuarios corporativos evaluar las medidas en varias dimensiones al mismo tiempo. Por ejemplo, si un usuario corporativo desea analizar las importaciones trimestrales que han llegado por aire desde Eastern Hemisphere y Western Hemisphere, puede emitir una consulta del cubo para recuperar el siguiente conjunto de datos.  
  
||||.|||Último|||  
|-|-|-|--------------|-|-|----------|-|-|  
||||All Sources|Eastern Hemisphere|Western Hemisphere|All Sources|Eastern Hemisphere|Western Hemisphere|  
|All Time|||25110|6547|18563|DEC-29-99|DEC-22-99|DEC-29-99|  
||1st half||11173|2977|8196|Jun-28-99|Jun-20-99|Jun-28-99|  
|||1st quarter|5108|1452|3656|Mar-30-99|Mar-19-99|Mar-30-99|  
|||2nd quarter|6065|1525|4540|Jun-28-99|Jun-20-99|Jun-28-99|  
||2nd half||13937|3570|10367|DEC-29-99|DEC-22-99|DEC-29-99|  
|||3rd quarter|6119|1444|4675|Sep-30-99|Sep-18-99|Sep-30-99|  
|||4th quarter|7818|2126|5692|DEC-29-99|DEC-22-99|DEC-29-99|  
  
 Una vez definido un cubo, se pueden crear agregaciones o cambiar agregaciones existentes para establecer opciones, como que las agregaciones se precalculen durante el procesamiento o se calculen en el momento de la consulta. **Tema relacionado:**[agregaciones y diseños de agregaciones](../../multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md).  
  
### <a name="mapping-measures-attributes-and-hierarchies"></a>Asignar medidas, atributos y jerarquías  
 Las medidas, los atributos y las jerarquías del cubo del ejemplo se derivan de las siguientes columnas de las tablas de dimensiones y de hechos del cubo.  
  
|Medida o atributo (nivel)|Miembros|Tabla de origen|Columna de origen|Valor de la columna de ejemplo|  
|------------------------------------|-------------|------------------|-------------------|-------------------------|  
|Medida de paquetes|No aplicable|ImportsFactTable|.|12|  
|Última medida|No aplicable|ImportsFactTable|Último|May-03-99|  
|Nivel Route Category en la dimensión Route|nonground,ground|RouteDimensionTable|Route_Category|Nonground|  
|Atributo Route en la dimensión Route|air,sea,road,rail|RouteDimensionTable|Ruta|Sea|  
|Atributo Hemisphere en la dimensión Source|Eastern Hemisphere,Western Hemisphere|SourceDimensionTable|Hemisphere|Eastern Hemisphere|  
|Atributo Continent en la dimensión Source|Africa,Asia,AustraliaEurope,N. America,S. America|SourceDimensionTable|Continente|Europe|  
|Atributo Half en la dimensión Time|1st half,2nd half|TimeDimensionTable|Half|2nd half|  
|Atributo Quarter en la dimensión Time|1st quarter,2nd quarter,3rd quarter,4th quarter|TimeDimensionTable|Trimestre|3rd quarter|  
  
 Los datos de una única celda de cubo suelen derivarse de varias filas de la tabla de hechos. Por ejemplo, la celda del cubo en la intersección del miembro air, el miembro Africa y el miembro 1st quarter contiene un valor que se deriva al agregar las siguientes filas de la **ImportsFactTable** tabla de hechos.  
  
|||||||  
|-|-|-|-|-|-|  
|Import_ReceiptKey|RouteKey|SourceKey|TimeKey|.|Último|  
|3516987|1|6|1|15|Ene-10-99|  
|3554790|1|6|1|40|19-Ene-99|  
|3572673|1|6|1|34|Jan-27-99|  
|3600974|1|6|1|45|Feb-02-99|  
|3645541|1|6|1|20|Feb-09-99|  
|3674906|1|6|1|36|Feb-17-99|  
  
 En la tabla anterior, cada fila tiene los mismos valores para el **RouteKey**, **SourceKey**, y **TimeKey** columnas, que indica que dichas filas contribuyen a la misma celda del cubo.  
  
 En este ejemplo se representa un cubo muy sencillo, en donde el cubo tiene un solo grupo de medida y todas las tablas de dimensiones se combinan en la tabla de hechos en un esquema en estrella. Otro esquema común es el esquema de copo de nieve, en el que una o más tablas de dimensiones se combinan con otra tabla de dimensiones, en lugar de combinarse directamente con la tabla de hechos. **Tema relacionado:**[dimensiones &#40;Analysis Services - datos multidimensionales&#41;](../../multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md).  
  
 Este ejemplo contiene una sola tabla de hechos. Cuando un cubo tiene varias tablas de hechos, las medidas de cada tabla de hechos se organizan en grupos de medida y un grupo de medida se relaciona con un determinado conjunto de dimensiones mediante relaciones de dimensiones definidas. Estas relaciones se definen mediante la especificación de las tablas participantes en la vista del origen de datos y la granularidad de la relación. **Tema relacionado:**[relaciones de dimensión](../../multidimensional-models-olap-logical-cube-objects/dimension-relationships.md).  
  
## <a name="see-also"></a>Vea también  
 [Bases de datos de modelos multidimensionales &#40;SSAS&#41;](../multidimensional-model-databases-ssas.md)  
  
  
