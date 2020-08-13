---
title: Propiedades de campo extendidas para una base de datos de Analysis Services | Microsoft Docs
description: Obtenga información sobre las propiedades de campo extendidas de una base de datos de Analysis Services y cómo incluir valores de propiedades de campo extendidas en el informe.
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
ms.assetid: 1d7d87e2-bf0d-4ebb-a287-80b5a967a3f2
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: beae593bc4673a1fd31d27c5f807553a2b960872
ms.sourcegitcommit: 9470c4d1fc8d2d9d08525c4f811282999d765e6e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/17/2020
ms.locfileid: "86458360"
---
# <a name="extended-field-properties-for-an-analysis-services-database-ssrs"></a>Propiedades de campo extendidas para una base de datos de Analysis Services (SSRS)
  La extensión de procesamiento de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] admite propiedades de campo extendidas. Las propiedades de campo extendidas son propiedades disponibles además de las propiedades de campo **Value** e **IsMissing** en el origen de datos y admitidas por la extensión de procesamiento de datos. Las propiedades extendidas no aparecen en el panel Datos de informe como parte de la colección de campos para un conjunto de datos de informe. Para incluir valores de propiedades de campo extendidas en el informe, escriba expresiones que las especifiquen por su nombre con la colección **Fields** integrada.  
  
 Las propiedades extendidas incluyen propiedades predefinidas y propiedades personalizadas. Las propiedades predefinidas son propiedades comunes para varios orígenes de datos que se asignan a nombres de propiedades de campo específicos y a las que se tiene acceso por su nombre con la colección **Fields** integrada. Las propiedades personalizadas son específicas de cada proveedor de datos y se puede acceder a ellas con la colección **Fields** integrada, pero solo con la sintaxis que usa el nombre de la propiedad extendida como una cadena.  
  
 Al usar el diseñador de consultas MDX para [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en modo gráfico para definir la consulta, se agrega automáticamente un conjunto predefinido de propiedades de celda y propiedades de dimensión a la consulta MDX. Solo puede usar las propiedades extendidas que se indican de forma específica en la consulta MDX del informe. En función del informe, puede que desee modificar el texto del comando MDX predeterminado para incluir otras propiedades de dimensión o personalizadas definidas en el cubo. Para más información sobre los campos extendidos disponibles en los orígenes de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], vea [Crear y usar los valores de propiedad &#40;MDX&#41;](https://msdn.microsoft.com/library/0cafb269-03c8-4183-b6e9-220f071e4ef2).  
  
## <a name="working-with-field-properties-in-a-report"></a>Trabajar con propiedades de campo en un informe  
 Las propiedades de campo extendidas incluyen propiedades predefinidas y propiedades específicas del proveedor de datos. Las propiedades de campo no aparecen con la lista de campos del panel **Datos de informe** , aunque estén en la consulta creada para un conjunto de datos; por tanto, las propiedades de campo no se pueden arrastrar a la superficie de diseño del informe. En su lugar, debe arrastrar el campo al informe y, después, cambiar la propiedad **Value** del campo a la propiedad que se desee usar. Por ejemplo, si ya se ha dado formato a los datos de celda de un cubo, puede usar la propiedad de campo FormattedValue con la siguiente expresión: `=Fields!FieldName.FormattedValue`.  
  
 Para hacer referencia a una propiedad extendida no predefinida, se utiliza la siguiente sintaxis en una expresión:  
  
-   *Fields!nombreDeCampo("nombreDePropiedad")*  
  
## <a name="predefined-field-properties"></a>Propiedades de campo predefinidas  
 En la mayoría de los casos, las propiedades de campo predefinidas se aplican a las medidas, niveles o dimensiones. Una propiedad de campo predefinida debe tener un valor correspondiente almacenado en el origen de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Si no existe un valor, o si (por ejemplo) especifica una propiedad de campo de solo medida en un nivel, la propiedad devuelve un valor NULL.  
  
 Para hacer referencia a una propiedad predefinida desde una expresión, se utiliza la sintaxis siguiente:  
  
-   *Fields!nombreDeCampo.nombreDePropiedad*  
  
-   *Fields!nombreDeCampo("nombreDePropiedad")*  
  
 En la siguiente tabla se ofrece una lista de las propiedades de campo predefinidas que se pueden usar.  
  
|**Property**|**Type**|**Descripción o valor esperado**|  
|------------------|--------------|---------------------------------------|  
|**Valor**|**Object**|Especifica el valor de los datos del campo.|  
|**IsMissing**|**Boolean**|Indica si se ha encontrado el campo en el conjunto de datos resultante.|  
|**UniqueName**|**String**|Devuelve el nombre completo de un nivel. Por ejemplo, el valor **UniqueName** de un empleado podría ser *[Empleado].[Departamento del empleado].[Departamento].&[Ventas].&[Jefe de ventas de Norteamérica].&[272]* .|  
|**BackgroundColor**|**String**|Devuelve el color de fondo del campo, definido en la base de datos.|  
|**Color**|**String**|Devuelve el color de primer plano del elemento, definido en la base de datos.|  
|**FontFamily**|**String**|Devuelve el nombre de la fuente del elemento, definido en la base de datos.|  
|**FontSize**|**String**|Devuelve el tamaño en puntos de la fuente del elemento, definido en la base de datos.|  
|**FontWeight**|**String**|Devuelve el peso de la fuente del elemento, definido en la base de datos.|  
|**FontStyle**|**String**|Devuelve el estilo de la fuente del elemento, definido en la base de datos.|  
|**TextDecoration**|**String**|Devuelve el formato de texto especial del elemento, definido en la base de datos.|  
|**FormattedValue**|**String**|Devuelve un valor con formato para una medida o cifra clave. Por ejemplo, la propiedad **FormattedValue** de **Cuota de importe de venta** devuelve un formato de moneda similar a $1,124,400.00.|  
|**Clave**|**Object**|Devuelve la clave de un nivel.|  
|**LevelNumber**|**Entero**|En jerarquías de elementos primarios y secundarios, devuelve el número de nivel o dimensión.|  
|**ParentUniqueName**|**String**|En jerarquías de elementos primarios y secundarios, devuelve el nombre completo del nivel primario.|  
  
> [!NOTE]  
>  Solo existirán valores para estas propiedades de campo extendidas si el origen de datos (por ejemplo, el cubo de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ) ofrece estos valores cuando el informe se ejecuta y recupera información para los conjuntos de datos. En ese caso, podrá hacer referencia a esos valores de propiedad de campo desde cualquier expresión mediante la sintaxis descrita en la sección siguiente. No obstante, dado que estos campos son específicos de este proveedor de datos, los cambios que se realicen en los valores no se guardarán con la definición de informe.  
  
### <a name="example-extended-properties"></a>Propiedades extendidas de ejemplo  
 Para ilustrar las propiedades extendidas, la consulta MDX	 y el conjunto de resultados siguientes incluyen varias propiedades de miembro disponibles en un atributo de dimensión definido para un cubo. Las propiedades de miembro incluidas son MEMBER_CAPTION, UNIQUENAME, Properties("Day Name"), MEMBER_VALUE, PARENT_UNIQUE_NAME y MEMBER_KEY.  
  
 Esta consulta MDX se ejecuta en el cubo de [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] de la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] DW que se incluye con las bases de datos de ejemplo de [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] .  
  
```  
WITH MEMBER [Measures].[DateCaption]   
      AS '[Date].[Date].CURRENTMEMBER.MEMBER_CAPTION'   
   MEMBER [Measures].[DateUniqueName]   
      AS '[Date].[Date].CURRENTMEMBER.UNIQUENAME'   
   MEMBER [Measures].[DateDayName]   
      AS '[Date].[Date].Properties("Day Name")'   
   MEMBER [Measures].[DateValueinOriginalDatatype]   
      AS '[Date].[Date].CURRENTMEMBER.MEMBER_VALUE'   
   MEMBER [Measures].[DateParentUniqueName]   
      AS '[Date].[Date].CURRENTMEMBER.PARENT_UNIQUE_NAME'   
   MEMBER [Measures].[DateMemberKeyinOriginalDatatype]   
      AS '[Date].[Date].CURRENTMEMBER.MEMBER_KEY'   
SELECT {  
   [Measures].[DateCaption],   
   [Measures].[DateUniqueName],   
   [Measures].[DateDayName],   
   [Measures].[DateValueinOriginalDatatype],  
   [Measures].[DateParentUniqueName],  
   [Measures].[DateMemberKeyinOriginalDatatype]  
   } ON COLUMNS , [Date].[Date].ALLMEMBERS ON ROWS   
FROM [Adventure Works]  
  
```  
  
 Al ejecutar esta consulta en un panel de consulta MDX, obtiene un conjunto de resultados con 1158 filas. Las primeras cuatro filas se muestran en la siguiente tabla.  
  
|DateCaption|DateUniqueName|DateDayName|DateValueinOriginalDatatype|DateParentUniqueName|DateMemberKeyinOriginalDatatype|  
|-----------------|--------------------|-----------------|---------------------------------|--------------------------|-------------------------------------|  
|All Periods|[Date].[Date].[All Periods]|(null)|(null)|(null)|0|  
|1-Jul-01|[Date].[Date].&[1]|Domingo|7/1/2001|[Date].[Date].[All Periods]|1|  
|2-Jul-01|[Date]. [Date]. & [2]|Lunes|7/2/2001|[Date].[Date].[All Periods]|2|  
|3-Jul-01|[Date].[Date].&[3]|Martes|7/3/2001|[Date].[Date].[All Periods]|3|  
  
 Las consultas MDX predeterminadas que se generan con el diseñador de consultas MDX en modo gráfico solo incluyen MEMBER_CAPTION y UNIQUENAME para las propiedades de dimensión. De manera predeterminada, estos valores siempre son del tipo de datos **String**.  
  
 Si necesita una propiedad de miembro con su tipo de datos original, puede incluir una propiedad MEMBER_VALUE adicional modificando la instrucción MDX predeterminada en el diseñador de consultas basado en texto. En la siguiente instrucción MDX simple, se ha agregado MEMBER_VALUE a la lista de propiedades de dimensión que se deben recuperar.  
  
```  
SELECT NON EMPTY {[Measures].[Order Count]} ON COLUMNS,   
NON EMPTY { ([Date].[Month of Year].[Month of Year] ) }   
DIMENSION PROPERTIES   
   MEMBER_CAPTION, MEMBER_UNIQUE_NAME, MEMBER_VALUE ON ROWS   
FROM [Adventure Works]  
CELL PROPERTIES   
   VALUE, BACK_COLOR, FORE_COLOR,   
   FORMATTED_VALUE, FORMAT_STRING,   
   FONT_NAME, FONT_SIZE, FONT_FLAGS  
```  
  
 Las primeras cuatro filas de resultado del panel de resultados MDX se muestran en la siguiente tabla.  
  
|Month of Year|Número de pedidos|  
|-------------------|-----------------|  
|January|2,481|  
|February|2,684|  
|March|2,749|  
|April|2,739|  
  
 Incluso si las propiedades forman parte de la instrucción SELECT de MDX, no aparecen en las columnas del conjunto de resultados. No obstante, los datos están disponibles para un informe mediante el uso de la característica de propiedades extendidas. En el panel de resultados de una consulta MDX de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], puede hacer doble clic en la celda para ver los valores de propiedades de celda si están establecidos en el cubo. Si hace doble clic en la primera celda de Order Count que contiene 1,379, verá una ventana emergente con las siguientes propiedades de celda:  
  
|Propiedad|Value|  
|--------------|-----------|  
|CellOrdinal|0|  
|VALOR|2481|  
|BACK_COLOR|(null)|  
|FORE_COLOR|(null)|  
|FORMATTED_VALUE|2,481|  
|FORMAT_STRING|#,#|  
|FONT_NAME|(null)|  
|FONT_SIZE|(null)|  
|FONT_FLAGS|(null)|  
  
 Si crea un conjunto de datos de informe con esta consulta y lo enlaza con una tabla, puede ver la propiedad VALUE predeterminada para un campo (por ejemplo, `=Fields!Month_of_Year!Value`). Si establece esta expresión como la expresión de ordenación para la tabla, el resultado es la ordenación alfabética de la tabla por mes, ya que el campo de valor usa un tipo de datos **String** . Para ordenar la tabla de modo que los meses aparezcan en el orden normal de enero a diciembre, use la siguiente expresión:  
  
```  
=Fields!Month_of_Year("MEMBER_VALUE")  
```  
  
 De este modo, se ordena el valor del campo en el tipo de datos de enteros original del origen de datos.  
  
## <a name="see-also"></a>Consulte también  
 [Expresiones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [Colecciones integradas en expresiones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder.md)   
 [Colección Campos del conjunto de datos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
  
  
