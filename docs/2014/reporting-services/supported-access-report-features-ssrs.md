---
title: Compatibilidad con características de informes de Access (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Report Designer [Reporting Services], Access reports
- functions [Reporting Services]
- controls [Reporting Services]
- Access reports [Reporting Services]
- properties [Reporting Services], Access reports
- importing reports
- modules [Reporting Services]
ms.assetid: 7ffec331-6365-4c13-8e58-b77a48cffb44
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 9088ab3e90b4fb341cc8125e45d498783953039d
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66100574"
---
# <a name="supported-access-report-features-ssrs"></a>Compatibilidad con características de informes de Access (SSRS)
  Cuando se importa un informe al Diseñador de informes, el proceso de importación convierte el informe de [!INCLUDE[msCoName](../includes/msconame-md.md)] Access en un archivo RDL (Report Definition Language) de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] admite varias características de Access; no obstante, debido a las diferencias entre Access y [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], algunos elementos deben modificarse ligeramente para que sean admitidos. En este tema, se describe cómo se convierten las características de informes de Access a RDL.  
  
## <a name="importing-access-reports"></a>Importar informes de Access  
 Algunas consultas contienen código específico de Access. El código de Access no se importa con el informe. Asimismo, si una consulta contiene cadenas incrustadas, es posible que el informe no se importe correctamente. Para solucionar este problema, sustituya las cadenas por un código de carácter. Por ejemplo, sustituya el carácter de la coma (,) por CHAR(34).  
  
 El proceso de importación no pasa correctamente el punto y coma (;) o caracteres de marcado XML (\<, >, etc.) en la información de la cadena de conexión. Si una cadena de conexión contiene un punto y coma, o un carácter de marcación XML, tendrá que establecer manualmente la contraseña en el nuevo informe una vez importado.  
  
 En el proceso de importación no se importa la configuración de conexión o de tiempo de espera general de la cadena de conexión. Posiblemente tenga que ajustar esta configuración después de importar el informe.  
  
 Si importa un informe que tiene una consulta que contiene parámetros de consulta, ésta no se convertirá al importar el informe. Para importar la consulta con el informe, reemplace temporalmente los parámetros de consulta del informe de Access por los valores incluidos en el código y, después de importar el informe, vuelva a reemplazarlos por los parámetros de consulta.  
  
## <a name="page-layout"></a>Diseño de página  
 El diseño de página en Access es distinto que en [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. Access organiza los elementos en la página utilizando "bandas", es decir, secciones organizadas verticalmente en la página. Estas secciones pueden incluir el encabezado y pie de página del informe, el encabezado y pie de página, grupos y detalles. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] proporciona un diseño más flexible. Las regiones de datos proporcionan agrupación y detalle, y se pueden colocar varias en cualquier parte del cuerpo del informe, incluso una junto a otra. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] también incluye un encabezado y pie de página "con bandas" parecido al encabezado y pie de página de Access.  
  
 Cuando se importa un informe desde Access en el Diseñador de informes, el pie y el encabezado de página del informe de Access se convierten en el pie y en el encabezado de página del informe de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. Los grupos y detalles se convierten en una región de datos de lista. El encabezado y el pie de página del informe se sitúan en el cuerpo del informe en lugar de en una banda diferente. Como resultado, la ubicación de los elementos puede ser ligeramente diferente a la del informe de Access.  
  
> [!NOTE]  
>  En algunos informes de Access, hay elementos de informe que parecen ser adyacentes entre sí pero en realidad pueden superponerse. Cuando el informe se importa mediante el Diseñador de informes, esta superposición no se corrige y puede generar resultados inesperados al ejecutar el informe.  
  
## <a name="data-sources"></a>Orígenes de datos  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] admite los orígenes de datos OLE DB, como [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Si va a importar informes de un archivo de proyecto de Access (.adp), la cadena de conexión del origen de datos se toma de la cadena de conexión del archivo .adp. Si va a importar informes de un archivo de base de datos de Access (.mdb o .accdb), la cadena de conexión podría apuntar a la base de datos de Access y es posible que deba corregirla después de la importación. Si el origen de datos del informe de Access es una consulta, la información de la misma se guarda sin modificar en el archivo RDL. Si el origen de datos del informe de Access es una tabla, en el proceso de conversión se crea una consulta basada en el nombre de la tabla y de los campos de la misma.  
  
## <a name="reports-with-custom-modules"></a>Informes con módulos personalizados  
 Si no hay personalizado [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] código contenida dentro de los módulos, no se convierte. Si el Diseñador de informes encuentra código durante el proceso de importación, se genera una advertencia y se muestra en el **lista de tareas** ventana.  
  
## <a name="report-controls"></a>Controles de informe  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] admite los siguientes controles de Access y los incluye en las definiciones de informe convertidas:  
  
|||||  
|-|-|-|-|  
|Image|Etiqueta|Línea|Rectángulo|  
|SubForm|SubReport<br /><br /> **Tenga en cuenta** mientras que un control SubReport se convierte en el informe principal, el subinforme propiamente dicho se convierte de forma independiente.|TextBox||  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] no admite los controles siguientes:  
  
|||||  
|-|-|-|-|  
|BoundObjectFrame|CheckBox|ComboBox|CommandButton|  
|CustomControl|ListBox|ObjectFrame|OptionButton|  
|TabControl|ToggleButton|||  
  
 Si el Diseñador de informes encuentra alguno de estos controles durante el proceso de importación, se genera una advertencia y se muestra en el **lista de tareas** ventana.  
  
 Otros controles, como ActiveX y Office Web Components, no se importan. Por ejemplo, si un informe de Access contiene un control Chart de OWC, no se convertirá al importar el informe.  
  
## <a name="report-properties"></a>Propiedades de informe  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] admite las siguientes propiedades, que están disponibles en la interfaz de usuario de Access. Las propiedades que solo están disponibles en el código no se admiten y no se incluyen a continuación.  
  
|||||  
|-|-|-|-|  
|BackColor|BackStyle|BorderColor|BorderStyle|  
|BorderWidth|BottomMargin|CanGrow (textbox)|CanShrink (textbox)|  
|Título|FontBold|FontItalic|FontName|  
|FontSize|FontUnderline|FontWeight|ForceNewPage|  
|ForeColor|Alto|HideDuplicates|Hyperlink|  
|IsHyperlink|IsVisible|KeepTogether (group)|Izquierda|  
|LeftMargin|LineSlant|LineSpacing|LinkChildFields|  
|LinkMasterFields|NewRowOrCol|PageFooter|PageHeader|  
|Páginas|Picture|PictureTiling (report)|ReadingOrder|  
|RepeatSection|RightMargin|RunningSum|SizeMode|  
|TextAlign|TOP|TopMargin|Ancho|  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] no admite las siguientes propiedades, que están disponibles en la interfaz de usuario de Access:  
  
|||||  
|-|-|-|-|  
|CanGrow (section)|CanShrink (section)|DecimalPlaces|FastLaserPrinting|  
|Filter|FilterOn|Formato|FormatConditions|  
|GrpKeepTogether|KeepTogether (section)|NumeralShapes|Orientación|  
|PaintPalette|PaletteSource|PictureAlignment|PicturePages|  
|PictureSizeMode|PictureTiling (image)|ScrollBars|SpecialEffect|  
|Vertical||||  
  
## <a name="grouping"></a>Agrupar  
 Access define un nivel de grupo mediante una combinación de tres propiedades: la expresión de grupo, la propiedad `GroupOn` y la propiedad `GroupInterval`. Un grupo que no tiene un encabezado o pie de grupo se combina con el grupo que contiene. Si el grupo no contiene otro grupo, se ordena la sección detallada y se quita el grupo.  
  
## <a name="expressions"></a>Expresiones  
 Access utiliza expresiones para especificar los valores que se muestran en los cuadros de texto. Access usa [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] como lenguaje de las expresiones, además de algunas funciones de agregado. El Diseñador de informes convierte estas expresiones de Access en expresiones de informe.  
  
### <a name="functions"></a>Funciones  
 Una definición de informe de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] utiliza [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] .NET como lenguaje nativo para las expresiones, mientras que Access 2002 utiliza Visual Basic. En la siguiente lista, se describen las funciones que admite [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
#### <a name="array-functions"></a>Funciones de matriz  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] admite las funciones de matriz siguientes:  
  
-   LBound  
  
-   UBound  
  
#### <a name="conversion-functions"></a>Funciones de conversión  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] admite las funciones de conversión siguientes:  
  
|||||  
|-|-|-|-|  
|Asc|CBool|CByte|CCur|  
|CDate|CDbl|CDec|Chr|  
|Chr$|CInt|CLng|CSng|  
|CStr|CVar|CVDate|Formato|  
|FormatCurrency|FormatDateTime|FormatNumber|FormatPercent|  
|Hex|Hex$|Nz|Oct|  
|Oct$|Str|Str$|StrConv|  
|Val||||  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] no admite las funciones de conversión siguientes:  
  
-   GUIDFromString  
  
-   StringFromGUID  
  
#### <a name="database-functions"></a>Funciones de base de datos  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] admite las funciones de base de datos siguientes:  
  
|||||  
|-|-|-|-|  
|CreateReport|GetObject|HyperlinkPart|Partición|  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] no admite las funciones de base de datos siguientes:  
  
|||||  
|-|-|-|-|  
|CodeDb|CreateControl|CreateForm|CreateGroupLevel|  
|CreateObject|CreateReportControl|CurrentDb|CurrentUser|  
|DeleteControl|DeleteReportControl|Eval|IMEStatus|  
|SysCmd||||  
  
#### <a name="datetime-functions"></a>Funciones de fecha y hora  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] admite las funciones de fecha y hora siguientes:  
  
|||||  
|-|-|-|-|  
|date|Date$|DateAdd|DateDiff|  
|DatePart|DateSerial|DateValue|Day|  
|Hour|Minute|Month|MonthName|  
|Ahora|Second|Time|Time$|  
|Timer|TimeSerial|TimeValue|Weekday|  
|WeekdayName|Year|||  
  
#### <a name="ddeole-functions"></a>Funciones DDE y OLE  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] no admite las funciones de DDE y OLE siguientes:  
  
|||||  
|-|-|-|-|  
|DDE|DDEIntitate|DDERequest|DDESend|  
|LoadPicture||||  
  
#### <a name="domain-aggregate-functions"></a>Funciones de agregado de dominio  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] no admite las funciones de agregado de dominio siguientes:  
  
|||||  
|-|-|-|-|  
|DAvg|DCount|DFirst|DLast|  
|DLookup|DMax|DMin|DStDev|  
|DStDevP|DSum|DVar|DVarP|  
  
#### <a name="error-handling-functions"></a>Funciones de control de errores  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] admite las funciones de control de errores siguientes:  
  
|||||  
|-|-|-|-|  
|Err|Error|Error$|IsError|  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] no admite las funciones de control de errores siguientes:  
  
-   CVErr  
  
#### <a name="financial-functions"></a>Funciones financieras  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] admite las funciones financieras siguientes:  
  
|||||  
|-|-|-|-|  
|DDB|FV|IPmt|IRR|  
|MIRR|NPer|NPV|Pmt|  
|PPmt|PV|Rate|SLN|  
|SYD||||  
  
#### <a name="interaction-functions"></a>Funciones de interacción  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] admite las funciones de interacción siguientes:  
  
|||||  
|-|-|-|-|  
|Comando|Command$|CurDir|CurDir$|  
|DeleteSetting|Dir|Dir$|Environ|  
|Environ$|EOF|FileAttr|FileDateTime|  
|FileLen|FreeFile|GetAllSettings|GetAttr|  
|GetSetting|Loc|LOF|QBColor|  
|RGB|SaveSetting|Seek|SetAttr|  
|Shell|Spc|Pestaña||  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] no admite las funciones de interacción siguientes:  
  
|||||  
|-|-|-|-|  
|DoEvents|Entrada|Entrada|Input$|  
  
#### <a name="inspection-functions"></a>Funciones de inspección  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] admite las funciones de inspección siguientes:  
  
|||||  
|-|-|-|-|  
|IsArray|IsDate|IsEmpty|IsError|  
|IsNull|IsNumeric|IsObject|TypeName|  
|VarType||||  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] no admite las funciones de inspección siguientes:  
  
-   IsMissing  
  
#### <a name="math-functions"></a>Funciones matemáticas  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] admite las funciones matemáticas siguientes:  
  
|||||  
|-|-|-|-|  
|Abs|Atn|Cos|Exp|  
|Fix|int|Log|Rnd|  
|Redondear|Sgn|Sin|Sqr|  
|Tan||||  
  
#### <a name="message-functions"></a>Funciones de mensajes  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] no admite las funciones de mensajes siguientes:  
  
|||||  
|-|-|-|-|  
|InputBox|InputBox$|MsgBox||  
  
#### <a name="program-flow-functions"></a>Funciones de flujo de programa  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] admite las funciones de flujo de programa siguientes:  
  
|||||  
|-|-|-|-|  
|Choose|IIf|Modificador||  
  
#### <a name="sql-aggregate-functions"></a>Funciones de agregado de SQL  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] admite las funciones de agregado de SQL siguientes:  
  
|||||  
|-|-|-|-|  
|Avg|Count|Max|Min|  
|StDev|StDevP|Sum|Var|  
|VarP||||  
  
#### <a name="text-functions"></a>Funciones de texto  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] admite las funciones de texto siguientes:  
  
|||||  
|-|-|-|-|  
|Formato|Format$|InStr|InStrRev|  
|LCase|LCase$|Izquierda|Left$|  
|Len|LTrim|LTrim$|Mid|  
|Mid$|Reemplazar|Derecha|Right$|  
|RTrim|Space|Space$|StrComp|  
|StrConv|String|String$|StrReverse|  
|Trim|Trim$|UCase|UCase$|  
  
### <a name="constants"></a>Constantes  
 Access no admite las constantes especiales de [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] (por ejemplo, `vbTrue`) en las expresiones, por lo que no es necesario realizar ninguna conversión. Sin embargo, hay una excepción: la palabra clave `Null` se convierte en `System.DbNull.Value`.  
  
### <a name="parameters"></a>Parámetros  
 Durante el proceso de importación, el Diseñador de informes examina cada expresión de un informe en busca de variables que no correspondan a nombres de campo o controles. Estas variables se agregan a los parámetros de informe.  
  
 El tipo de datos de los parámetros de procedimientos almacenados siempre se importa como String. Una vez importado el informe, debe cambiar manualmente el parámetro al tipo de datos correcto.  
  
### <a name="object-names"></a>Nombres de objeto  
 Access permite que los campos tengan el mismo nombre que los controles; [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], no. [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 6.0 permite espacios en los nombres de variable; Visual Basic .NET no los permite. En el proceso de importación, se reemplazan los nombres de todos estos objetos por nombres válidos y se asignan nombres únicos si varios objetos tienen el mismo nombre. Se examina cada expresión y los nombres de variables que corresponden a objetos cuyo nombre ha cambiado se reemplazan por nombres nuevos.  
  
## <a name="rectangles-and-containment"></a>Rectángulos y contenedores  
 En una definición de informe de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], los rectángulos pueden contener otros elementos de informe. Un rectángulo de mayor tamaño que el elemento de informe y que solape más del 90 por ciento de su área se convierte en un contenedor del elemento de informe.  
  
## <a name="bitmaps"></a>Mapas de bits  
 Todos los mapas de bits incrustados en un informe se convierten al formato .bmp cuando se importa el informe, independientemente de su formato inicial. Por ejemplo, si el informe contiene archivos .jpg y .gif, los recursos finales importados con el informe son archivos .bmp. Los mapas de bits se guardan como imágenes incrustadas en el informe. Para obtener información sobre las imágenes incrustadas, vea [imágenes &#40;generador de informes y SSRS&#41;](report-design/images-report-builder-and-ssrs.md).  
  
## <a name="other-considerations"></a>Otras consideraciones  
 Además de los elementos anteriores, también cabe destacar lo siguiente en relación con los informes importados desde Access:  
  
-   El formato condicional no se convierte.  
  
-   El campo de descripción de las propiedades del informe en Access no se convierte.  
  
  
