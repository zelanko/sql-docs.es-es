---
title: Miembros calculados en subselecciones y subcubos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 6e35e8f7-ae1c-4549-8432-accf036d2373
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d4c7b695882605eacd19d61bf6fe2cc71d8a6048
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/26/2018
ms.locfileid: "50148260"
---
# <a name="calculated-members-in-subselects-and-subcubes"></a>Miembros calculados en subselecciones y subcubos
  En las versiones anteriores, no se admitían miembros calculados en subselecciones ni subcubos. Sin embargo, a partir de SQL Server 2008 se permiten y habilitan por una propiedad de conexión. Además, se ha introducido un nuevo comportamiento de los miembros calculados en subselecciones y subcubos en SQL Server 2008 R2.  
  
## <a name="calculated-members-in-subselects-and-subcubes"></a>Miembros calculados en subselecciones y subcubos  
 El `SubQueries` propiedad de cadena de conexión de <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A> o `DBPROPMSMDSUBQUERIES` propiedad [propiedades XMLA compatibles &#40;XMLA&#41; ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties) define el comportamiento o concesión de miembros calculados o calculados establece en subselecciones o subcubos. En el contexto de este documento, subselección hace referencia a subselecciones y subcubos, a menos que se indique lo contrario.  
  
 La propiedad SubQueries permite los siguientes valores.  
  
|||  
|-|-|  
|Valor|Descripción|  
|0|Los miembros calculados no se permiten en subselecciones ni en subcubos.<br /><br /> Se produce un error al evaluar la subselección o subcubo si se hace referencia a un miembro calculado.|  
|1|Los miembros calculados se permiten en subselecciones y subcubos pero sin que se introduzca ningún miembro antecesor en el subespacio que se devuelve.|  
|2|Los miembros calculados se permiten en subselecciones y subcubos y los miembros antecesores se introducen en el subespacio que se devuelve. Asimismo, la granularidad mixta se permite en la selección de miembros calculados.|  
  
 Usar valores de 1 o 2 en la propiedad SubQueries permite usar miembros calculados para filtrar el subespacio de subselecciones que se devuelve.  
  
 Un ejemplo ayudará a clarificar el concepto; primero se debe crear un miembro calculado y luego una consulta de subselección emitida para mostrar el comportamiento anteriormente mencionado.  
  
 En el siguiente ejemplo se crea un miembro calculado que agrega [Seattle Metro] como una ciudad a la jerarquía [Geography].[Geography] dentro del estado de Washington.  
  
 Para ejecutar el ejemplo, la cadena de conexión debe contener la propiedad SubQueries con un valor de 1 y todas las instrucciones MDX se deben ejecutar en la misma sesión.  
  
 Primero emita la siguiente expresión MDX:  
  
```  
//Remember to set Subqueries=1 in the connection string prior  
//to issue these commands  
//--> AS2008 behavior  
CREATE MEMBER [Adventure Works].[Geography].[Geography].[State-Province].&[WA]&[US].[Seattle Metro Agg]   
   AS  AGGREGATE(   
                 {   
                   [Geography].[Geography].[City].&[Bellevue]&[WA]  
                 , [Geography].[Geography].[City].&[Issaquah]&[WA]  
                 , [Geography].[Geography].[City].&[Redmond]&[WA]  
                 , [Geography].[Geography].[City].&[Seattle]&[WA]  
                 }  
                )    
```  
  
 A continuación, emita la siguiente consulta MDX para ver miembros calculados permitidos en las subselecciones.  
  
```  
Select [Date].[Calendar Year].members on 0,  
       [Geography].[Geography].allmembers on 1  
from (Select {[Geography].[Geography].[State-Province].&[WA]&[US].[Seattle Metro Agg]} on 0 from [Adventure Works])  
Where [Measures].[Reseller Sales Amount]  
```  
  
 Los resultados obtenidos son:  
  
|||||||  
|-|-|-|-|-|-|  
||All Periods|CY 2001|CY 2002|CY 2003|CY 2004|  
|Seattle Metro Agg|$2,383,545.69|$291,248.93|$763,557.02|$915,832.36|$412,907.37|  
  
 Tal y como hemos dicho antes, los antecesores de [Seattle Metro] no existen en el subespacio devuelto, cuando SubQueries=1, por lo tanto [Geography].[Geography].allmembers solo contiene el miembro calculado.  
  
 Si se ejecuta el ejemplo usando SubQueries=2, en la cadena de conexión los resultados obtenidos son:  
  
|||||||  
|-|-|-|-|-|-|  
||All Periods|CY 2001|CY 2002|CY 2003|CY 2004|  
|All Geographies|(null)|(null)|(null)|(null)|(null)|  
|United States|(null)|(null)|(null)|(null)|(null)|  
|Washington|(null)|(null)|(null)|(null)|(null)|  
|Seattle Metro Agg|$2,383,545.69|$291,248.93|$763,557.02|$915,832.36|$412,907.37|  
  
 Como hemos comentado, al usar SubQueries=2, los antecesores de [Seattle Metro] existen en el subespacio devuelto pero no tienen valores porque no hay ningún miembro normal para suministrar las agregaciones. Por consiguiente, los valores NULL se proporcionan para todos los miembros antecesores del miembro calculado en este ejemplo.  
  
 Para entender el comportamiento anterior, es útil entender que los miembros calculados no contribuyen a las agregaciones de sus miembros primarios como lo hacen los miembros normales; lo primero implica que el filtrado realizado solo por miembros calculados generará antecesores vacíos porque no hay miembros normales para contribuir a los valores agregados del subespacio que resulta. Si agrega miembros regulares a la expresión de filtrado, entonces los valores agregados procederán de esos miembros regulares. Siguiendo con el ejemplo anterior, si la ciudad de Portland, en Oregón, y Spokane, en Washington, se agregan al mismo eje en el que aparece el miembro calculado; como se muestra en la expresión MDX siguiente:  
  
```  
Select [Date].[Calendar Year].members on 0,  
       [Geography].[Geography].allmembers on 1  
from (Select {  
               [Seattle Metro Agg]  
             , [Geography].[Geography].[City].&[Portland]&[OR]  
             , [Geography].[Geography].[City].&[Spokane]&[WA]  
             } on 0 from [Adventure Works]  
     )  
Where [Measures].[Reseller Sales Amount]  
```  
  
 Se obtienen los siguientes resultados.  
  
|||||||  
|-|-|-|-|-|-|  
||All Periods|CY 2001|CY 2002|CY 2003|CY 2004|  
|All Geographies|$235,171.62|$419.46|$4,996.25|$131,788.82|$97,967.09|  
|United States|$235,171.62|$419.46|$4,996.25|$131,788.82|$97,967.09|  
|Oregon|$30,968.25|$419.46|$4,996.25|$17,442.97|$8,109.56|  
|Portland|$30,968.25|$419.46|$4,996.25|$17,442.97|$8,109.56|  
|97205|$30,968.25|$419.46|$4,996.25|$17,442.97|$8,109.56|  
|Washington|$204,203.37|(null)|(null)|$114,345.85|$89,857.52|  
|Spokane|$204,203.37|(null)|(null)|$114,345.85|$89,857.52|  
|99202|$204,203.37|(null)|(null)|$114,345.85|$89,857.52|  
|Seattle Metro Agg|$2,383,545.69|$291,248.93|$763,557.02|$915,832.36|$412,907.37|  
  
 En los resultados anteriores, los valores agregados para [All Geographies], [United States], [Oregon] y [Washington] proceden de agregar los descendientes de &[Portland]&[OR] y &[Spokane]&[WA]. Nada procede del miembro calculado.  
  
### <a name="remarks"></a>Comentarios  
 Solo se permiten miembros calculados globales o de sesión en las expresiones de subselección o subcubo. Si existen miembros calculados de consulta en la expresión MDX, se producirá un error cuando se evalúe la expresión de subselección o subcubo.  
  
## <a name="see-also"></a>Vea también  
 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>   
 [Subselecciones en las consultas](subselects-in-queries.md)   
 [Propiedades XMLA compatibles &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties)  
  
  
