---
description: 'Manipulación de datos de MDX: DRILLTHROUGH'
title: Instrucción DRILLTHROUGH (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ee68e6cbb22bc817d478490315ab88ccb87e4ad4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88387049"
---
# <a name="mdx-data-manipulation---drillthrough"></a>Manipulación de datos de MDX: DRILLTHROUGH


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
  
## <a name="remarks"></a>Observaciones  
 La obtención de detalles es una operación en la que un usuario final selecciona una única celda de un cubo y recupera un conjunto de resultados de los datos de origen de esa celda para obtener información más detallada. De forma predeterminada, un conjunto de resultados de obtención de detalles proviene de las filas de la tabla evaluadas para calcular el valor de la celda del cubo seleccionada. Para que los usuarios finales puedan obtener detalles, las aplicaciones cliente deben admitir esta función. En [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , los resultados se recuperan directamente desde el almacenamiento MOLAP, a menos que se consulten las particiones o dimensiones ROLAP.  
  
> [!IMPORTANT]  
>  La seguridad de obtención de detalles se basa en las opciones de seguridad generales definidas en el cubo. Si un usuario no puede obtener algunos detalles mediante MDX, la obtención de detalles también limitará al usuario exactamente de la misma manera.  
  
 Una instrucción MDX especifica la celda sujeto. El valor especificado por el argumento **MAXROWS** indica el número máximo de filas que debe devolver el conjunto de filas resultante.  
  
 De forma predeterminada, el número máximo de filas que se devuelven es 10.000 filas. Esto significa que si deja el **MAXROWS** sin especificar, obtendrá 10.000 filas o menos. Si este valor es demasiado bajo para su escenario, puede establecer **MAXROWS** en un número más alto, como `MAXROWS 20000` . Si es demasiado bajo en general, puede aumentar el valor predeterminado cambiando la propiedad del servidor **OLAP\Query\DefaultDrillthroughMaxRows** . Para obtener más información sobre cómo cambiar esta propiedad, vea [propiedades del servidor en Analysis Services](https://docs.microsoft.com/analysis-services/server-properties/server-properties-in-analysis-services).  
  
 A menos que se especifique lo contrario, las columnas devueltas incluyen todos los atributos de granularidad de todas las dimensiones relacionadas con el grupo de medida de la medida especificada, excepto las dimensiones de varios a varios. Las dimensiones de cubo van precedidas por $ para diferenciar entre dimensiones y grupos de medida. La cláusula **Return** se utiliza para especificar las columnas devueltas por la consulta de obtención de detalles. La cláusula **Return** puede aplicar las siguientes funciones a un solo atributo u medida.  
  
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
  
## <a name="see-also"></a>Consulte también  
 [Instrucciones de manipulación de datos de MDX &#40;MDX&#41;](../mdx/mdx-data-manipulation-statements-mdx.md)  
  
  
