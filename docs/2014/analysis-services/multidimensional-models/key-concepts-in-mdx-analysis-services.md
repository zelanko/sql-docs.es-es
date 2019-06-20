---
title: Conceptos clave para MDX (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Multidimensional Expressions [Analysis Services], about MDX
- dimensional modeling [MDX]
- MDX [Analysis Services], about MDX
- Multidimensional Expressions [Analysis Services], dimensional modeling
- MDX [Analysis Services], dimensional modeling
ms.assetid: 4797ddc8-6423-497a-9a43-81a1af7eb36c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b51c763987fdfe8bbaf08851094a5e6e6d267c36
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66074860"
---
# <a name="key-concepts-in-mdx-analysis-services"></a>Conceptos clave de MDX (Analysis Services)
  Para poder utilizar las expresiones multidimensionales (MDX) para consultar datos multidimensionales o crear expresiones MDX en un cubo, viene bien conocer los conceptos y los términos multidimensionales.  
  
 La mejor forma de empezar es con un ejemplo de resumen de datos que ya conozca y, entonces, ver cómo se relacionan con él las MDX. Esta es una tabla dinámica creada en Excel, se rellena con datos de un cubo de ejemplo de Analysis Services.  
  
 ![PivotTable con medidas y dimensiones que se mencionan](../media/ssas-keyconcepts-pivot1-measures-dimensions.png "PivotTable con medidas y dimensiones que se mencionan")  
  
## <a name="measures-and-dimensions"></a>Medidas y dimensiones  
 Un cubo de Analysis Services consta de medidas, dimensiones y atributos de dimensiones, los cuales resultan evidentes en el ejemplo de tabla dinámica.  
  
 **Medidas** son los valores de datos numéricos que encontramos en celdas, agregados por medio de una suma, recuento, porcentaje, valor mínimo, valor máximo o valor medio. Los valores de medidas son dinámicos, se calculan en tiempo real, en respuesta a la navegación e interacción con la tabla dinámica. En este ejemplo, las celdas muestran las cantidades de ventas de cada distribuidor que aumentan o disminuyen en función de si se expanden o contraen los ejes. Puede obtener la cantidad de ventas de cada distribuidor para cualquier combinación de fecha (año, trimestre, mes o fecha) y de territorio de ventas (grupo de países, país o región), resumidas para un contexto en particular. Otros términos sinónimos de "medidas" son hechos (en los almacenes de datos) y campos calculados (en los modelos de datos tabulares y Excel).  
  
 Las**dimensiones** se muestran en los ejes de columnas y filas de una tabla dinámica y son las que dan significado a las medidas. Las dimensiones equivalen a las tablas en un modelo de datos relacional. Algunos ejemplos de dimensiones son tiempo, geografía, productos, clientes, empleados, etc. Este ejemplo tiene dos dimensiones, Territorio de ventas en las filas y Fecha en la parte superior, pero puede arrastrar y soltar fácilmente otras dimensiones asociadas a las ventas del distribuidor, como Promociones o Productos, para ver el comportamiento de las ventas a lo largo de estas dimensiones. Las posibilidades de explorar datos de formas interesantes depende de las dimensiones que se creen y de si están relacionados con tablas de hechos en el origen de datos.  
  
 Los**atributos de la dimensión** son los elementos con nombre dentro de una dimensión, el equivalente a las columnas en una tabla. En este ejemplo, los atributos de la dimensión Territorio de ventas son el grupo de países (Europa, América del Norte, Pacífico), el país (Canadá, Estados Unidos) y la región (Central, Noreste, Noroeste, Sureste, Suroeste).  
  
 Cada atributo tiene una colección de valores de datos, o miembros, asociada. En nuestro ejemplo, los miembros del atributo Grupo de países son Europa, América del Norte y Pacífico. Los**miembros** son los valores de datos que pertenecen a un atributo.  
  
> [!NOTE]  
>  Un aspecto de los modelos de datos es formalizar las pautas y las relaciones que ya existen en los propios datos. Cuando se trabaja con datos clasificados en una jerarquía natural, como es el caso de países-regiones-ciudades, se puede formalizar esa relación creando una **relación de atributos**. Una relación de atributo es una relación uno a varios entre atributos, por ejemplo, una relación entre un estado y una ciudad: un estado tiene muchas ciudades, pero una ciudad pertenece a un solo estado. Creación de relaciones de atributo en el modelo acelera el rendimiento de las consultas, por lo que es una práctica recomendada para crearlos si los datos lo admiten. Puede crear una relación de atributos en el Diseñador de dimensiones en SQL Server Data Tools. Vea [Define Attribute Relationships](attribute-relationships-define.md).  
  
 En Excel, los metadatos del modelo aparecen en la lista de campos de las tablas dinámicas.  Compare la tabla dinámica anterior con la lista de campos siguiente. Observe que la lista de campos contienen Territorio de ventas, Grupo, País, Región (metadatos), mientras que la tabla dinámica solo contiene miembros (valores de datos). Conocer la forma de los iconos puede ayudarnos a relacionar fácilmente los elementos de un modelo multidimensional con una tabla dinámica de Excel.  
  
 ![Lista de campos de tabla dinámica](../media/ssas-keyconcepts-ptfieldlist.png "lista de campos de tabla dinámica")  
  
## <a name="attribute-hierarchies"></a>Jerarquías de atributo  
 Casi por intuición, sabe que los valores de una tabla dinámica suben o bajan al expandir y contraer los niveles a lo largo de cada eje, pero ¿por qué? La respuesta se encuentra en las jerarquías de los atributos.  
  
 Contraiga todos los niveles y fíjese en los totales generales de cada Grupo de países y Año natural. Este valor procede de lo que se conoce como **miembro (Todos)** de una jerarquía. El miembro (Todos) es un valor calculado de todos los miembros de una jerarquía de atributo.  
  
-   El miembro (Todos) de todos los Grupos de países y Fechas combinados es $80.450.596,98.  
  
-   El miembro (Todos) del año natural 2008 es $16.038.062,60  
  
-   El miembro (Todos) de Pacífico es $1.594.335,38  
  
 Las agregaciones como estas están precalculadas y se almacenan con antelación, lo que forma parte del secreto de la rápida respuesta de las consultas de Analysis Services.  
  
 ![Tabla dinámica con todos los miembros que se mencionan](../media/ssas-keyconcepts-pivot2-allmember.png "tabla dinámica con todos los miembros que se mencionan")  
  
 Vaya expandiendo la jerarquía y llegará al nivel más bajo. Es lo que se conoce como el **miembro "hoja"**. Un miembro hoja es un miembro de una jerarquía que no posee miembros secundarios. En este ejemplo, Australia es el miembro hoja.  
  
 ![Tabla dinámica con documentos de calle de miembro hoja](../media/ssas-keyconcepts-pivot3-leafparent.PNG "tabla dinámica con documentos de calle de miembro hoja")  
  
 Todo lo que está por encima se denomina **miembro "primario"**. Pacífico es el miembro primario de Australia.  
  
 **Los componentes de una jerarquía de atributo**  
  
 Juntos, todos estos conceptos crean el concepto de una **jerarquía de atributo**. Una jerarquía de atributo es una jerarquía de miembros de atributo que contiene los siguientes niveles:  
  
-   Un nivel hoja que contiene cada miembro de atributo distintivo; cada miembro del nivel hoja también se conoce como **miembro hoja**.  
  
-   Niveles intermedios si la jerarquía de atributo es una jerarquía de elementos primarios y secundarios (se aborda en detalle más adelante).  
  
-   Un miembro (Todos) que contiene el valor agregado de todos los atributos secundarios. Si lo desea, puede ocultar o desactivar el nivel (All) cuando no tiene sentido para los datos. Por ejemplo, aunque el código de producto es numérico, no sería sentido suma o promedio ni agregar todos los códigos de producto.  
  
> [!NOTE]  
>  Los programadores de BI suelen definir las propiedades de la jerarquía de atributo para conseguir ciertos comportamientos en las aplicaciones cliente o conseguir determinadas ventajas en la actuación. Por ejemplo, establecería AttributeHierarchyEnabled = False en atributos para el que el miembro (All) no tiene sentido. Otra opción sería, sencillamente, ocultar el miembro (Todos), en cuyo caso se definiría AttributeHierarchyVisible=False. Vea [Dimension Attribute Properties Reference](dimension-attribute-properties-reference.md) para conocer más detalles de las propiedades.  
  
## <a name="navigation-hierarchies"></a>Navegación por las jerarquías  
 En la tabla dinámica (al menos en este ejemplo), los ejes de fila y columna se expanden para mostrar los niveles inferiores de los atributos. Se puede conseguir un árbol expandible mediante la navegación por las jerarquías creadas en un modelo.  En el modelo de ejemplo AdventureWorks, la dimensión Territorio de ventas tiene una jerarquía multinivel que comienza por Grupo de países, seguido por País y Región.  
  
 Como puede ver, las jerarquías se utilizan para dar una ruta de navegación en una tabla dinámica u otros objetos de resumen de datos. Hay dos tipos básicos: equilibrados y no equilibrados.  
  
 **Jerarquías equilibradas**  
  
|||  
|-|-|  
|![PivotTable con jerarquía equilibrada mencionada](../media/ssas-keyconcepts-pivot4-balancedhierarchy.PNG "PivotTable con jerarquía equilibrada mencionada")|Una **jerarquía equilibrada** es una jerarquía en la que existe el mismo número de niveles entre el nivel superior y cualquier miembro hoja.<br /><br /> Una **jerarquía natural** es la que combina de forma natural los datos subyacentes. Algunos ejemplos comunes son País-Región-Provincia o Año-Mes-Día o Categoría-Subcategoría, donde se puede predecir de qué nivel se desprende cada nivel subordinado.<br /><br /> En un modelo multidimensional, la mayoría de las jerarquías son jerarquías equilibradas y muchas de ellas también son naturales.<br /><br /> Otro término sobre modelos relacionado es una `user-defined hierarchy`, que se suele utilizar por oposición a las jerarquías de atributo. Designa sencillamente una jerarquía creada por el programador de BI, por oposición a las jerarquías de atributo, generadas automáticamente por Analysis Services cuando se define un atributo.|  
  
 **Jerarquías desequilibradas**  
  
|||  
|-|-|  
|![PivotTable con jerarquía desigual mencionada](../media/ssas-keyconcepts-pivot15-raggedhierarchy.PNG "PivotTable con jerarquía desigual mencionada")|Una **jerarquía desigual** o **desequilibrada** es una jerarquía en la que el número de niveles entre el nivel superior y los miembros hoja es distinto. Nuevamente, es una jerarquía creada por el programador de BI, pero en este caso existen espacios en los datos.<br /><br /> En el modelo de ejemplo AdventureWorks, Territorio de ventas ilustra una jerarquía desigual porque Estados Unidos tiene un nivel adicional (Regiones) que no existe en otros países del ejemplo.<br /><br /> Las jerarquías desiguales plantean un reto para los programadores de BI si la aplicación cliente no controla las jerarquías desiguales con elegancia. En el modelo de Analysis Services, se puede crear una **jerarquía de tipo primario-secundario** que defina explícitamente una relación entre datos de varios niveles, eliminando toda ambigüedad en lo que respecta a cómo se relaciona un nivel con el siguiente. Vea [Parent-Child Hierarchy](parent-child-dimension.md) .|  
  
## <a name="key-attributes"></a>Atributos clave  
 Los modelos son una colección de objetos relacionados que requieren claves e índices para establecer las asociaciones. Los modelos de Analysis Services no son diferentes. Para cada dimensión (recuerde que es equivalente a una tabla en un modelo relacional), hay un atributo clave. El **atributo clave** se usa en relaciones de clave externa con la tabla de hechos (grupo de medidas). Todos los atributos sin clave de la dimensión están enlazados (directa o indirectamente) con el atributo clave.  
  
 Con frecuencia, aunque no siempre, el atributo clave es también el **Atributo de granularidad**. Granularidad significa el nivel de detalle o precisión dentro de los datos. También en esta ocasión poner un ejemplo común es la mejor forma de entenderlo. Tenga en cuenta los valores de fecha: Para las ventas diarias, se necesita valores de fecha especificados para el día. las cuotas, trimestralmente podría ser suficiente, pero si los datos analíticos constan de los resultados de un evento deportivo carrera, el nivel de detalle necesario que sea de milisegundos. El nivel de precisión en los valores de datos se conoce como grano.  
  
 Moneda es otro ejemplo: una aplicación financiera puede realizar un seguimiento de los valores monetarios hasta muchas posiciones decimales, mientras que el captador de fondos de tu escuela local es posible que solo necesitará valores próximos al euro. Comprender el concepto de grano es importante para evitar el almacenamiento de datos innecesarios. Recortar los milisegundos de una marca de tiempo o céntimos del importe de ventas puede ahorrar espacio de almacenamiento y tiempo de procesamiento cuando el nivel de detalle no es importante para el análisis que se hará.  
  
 Para definir el atributo de granularidad, use la pestaña Uso de dimensiones en el Diseñador de cubos de SQL Server Data Tools. En el modelo de ejemplo AdventureWorks, el atributo clave de la dimensión Fecha es la clave Fecha. En Pedidos de ventas, el atributo de granularidad es equivalente al atributo clave. En Objetivos de ventas, el nivel de granularidad es trimestral y, por tanto, el atributo de granularidad se define en Trimestre natural.  
  
 ![Modelo que muestra el atributo de granularidad](../media/ssas-keyconcepts-granularityattrib.png "que muestra el atributo de granularidad del modelo")  
  
> [!NOTE]  
>  Si el atributo de granularidad y el atributo clave son diferentes, los atributos que no son clave deben vincularse, directa o indirectamente, con el atributo de granularidad. Dentro de un cubo, el atributo de granularidad define la granularidad de una dimensión.  
  
## <a name="query-scope-cube-space"></a>Ámbito de la consulta (espacio de cubo)  
 El ámbito de una consulta define los límites en los que se seleccionan los datos. Va desde el cubo completo (un cubo es el objeto de consulta más grande) hasta una celda.  
  
 El**espacio de cubo** es el producto de los miembros de las jerarquías de atributo de un cubo con las medidas de un cubo.  
  
 Un**subcubo** es un subconjunto de un cubo que representa una vista filtrada del cubo. Los subcubos pueden definirse con una instrucción Scope en el script de cálculo MDX o en la cláusula de subselección de una consulta MDX, o como un cubo de sesión.  
  
 La**celda** es el espacio en la intersección de un miembro del miembro de dimensión de medidas y un miembro de cada jerarquía de atributo en un cubo.  
  
## <a name="other-modeling-terms"></a>Otros términos sobre los modelos  
 En esta sección es una colección de los conceptos y términos que difícilmente encajarían en otras secciones, pero debe saber acerca de.  
  
 Un**miembro calculado** es un miembro de dimensión que se define y calcula en tiempo de consulta. Un miembro calculado puede definirse en una consulta de usuario o en el script de cálculo MDX; se almacena en el servidor. Un miembro calculado corresponde a filas de la tabla de dimensiones de la dimensión en la que se define.  
  
 Un**recuento distintivo** es un tipo especial de medida que se utiliza para elementos de datos que solo se deben contar una vez. En el modelo de ejemplo AdventureWorks se incluyen medidas de recuento distintivo para los Pedidos por Internet, los Pedidos de distribuidores y los Pedidos de ventas.  
  
 Los**grupos de medidas** son una colección de una o más medidas. Principalmente, son definidos por el usuario y se usan para mantener juntas medidas relacionadas entre sí. Las medidas de recuentos distintivos son una excepción. Estas se colocan siempre en un grupo de medidas exclusivo que contiene únicamente la medida distintiva. No puede ver el grupo de medida en la ilustración de ejemplo de tabla dinámica, pero aparece en una lista de campos de tabla dinámica, como una colección de medidas.  
  
 Una**dimensión de medidas** es la dimensión que contiene todas las medidas de un cubo. No se expone en un modelo multidimensional que se crean en SQL Server Data Tools, pero existe exactamente igual. Como contiene medidas, todos los miembros de una dimensión de medidas suelen agregarse (por lo general mediante una operación de suma o de recuento).  
  
 **Dimensiones de bases de datos y dimensiones de cubos**. En un modelo, se puede definir dimensiones independientes que después se incluyen en cualquier número de cubos en el mismo modelo. Cuando se agrega una dimensión a un cubo, se denomina una dimensión de cubo. Por sí mismo dentro de un proyecto, como un elemento independiente en el Explorador de objetos, denomina dimensión de base de datos. ¿Por qué es necesario hacer una distinción? Porque se pueden definir las propiedades independientemente. En la documentación del producto, verá usan ambos términos, por lo que merece la pena entender su significado.  
  
## <a name="next-steps"></a>Pasos siguientes  
 Ahora que tiene ciertos conocimientos de los conceptos y la terminología más importante, puede continuar con otros temas, en los que se explican mejor conceptos fundamentales de Analysis Services:  
  
-   [Consulta de MDX básica &#40;MDX&#41;](mdx/mdx-query-the-basic-query.md)  
  
-   [Script MDX básico &#40;MDX&#41;](mdx/the-basic-mdx-script-mdx.md)  
  
-   [Creación de modelos multidimensionales &#40;tutorial de Adventure Works&#41;](../multidimensional-modeling-adventure-works-tutorial.md)  
  
## <a name="see-also"></a>Vea también  
 [Cube Space](mdx/cube-space.md)   
 [Tuplas](mdx/tuples.md)   
 [Autoexists](mdx/autoexists.md)   
 [Trabajar con miembros, tuplas y conjuntos &#40;MDX&#41;](mdx/working-with-members-tuples-and-sets-mdx.md)   
 [Totales visuales y totales no visuales](mdx/visual-totals-and-non-visual-totals.md)   
 [Aspectos básicos de las consultas MDX &#40;Analysis Services&#41;](mdx/mdx-query-fundamentals-analysis-services.md)   
 [Aspectos básicos de scripting MDX &#40;Analysis Services&#41;](mdx/mdx-scripting-fundamentals-analysis-services.md)   
 [Referencia del lenguaje MDX &#40;MDX&#41;](/sql/mdx/mdx-language-reference-mdx)   
 [Referencia de expresiones multidimensionales &#40;MDX&#41;](/sql/mdx/multidimensional-expressions-mdx-reference)  
  
  
