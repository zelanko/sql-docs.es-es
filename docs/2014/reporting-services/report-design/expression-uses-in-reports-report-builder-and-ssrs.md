---
title: Usar expresiones en informes (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- expressions [Reporting Services], about expressions
ms.assetid: 76b9ed31-5aec-40fc-bb88-a1c1b0ab3fc3
caps.latest.revision: 57
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 0a65acdb83f7a9bccc36751a760d61133597caf8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36107818"
---
# <a name="expression-uses-in-reports-report-builder-and-ssrs"></a>Usar expresiones en informes (Generador de informes y SSRS)
  Las expresiones se usan durante la definición de informe para especificar o calcular valores para: parámetros, consultas, filtros, propiedades de elementos de informe, definiciones de ordenación y de grupos, propiedades de cuadros de texto, marcadores, mapas de documento, contenido de encabezados y pies de página dinámicos, imágenes y definiciones de orígenes de datos dinámicas. En este tema, se proporcionan ejemplos de los muchos lugares en los que se pueden usar expresiones para modificar el contenido o el aspecto de un informe. Esta lista no es una lista completa. Puede establecer una expresión para una propiedad de un cuadro de diálogo que muestre el botón (**fx**) de la expresión o en una lista desplegable que muestre **\<Expression...>**.  
  
 Las expresiones pueden ser simples o complejas. Las*expresiones simples* contienen una referencia a un único campo de conjunto de datos, parámetro o campo integrado. Las expresiones complejas pueden contener varias referencias, operadores y llamadas a función integrados. Por ejemplo, una expresión compleja podría incluir la función Sum aplicada al campo Sales.  
  
 Las expresiones se escriben en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]. Una expresión comienza por un signo igual (=) seguido de una combinación de referencias a colecciones integradas, como campos y parámetros de conjunto de datos, constantes, funciones y operadores.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="Simple"></a> Usar expresiones simples  
 Las expresiones simples aparecen en la superficie de diseño y en los cuadros de diálogo entre corchetes, por ejemplo, un campo de conjunto de datos aparece como `[ProductID]`. Este tipo de expresiones se crea automáticamente cuando se arrastra un campo desde un conjunto de datos hasta un cuadro de texto. Se crea un marcador de posición y la expresión define el valor subyacente. También puede escribir directamente las expresiones en una celda o en un cuadro de texto de la región de datos, tanto en la superficie de diseño como en un cuadro de diálogo (por ejemplo, `[ProductID]`).  
  
 En la tabla siguiente, se muestran ejemplos de cómo se pueden usar las expresiones simples. En la tabla se describe la funcionalidad, la propiedad que se va a establecer, el cuadro de diálogo que se usa normalmente para establecerla y el valor de la propiedad. Puede escribir la expresión simple directamente en la superficie de diseño, en un cuadro de diálogo o en el panel de propiedades, o puede modificarla en el cuadro de dialogo Expresión, tal y como lo haría con cualquier expresión.  
  
|Funcionalidad|Propiedad, contexto y cuadro de diálogo|Valor de la propiedad|  
|-------------------|---------------------------------------|--------------------|  
|Especificar un campo de conjunto de datos para mostrarlo en un cuadro de texto.|Propiedad Value de un marcador de posición dentro de un cuadro de texto. Use **Propiedades del marcador de posición (cuadro de diálogo), General**.|`[Sales]`|  
|Valores agregados para un grupo.|Propiedad Value de un marcador de posición dentro de una fila asociada a un grupo de Tablix. Use **Propiedades de cuadro de texto (cuadro de diálogo)**.|`[Sum(Sales)]`|  
|Incluir un número de página.|Propiedad Value de un marcador de posición dentro de un cuadro de texto situado en un encabezado de página. Use **Propiedades de cuadro de texto (cuadro de diálogo), General**.|`[&PageNumber]`|  
|Mostrar un valor de parámetro seleccionado.|Propiedad Value de un marcador de posición dentro de un cuadro de texto de la superficie de diseño. Use **Propiedades de cuadro de texto (cuadro de diálogo), General**.|`[@SalesThreshold]`|  
|Especificar una definición de grupo para una región de datos.|Expresión de grupo del grupo de Tablix. Use **Propiedades de grupo de Tablix (cuadro de diálogo), General**.|`[Category]`|  
|Excluir de una tabla un valor de campo específico.|Ecuación de filtro de Tablix. Use **Propiedades de Tablix (cuadro de diálogo), Filtros**.|Como tipo de datos, seleccione **Integer**.<br /><br /> `[Quantity]`<br /><br /> `>`<br /><br /> `100`|  
|Incluir solo un valor específico para un filtro de grupo.|Ecuación de filtro del grupo de Tablix. Use **Propiedades de grupo de Tablix (cuadro de diálogo), Filtros**.|`[Category]`<br /><br /> `=`<br /><br /> `Clothing`|  
|Excluir valores específicos de varios campos de un conjunto de datos.|Ecuación de filtro de un grupo de Tablix. Use **Propiedades de Tablix (cuadro de diálogo), Filtros**.|`=[Color]`<br /><br /> `<>`<br /><br /> `Red`<br /><br /> `=[Color]`<br /><br /> `<>`<br /><br /> `Blue`|  
|Especificar el criterio de ordenación en función de un campo existente en una tabla.|Expresión de ordenación de Tablix. Use **Propiedades de Tablix (cuadro de diálogo), Ordenar**.|`[SizeSortOrder]`|  
|Vincular un parámetro de consulta a un parámetro de informe.|Colección de parámetros del conjunto de datos. Use **Propiedades del conjunto de datos (cuadro de diálogo), Parámetros**.|`[@Category]`<br /><br /> `[@Category]`|  
|Pasar un parámetro de un informe principal a un subinforme.|Colección de parámetros del subinforme. Use **Propiedades del subinforme (cuadro de diálogo), Parámetros**.|`[@Category]`<br /><br /> `[@Category]`|  
  
 
  
##  <a name="Complex"></a> Usar expresiones complejas  
 Las expresiones complejas pueden contener varias referencias integradas, operadores y llamadas a función, y aparecen en la superficie de diseño como `<<Expr>>`. Para ver o cambiar el texto de la expresión, debe abrir el cuadro de diálogo **Expresión** o escribir directamente en el panel Propiedades. En la tabla siguiente, se muestran las formas más habituales de usar una expresión compleja para mostrar u organizar datos o para cambiar el aspecto de un informe, incluida la propiedad que se va a establecer, el cuadro de diálogo que se usa normalmente para establecerla y el valor de la propiedad. Puede escribir una expresión directamente en un cuadro de diálogo, en la superficie de diseño o en el panel de propiedades.  
  
|Funcionalidad|Propiedad, contexto y cuadro de diálogo|Valor de la propiedad|  
|-------------------|---------------------------------------|--------------------|  
|Calcular los valores agregados para un conjunto de datos.|Propiedad Value de un marcador de posición dentro de un cuadro de texto. Use **Propiedades del marcador de posición (cuadro de diálogo), General**.|`=First(Fields!Sales.Value,"DataSet1")`|  
|Concatenar texto y expresiones en el mismo cuadro de texto.|Propiedad Value de un marcador de posición dentro de un cuadro de texto situado en un encabezado o pie de página. Use **Propiedades del marcador de posición (cuadro de diálogo), General**.|`="This report began processing at " & Globals!ExecutionTime`|  
|Calcular un valor agregado para un conjunto de datos de otro ámbito.|Propiedad Value de un marcador de posición dentro de un cuadro de texto situado en un grupo de Tablix. Use **Propiedades del marcador de posición (cuadro de diálogo), General**.|`=Max(Fields!Total.Value,"DataSet2)`|  
|Dar formato a los datos de un cuadro de texto en función del valor.|Propiedad Color de un marcador de posición dentro de un cuadro de texto de la fila de detalles de Tablix. Use **Propiedades de cuadro de texto (cuadro de diálogo), Fuente**.|`=IIF(Fields!TotalDue.Value < 10000,"Red","Black")`|  
|Calcular un valor una sola vez y hacer referencia a él en el informe.|Propiedad Value de una variable de informe. Use **Propiedades del informe (cuadro de diálogo), Variables**.|`=Variables!MyCalculation.Value`|  
|Incluir valores específicos de varios campos de un conjunto de datos.|Ecuación de filtro de un grupo de Tablix. Use **Propiedades de Tablix (cuadro de diálogo), Filtros**.|Como tipo de datos, seleccione **Boolean**.<br /><br /> `=IIF(InStr(Fields!Subcat.Value,"Shorts")=0 AND (Fields!Size.Value="M" OR Fields!Size.Value="S"),TRUE, FALSE)`<br /><br /> `=`<br /><br /> `TRUE`|  
|Ocultar un cuadro de texto en la superficie de diseño y permitir que el usuario pueda volver a mostrarlo con un parámetro Boolean denominado *Show*.|Propiedad Hidden de un cuadro de texto. Use **Propiedades de cuadro de texto (cuadro de diálogo), Visibilidad**.|`=Not Parameters!` *Show\<parámetro booleano>* `.Value`|  
|Especificar contenido dinámico para el encabezado o el pie de página.|Propiedad Value de un marcador de posición dentro de un cuadro de texto situado en el encabezado o pie de página.|`="Page " & Globals!PageNumber & " of "  & Globals!TotalPages`|  
|Especificar un origen de datos de forma dinámica mediante un parámetro.|Cadena de conexión del origen de datos. Use **Propiedades del origen de datos (cuadro de diálogo), General**.|`="Data Source=" & Parameters!ServerName.Value & ";initial catalog=AdventureWorks2012"`|  
|Identificar todos los valores de un parámetro de varios valores elegidos por el usuario.|Propiedad Value de un marcador de posición dentro de un cuadro de texto. Use **Propiedades de Tablix (cuadro de diálogo), Filtros**.|`=Join(Parameters!MyMultivalueParameter.Value,", ")`|  
|Especificar saltos de página cada 20 filas en un Tablix sin otros grupos.|Expresión de grupo de un grupo de Tablix. Use **Propiedades de grupo de Tablix (cuadro de diálogo), Saltos de página**. Seleccione la opción **Entre cada instancia de un grupo**.|`=Ceiling(RowNumber(Nothing)/20)`|  
|Especificar la visibilidad condicional en función de un parámetro.|Propiedad Hidden de Tablix. Use **Propiedades de Tablix (cuadro de diálogo), Visibilidad**.|`=Not Parameters!<` *parámetro booleano* `>.Value`|  
|Especificar una fecha con formato para una referencia cultural concreta.|Propiedad Value de un marcador de posición dentro de un cuadro de texto de una región de datos. Use **Propiedades de cuadro de texto (cuadro de diálogo), General**.|`=Fields!OrderDate.Value.ToString(System.Globalization.CultureInfo.CreateSpecificCulture("de-DE"))`|  
|Concatenar una cadena y un número con formato de porcentaje con dos decimales.|Propiedad Value de un marcador de posición dentro de un cuadro de texto de una región de datos. Use **Propiedades de cuadro de texto (cuadro de diálogo), General**.|`="Growth Percent: " & Format(Fields!Growth.Value,"p2")`|  
  
 
  
## <a name="see-also"></a>Vea también  
 [Expresiones &#40;Generador de informes y SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [Ejemplos de expresiones &#40;Generador de informes y SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [Parámetros de informe &#40;Generador de informes y Diseñador de informes&#41;](report-parameters-report-builder-and-report-designer.md)   
 [Ejemplos de ecuaciones de filtro &#40;el generador de informes SSRS&#41;](filter-equation-examples-report-builder-and-ssrs.md)   
 [Filtrar, agrupar y ordenar datos &#40;Generador de informes y SSRS&#41;](filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Encabezados y pies de página &#40;el generador de informes SSRS&#41;](page-headers-and-footers-report-builder-and-ssrs.md)   
 [Aplicar formato a texto y marcadores de posición &#40;el generador de informes SSRS&#41;](formatting-text-and-placeholders-report-builder-and-ssrs.md)   
 [Ocultar un elemento &#40;Generador de informes y SSRS&#41;](../report-builder/hide-an-item-report-builder-and-ssrs.md)  
  
  