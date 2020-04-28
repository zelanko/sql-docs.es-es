---
title: Conceptos de CSDLBI | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
ms.assetid: 2fbdf621-a94d-4a55-a088-3d56d65016ac
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9a51393748d47159cfc4cf6bf8bd25e50307cfb7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "79525446"
---
# <a name="csdlbi-concepts"></a>Conceptos de CSDLBI
  El lenguaje de definición de esquemas conceptuales con anotaciones BI (CSDLBI) se basa en Entity Data Framework, que es una abstracción para representar datos de una forma que permita el acceso, la consulta o la exportación de conjuntos de datos diversos mediante programación. CSDLBI se emplea para representar modelos de datos creados mediante [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] porque admite informes y aplicaciones completos controlados por datos.  
  
 En esta sección se explica cómo se asigna la representación CSDLBI a los modelos de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] (tanto tabulares como multidimensionales), y se muestran ejemplos de cada tipo de modelo.  
  
 Los ejemplos usados para ilustrar estos conceptos se han tomado de la base de datos de ejemplo AdventureWorks, disponible en Codeplex. Para obtener más información acerca de los ejemplos, vea [ejemplos de Adventure Works para SQL Server](https://go.microsoft.com/fwlink/?linkID=220093).  
  
## <a name="structure-of-a-tabular-model-in-csdlbi"></a>Estructura de un modelo tabular en CSDLBI  
 Un documento CSDLBI que describe un modelo de informe y sus datos comienza con la instrucción XSD, seguida de la definición de un modelo.  
  
 El modelo es un espacio de nombres, que contiene las siguientes entidades, asociaciones y propiedades principales:  
  
-   Con `EntityContainer` se enumeran las tablas del modelo.  
  
-   Cada tabla aparece con `EntityContainer` como `EntitySet`.  
  
-   Cada relación entre dos tablas se describe como conjunto `AssociationSet` que define los extremos y roles de la relación.  
  
-   El elemento `EntityType` se amplía para que BISM proporcione detalles adicionales sobre las tablas y las columnas que contienen, incluidas las propiedades para fines de ordenación y visualización.  
  
-   El elemento `Measure` define los cálculos que se pueden usar en el modelo. Una medida se puede convertir en KPI al agregar un conjunto de atributos de presentación especiales, mediante el nuevo elemento `KPI`.  
  
-   No hay representación independiente de las perspectivas. Las columnas y tablas que no están incluidas en una perspectiva se encuentran en el CSDL pero se marcan con el atributo `Hidden`.  
  
### <a name="entities-entitysets-and-entitytypes"></a>Entidades, EntitySets y EntityTypes  
 La noción de una entidad en Entity Data Framework se amplía para representar columnas y tablas del modelo de datos. El extracto siguiente muestra la lista de elementos `EntitySet` de un modelo simple que solo contiene tres tablas.  
  
```  
<EntityContainer Name="SimpleModel">  
<EntitySet Name="DimCustomer"EntityType="SimpleModel.DimCustomer">  
     <bi:EntitySet />  
   </EntitySet>  
<EntitySet Name="DimDate" EntityType="SimpleModel.DimDate">  
     <bi:EntitySet />  
   </EntitySet>  
<EntitySet Name="DimGeography" EntityType="SimpleModel.DimGeography">  
     <bi:EntitySet />  
   </EntitySet> />  
  
```  
  
 `EntitySet` no contiene información acerca de las columnas o los datos de la tabla. La descripción detallada de las columnas y sus propiedades se proporcionan en el elemento EntityType.  
  
 El elemento `EntitySet` para cada entidad (tabla) incluye una colección de propiedades que definen la columna de clave, el tipo de datos y la longitud de la columna, la nulabilidad, el comportamiento de ordenación, etc. Por ejemplo, el extracto de CSDL siguiente describe tres columnas de la tabla Customer. La primera columna es una columna oculta especial que usa el modelo internamente.  
  
```  
<EntityType Name="Customer">  
  <Key>  
     <PropertyRef Name="RowNumber" />  
  </Key>  
    <Property Name="RowNumber" Type="Int64" Nullable="false">  
     <bi:Property Hidden="true" Contents="RowNumber"  
       Stability="RowNumber" />  
    </Property>  
    <Property Name="CustomerKey" Type="Int64" Nullable="false">  
      <bi:Property />  
    </Property>  
     <Property Name="FirstName" Type="String" MaxLength="Max" FixedLength="false">  
       <bi:Property />  
      </Property>  
  
```  
  
 Para limitar el tamaño del documento de CSDLBI que se genera, las propiedades que aparecen varias veces en una entidad se especifican mediante una referencia a una propiedad existente, de modo que solo es necesario indicar la propiedad una vez para `EntityType`. La aplicación cliente puede obtener el valor de la propiedad mediante la búsqueda del elemento `EntityType` que coincide con `OriginEntityType`.  
  
### <a name="relationships"></a>Relaciones  
 En Entity Data Framework, las relaciones se definen como *asociaciones* entre entidades.  
  
 Las asociaciones siempre tienen exactamente dos extremos, uno que apunta a un campo o columna de una tabla. Por lo tanto, son posibles múltiples relaciones entre dos tablas, si las relaciones tienen extremos distintos. Un nombre de rol se asigna a los extremos de la asociación, e indica como se usa la asociación en el contexto del modelo de datos. Un ejemplo de un nombre de rol podría **enviarse**, cuando se aplica a un identificador de cliente relacionado con el identificador de cliente en una tabla de pedidos.  
  
 La representación CSDLBI del modelo también contiene atributos en la asociación que determinan cómo se asignan las entidades entre sí en términos de *multiplicidad* de la asociación. La multiplicidad indica si el atributo o la columna en el extremo de una relación entre tablas está en el lado uno de una relación o en el lado de varios. No hay ningún valor independiente para las relaciones uno a uno. Las anotaciones CSDLBI admiten la multiplicidad de 0 (lo que significa que la entidad no está asociada a nada) o 0..1, lo que significa una relación de uno a uno o una relación de uno a varios.  
  
 El ejemplo siguiente representa la salida CSDLBI para una relación entre las tablas Date y ProductInventory, donde las dos tablas están combinadas por la columna DateAlternateKey. Observe que, de forma predeterminada, el nombre de `AssociationSet` es el nombre completo de las columnas que intervienen en la relación. No obstante, puede cambiar este comportamiento al diseñar el modelo, para usar otro formato de nomenclatura.  
  
```  
<AssociationSet Name="ProductInventory_Date_DateKey" Association="Model.ProductInventory_Date_DateKey">  
              <End EntitySet="ProductInventory" />  
              <End EntitySet="Date" />  
              <bi:AssociationSet />  
            </AssociationSet>  
  
```  
  
### <a name="visualization-and-navigation-properties"></a>Propiedades de visualización y navegación  
 Una parte importante de las anotaciones CSDLBI son las propiedades para definir la presentación en el nivel de informe y para navegar por las relaciones entre las entidades. Normalmente, cuando se crea un modelo de datos, no se considera importante controlar cómo se ordenan o agrupan los datos, o cuál podría ser el valor predeterminado, en el suposición de que la aplicación cliente especificara la ordenación y otros detalles de presentación. No obstante, los modelos tabulares de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] están diseñados para la integración con el cliente de informes de [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], e incluyen propiedades y atributos que admiten la presentación de entidad desde el modelo de datos en la superficie de diseño de informes.  
  
 Las extensiones para la visualización incluyen atributos para especificar la agregación predeterminada que se usará con datos numéricos, para indicar que un campo de texto apunta a una dirección URL de una imagen o para especificar el campo que se emplea para ordenar el campo actual.  
  
### <a name="name-properties-and-naming-conventions"></a>Propiedades de nombre y convenciones de nomenclatura  
 El esquema CSDLBI indica que cada entidad tiene un nombre único y un identificador que se puede usar como clave. Además, algunas entidades pueden tener leyendas que usan para la visualización y nombres contextuales que cambian en función de dónde se usa la entidad.  
  
 El elemento `Documentation` ofrece a los diseñadores de informes la posibilidad de indicar una descripción de la entidad para ayudar a los usuarios empresariales a comprender el significado de los datos. Algunas entidades también permiten uno o varios atributos `Annotation`, que proporcionan metadatos adicionales para su consumo por parte de la aplicación o los clientes.  
  
 Al generar un modelo, las herramientas de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y los nombres que se crean para los objetos siguen las convenciones de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para la nomenclatura de objetos y la unicidad de los nombres. No obstante, debido a que CSDLBI está basado en Entity Data Framework (EDF), lo que requiere que los nombres cumplan las convenciones de los identificadores de C#, cuando el servidor crea la salida CSDLBI para un modelo, toma los nombres usados en el esquema de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y crea automáticamente nuevos nombres de objeto que cumplen los requisitos de EDF. En la tabla siguiente se describen las operaciones por las que se generan los nuevos nombres.  
  
|Regla|Acción|  
|----------|------------|  
|Sin caracteres prohibidos|Los caracteres prohibidos se reemplazan por el carácter de subrayado.|  
|Los nombres deben ser únicos|Si dos cadenas son iguales, una se convierte en única anexando un carácter de subrayado además de un número|  
  
> [!WARNING]  
>  Las leyendas y los calificadores tienen traducciones y, para un determinado idioma, uno u otro podría estar presente. Esto significa que en caso de que se concatenen un calificador y un nombre o un calificador y una leyenda, las cadenas podrían estar en dos idiomas distintos.  
  
## <a name="additions-to-support-multidimensional-models"></a>Adiciones para admitir modelos multidimensionales  
 La versión 1.0 de las anotaciones CSDLBI solo admitía modelos tabulares. En la versión 1.1 se agregó compatibilidad con los modelos multidimensionales (cubos OLAP) creados mediante herramientas tradicionales de desarrollo de BI. Por consiguiente, ahora se puede emitir una solicitud XML a un modelo multidimensional y recibir una definición CSDLBI del modelo, para su uso en los informes.  
  
 **Cubos:** Un SQL Server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] base de datos tabular solo puede contener un modo. En cambio, cada base de datos multidimensional puede contener varios cubos y cada base de datos está asociada a un cubo predeterminado. Por lo tanto, al emitir una solicitud XML en un servidor multidimensional, es necesario especificar el cubo; en caso contrario, se devolverá el XML del cubo predeterminado.  
  
 Por lo demás, la representación de un cubo es muy similar a la de una base de datos de modelo tabular. El nombre del cubo y el cubo corresponden al nombre de la base de datos tabular y al identificador de la base de datos.  
  
 **Dimensiones:** Una dimensión se representa en CSDLBI como una entidad (tabla) con columnas y propiedades. Tenga en cuenta que, aunque no se incluya en una perspectiva, una dimensión incluida en el modelo se representará en la salida de CSDL marcada como `Hidden`.  
  
 **Perspectivas:** Un cliente puede solicitar CSDL para perspectivas individuales. Para obtener más información, vea [DISCOVER_CSDL_METADATA conjunto de filas](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-csdl-metadata-rowset).  
  
 **Jerarquías:** Las jerarquías se admiten y representan en CSDLBI como un conjunto de niveles.  
  
 **Miembros:** Se ha agregado compatibilidad con el miembro predeterminado y los valores predeterminados se agregan automáticamente a la salida de CSDLBI.  
  
 **Miembros calculados:** Los modelos multidimensionales admiten miembros calculados para los secundarios de **todos** con un único miembro real.  
  
 **Atributos de dimensión:** En la salida de CSDLBI, se admiten los atributos de dimensión y se marcan automáticamente como no agregables.  
  
 **KPI:** Los KPI se admiten en la versión 1,1 de CSDLBI, pero la representación ha cambiado. Antes, un KPI era una propiedad de una medida. En la versión 1,1, el elemento KPI puede agregarse a una medida  
  
 **Nuevas propiedades:** Se han agregado atributos adicionales para admitir los modelos DirectQuery.  
  
 **Limitaciones:** No se admite la seguridad de celda.  
  
## <a name="see-also"></a>Consulte también  
 [Anotaciones de CSDL para Business Intelligence &#40;CSDLBI&#41;](/analysis-services/csdlbi/csdl-annotations-for-business-intelligence-csdlbi)  
  
  
