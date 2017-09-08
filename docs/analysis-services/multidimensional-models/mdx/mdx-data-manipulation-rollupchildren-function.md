---
title: "Trabajar con la función RollupChildren (MDX) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- queries [MDX], RollupChildren function
- RollupChildren function
- custom member properties [MDX]
- IIf function
ms.assetid: 03c624d4-f277-451d-9995-623a07ea2f86
caps.latest.revision: 27
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: aa1200dd746dcb1ffc7ae7372b0d85a3d60d49f2
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="mdx-data-manipulation---rollupchildren-function"></a>Manipulación de datos MDX - RollupChildren, función
  La función MDX (expresiones multidimensionales) [RollupChildren](../../../mdx/rollupchildren-mdx.md) acumula los elementos secundarios de un miembro con la aplicación de un operador unario diferente a cada elemento secundario y devuelve el valor de este resumen como un número. El operador unario utilizado puede ser proporcionado mediante una propiedad de miembro asociada al miembro secundario, o bien puede ser una expresión de cadena proporcionada directamente a la función.  
  
## <a name="rollupchildren-function-examples"></a>Ejemplos de la función RollupChildren  
 El uso de la función **RollupChildren** en instrucciones MDX (expresiones multidimensionales) es fácil de explicar, pero esta función puede tener un impacto muy variado en las consultas MDX.  
  
 El efecto de la función **RollupChildren** se produce en las consultas MDX diseñadas para realizar un análisis selectivo de los datos del cubo existentes. Por ejemplo, la tabla siguiente contiene una lista de los miembros secundarios del miembro primario Net Sales, con sus operadores unarios (representados por la propiedad de miembro **UNARY_OPERATOR** ) entre paréntesis.  
  
|Miembro primario|Miembro secundario|  
|-------------------|------------------|  
|Ventas netas|Domestic Sales (+)<br /><br /> Domestic Returns (-)<br /><br /> Foreign Sales (+)<br /><br /> Foreign Returns (-)|  
  
 El miembro primario Net Sales actualmente proporciona un total de ventas netas menos los valores de ventas domésticas y extranjeras brutas, con los valores de las ventas domesticas y extranjeras restados como parte del resumen.  
  
 Sin embargo, suponga que desea proporcionar una previsión rápida y simple de las ventas brutas domésticas y extranjeras más el 10% y omitir los valores devueltos de ventas domésticas y extranjeras. Para calcular este valor puede utilizar la función **RollupChildren** de dos maneras: con una propiedad de miembro personalizado o con la función **IIf** .  
  
### <a name="using-a-custom-member-property"></a>Usar una propiedad de miembro personalizado  
 Si el cálculo de resumen se va a realizar habitualmente, un método es crear una propiedad de miembro que almacene el operador que se vaya a utilizar para cada secundario para una función determinada. En la siguiente tabla se muestran los operadores unarios válidos y se describe el resultado esperado.  
  
|Operador|Resultado|  
|--------------|------------|  
|+|total = total + elemento secundario actual|  
|-|total = total - elemento secundario actual|  
|*|total = total * elemento secundario actual|  
|/|total = total / elemento secundario actual|  
|~|El elemento secundario no se utiliza en el resumen. El valor del elemento secundario se omite.|  
  
 Por ejemplo, se podría crear una propiedad de miembro llamada **SALES_OPERATOR** a la que se le asignen los siguientes operadores unarios, como se muestra en la tabla siguiente.  
  
|Miembro primario|Miembro secundario|  
|-------------------|------------------|  
|Ventas netas|Domestic Sales (+)<br /><br /> Domestic Returns (~)<br /><br /> Foreign Sales (+)<br /><br /> Foreign Returns (~)|  
  
 Con esta nueva propiedad de miembro, la siguiente instrucción MDX llevaría a cabo la operación de estimación de ventas brutas de forma rápida y eficaz (omitiendo los valores devueltos para las ventas domésticas y extranjeras):  
  
```  
RollupChildren([Net Sales], [Net Sales].CurrentMember.Properties("SALES_OPERATOR")) * 1.1  
```  
  
 Cuando se llama a la función, el valor de cada secundario se aplica a un total utilizando el operador almacenado en la propiedad de miembro. Los miembros de los valores domésticos y extranjeros devueltos se omiten y el total del resumen devuelto por la función **RollupChildren** se multiplica por 1.1.  
  
### <a name="using-the-iif-function"></a>Usar la función IIf  
 Si la operación del ejemplo no es común o se aplica únicamente a una consulta MDX, se puede utilizar la función [IIf](../../../mdx/iif-mdx.md) con la función **RollupChildren** para proporcionar el mismo resultado. La siguiente consulta MDX proporciona el mismo resultado que el ejemplo anterior, pero sin recurrir al uso de una propiedad de miembro personalizado:  
  
```  
RollupChildren([Net Sales], IIf([Net Sales].CurrentMember.Properties("UNARY_OPERATOR") = "-", "~", [Net Sales].CurrentMember.Properties("UNARY_OPERATOR))) * 1.1  
```  
  
 La instrucción MDX examina el operador unario del miembro secundario. Si el operador unario se usa para una resta (como sucede con los miembros de los valores nacionales y extranjeros devueltos), la función **IIf** sustituye al operador unario tilde (~). De lo contrario, la función **IIf** utiliza el operador unario del miembro secundario. Finalmente, el total de resumen devuelto se multiplica por 1.1 para proporcionar el valor de predicción de las ventas brutas domésticas y extranjeras.  
  
## <a name="see-also"></a>Vea también  
 [Manipular datos &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-data-manipulation-manipulating-data.md)  
  
  
