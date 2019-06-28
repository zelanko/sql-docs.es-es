---
title: Expresiones (Generador de informes y SSRS) | Microsoft Docs
ms.prod: sql-server-2014
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 76d3ac86-650c-46fe-8086-8b3edcea3882
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.custom: ''
ms.date: 06/13/2017
ms.openlocfilehash: 3660ecee1271d4fd2673b0dfe9107a8fb5c52e88
ms.sourcegitcommit: 0a4879dad09c6c42ad1ff717e4512cfea46820e9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/27/2019
ms.locfileid: "67413014"
---
# <a name="expressions-report-builder-and-ssrs"></a>Expresiones (Generador de informes y SSRS)

Las expresiones se utilizan ampliamente a lo largo de un informe para recuperar, calcular, mostrar, agrupar, ordenar, filtrar y parametrizar datos y darles formato. Muchas propiedades de elementos de informe pueden establecerse en una expresión. Las expresiones le ayudan a controlar el contenido, el diseño y la interactividad de un informe. Las expresiones se escriben en [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)], se guardan en la definición de informe y son evaluadas por el procesador de informes al ejecutar el informe.  

A diferencia de aplicaciones como [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Office Excel en que se trabaja directamente con datos en una hoja de cálculo, en un informe se trabaja con expresiones que son marcadores de posición para los datos. Para ver los datos reales de las expresiones evaluadas, debe obtener una vista previa del informe. Al ejecutar el informe, el procesador de informes evalúa cada expresión a medida que combina los datos del informe y elementos de diseño del informe, como tablas y gráficos.  

Cuando diseña un informe, muchas expresiones de los elementos de informe se establecen automáticamente. Por ejemplo, al arrastrar un campo desde el panel de datos hasta una celda de la tabla en la superficie de diseño del informe, el valor del cuadro de texto se establece en una expresión simple para el campo. En la siguiente figura, el panel Datos de informe muestra el identificador de los campos de conjunto de datos Name, SalesTerritory, Code y Sales. Se han agregado tres campos a la tabla: [Name], [Code] y [Sales]. La notación [Name] en la superficie de diseño representa la expresión `=Fields!Name.Value`subyacente.  

![rs_DataDesignandPreview](../media/rs-datadesignandpreview.gif "rs_DataDesignandPreview")  

Al obtener una vista previa del informe, el procesador de informes combina la región de datos de la tabla con los datos reales de la conexión de datos y muestra una fila en la tabla para cada fila del conjunto de resultados.  

Para escribir expresiones manualmente, seleccione un elemento en la superficie de diseño y use los menús contextuales y los cuadros de diálogo para establecer las propiedades del elemento. Cuando vea el botón ***(fx)*** o el valor `<Expression>` en una lista desplegable, sabrá que puede establecer la propiedad en una expresión. Para obtener más información, vea [Agregar una expresión &#40;Generador de informes y SSRS&#41;](add-an-expression-report-builder-and-ssrs.md).  

Para obtener más información y ejemplos, vea los siguientes temas:  

-   [Usar expresiones en informes &#40;Generador de informes y SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)  

-   [Ejemplos de expresiones &#40;Generador de informes y SSRS&#41;](expression-examples-report-builder-and-ssrs.md)  

-   [Ejemplos de ecuaciones de filtro &#40;Generador de informes y SSRS&#41;](filter-equation-examples-report-builder-and-ssrs.md)  

-   [Ejemplos de expresión de grupo &#40;Generador de informes y SSRS&#41;](group-expression-examples-report-builder-and-ssrs.md)  

-   [Tutoriales &#40;generador de informes&#41;](../report-builder-tutorials.md)  

-   [Tutoriales de Reporting Services &#40;SSRS&#41;](../reporting-services-tutorials-ssrs.md)  

-   [Ejemplos de informes (Generador de informes y SSRS)](https://go.microsoft.com/fwlink/?LinkId=198283)  

Para desarrollar expresiones complejas o expresiones que utilizan código personalizado o ensamblados personalizados, recomendamos utilizar el Diseñador de informes en [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]. Para obtener más información, vea [Referencias a ensamblados y código personalizado en expresiones en el Diseñador de informes &#40;SSRS&#41;](custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)subyacente.  

> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  

##  <a name="Types"></a> Descripción de las expresiones simples y complejas  
Las expresiones comienzan por un signo igual (=) y se escriben en [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]. Las expresiones pueden incluir una combinación de constantes, operadores y referencias a valores integrados (campos, colecciones y funciones) y a código externo o personalizado.  

Puede utilizarlas para especificar el valor de muchas propiedades de elementos de informe. Las propiedades más comunes son los valores de los cuadros de texto y el texto de los marcadores de posición. Normalmente, si un cuadro de texto contiene solo una expresión, esta es el valor de la propiedad de cuadro de texto. Si un cuadro de texto contiene varias expresiones, cada una es el valor de texto del marcador de posición en el cuadro de texto.  

De forma predeterminada, las expresiones aparecen en la superficie de diseño del informe como *expresiones simples* o *expresiones complejas*.  

-   **Simple** : las expresiones simples contienen una referencia a un solo elemento de una colección integrada, como un campo de conjunto de datos, un parámetro o un campo integrado. En la superficie de diseño, una expresión simple aparece entre corchetes. Por ejemplo, `[FieldName]` corresponde a la expresión `=Fields!FieldName.Value`subyacente. Las expresiones simples se crean automáticamente al crear el diseño del informe y arrastrar los elementos del panel Datos de informe a la superficie de diseño. Para obtener más información sobre los símbolos que representan diferentes colecciones integradas, vea [Descripción de los símbolos de prefijo en expresiones simples](#DisplayText).  

-   **Compleja** : las expresiones complejas contienen referencias a varias referencias, operadores y llamadas a función integradas. Una expresión compleja aparece como <\<Expr>> cuando el valor de expresión incluye más de una referencia simple. Para ver la expresión, mantenga el mouse sobre ella y use la información sobre herramientas. Para modificar la expresión, ábrala en el cuadro de diálogo **Expresión** .  

La siguiente figura muestra expresiones simples y complejas típicas para cuadros de texto y el texto de los marcadores de posición.  

![rs_ExpressionDefaultFormat](../media/rs-expressiondefaultformat.gif "rs_ExpressionDefaultFormat")  

Para mostrar valores de ejemplo en lugar del texto de las expresiones, aplique el formato al cuadro de texto o al texto del marcador de posición. La siguiente figura muestra la superficie de diseño del informe alternada para mostrar los valores de ejemplo:  

![rs_ExpressionSampleValuesFormat](../media/rs-expressionsamplevaluesformat.gif "rs_ExpressionSampleValuesFormat")  

Para más información, vea [Aplicar formato a texto y a marcadores de posición &#40;Generador de informes y SSRS&#41;](formatting-text-and-placeholders-report-builder-and-ssrs.md).  

## <a name="DisplayText"></a> Descripción de los símbolos de prefijo en expresiones simples  

Las expresiones simples usan símbolos para indicar si la referencia es a un campo, un parámetro, una colección integrada o la colección ReportItems. En la tabla siguiente, se muestran ejemplos de texto mostrado junto con el texto de la expresión correspondiente:  

|Elemento|Ejemplo de texto mostrado|Ejemplo de texto de expresión|  
|----------|--------------------------|-----------------------------|  
|Campos de conjunto de datos|`[Sales]`<br /><br /> `[SUM(Sales)]`<br /><br /> `[FIRST(Store)]`|`=Fields!Sales.Value`<br /><br /> `=Sum(Fields!Sales.Value)`<br /><br /> `=First(Fields!Store.Value)`|  
|Parámetros de informe|`[@Param]`<br /><br /> `[@Param.Label]`|`=Parameters!Param.Value`<br /><br /> `=Parameters!Param.Label`|  
|Campos integrados|`[&ReportName]`|`=Globals!ReportName.Value`|  
|Caracteres literales usados para el texto mostrado|`\[Sales\]`|`[Sales]`|  



##  <a name="References"></a> Escribir expresiones complejas  
Las expresiones pueden incluir referencias a funciones, operadores, constantes, campos, parámetros, elementos de colecciones integradas y referencias a código personalizado incrustado o a ensamblados personalizados.  

> [!NOTE]
>  Para desarrollar expresiones complejas o expresiones que utilizan código personalizado o ensamblados personalizados, recomendamos utilizar el Diseñador de informes en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]. Para obtener más información, vea [Referencias a ensamblados y código personalizado en expresiones en el Diseñador de informes &#40;SSRS&#41;](custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)subyacente.  

En la tabla siguiente se enumeran los tipos de referencias que se pueden incluir en una expresión:  

|Referencias|Descripción|Ejemplo|  
|----------------|-----------------|-------------|  
|[Constantes](expressions-report-builder-and-ssrs.md)|Describe las constantes a las que puede tener acceso interactivamente para las propiedades que requieren valores constantes, por ejemplo los colores de fuente.|`="Blue"`|  
|[Operadores](operators-in-expressions-report-builder-and-ssrs.md)|Describe los operadores que puede utilizar para combinar referencias en una expresión. Por ejemplo, el operador `&` se utiliza para concatenar cadenas.|`="The report ran at: " & Globals!ExecutionTime & "."`|  
|[Colecciones integradas](built-in-collections-in-expressions-report-builder.md)|Describe las colecciones integradas que puede incluir en una expresión; por ejemplo, `Fields`, `Parameters`y `Variables`.|`=Fields!Sales.Value`<br /><br /> `=Parameters!Store.Value`<br /><br /> `=Variables!MyCalculation.Value`|  
|[Funciones integradas de informe y de agregado](report-builder-functions-aggregate-functions-reference.md)|Describe funciones integradas, como `Sum` o `Previous`, a las que puede tener acceso desde una expresión.|`=Previous(Sum(Fields!Sales.Value))`|  
|[Referencias a ensamblados y código personalizado en expresiones en el Diseñador de informes &#40;SSRS&#41;](custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)|Describe cómo puede obtener acceso a las clases integradas de CLR <xref:System.Math> y <xref:System.Convert>, a otras clases de CLR, a funciones de biblioteca en tiempo de ejecución de [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] o a métodos de un ensamblado externo.<br /><br /> Describe cómo puede tener acceso a código personalizado incrustado en un informe, o que se compila e instala como un ensamblado personalizado en el cliente de informes y en el servidor de informes.|`=Sum(Fields!Sales.Value)`<br /><br /> `=CDate(Fields!SalesDate.Value)`<br /><br /> `=DateAdd("d",3,Fields!BirthDate.Value)`<br /><br /> `=Code.ToUSD(Fields!StandardCost.Value)`|  



##  <a name="Valid"></a> Validar las expresiones  
Cuando cree una expresión para una propiedad de elemento de informe determinada, las referencias que puede incluir en una expresión dependen de los valores que la propiedad del elemento de informe pueda aceptar y del ámbito en el que se evalúa la propiedad. Por ejemplo:  

-   De forma predeterminada, la expresión [Suma] calcula la suma de los datos que están en el ámbito en el momento en que se evalúa la expresión. Para una celda de la tabla, el ámbito depende de la fila y las pertenencias a los grupos de columnas. Para obtener más información, vea [Ámbito de expresión para los totales, agregados y colecciones integradas &#40;Generador de informes y SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)subyacente.  

-   Para el valor de una propiedad Font, el valor se debe evaluar como el nombre de una fuente.  

-   La sintaxis de la expresión se valida en tiempo de diseño. La validación del ámbito de la expresión se produce al publicar el informe. En el caso de la validación que depende de los datos reales, los errores se pueden detectar solo en tiempo de ejecución. Algunas de estas expresiones generan #Error como un mensaje de error en el informe representado. Para ayudar a determinar los problemas de este tipo de error, debe utilizar el Diseñador de informes en [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]. El Diseñador de informes proporciona un ventana de salida que proporciona más información acerca de estos errores.  

Para obtener más información, vea [Referencia de expresiones &#40;Generador de informes y SSRS&#41;](expression-reference-report-builder-and-ssrs.md)subyacente.  

## <a name="Section"></a> En esta sección

[Agregar una expresión &#40;Generador de informes y SSRS&#41;](add-an-expression-report-builder-and-ssrs.md)  

[Usar expresiones en informes &#40;Generador de informes y SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)  

[Ámbito de expresión para los totales, agregados y colecciones integradas &#40;Generador de informes y SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  

[Referencia de expresiones &#40;Generador de informes y SSRS&#41;](expression-reference-report-builder-and-ssrs.md)  

## <a name="see-also"></a>Vea también

- [Expresión (cuadro de diálogo)](../expression-dialog-box.md)   
- [Expresión &#40;cuadro de diálogo del Generador de informes&#41;](../expression-dialog-box-report-builder.md)