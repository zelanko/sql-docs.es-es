---
title: Instrucción de obtención de detalles (MDX) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DRILLTHROUGH
dev_langs:
- kbMDX
helpviewer_keywords:
- DRILLTHROUGH statement
- retrieving data
- data retrieval [MDX]
ms.assetid: dfa22755-0ed4-4bba-9c31-7ade26d9ebdb
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 0fe45ea048258151182c58be6537afa1dd34f3b8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="mdx-data-manipulation---drillthrough"></a>Manipulación de datos MDX - obtención de detalles
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Recupera filas de la tabla subyacente que se han utilizado para crear una celda especificada de un cubo.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DRILLTHROUGH[MAXROWSUnsigned_Integer]   
      <MDX SELECT statement>   
      [RETURNSet_of_Attributes_and_Measures   
            [,Set_of_Attributes_and_Measures ...]  
      ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *Unsigned_Integer*  
 Valor entero positivo.  
  
 *Instrucción MDX SELECT*  
 Cualquier instrucción SELECT de MDX (Expresiones multidimensionales) válida.  
  
 *Set_of_Attributes_and_Measures*  
 Lista separada por comas de atributos de dimensión y medidas.  
  
## <a name="remarks"></a>Comentarios  
 La obtención de detalles es una operación en la que un usuario final selecciona una única celda de un cubo y recupera un conjunto de resultados de los datos de origen de esa celda para obtener información más detallada. De forma predeterminada, un conjunto de resultados de obtención de detalles proviene de las filas de la tabla evaluadas para calcular el valor de la celda del cubo seleccionada. Para que los usuarios finales puedan obtener detalles, las aplicaciones cliente deben admitir esta función. En [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], los resultados se recuperan directamente desde el almacenamiento MOLAP, a menos que se consultan las particiones ROLAP o dimensiones.  
  
> [!IMPORTANT]  
>  La seguridad de obtención de detalles se basa en las opciones de seguridad generales definidas en el cubo. Si un usuario no puede obtener algunos detalles mediante MDX, la obtención de detalles también limitará al usuario exactamente de la misma manera.  
  
 Una instrucción MDX especifica la celda sujeto. El valor especificado por el **MAXROWS** argumento indica el número máximo de filas que se deben devolver el conjunto de filas resultante.  
  
 De forma predeterminada, el número máximo de filas que se devuelven es 10.000 filas. Esto significa que si deja **MAXROWS** no se especifica, obtendrá 10.000 filas o menos. Si este valor es demasiado bajo para el escenario, puede establecer **MAXROWS** en un número más alto, como `MAXROWS 20000`. Si es demasiado bajo en general, puede aumentar el valor predeterminado cambiando el **OLAP\Query\DefaultDrillthroughMaxRows** propiedad del servidor. Para obtener más información acerca de cómo cambiar esta propiedad, vea [propiedades del servidor de Analysis Services](../analysis-services/server-properties/server-properties-in-analysis-services.md).  
  
 A menos que se especifique lo contrario, las columnas devueltas incluyen todos los atributos de granularidad de todas las dimensiones relacionadas con el grupo de medida de la medida especificada, excepto las dimensiones de varios a varios. Las dimensiones de cubo van precedidas por $ para diferenciar entre dimensiones y grupos de medida. El **devolver** cláusula se utiliza para especificar las columnas devueltas por la consulta de obtención de detalles. Las siguientes funciones se pueden aplicar a un único atributo o medida mediante la **devolver** cláusula.  
  
 Name(attribute_name)  
 Devuelve el nombre del miembro de atributo especificado.  
  
 UniqueName(attribute_name)  
 Devuelve el nombre único del miembro de atributo especificado.  
  
 Key(attribute_name[, N])  
 Devuelve la clave del miembro de atributo especificado, donde N especifica la columna de la clave compuesta (si la hubiera). El valor predeterminado de N es 1.  
  
 Caption(attribute_name)  
 Devuelve el título del miembro de atributo especificado.  
  
 MemberValue(attribute_name)  
 Devuelve el valor de miembro del miembro de atributo especificado.  
  
 CustomRollup(attribute_name)  
 Devuelve la expresión de resumen personalizada del miembro de atributo especificado.  
  
 CustomRollupProperties(attribute_name)  
 Devuelve las propiedades de resumen personalizadas del miembro de atributo especificado.  
  
 UnaryOperator(attribute_name)  
 Devuelve el operador unario del miembro de atributo especificado.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente especifica la celda del mes de julio de 2007 para la medida Reseller Sales Amount (la medida predeterminada) para el país Australia. La cláusula RETURN especifica que se devuelven los datos de cada venta, el nombre del modelo de producto, el nombre del empleado, el importe de venta, el importe de impuestos y los valores de costo del producto subyacentes de esta celda.  
  
```  
DRILLTHROUGH  
SELECT  
   ([Date].[Calendar].[Month].[July 2007])  
ON 0   
FROM [Adventure Works]  
WHERE [Geography].[Country].[Australia]  
RETURN   
  [$Date].[Date]  
  ,KEY([$Product].[Model Name])  
  ,NAME([$Employee].[Employee])  
  ,[Reseller Sales].[Reseller Sales Amount]  
  ,[Reseller Sales].[Reseller Tax Amount]  
  ,[Reseller Sales].[Reseller Standard Product Cost]  
```  
  
## <a name="see-also"></a>Vea también  
 [Instrucciones de manipulación de datos MDX &#40;MDX&#41;](../mdx/mdx-data-manipulation-statements-mdx.md)  
  
  
