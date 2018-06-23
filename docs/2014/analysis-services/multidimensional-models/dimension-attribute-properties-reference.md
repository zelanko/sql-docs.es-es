---
title: Referencia de propiedades de atributo de dimensión | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- properties [Analysis Services], attributes
- attributes [Analysis Services], properties
ms.assetid: 7f83d1cb-4732-424f-adc5-2449c1dd1008
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: cc66df28276802d7d397e498ceb1a22abdedb80e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36103637"
---
# <a name="dimension-attribute-properties-reference"></a>Referencia de las propiedades de los atributos de dimensión
  En [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], existen numerosas propiedades que determinan el funcionamiento de las dimensiones y sus atributos. En la siguiente tabla se enumeran y describen cada una de estas propiedades de los atributos.  
  
|Property|Descripción|  
|--------------|-----------------|  
|`AttributeHierarchyDisplayFolder`|Identifica la carpeta en la que se va a mostrar la jerarquía de atributos asociada a los usuarios finales.|  
|`AttributeHierarchyEnabled`|Determina si [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ha generado una jerarquía de atributos para el atributo. Si la jerarquía de atributos no está habilitada, no es posible utilizar el atributo en una jerarquía definida por el usuario ni se puede hacer referencia a la jerarquía de atributos en instrucciones MDX (expresiones multidimensionales).|  
|`AttributeHierarchyOptimizedState`|Determina el nivel de optimización aplicado a la jerarquía de atributos. De forma predeterminada, una jerarquía de atributos está `FullyOptimized`, lo que significa que [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] genera índices para ella a fin de mejorar el rendimiento de las consultas. La otra opción, `NotOptimized`, significa que no se generan índices para la jerarquía de atributos. Usar `NotOptimized` es útil si la jerarquía de atributo se usa para propósitos distintos de la consulta, porque se construye ningún índice adicional para el atributo. Las jerarquías de atributos se pueden utilizar también para ordenar otro atributo.|  
|`AttributeHierarchyOrdered`|Determina si la jerarquía de atributos asociada está ordenada. El valor predeterminado es `True`. Sin embargo, si una jerarquía de atributo no se utilizará para las consultas, puede ahorrar tiempo de procesamiento cambiando el valor de esta propiedad en `False`.|  
|`AttributeHierarchyVisible`|Determina si la jerarquía de atributos es visible para las aplicaciones cliente. El valor predeterminado es `True`. Sin embargo, si una jerarquía de atributo no se utilizará para las consultas, puede ahorrar tiempo de procesamiento cambiando el valor de esta propiedad en `False`.|  
|`CustomRollupColumn`|Especifica la columna que define una fórmula de resumen personalizado.|  
|`CustomRollupPropertiesColumn`|Especifica la columna que contiene las propiedades de una fórmula de resumen personalizado.|  
|`DefaultMember`|Especifica una expresión MDX (expresiones multidimensionales) que define la medida predeterminada para el atributo.|  
|`Description`|Contiene la descripción del atributo.|  
|`DiscretizationBucketCount`|Contiene el número de depósitos en los que discretizar.|  
|`DiscretizationMethod`|Define el método que se va a utilizar para la discretización.|  
|`EstimatedCount`|Especifica el número estimado de miembros del atributo. El valor predeterminado es cero hasta que se ejecuta el Asistente para diseñar agregaciones. Puede dejar que el asistente cuente el número de registros o bien especificar un valor estimado. Especifique un valor manualmente si conoce el número de miembros y desea ahorrarse el tiempo necesario para realizar la consulta del recuento en la base de datos. Si trabaja con un subconjunto de prueba de los datos de producción, puede utilizar los recuentos de los datos de producción de forma que el diseño de agregaciones se optimice para los datos de producción en lugar de hacerlo para los datos de prueba.|  
|`GroupingBehavior`|Un valor definido por el usuario que proporciona una sugerencia a las aplicaciones cliente sobre cómo agrupar atributos.|  
|`ID`|Contiene el identificador (Id.) único de la dimensión.|  
|`InstanceSelection`|Proporciona una sugerencia a las aplicaciones cliente sobre cómo se debe mostrar una lista de elementos, según el número estimado de elementos de la lista. Las opciones disponibles son las siguientes:<br /><br /> **None** No se proporciona ninguna sugerencia a la aplicación cliente. Este es el valor predeterminado.<br /><br /> **DropDown** El número de elementos es lo suficientemente pequeño como para mostrarlos en una lista desplegable.<br /><br /> **List** El número de elementos es demasiado grande para una **lista**desplegable, pero no necesita filtrado.<br /><br /> **FilteredList** El número de elementos es lo suficientemente grande como para requerir que los usuarios filtren los elementos que se van a mostrar.<br /><br /> **MandatoryFilter** El número de elementos es tan grande que siempre se debe filtrar.|  
|`IsAggregatable`|Especifica si se pueden agregar los valores de los miembros del atributo. El valor predeterminado es `True`, lo que significa que la jerarquía de atributo contiene un nivel (All). Si el valor de esta propiedad es `False`, la jerarquía de atributos no contiene ningún nivel (All).|  
|`KeyColumns`|Contiene la columna o columnas que representan la clave del atributo, que es la columna de la tabla relacional subyacente de la vista del origen de datos a la que está enlazada el atributo. El valor de esta columna para cada miembro se muestra a los usuarios a menos que se especifique un valor para la propiedad `NameColumn`.|  
|`MemberNamesUnique`|Determina si los nombres de miembros de la jerarquía de atributos deben ser únicos.|  
|`MembersWithData`|Es utilizada por los atributos primarios para determinar si se van a mostrar los miembros de datos para los miembros no hoja del atributo primario. Valor de esta propiedad es utiliza únicamente cuando el valor de la `Usage` propiedad está establecida en Parent. Esto significa que se ha definido una jerarquía de atributos primarios y secundarios. Las opciones disponibles son las siguientes:<br /><br /> **NonLeafDataHidden** Se ocultan los datos no hoja.<br /><br /> **NonLeafDataVisible** Los datos no hoja son visibles.|  
|`MembersWithDataCaption`|Proporciona una cadena de plantilla utilizada por los atributos primarios para crear títulos para los miembros de datos generados por el sistema en el atributo primario. Valor de esta propiedad es utiliza únicamente cuando el valor de la `Usage` propiedad está establecida en Parent. Esto significa que se ha definido una jerarquía de atributos primarios y secundarios.|  
|`Name`|Contiene el nombre descriptivo del atributo.|  
|`NameColumn`|Identifica la columna que proporciona el nombre del atributo que se muestra a los usuarios, en lugar del valor de la columna de clave del atributo. Esta columna se utiliza cuando el valor de la columna de clave de un miembro de atributo es críptico o no útil para el usuario, o bien cuando la columna de clave está basada en una clave compuesta. La propiedad `NameColumn` no se utiliza en jerarquías primaria-secundaria, en lugar de ello, se utiliza la propiedad `NameColumn` para miembros secundarios como nombres de miembro en una jerarquía de atributos primarios y secundarios.|  
|`NamingTemplate`|Define cómo se denominan los niveles en una jerarquía de elementos primarios y secundarios construida para el atributo primario. Valor de esta propiedad es utiliza únicamente cuando el valor de la `Usage` propiedad está establecida en Parent. Esto significa que se ha definido una jerarquía de atributos primarios y secundarios.|  
|`OrderBy`|Describe cómo ordenar los miembros incluidos en la jerarquía de atributos. El valor predeterminado es el nombre, que especifica que el orden de los miembros del atributo se basa en el valor de la `NameColumn` propiedad, si existe. En caso contrario, los miembros se ordenan por el valor de la columna de clave. Las opciones disponibles son las siguientes:<br /><br /> `NameColumn` Ordena por el valor de la `NameColumn` propiedad.<br /><br /> **Key** Se ordena por el valor de la columna de clave del miembro del atributo.<br /><br /> **AttributeKey** Se ordena por el valor de la clave de miembro de un atributo especificado, que debe tener una relación de atributo con el atributo.<br /><br /> **AttributeName** Se ordena por el valor del nombre de miembro de un atributo especificado, que debe tener una relación de atributo con el atributo.|  
|`OrderByAttribute`|Identifica el atributo por el que se van a ordenar los miembros de la jerarquía de atributos.|  
|`RootMemberIf`|Determina cómo se identifican los miembros raíz o superiores de una jerarquía de elementos primarios y secundarios. Valor de esta propiedad es utiliza únicamente cuando el valor de la `Usage` propiedad está establecida en Parent. Esto significa que se ha definido una jerarquía de atributos primarios y secundarios. El valor predeterminado es `ParentIsBlankSelfOrMissing`, lo que significa que solo se tratan como miembros raíz los miembros que cumplen una o más de las condiciones descritas para `ParentIsBlank`, `ParentIsSelf` o `ParentIsMissing`. También están disponibles los siguientes valores:<br /><br /> `ParentIsBlank` Solo los miembros con un valor null, cero o una cadena vacía en la columna de clave o columnas se tratan como miembros raíz.<br /><br /> `ParentIsSelf` Solo los miembros como elementos primarios se tratan como miembros raíz.<br /><br /> `ParentIsMissing` Únicamente los miembros cuyos elementos primarios no se pueden encontrar se tratan como miembros raíz.|  
|`Type`|Contiene el tipo del atributo. Para más información, vea [Configurar tipos de atributos](attribute-properties-configure-attribute-types.md).|  
|`UnaryOperatorColumn`|Especifica la columna que proporciona operadores unarios. Es un enlace del tipo DataItem que define los detalles de una columna que proporciona un operador unario.|  
|`Usage`|Describe cómo se utiliza un atributo.<br /><br /> Las opciones disponibles son las siguientes:<br /><br /> `Regular` El atributo es un atributo normal. Este es el valor predeterminado.<br /><br /> **Key** El atributo es un atributo clave.<br /><br /> **Parent** El atributo es un atributo primario.|  
|`ValueColumn`|Identifica la columna que proporciona el valor del atributo. Si el `NameColumn` del atributo se especifica, el mismo `DataItem` valores se utilizan como valores predeterminados para el `ValueColumn` elemento. Si no se especifica el elemento `NameColumn` del atributo y la colección `KeyColumns` del mismo contiene un único elemento `KeyColumn` que representa una columna de clave con un tipo de datos de cadena, se utilizan los mismos valores de `DataItem` como valores predeterminados para el elemento `ValueColumn`.|  
  
> [!NOTE]  
>  Para obtener más información sobre cómo establecer valores para la `KeyColumn` propiedad cuando se trabaja con valores nulos y otros problemas de integridad de datos, vea [controlar problemas de integridad de datos en Analysis Services 2005](http://go.microsoft.com/fwlink/?LinkId=81891).  
  
> [!NOTE]  
>  El miembro predeterminado en un jerarquía de atributo se usa para evaluar expresiones cuando un miembro de una jerarquía de atributo no se incluye explícitamente en una consulta. El miembro predeterminado de un atributo se especifica mediante el `DefaultMember` propiedad del atributo. Siempre que se incluya una jerarquía de una dimensión en una consulta, se omiten todos los miembros predeterminados de los atributos correspondientes a los niveles de la jerarquía. Si no se incluye ninguna jerarquía de una dimensión en una consulta, se usan los miembros predeterminados para todos los atributos de la dimensión. Para más información sobre los miembros predeterminados, vea [Definir un miembro predeterminado](attribute-properties-define-a-default-member.md).  
  
## <a name="see-also"></a>Vea también  
 [Atributos y jerarquías de atributos](../multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)  
  
  