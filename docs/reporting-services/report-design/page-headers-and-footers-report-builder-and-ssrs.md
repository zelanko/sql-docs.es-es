---
title: "Página encabezados y pies de página (generador de informes y SSRS) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- "10125"
- sql13.rtp.rptdesigner.pagefooter.border.f1
- "10121"
- "10120"
- "10122"
- sql13.rtp.rptdesigner.pageheader.general.f1
- "10123"
- sql13.rtp.rptdesigner.pageheader.fill.f1
- sql13.rtp.rptdesigner.pageheader.border.f1
- sql13.rtp.rptdesigner.pagefooter.fill.f1
- sql13.rtp.rptdesigner.pagefooter.general.f1
- "10124"
ms.assetid: 4fb9faac-511e-404a-b8d7-1f2e3cb47b11
caps.latest.revision: 6
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f89d2e283daf9b9ac107c098d38db4feab17a736
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="page-headers-and-footers-report-builder-and-ssrs"></a>Encabezados y pies de página (Generador de informes y SSRS)
  Un informe puede contener un encabezado y un pie de página que aparecen en la parte superior e inferior de cada página, respectivamente. Los encabezados y pies de página pueden contener texto estático, imágenes, líneas, rectángulos, bordes, color de fondo, imágenes de fondo y expresiones. Las expresiones incluyen referencias a campos de conjunto de datos para informes que tienen un conjunto de datos y llamadas a funciones de agregado que incluyen el conjunto de datos como ámbito.  
  
> [!NOTE]  
>  Cada extensión de representación procesa las páginas de forma diferente. Para más información sobre las extensiones de representación y paginación de informes, vea [Paginación en Reporting Services &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md).  
  
 De forma predeterminada, los informes tienen pies de página, pero no encabezados de página. Para más información sobre cómo agregarlas o quitarlas, vea [Agregar o quitar un encabezado o un pie de página &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/add-or-remove-a-page-header-or-footer-report-builder-and-ssrs.md).  
  
 Normalmente, los encabezados y pies contienen números de página, títulos de informe y otras propiedades de informe. Para más información sobre cómo agregar estos elementos al encabezado o pie de página del informe, vea [Mostrar números de página u otras propiedades del informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/display-page-numbers-or-other-report-properties-report-builder-and-ssrs.md).  
  
 Una vez creado el encabezado o pie de página, este aparece en cada una de las páginas del informe. Para más información sobre cómo eliminar encabezados y pies de página en la primera y la última página, vea [Ocultar un encabezado o un pie de página en la primera o en la última página &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/hide-a-page-header-or-footer-on-the-first-or-last-page-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="report-headers-and-footers"></a>Encabezados y pies de página del informe  
 Los encabezados y los pies de página no son lo mismo que los encabezados y los pies de informe. Los informes no tienen un área especial para situar el encabezado o el pie. Un encabezado de informe se compone de elementos de informe que se sitúan en la parte superior del cuerpo del informe en la superficie de diseño del informe. Solo aparecen una vez como el primer contenido del informe. Un pie de informe se compone de elementos de informe que se sitúan en la parte inferior del cuerpo del informe. Solo aparecen una vez como el último contenido del informe.  
  
## <a name="displaying-variable-data-in-a-page-header-or-footer"></a>Mostrar datos variables en un encabezado o pie de página  
 El contenido de los encabezados y los pies de página puede ser estático, aunque es habitual usarlos para mostrar contenido variable, como números de página o información sobre el contenido de una página. Para mostrar datos variables distintos en cada página, debe usar una expresión.  
  
 Si solo hay un conjunto de datos definido en el informe, podrá agregar expresiones simples como `[FieldName]` al encabezado o pie de página. Arrastre el campo desde la colección de campos de conjunto de datos del panel Datos de informe o desde la colección de campos integrados hasta el encabezado o pie de página. Se agrega un cuadro de texto con la expresión adecuada de forma automática.  
  
 Para calcular sumas u otros agregados con los valores de la página, puede usar expresiones de agregado que especifiquen ReportItems o el nombre de un conjunto de datos. La colección ReportItems es la colección de cuadros de texto de cada página después de haber tenido lugar la representación del informe. El nombre del conjunto de datos debe hallarse en la definición de informe. En la tabla siguiente, se muestran los elementos que se admiten en cada tipo de expresión de agregado:  
  
|Admitido en la expresión|Agregados de ReportItems|Agregados de conjunto de datos (el ámbito debe ser el nombre del conjunto de datos)|  
|-----------------------------|----------------------------|----------------------------------------------------------|  
|Cuadros de texto del cuerpo del informe|Sí|No|  
|&PageNumber|Sí|No|  
|&TotalPages|Sí|No|  
|Aggregate, función|Sí. Por ejemplo,<br /><br /> `=First(ReportItems!TXT_LastName.Value)`|Sí. Por ejemplo,<br /><br /> `=Max(Quantity.Value,"DataSet1")`|  
|Colección de campos para los elementos de la página|Indirectamente. Por ejemplo,<br /><br /> `=Sum(ReportItems!Textbox1.Value)`|Sí. Por ejemplo,<br /><br /> `=Sum(Fields!Quantity.Value,"DataSet1")`|  
|Imagen enlazada a datos|Indirectamente. Por ejemplo, `=ReportItems!TXT_Photo.Value`|Sí. Por ejemplo,<br /><br /> `=First(Fields!Photo.Value,"DataSet1")`|  
  
 Las secciones siguientes de este tema muestran expresiones listas para usar que generan datos variables usados habitualmente en los encabezados y pies de página. También hay una sección en la que se explica la forma en que la extensión de representación en Excel procesa encabezados y pies de página. Para más información sobre las expresiones, vea [Expresiones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md).  
  
### <a name="adding-calculated-page-totals-to-a-header-or-footer"></a>Agregar un total de páginas calculado a un encabezado o pie de página  
 En algunos informes, resulta útil incluir un valor calculado en el encabezado o pie de página; por ejemplo, una suma total por página si la página incluye valores numéricos. Dado que no se puede hacer referencia a los campos directamente, la expresión que use en el encabezado o pie de página debe hacer referencia al nombre del elemento del informe (por ejemplo, un cuadro de texto), en lugar de a un campo de datos:  
  
 `=Sum(ReportItems!Textbox1.Value)`  
  
 Si el cuadro de texto se encuentra en una tabla o lista que contiene filas de datos repetidas, el valor que aparezca en el encabezado o pie de página en tiempo de ejecución será una suma de los valores de todos los datos de la instancia de `TextBox1` en la tabla o lista de la página actual.  
  
 Si usa extensiones de representación diferentes para ver el informe, es probable que al calcular los totales de página también obtenga resultados diferentes. El resultado paginado se calcula de forma diferente para cada extensión de representación. La misma página que ve en HTML puede mostrar totales diferentes cuando se ve en PDF si la cantidad de datos que aparece en la página PDF es diferente. Para más información, vea [Comportamientos de la representación &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md).  
  
### <a name="for-reports-with-multiple-datasets"></a>Para informes con varios conjuntos de datos  
 Si se trata de informes con más de un conjunto de datos, no podrá agregar campos ni imágenes enlazadas a datos directamente en un encabezado o pie de página. Sin embargo, sí podrá escribir una expresión que haga referencia indirectamente al campo o imagen enlazada a datos que desee usar en un encabezado o pie de página.  
  
 Para usar datos variables en un encabezado o pie de página:  
  
-   Agregue un cuadro de texto al encabezado o pie de página.  
  
-   En el cuadro de texto, escriba una expresión que genere los datos variables que desea que aparezcan.  
  
-   En la expresión, incluya referencias a elementos de informe de la página; por ejemplo, puede hacer referencia a un cuadro de texto que contenga datos de un campo concreto. No incluya una referencia directa a campos de un conjunto de datos. Por ejemplo, no puede usar la expresión `[LastName]`. Para mostrar el contenido de la primera instancia de un cuadro de texto denominado `TXT_LastName`, puede usar la expresión siguiente:  
  
     `=First(ReportItems!TXT_LastName.Value)`  
  
 No puede usar funciones de agregado en campos del encabezado o pie de página. Solo puede usar funciones de agregado en elementos de informe del cuerpo del informe. Para consultar expresiones comunes en encabezados y pies de página, vea [Ejemplos de expresiones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md).  
  
#### <a name="adding-a-data-bound-image-to-a-header-or-footer"></a>Agregar una imagen enlazada a datos a un encabezado o pie de página  
 Puede usar datos de imágenes almacenados en una base de datos en el encabezado o pie de página. Sin embargo, no puede hacer referencia a campos de la base de datos directamente desde el elemento de informe Imagen. En su lugar, debe agregar un cuadro de texto al cuerpo del informe y, a continuación, asignar dicho cuadro de texto al campo de datos que contiene la imagen (tenga en cuenta que el valor debe estar en formato codificado base64). Puede ocultar el cuadro de texto en el cuerpo del informe para evitar que se muestre la imagen con codificación base64. A continuación, puede hacer referencia al valor del cuadro de texto oculto desde el elemento de informe Imagen en el encabezado o pie de página.  
  
 Por ejemplo, imagine que tiene un informe que consta de páginas de información de producto. En el encabezado de cada página, desea que aparezca una fotografía del producto. Para imprimir una imagen almacenada en el encabezado del informe, defina un cuadro de texto oculto denominado `TXT_Photo` en el cuerpo del informe que recupere la imagen de la base de datos y use una expresión para asignarle un valor:  
  
 `=Convert.ToBase64String(Fields!Photo.Value)`  
  
 En el encabezado, agregue un elemento de informe Imagen que use el cuadro de texto `TXT_Photo` , descodificado para mostrar la imagen:  
  
 `=Convert.FromBase64String(ReportItems!TXT_Photo.Value)`  
  
## <a name="using-headers-and-footers-to-position-text"></a>Usar encabezados y pies de página para colocar texto  
 Puede usar encabezados y pies de página para colocar texto en una página. Por ejemplo, suponga que está creando un informe que desea enviar por correo a los clientes. Puede utilizar un encabezado o pie de página para colocar la dirección del cliente de forma que aparezca en una ventanilla de sobre cuando doble el informe.  
  
 Si solamente utiliza un cuadro de texto para llenar un encabezado o pie de página, puede ocultar este cuadro de texto en el cuerpo del informe. La colocación del cuadro de texto en el cuerpo del informe puede influir en si el valor aparece en el encabezado o el pie de página de la primera o la última página de un informe. Por ejemplo, si tiene tablas, matrices o listas que hacen que el informe ocupe varias páginas, el valor del cuadro de texto oculto aparecerá en la última página. Si desea que aparezca en la primera página, coloque el cuadro de texto oculto en la parte superior del cuerpo del informe.  
  
## <a name="designing-reports-with-page-headers-and-footers-for-specific-renderers"></a>Diseñar informes con encabezados y pies de página para representadores específicos  
 Cuando se procesa un informe, se combinan los datos y la información sobre el diseño. Cuando se ve un informe, la información combinada se pasa a un representador que determina la cantidad de datos que caben en cada página del informe.  
  
 Si usa un explorador para ver un informe del servidor de informes, el representador de HTML controlará el contenido que se ve en cada una de las páginas. Si piensa entregar los informes en un formato diferente del que se usa para verlos, o si piensa imprimir los informes en un formato concreto, es posible que le interese optimizar el diseño del informe para el representador que va a usar para el formato final. Para más información sobre la paginación de informes, vea [Paginación en Reporting Services &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md).  
  
### <a name="working-with-page-headers-and-footers-in-excel"></a>Trabajar con encabezados y pies de página en Excel  
 Cuando defina encabezados y pies de página en informes destinados a la extensión de representación en Excel, siga estas instrucciones para lograr los mejores resultados:  
  
-   Utilice pies de página para mostrar números de página.  
  
-   Utilice encabezados de página para mostrar imágenes, títulos y otro texto. No ponga números de página en el encabezado.  
  
 En Excel, los pies de página tienen un diseño limitado. Si define un informe que incluya elementos complejos en el pie de página, este pie no se procesará de la forma esperada cuando se muestre el informe en Excel.  
  
 La extensión de representación en Excel puede albergar imágenes y la ubicación absoluta de elementos de informe complejos y simples en el encabezado de página. Un efecto secundario de admitir un diseño de encabezado de página más complejo es que se reduce la posibilidad de usar números de página calculados en el encabezado. En la extensión de representación en Excel, la configuración predeterminada hace que los números totales de páginas se calculen según el número de hojas de cálculo. Dependiendo de la forma en que defina el informe, se pueden producir números de página incorrectos. Por ejemplo, suponga que tiene un informe que representa una sola hoja de cálculo grande que se imprime en cuatro páginas. Si incluye la información de números de página en el encabezado, cada página impresa mostrará "Página 1 de 1" en el encabezado.  
  
 Un recuento de páginas más preciso se basa en páginas lógicas que guardan correlación con las dimensiones de una página impresa. En Excel, el pie de página utiliza números de página lógica de forma automática. Para colocar el recuento de páginas lógicas en el encabezado de página, debe configurar los valores de información de dispositivo para que utilice encabezados simples. Tenga en cuenta que, cuando utilice encabezados simples, eliminará la capacidad de administrar el diseño de informes complejos en la región del encabezado.  
  
 Para más información, vea [Exportar a Microsoft Excel &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-builder/exporting-to-microsoft-excel-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Vea también  
 [Incrustar una imagen en un informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/embed-an-image-in-a-report-report-builder-and-ssrs.md)   
 [Rectángulos y líneas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/rectangles-and-lines-report-builder-and-ssrs.md)  
  
  
