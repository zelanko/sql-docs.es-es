---
title: Propiedades de miembro intrínsecas (MDX) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e54aa6bb53e6ce9f34e6647927f29b7aadb97180
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62740255"
---
# <a name="mdx-member-properties---intrinsic-member-properties"></a>Propiedades de miembro MDX: propiedades de miembro intrínsecas
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] expone propiedades intrínsecas de los miembros de dimensión que se pueden incluir en una consulta para devolver datos o metadatos adicionales para usarlos en una aplicación personalizada o como ayuda durante la investigación o la construcción de un modelo. Si utiliza las herramientas de cliente de SQL Server, puede ver las propiedades intrínsecas en SQL Server Management Studio (SSMS).  
  
 Las propiedades intrínsecas son **ID**, **KEY**, **KEYx**y **NAME**, que son las propiedades que exponen todos los miembros de cualquier nivel. También puede devolver información de posición, como **LEVEL_NUMBER** o **PARENT_UNIQUE_NAME**, entre otros.  
  
 Dependiendo de cómo se crea la consulta, y de la aplicación cliente que se utiliza para ejecutar las consultas, las propiedades de miembro pueden o no estar visibles en el conjunto de resultados. Si utiliza SQL Server Management Studio para probar o ejecutar consultas, puede hacer doble clic en un miembro del conjunto de resultados para abrir el cuadro de diálogo Propiedades del miembro, que muestra los valores de cada propiedad de miembro intrínseca.  
  
 Para obtener una introducción sobre el modo de utilizar y ver las propiedades de miembro de dimensión, vea [Visualización de las propiedades de miembro de SSAS en una ventana de consulta MDX en SSMS](http://go.microsoft.com/fwlink/?LinkId=317362).  
  
> [!NOTE]
>  Como proveedor que cumple con la sección OLAP de la especificación OLE DB con fecha de marzo de 1999 (2.6), [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] admite las propiedades de miembro intrínsecas que se describen en este tema.  
> 
>  Es posible que otros proveedores además de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] admitan propiedades de miembro intrínsecas adicionales. Para obtener más información acerca de las propiedades de miembro intrínsecas compatibles con otros proveedores, vea la documentación que suministra cada uno de ellos.  
  
## <a name="types-of-member-properties"></a>Tipos de propiedades de miembro  
 Las propiedades de miembro intrínsecas compatibles con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] son de dos tipos:  
  
 Propiedades de miembro contextuales  
 Estas propiedades de miembro deben utilizarse en el contexto de una jerarquía o un nivel específicos y proporcionan valores para cada miembro de la dimensión o el nivel especificado.  
  
 Observe cómo se incluye en el ejemplo siguiente la ruta de acceso de la propiedad **KEY** : `MEMBER [Measures].[Parent Member Key] AS [Product].[Product Categories].CurrentMember.Parent.PROPERTIES("KEY")`.  
  
 Propiedades de miembro no contextuales  
 Estas propiedades de miembro no pueden utilizarse en el contexto de una dimensión o un nivel específicos y devuelven los valores para todos los miembros de un eje.  
  
 Las propiedades no contextuales son independientes y no incluyen información de ruta de acceso. Observe que no se especifica ni la dimensión ni el nivel para **PARENT_UNIQUE_NAME** en el ejemplo siguiente: `DIMENSION PROPERTIES PARENT_UNIQUE_NAME ON COLUMNS`  
  
 Independientemente de si la propiedad de miembro intrínseca es contextual o no, se rige por las siguientes reglas:  
  
-   Únicamente se pueden especificar las propiedades de miembro intrínsecas relacionadas con los miembros de dimensión que se proyectan en el eje.  
  
-   Se pueden mezclar solicitudes de propiedades de miembro contextuales con propiedades de miembro intrínsecas no contextuales en la misma consulta.  
  
-   Se puede utilizar la palabra clave **PROPERTIES** para realizar consultas sobre las propiedades.  
  
 En las secciones siguientes se describen las distintas propiedades de miembro intrínsecas contextuales y no contextuales disponibles en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]y cómo usar la palabra clave **PROPERTIES** con cada tipo de propiedad.  
  
## <a name="context-sensitive-member-properties"></a>Propiedades de miembro contextuales  
 Todos los miembros de dimensión y de nivel admiten una lista de propiedades de miembro intrínsecas contextuales. En la siguiente tabla se incluyen estas propiedades contextuales.  
  
|Property|Descripción|  
|--------------|-----------------|  
|**ID**|Id. interno del miembro.|  
|**Key**|Valor de la clave de miembro en el tipo de datos original. MEMBER_KEY se incluye por cuestiones de compatibilidad con versiones anteriores.  La propiedad MEMBER_KEY tiene el mismo valor que KEY0 para las claves no compuestas y es NULL para las claves compuestas.|  
|**KEYx**|Clave del miembro, donde x es el valor ordinal (con base cero) de la clave. KEY0 está disponible para las claves compuestas y no compuestas, pero se usa principalmente para las claves compuestas.<br /><br /> Para las claves compuestas, el conjunto KEY0, KEY1, KEY2, etc. forma la clave compuesta. Puede utilizar cualquiera de ellas por separado en una consulta para devolver esa parte de la clave compuesta. Por ejemplo, si se especifica KEY0, se devuelve la primera parte de la clave compuesta, si se especifica KEY1, se devuelve la parte siguiente de la clave compuesta, y así sucesivamente.<br /><br /> Si la clave no es compuesta, KEY0 equivale a **Key**.<br /><br /> Tenga en cuenta que **KEYx** se puede utilizar tanto con contexto como sin contexto. Por esta razón, aparece en las dos listas.<br /><br /> Para obtener un ejemplo de cómo usar esta propiedad de miembro, vea [una sencilla curiosidad de MDX: Key0, Key1, Key2](http://go.microsoft.com/fwlink/?LinkId=317364).|  
|**Name**|Nombre del miembro.|  
  
### <a name="properties-syntax-for-context-sensitive-properties"></a>Sintaxis de PROPERTIES para las propiedades contextuales  
 Estas propiedades de miembro se utilizan en el contexto de una dimensión o un nivel específicos y proporcionan valores de cada miembro de la dimensión o el nivel especificados.  
  
 En el caso de las propiedades de miembro de dimensión, el nombre de la propiedad debe ir precedido del nombre de la dimensión a la que se aplica la propiedad. En el siguiente ejemplo se muestra la sintaxis adecuada:  
  
 `DIMENSION PROPERTIES Dimension.Property_name`  
  
 En el caso de las propiedades de miembro de nivel, el nombre de la propiedad puede ir precedido solamente del nombre de nivel o, si se requieren especificaciones adicionales, del nombre de la dimensión y del nivel. En el siguiente ejemplo se muestra la sintaxis adecuada:  
  
 `DIMENSION PROPERTIES [Dimension.]Level.Property_name`  
  
 Para ilustrar lo explicado, suponga que desea devolver todos los nombres de cada uno de los miembros a los que se hace referencia en la dimensión `[Sales]` . Para devolver estos nombres, es preciso utilizar la siguiente instrucción en una consulta de expresiones multidimensionales (MDX):  
  
 `DIMENSION PROPERTIES [Sales].Name`  
  
## <a name="non-context-sensitive-member-properties"></a>Propiedades de miembro no contextuales  
 Todos los miembros admiten una lista de propiedades de miembro intrínsecas idénticas independientemente del contexto. Estas propiedades proporcionan información adicional que pueden usar las aplicaciones para mejorar la experiencia del usuario.  
  
 En la tabla siguiente se incluyen las propiedades intrínsecas no contextuales compatibles con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
> [!NOTE]  
>  Las columnas del conjunto de filas del esquema MEMBERS admiten las propiedades de miembro intrínsecas incluidas en la siguiente tabla. Para más información sobre el conjunto de filas de esquema **MEMBERS** , vea [Conjunto de filas MDSCHEMA_MEMBERS](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db-olap/mdschema-members-rowset).  
  
|Property|Descripción|  
|--------------|-----------------|  
|**CATALOG_NAME**|Nombre del cubo al que pertenece este miembro.|  
|**CHILDREN_CARDINALITY**|Número de elementos secundarios que tiene este miembro. Puede ser una estimación; por tanto, no debe pensar que este valor es el recuento exacto. Los proveedores deben devolver la mejor estimación posible.|  
|**CUSTOM_ROLLUP**|Expresión de miembro personalizado.|  
|**CUSTOM_ROLLUP_PROPERTIES**|Propiedades de miembro personalizado.|  
|**DESCRIPTION**|Descripción legible del miembro.|  
|**DIMENSION_UNIQUE_NAME**|Nombre único de la dimensión a la que pertenece este miembro. Los proveedores que generan nombres únicos por calificación tienen delimitados todos los componentes del nombre.|  
|**HIERARCHY_UNIQUE_NAME**|Nombre único de la jerarquía. Si el miembro pertenece a más de una jerarquía, se incluye una fila por cada jerarquía a la que pertenece el miembro. Los proveedores que generan nombres únicos por calificación tienen delimitados todos los componentes del nombre.|  
|**IS_DATAMEMBER**|Valor booleano que indica si el miembro es un miembro de datos.|  
|**IS_PLACEHOLDERMEMBER**|Valor booleano que indica si el miembro es un marcador de posición.|  
|**KEYx**|Clave del miembro, donde x es el valor ordinal (con base cero) de la clave. KEY0 está disponible para claves compuestas y no compuestas.<br /><br /> Si la clave no es compuesta, KEY0 equivale a **Key**.<br /><br /> Para las claves compuestas, el conjunto KEY0, KEY1, KEY2, etc. forma la clave compuesta. Puede hacer referencia a cualquiera de ellas por separado en una consulta para devolver esa parte de la clave compuesta. Por ejemplo, si se especifica KEY0, se devuelve la primera parte de la clave compuesta, si se especifica KEY1, se devuelve la parte siguiente de la clave compuesta, y así sucesivamente.<br /><br /> Tenga en cuenta que **KEYx** se puede utilizar tanto con contexto como sin contexto. Por esta razón, aparece en las dos listas.<br /><br /> Para obtener un ejemplo de cómo usar esta propiedad de miembro, vea [una sencilla curiosidad de MDX: Key0, Key1, Key2](http://go.microsoft.com/fwlink/?LinkId=317364).|  
|**LCID** *x*|Traducción del título de miembro al valor hexadecimal del id. de configuración regional, donde *x* es el valor decimal del id. de configuración regional (por ejemplo, LCID1009 como inglés de Canadá). Disponible únicamente si la traducción tiene una columna de descripción enlazada al origen de datos.|  
|**LEVEL_NUMBER**|Distancia al miembro desde la raíz de la jerarquía. El nivel raíz es cero.|  
|**LEVEL_UNIQUE_NAME**|Nombre único del nivel al que pertenece el miembro. Los proveedores que generan nombres únicos por calificación tienen delimitados todos los componentes del nombre.|  
|**MEMBER_CAPTION**|Etiqueta o descripción asociada al miembro. El título se utiliza principalmente para la visualización. Si no existe ningún título, la consulta devuelve **MEMBER_NAME**.|  
|**MEMBER_KEY**|Valor de la clave de miembro en el tipo de datos original. MEMBER_KEY se incluye por cuestiones de compatibilidad con versiones anteriores.  La propiedad MEMBER_KEY tiene el mismo valor que KEY0 para las claves no compuestas y es NULL para las claves compuestas.|  
|**MEMBER_NAME**|Nombre del miembro.|  
|**MEMBER_TYPE**|Tipo del miembro. Esta propiedad admite cualquiera de los siguientes valores:<br /><br /> **MDMEMBER_TYPE_REGULAR**<br /><br /> **MDMEMBER_TYPE_ALL**<br /><br /> **MDMEMBER_TYPE_FORMULA**<br /><br /> **MDMEMBER_TYPE_MEASURE**<br /><br /> **MDMEMBER_TYPE_UNKNOWN**<br /><br /> <br /><br /> Nota: MDMEMBER_TYPE_FORMULA tiene precedencia sobre MDMEMBER_TYPE_MEASURE. Por lo tanto, si hay un miembro (calculado) de fórmula en la dimensión de medidas, la propiedad **MEMBER_TYPE** del miembro calculado será MDMEMBER_TYPE_FORMULA.|  
|**MEMBER_UNIQUE_NAME**|Nombre único del miembro. Los proveedores que generan nombres únicos por calificación tienen delimitados todos los componentes del nombre.|  
|**MEMBER_VALUE**|Valor del miembro en el tipo de datos original.|  
|**PARENT_COUNT**|Número de primarios que tiene este miembro.|  
|**PARENT_LEVEL**|Distancia al primario del miembro desde el nivel raíz de la jerarquía. El nivel raíz es cero.|  
|**PARENT_UNIQUE_NAME**|Nombre único del elemento primario del miembro. Se devuelve**NULL** para todos los miembros del nivel raíz. Los proveedores que generan nombres únicos por calificación tienen delimitados todos los componentes del nombre.|  
|**SKIPPED_LEVELS**|El número de niveles omitidos para el miembro.|  
|**UNARY_OPERATOR**|Operador unario del miembro.|  
|**UNIQUE_NAME**|El nombre completo del miembro, con este formato: [dimensión].[nivel].[key6.]|  
  
### <a name="properties-syntax-for-non-context-sensitive-properties"></a>Sintaxis de PROPERTIES para las propiedades no contextuales  
 Use la sintaxis siguiente para especificar una propiedad de miembro intrínseca no contextual con la palabra clave **PROPERTIES** :  
  
 `DIMENSION PROPERTIES Property`  
  
 Tenga en cuenta que esta sintaxis no permite calificar la propiedad con una dimensión o un nivel. La propiedad no puede calificarse porque las propiedades de miembro intrínsecas no contextuales se aplican a todos los miembros de un eje.  
  
 Por ejemplo, una instrucción MDX que especifique la propiedad de miembro intrínseca **DESCRIPTION** debería tener la siguiente sintaxis:  
  
 `DIMENSION PROPERTIES DESCRIPTION`  
  
 Esta instrucción devuelve la descripción de cada miembro de la dimensión del eje. Si intenta calificar la propiedad con una dimensión o un nivel, como en *Dimension*`.DESCRIPTION` o en *Level*`.DESCRIPTION`, no se validará la instrucción.  
  
### <a name="example"></a>Ejemplo  
 En los ejemplos siguientes se muestran consultas MDX que devuelven propiedades intrínsecas.  
  
 **Ejemplo 1: Usar propiedades intrínsecas contextuales en consulta**  
  
 El ejemplo siguiente devuelve el identificador principal, la clave y el nombre de cada categoría de producto. Observe cómo las propiedades se exponen como medidas. Esto permite ver las propiedades en un conjunto de celdas al ejecutar la consulta, en lugar de usar el cuadro de diálogo Propiedades del miembro de SSMS. Puede ejecutar una consulta como esta para recuperar los metadatos de miembro de un cubo implementado previamente.  
  
```  
WITH  
MEMBER [Measures].[Parent Member ID] AS  
 [Product].[Product Categories].CurrentMember.Parent.PROPERTIES("ID")  
MEMBER [Measures].[Parent Member Key] AS  
 [Product].[Product Categories].CurrentMember.Parent.PROPERTIES("KEY")  
MEMBER [Measures].[Parent Member Name] AS  
 [Product].[Product Categories].CurrentMember.Parent.PROPERTIES("Name")  
SELECT  
 {[Measures].[Parent Member ID], [Measures].[Parent Member Key], [Measures].[Parent Member Name] } on COLUMNS,   
 [Product].[Product Categories].AllMembers on ROWS  
FROM [Adventure Works]  
```  
  
 **Ejemplo 2: Propiedades intrínsecas no contextuales**  
  
 El ejemplo siguiente contiene la lista completa de propiedades intrínsecas no contextuales. Después de ejecutar la consulta en SSMS, haga clic en los distintos miembros para ver las propiedades en el cuadro de diálogo Propiedades del miembro.  
  
```  
SELECT [Measures].[Sales Amount Quota] on COLUMNS,  
[Employee].[Employees].members  
DIMENSION PROPERTIES  
 CATALOG_NAME ,   
 CHILDREN_CARDINALITY ,  
 CUSTOM_ROLLUP ,   
 CUSTOM_ROLLUP_PROPERTIES ,   
 DESCRIPTION ,   
 DIMENSION_UNIQUE_NAME ,   
 HIERARCHY_UNIQUE_NAME ,  
 IS_DATAMEMBER ,   
 IS_PLACEHOLDERMEMBER ,   
 KEY0 ,  
 LCID ,  
 LEVEL_NUMBER ,  
 LEVEL_UNIQUE_NAME ,  
 MEMBER_CAPTION ,   
 MEMBER_KEY ,   
 MEMBER_NAME ,   
 MEMBER_TYPE ,  
 MEMBER_UNIQUE_NAME ,   
 MEMBER_VALUE ,   
 PARENT_COUNT ,   
 PARENT_LEVEL ,   
 PARENT_UNIQUE_NAME ,  
 SKIPPED_LEVELS ,   
 UNARY_OPERATOR ,   
 UNIQUE_NAME    
 ON ROWS  
FROM [Adventure Works]  
WHERE [Employee].[Employee Department].[Department].&[Sales]  
```  
  
 **Ejemplo 3: Devolver las propiedades de miembro como datos en un conjunto de resultados**  
  
 El siguiente ejemplo devuelve la descripción traducida del miembro de la categoría de producto en la dimensión Product del cubo de Adventure Works para las configuraciones regionales especificadas.  
  
```  
WITH   
MEMBER Measures.CategoryCaption AS Product.Category.CurrentMember.MEMBER_CAPTION  
MEMBER Measures.SpanishCategoryCaption AS Product.Category.CurrentMember.Properties("LCID3082")  
MEMBER Measures.FrenchCategoryCaption AS Product.Category.CurrentMember.Properties("LCID1036")  
SELECT   
{ Measures.CategoryCaption, Measures.SpanishCategoryCaption, Measures.FrenchCategoryCaption } ON 0  
,[Product].[Category].MEMBERS ON 1  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>Vea también  
 [PeriodsToDate &#40;MDX&#41;](../../../mdx/periodstodate-mdx.md)   
 [Children &#40;MDX&#41;](../../../mdx/children-mdx.md)   
 [Hierarchize &#40;MDX&#41;](../../../mdx/hierarchize-mdx.md)   
 [Count &#40;Set&#41; &#40;MDX&#41;](../../../mdx/count-set-mdx.md)   
 [Filter &#40;MDX&#41;](../../../mdx/filter-mdx.md)   
 [AddCalculatedMembers &#40;MDX&#41;](../../../mdx/addcalculatedmembers-mdx.md)   
 [DrilldownLevel &#40;MDX&#41;](../../../mdx/drilldownlevel-mdx.md)   
 [Properties &#40;MDX&#41;](../../../mdx/properties-mdx.md)   
 [PrevMember &#40;MDX&#41;](../../../mdx/prevmember-mdx.md)   
 [Usar las propiedades de miembro &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-member-properties.md)   
 [Referencia de funciones MDX &#40;MDX&#41;](../../../mdx/mdx-function-reference-mdx.md)  
  
  
