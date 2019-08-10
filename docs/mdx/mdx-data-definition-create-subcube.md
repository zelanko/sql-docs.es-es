---
title: CREATE subcube (instrucción, MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f137e8c377c94a60fdcfd8f1534069cef4b28f66
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2019
ms.locfileid: "68887439"
---
# <a name="mdx-data-definition---create-subcube"></a>Definición de datos de MDX: SUBCUBE


  Redefine el espacio del cubo de un cubo o subcubo especificado a un subcubo especificado. Esta instrucción cambia el espacio aparente del cubo para operaciones posteriores.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
CREATE SUBCUBE Cube_Name AS Select_Statement  
                                                  | NON VISUAL ( Select_Statement )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Cube_Name*  
 Expresión de cadena válida que proporciona el nombre del cubo o la perspectiva que se está restringiendo, que se convierte en el nombre del subcubo.  
  
 *Select_Statement*  
 Expresión MDX (Expresiones multidimensionales) válida SELECT que no contiene cláusulas WITH, NON EMPTY o HAVING y no solicita propiedades de dimensión o celda.  
  
 Vea [instrucción &#40;Select de&#41; MDX](../mdx/mdx-data-manipulation-select.md) para obtener una explicación detallada de la sintaxis de las instrucciones SELECT y la cláusula Nonvisual.  
  
## <a name="remarks"></a>Comentarios  
 Cuando se excluyen los miembros predeterminados de la definición de un subcubo, las coordenadas cambian a su vez. Para los atributos que pueden agregarse, el miembro predeterminado se mueve al miembro [Todos]. Para los atributos que no pueden agregarse, el miembro predeterminado se mueve a un miembro que existe en el subcubo. En la tabla siguiente se ofrece un ejemplo de subcubo y las combinaciones de miembros predeterminados.  
  
|Miembro predeterminado original|Puede agregarse|Subselección|Miembro predeterminado revisado|  
|-----------------------------|-----------------------|---------------|----------------------------|  
|Time.Year.All|Sí|{Time.Year.2003}|Sin cambios|  
|Time. Year. [1997]|Sí|{Time.Year.2003}|Time.Year.All|  
|Time. Year. [1997]|Sin|{Time.Year.2003}|Time. Year. [2003]|  
|Time. Year. [1997]|Sí|{Time.Year.2003, Time.Year.2004}|Time.Year.All|  
|Time. Year. [1997]|Sin|{Time.Year.2003, Time.Year.2004}|Time.Year.[2003] o<br /><br /> Time.Year.[2004]|  
  
 Los miembros [Todos] siempre existirán en un subcubo.  
  
 Los objetos de sesión creados en el contexto de un área de subcubo se quitan cuando se quita el subcubo.  
  
 Para obtener más información acerca de los subcubos, vea compilar subcubos [en &#40;MDX&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/building-subcubes-in-mdx-mdx)MDX.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente crea un subcubo que limita el espacio aparente del cubo a los miembros que existen con el país Canadá. A continuación, utiliza la función Members para devolver todos los miembros del nivel Country de la jerarquía definida por el usuario Geography, que devuelve solo el país de Canadá.  
  
```  
CREATE SUBCUBE [Adventure Works] AS  
   SELECT [Geography].[Country].&[Canada] ON 0  
   FROM [Adventure Works]  
  
SELECT [Geography].[Country].[Country].MEMBERS ON 0  
   FROM [Adventure Works]  
  
```  
  
 En el ejemplo siguiente se crea un subcubo que limita el espacio aparente del cubo a los miembros {Accessories, Clothing} de Products.Category y {[Value Added Reseller], [Warehouse]} en Resellers.[Business Type].  
  
 `CREATE SUBCUBE [Adventure Works] AS`  
  
 `Select {[Category].Accessories, [Category].Clothing} on 0,`  
  
 `{[Business Type].[Value Added Reseller], [Business Type].[Warehouse]} on 1`  
  
 `from [Adventure Works]`  
  
 La consulta de todos los miembros del subcubo en Products.Category y Resellers. [Business Type] con el MDX siguiente:  
  
 `select [Category].members on 0,`  
  
 `[Business Type].members on 1`  
  
 `from [Adventure Works]`  
  
 `where [Measures].[Reseller Sales Amount]`  
  
 Produce los resultados siguientes:  
  
|||||  
|-|-|-|-|  
||All Products|Accessories|Clothing|  
|All Resellers|$2,031,079.39|$506,172.45|$1,524,906.93|  
|Value Added Reseller|$767,388.52|$175,002.81|$592,385.71|  
|Warehouse|$1,263,690.86|$331,169.64|$932,521.23|  
  
 Si se quita y se vuelve a crear el subcubo con la cláusula NO VISUAL, se creará un subcubo con los verdaderos totales de todos los miembros de Products.Category y Resellers.[Business Type], estén o no visibles en el subcubo.  
  
 `CREATE SUBCUBE [Adventure Works] AS`  
  
 `NON VISUAL (Select {[Category].Accessories, [Category].Clothing} on 0,`  
  
 `{[Business Type].[Value Added Reseller], [Business Type].[Warehouse]} on 1`  
  
 `from [Adventure Works])`  
  
 La ejecución de la misma consulta MDX anterior:  
  
 `select [Category].members on 0,`  
  
 `[Business Type].members on 1`  
  
 `from [Adventure Works]`  
  
 `where [Measures].[Reseller Sales Amount]`  
  
 Produce los resultados diferentes siguientes:  
  
|||||  
|-|-|-|-|  
||All Products|Accessories|Clothing|  
|All Resellers|$80,450,596.98|$571,297.93|$1,777,840.84|  
|Value Added Reseller|$34,967,517.33|$175,002.81|$592,385.71|  
|Warehouse|$38,726,913.48|$331,169.64|$932,521.23|  
  
 La columna [All Products] y la fila [All Resellers] contienen los totales de todos los miembros y no solo de los que están visibles.  
  
## <a name="see-also"></a>Vea también  
 [Conceptos clave de MDX &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services)   
 [Instrucciones &#40;de scripting de MDX MDX&#41;](../mdx/mdx-scripting-statements-mdx.md)   
 [DROP subcube, &#40;instrucción MDX&#41;](../mdx/mdx-data-definition-drop-subcube.md)   
 [SELECT &#40;Instrucción, MDX&#41;](../mdx/mdx-data-manipulation-select.md)  
  
  
