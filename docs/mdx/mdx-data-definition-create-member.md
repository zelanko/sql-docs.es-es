---
title: Instrucción CREATE MEMBER (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 432438fe9a6e1b39c849188050b67f816d895187
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63250209"
---
# <a name="mdx-data-definition---create-member"></a>Definición de datos de MDX: CREATE MEMBER


  Crea un miembro calculado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
CREATE [ SESSION ] [HIDDDEN] [ CALCULATED ] MEMBER CURRENTCUBE | Cube_Name.Member_Name   
   AS MDX_Expression  
      [,Property_Name = Property_Value, ...n]  
......[,SCOPE_ISOLATION = CUBE]  
```  
  
## <a name="arguments"></a>Argumentos  
 *Cube_Name*  
 Expresión de cadena válida que proporciona el nombre del cubo donde se creará el miembro.  
  
 *Member_Name*  
 Expresión de cadena válida que proporciona un nombre de miembro. Especifique un nombre completo para crear un miembro dentro de una dimensión que no sea la dimensión Measures. Si no proporciona un nombre de miembro completo, el miembro se creará en la dimensión Measures.  
  
 *MDX_Expression*  
 Expresión MDX (Expresiones multidimensionales) válida.  
  
 *Property_Name*  
 Cadena válida que proporciona el nombre de una propiedad de miembro calculado.  
  
 *Property_Value*  
 Expresión escalar válida que define el valor de la propiedad de miembro calculado.  
  
## <a name="remarks"></a>Comentarios  
 La instrucción CREATE MEMBER define los miembros calculados disponibles durante la sesión y que, por lo tanto, se pueden utilizar en varias consultas mientras la sesión esté activa. Para obtener más información, consulte [crear los miembros calculados &#40;MDX&#41;](../analysis-services/multidimensional-models/mdx/mdx-calculated-members-session-scoped-calculated-members.md).  
  
 También puede definir un miembro calculado para su uso en una sola consulta. Para definir un miembro calculado limitado a una sola consulta, use la cláusula WITH de la instrucción SELECT. Para obtener más información, consulte [crear los miembros calculados &#40;MDX&#41;](../analysis-services/multidimensional-models/mdx/mdx-calculated-members-query-scoped-calculated-members.md).  
  
 *Property_name* puede hacer referencia a las propiedades de cualquier miembro calculado estándar u opcionales. Las propiedades de miembro estándares se indican más adelante, en este mismo tema. Los miembros calculados creados mediante CREATE MEMBER y sin un **sesión** valor tienen ámbito de sesión. Además, las cadenas incluidas en las definiciones del miembro calculado se delimitan mediante comillas dobles. Este método es distinto del definido por OLE DB, en el que las cadenas deben delimitarse con comillas simples.  
  
 Si especifica un cubo distinto del que está conectado actualmente, se genera un error. Por lo tanto, debe utilizar CURRENTCUBE en lugar de un nombre de cubo para indicar el cubo actual.  
  
 Para obtener más información acerca de las propiedades de miembro definidas por OLE DB, vea la documentación de OLE DB.  
  
## <a name="scope"></a>Ámbito  
 Los miembros calculados pueden existir en cualquiera de los ámbitos que se incluyen en la siguiente tabla:  
  
 Ámbito de consulta  
 La visibilidad y la duración del miembro calculado se limita a la consulta. El miembro calculado se define en una consulta individual. El ámbito de consulta prevalece sobre el ámbito de sesión. Para obtener más información, consulte [crear los miembros calculados &#40;MDX&#41;](../analysis-services/multidimensional-models/mdx/mdx-calculated-members-query-scoped-calculated-members.md).  
  
 Ámbito de sesión  
 La visibilidad y duración del miembro calculado se limita a la sesión en la que se crea. (La duración es menor que la duración de la sesión si se emite una instrucción DROP MEMBER en el miembro calculado). La instrucción CREATE MEMBER crea a un miembro calculado con ámbito de sesión.  
  
### <a name="scope-isolation"></a>Aislamiento de ámbito  
 Cuando un script MDX (Expresiones multidimensionales) de cubo contiene miembros calculados, éstos se resuelven de forma predeterminada antes de que se resuelva cualquier cálculo de ámbito de sesión y cualquier cálculo definido por la consulta.  
  
> [!NOTE]  
>  En determinados escenarios, la [Aggregate (MDX)](../mdx/aggregate-mdx.md) función y el [VisualTotals (MDX)](../mdx/visualtotals-mdx.md) función no exhiben este comportamiento.  
  
 El comportamiento permite a las aplicaciones cliente genéricas trabajar con cubos que contienen cálculos complejos, sin tener en cuenta la implementación específica de los cálculos. Sin embargo, en determinados escenarios, es posible que desee ejecutar la sesión o miembros calculados de ámbito de consulta antes de determinados cálculos en el cubo y que no la **agregado** función ni la **VisualTotals** función son aplicables. Para lograr esto, utilice la propiedad de cálculo de SCOPE_ISOLATION.  
  
#### <a name="example"></a>Ejemplo  
 A continuación, se muestra un ejemplo de script de un escenario donde es necesaria la propiedad de cálculo SCOPE_ISOLATION para generar el resultado correcto.  
  
 **Script MDX del cubo:**  
  
```  
CREATE MEMBER CURRENTCUBE.Measures.ProfitRatio AS 'Measures.[Store Sales]/Measures.[Store Cost]', SOLVE_ORDER = 10  
```  
  
 **Consulta MDX:**  
  
```  
WITH MEMBER [Customer].[Customers].[USA]. USAWithoutWA AS  
[Customer].[Customers].[Country].&[USA] - [Customer].[Customers].[State Province.&[WA], SOLVE_ORDER=5  
SELECT {USAWithoutWA} ON 0 FROM SALES  
WHERE ProfitRatio  
```  
  
 El resultado deseado de la consulta anterior es el ratio de ventas en USA sin WA, para almacenar el costo de USA sin WA. La consulta anterior no devuelve el resultado deseado, sino la ratio de EE.UU. menos la ratio de WA, que es un resultado que carece de significado. Para obtener el resultado deseado, puede utilizar la propiedad de cálculo SCOPE_ISOLATION.  
  
 **Consulta de MDX mediante la propiedad de cálculo SCOPE_ISOLATION:**  
  
```  
WITH MEMBER [Customer].[Customers].[USA]. USAWithoutWA AS  
[Customer].[Customers].[Country].&[USA] - [Customer].[Customers].[State Province.&[WA], SOLVE_ORDER=5  
,SCOPE_ISOLATION=CUBE  
SELECT {USAWithoutWA} ON 0 FROM SALES  
WHERE ProfitRatio  
```  
  
## <a name="standard-properties"></a>Propiedades estándar  
 Cada miembro calculado tiene un conjunto de propiedades predeterminadas. Cuando una aplicación cliente está conectada a [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], las propiedades predeterminadas son compatibles o disponibles para ser compatibles, como el administrador elige.  
  
 Puede haber otras propiedades de miembro adicionales disponibles, según la definición del cubo. Las siguientes propiedades representan información relevante para el nivel de dimensión del cubo.  
  
|Identificador de la propiedad|Significado|  
|-------------------------|-------------|  
|SOLVE_ORDER|Orden de resolución del miembro calculado en aquellos casos en los que un miembro calculado haga referencia a otro miembro calculado (es decir, cuando exista una intersección de miembros calculados).|  
|FORMAT_STRING|Una cadena de formato de estilo de Office que la aplicación cliente puede utilizar al mostrar los valores de celda.|  
|VISIBLE|Valor que indica si el miembro calculado es visible en el conjunto de filas del esquema. Calculados visibles se pueden agregar miembros a un conjunto con el [AddCalculatedMembers](../mdx/addcalculatedmembers-mdx.md) función. Un valor distinto de cero indica que el miembro calculado es visible. El valor predeterminado para esta propiedad es *Visible*.<br /><br /> Los miembros calculados no visibles (cuando el valor se establece en cero) suelen utilizarse como pasos intermedios en miembros calculados más complejos. También otros tipos de miembro, como las medidas, pueden hacer referencia a estos miembros calculados.|  
|NON_EMPTY_BEHAVIOR|Medida o conjunto utilizados para determinar el comportamiento de los miembros calculados al resolver celdas vacías.<br /><br /> **\*\* Advertencia \* \***  esta propiedad está desusada. No la active. Vea [Características en desuso de Analysis Services en SQL Server 2016](../analysis-services/deprecated-analysis-services-features-in-sql-server-2016.md) para obtener detalles.|  
|CAPTION|Cadena que utiliza la aplicación cliente como título para el miembro.|  
|DISPLAY_FOLDER|Cadena que identifica la ruta de la carpeta que usa la aplicación cliente para mostrar el miembro. La aplicación cliente define el separador de niveles de carpetas. Para las herramientas y clientes proporcionados por [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], la barra diagonal inversa (\\) es el separador de niveles. Si va a asignar varias carpetas para mostrar a un miembro definido, utilice un punto y coma (;) para separar las carpetas.|  
|ASSOCIATED_MEASURE_GROUP|Nombre del grupo de medida al que se asocia el miembro.|  
  
## <a name="see-also"></a>Vea también  
 [DROP MEMBER, instrucción &#40;MDX&#41;](../mdx/mdx-data-definition-drop-member.md)   
 [UPDATE MEMBER, instrucción &#40;MDX&#41;](../mdx/mdx-data-definition-update-member.md)   
 [Instrucciones de definición de datos MDX &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
