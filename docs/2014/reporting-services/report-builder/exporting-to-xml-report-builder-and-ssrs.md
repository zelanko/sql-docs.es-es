---
title: Exportar a XML (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 11d72068-2d97-495e-948f-12d1e8c1957d
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 11bb46bc593a95811c56a5489fd5489ca72ca917
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37223275"
---
# <a name="exporting-to-xml-report-builder-and-ssrs"></a>Exportar a XML (Generador de informes y SSRS)
  La extensión de presentación en XML devuelve un informe en formato XML. El esquema XML del informe es específico de éste y solamente contiene datos. La extensión de representación en XML no representa la información de diseño ni mantiene la paginación. El XML que genera esta extensión se puede importar a una base de datos, se puede usar como mensaje de datos XML o se puede enviar a una aplicación personalizada.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="ReportItems"></a> Elementos de informe  
 En la tabla siguiente se describe cómo se representan los elementos de informe.  
  
|Elemento|Comportamiento de la representación|  
|----------|------------------------|  
|Informe|Se representa como el elemento de nivel superior del documento XML.|  
|Regiones de datos|Se representa como un elemento dentro del elemento de su contenedor. Entre las regiones de datos se incluyen la tabla, la matriz y la lista que muestran los datos en forma de texto y de gráficos, las barras de datos, los minigráficos, los medidores y los indicadores que visualizan los datos.|  
|Secciones de grupo y de detalles|Cada instancia se representa como un elemento dentro del elemento de su contenedor.|  
|Cuadro de texto|Se representa como un atributo o elemento dentro de su contenedor.|  
|Rectángulo|Se representa como un elemento dentro de su contenedor.|  
|Grupos de columnas de matriz|Se representan como elementos dentro de grupos de filas.|  
|Mapa|Se representa como un elemento dentro del elemento de su contenedor. Las capas de mapa son elementos secundarios del mapa. Cada capa de mapa incluye los elementos y los atributos de los miembros del mapa.|  
|Gráfico|Se representa como un elemento dentro del elemento de su contenedor. Las series son elementos secundarios del gráfico y las categorías son los elementos secundarios de una serie. Representa todas las etiquetas de gráfico de cada valor de gráfico. Las etiquetas y los valores se incluyen como atributos.|  
|Barra de datos|Se representan como un elemento dentro del elemento de su contenedor, de forma similar a un gráfico. Normalmente, una barra de datos no incluye jerarquías o etiquetas, solo valores.|  
|Minigráfico|Se representan como un elemento dentro del elemento de su contenedor, de forma similar a un gráfico. Normalmente, un minigráfico no incluye jerarquías ni etiquetas, solo valores.|  
|Medidor|Se representa como un elemento dentro del elemento de su contenedor. Se representa como un único elemento con los valores máximo y mínimo de la escala, los valores inicial y final del intervalo, y el valor del puntero como atributos.|  
|Indicador|Se representa como un elemento dentro del elemento de su contenedor, de forma similar a un medidor. Se representa como un único elemento con el nombre del estado activo, los estados disponibles y el valor de los datos como atributos.|  
  
 Los informes que se representan con la extensión de representación en XML también siguen estas reglas:  
  
-   Los elementos y atributos XML se representan en el orden en que aparecen en la definición de informe.  
  
-   No se tiene en cuenta la paginación.  
  
-   No se representan los encabezados y pies de página.  
  
-   No se representan los elementos ocultos que no se pueden mostrar mediante alternancia. Inicialmente, se representan los elementos visibles y los elementos ocultos que se pueden mostrar mediante un control de alternancia.  
  
-   Se omiten `Images, lines, and custom report items`.  
  
 ![Icono de flecha usado con el vínculo Volver al principio](../../2014-toc/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio")[Volver al principio](#BackToTop)  
  
##  <a name="DataTypes"></a> Tipos de datos  
 Al elemento o atributo del cuadro de texto se le asigna un tipo de datos XSD según los valores que muestra el cuadro de texto.  
  
|Si todos los valores del cuadro de texto son|El tipo de datos asignado es|  
|--------------------------------|---------------------------|  
|`Int16`, `Int32`, `Int64`, `UInt16`, `UInt32`, `UInt64`, `Byte`, `SByte`|**xsd:integer**|  
|`Decimal` (o `Decimal` y cualquier tipo de datos integer o byte)|**xsd:decimal**|  
|`Float` (o `Decimal` y cualquier tipo de datos integer o byte)|**xsd:float**|  
|`Double` (o `Decimal` y cualquier tipo de datos integer o byte)|**xsd:double**|  
|`DateTime or DateTime Offset`|**xsd:dateTime**|  
|`Time`|**xsd:cadena**|  
|`Boolean`|**xsd:boolean**|  
|`String`, `Char`|**xsd:cadena**|  
|Otros|**xsd:cadena**|  
  
 ![Icono de flecha usado con el vínculo Volver al principio](../../2014-toc/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio")[Volver al principio](#BackToTop)  
  
##  <a name="XMLSpecificRenderingRules"></a> Reglas de representación específicas de XML  
 En las secciones siguientes se describe cómo interpreta los elementos del informe la extensión de representación en XML.  
  
### <a name="report-body"></a>Cuerpo del informe  
 Un informe se representa como el elemento raíz del documento XML. El nombre del elemento procede del conjunto de propiedades DataElementName del panel Propiedades.  
  
 Las definiciones del espacio de nombres y los atributos de referencia del esquema XML también se incluyen en el elemento de informe. Las variables se indican en negrita:  
  
 \<**Informe** xmlns = "**SchemaName**" xmlns: xsi = "http://www.w3.org/2001/XMLSchema-instance" xsi:**schemaLocation**= "**SchemaNameReportURL**&amp;3aSchema rc % = True"nombre ="ReportName">  
  
 Los valores de las variables son los siguientes:  
  
|Nombre|Valor|  
|----------|-----------|  
|Informe|Report.DataElementName|  
|ReportURL|Dirección URL absoluta con codificación URL al informe en el servidor.|  
|SchemaName|Report.SchemaName. Si es NULL, Report.Name. Si se usa Report.Name, primero se codifica con XmlConvert.EncodeLocalName.|  
|ReportName|Nombre del informe.|  
  
### <a name="text-boxes"></a>Cuadros de texto  
 Los cuadros de texto se representan como elementos o atributos según la propiedad RDL DataElementStyle. El nombre del elemento o atributo procede de la propiedad RDL TextBox.DataElementName.  
  
### <a name="charts-data-bars-and-sparklines"></a>Gráficos, barras de datos y minigráficos  
 Los gráficos, las barras de datos y los minigráficos se representan en XML. Los datos son estructurados.  
  
### <a name="gauges-and-indicators"></a>Medidores e indicadores  
 Los medidores y los indicadores se representan en XML. Los datos son estructurados.  
  
### <a name="subreports"></a>Subinformes  
 Los subinformes se representan como elementos. El nombre del elemento se toma de la propiedad RDL DataElementName. El valor de la propiedad TextBoxesAsElements del informe invalida el valor correspondiente del subinforme. Los atributos de espacio de nombres y XSLT no se agregan al elemento de subinforme.  
  
### <a name="rectangles"></a>Rectángulos  
 Los rectángulos se representan como elementos. El nombre del elemento se toma de la propiedad RDL DataElementName.  
  
### <a name="custom-report-items"></a>Elementos de informe personalizados  
 Los CustomReportItems (CRI) no son visibles para la extensión de representación. Si existe algún elemento de informe personalizado en el informe, la extensión de representación lo representa como un elemento de informe convencional.  
  
### <a name="images"></a>Imágenes  
 Las imágenes no se representan.  
  
### <a name="lines"></a>Líneas  
 Las líneas no se representan.  
  
 ![Icono de flecha usado con el vínculo Volver al principio](../../2014-toc/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio")[Volver al principio](#BackToTop)  
  
### <a name="tables-matrices-and-lists"></a>Tablas, matrices y listas  
 Las tablas, matrices y listas se representan como un elemento. El nombre del elemento procede de la propiedad RDL DataElementName de Tablix.  
  
#### <a name="rows-and-columns"></a>Filas y columnas  
 Las columnas se representan dentro de las filas.  
  
#### <a name="tablix-corner"></a>Esquina de Tablix  
 La esquina no se representa. Solo se representa el contenido de la esquina.  
  
#### <a name="tablix-cells"></a>Celdas de Tablix  
 Las celdas de Tablix se representan como elementos. El nombre del elemento se toma de la propiedad RDL DataElementName de la celda.  
  
#### <a name="automatic-subtotals"></a>Subtotales automáticos  
 Los subtotales automáticos de Tablix no se representan.  
  
#### <a name="row-and-column-items-that-do-not-repeat-with-a-group"></a>Elementos de fila y de columna que no se repiten con un grupo  
 Los elementos que no repiten con un grupo, como las etiquetas, los subtotales y los totales, se representan como elementos. El nombre del elemento procede de la propiedad RDL TablixMember.DataElementName.  
  
 La propiedad RDL TablixMember.DataElementOutput controla si se representa un elemento no repetitivo.  
  
 Si no se proporciona la propiedad DataElementName del miembro de Tablix, se genera dinámicamente un nombre para el elemento no repetitivo en este formato:  
  
 RowX: para las filas no repetitivas, donde X es un índice de fila de base cero dentro del elemento primario actual.  
  
 ColumnY: para las columnas no repetitivas, donde Y es un índice de columna de base cero dentro del elemento primario actual.  
  
 Un encabezado no repetitivo se representa como un elemento secundario de la fila o la columna que no se repite dentro de un grupo.  
  
 Si un miembro no repetitivo no tiene ninguna celda de Tablix correspondiente, no se representa. Esto puede ocurrir en el caso de una celda de Tablix que abarca más de una columna.  
  
#### <a name="rows-and-columns-that-repeat-with-a-group"></a>Filas y columnas que se repiten dentro de un grupo  
 Las filas y las columnas que se repiten dentro de un grupo se representan según las reglas Tablix.DataElementOutput. El nombre del elemento se toma de la propiedad DataElementName.  
  
 Cada valor único dentro de un grupo se representa como un elemento secundario del grupo. El nombre del elemento se toma de la propiedad Group.DataElementName.  
  
 Si el valor de la propiedad DataElementOutput es igual al de la salida, el encabezado de un elemento repetitivo se representa como un elemento secundario del elemento de detalle.  
  
 ![Icono de flecha usado con el vínculo Volver al principio](../../2014-toc/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio")[Volver al principio](#BackToTop)  
  
##  <a name="CustomFormatsXSLTransformations"></a> Formatos personalizados y transformaciones XSL  
 Los archivos XML generados por la extensión de representación en XML se pueden transformar prácticamente a cualquier formato mediante las transformaciones XSL (XSLT). Esta funcionalidad se puede usar para generar datos en formatos todavía no admitidos por las extensiones de representación existentes. Se recomienda utilizar la extensión de representación en XML y XSLT antes de intentar crear una extensión de representación propia.  
  
 ![Icono de flecha usado con el vínculo Volver al principio](../../2014-toc/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio")[Volver al principio](#BackToTop)  
  
##  <a name="DuplicateName"></a> Nombres duplicados  
 Si hay nombres de elementos de datos duplicados dentro del mismo ámbito, el representador muestra un mensaje de error.  
  
 ![Icono de flecha usado con el vínculo Volver al principio](../../2014-toc/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio")[Volver al principio](#BackToTop)  
  
##  <a name="XSLTTransformations"></a> Transformaciones XSLT  
 El representador de XML puede aplicar una transformación XSLT en el servidor a los datos XML originales. Cuando se aplica una XSLT, el representador genera el contenido transformado en lugar de los datos XML originales. La transformación se produce en el servidor, no en el cliente.  
  
 La transformación XSLT que se debe aplicar a la salida se define en el archivo de definición de informe con la propiedad DataTransform del informe o con el parámetro *DeviceInfo* de XSLT. Si se establece cualquiera de estos valores, la transformación se produce cada vez que se usa el representador de XML. Cuando se usan suscripciones, la transformación XSLT se debe definir en la propiedad RDL DataTransform.  
  
 Si se especifica un archivo XSLT, tanto con la propiedad de definición DataTransform como con la configuración de la información del dispositivo, primero se produce la transformación XSLT especificada en DataTransform y después la establecida mediante la configuración de la información del dispositivo.  
  
 ![Icono de flecha usado con el vínculo Volver al principio](../../2014-toc/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio")[Volver al principio](#BackToTop)  
  
###  <a name="DeviceInfo"></a> Configuración de la información del dispositivo  
 Puede cambiar parte de la configuración predeterminada de este representador cambiando valores de configuración de la información del dispositivo como los siguientes:  
  
-   La transformación (XSLT) que se aplicará al XML.  
  
-   El tipo MIME del documento XML.  
  
-   Si se van a aplicar cadenas de formato a los datos.  
  
-   Si se va a aplicar sangría a los resultados XML.  
  
-   Si se va a incluir el nombre del esquema XML.  
  
-   La codificación del documento XML.  
  
-   La extensión de archivo del documento XML.  
  
 Para obtener más información, vea [XML Device Information Settings](../xml-device-information-settings.md).  
  
 ![Icono de flecha usado con el vínculo Volver al principio](../../2014-toc/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio")[Volver al principio](#BackToTop)  
  
## <a name="see-also"></a>Vea también  
 [Paginación en Reporting Services &#40;Generador de informes y SSRS&#41;](../report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [Comportamientos de la representación &#40;Generador de informes y SSRS&#41;](../report-design/rendering-behaviors-report-builder-and-ssrs.md)   
 [Funcionalidad interactiva para diferentes extensiones de representación de informes &#40;generador de informes y SSRS&#41;](interactive-functionality-different-report-rendering-extensions.md)   
 [Representar elementos de informe &#40;Generador de informes y SSRS&#41;](../report-design/rendering-report-items-report-builder-and-ssrs.md)   
 [Tablas, matrices y listas &#40;Generador de informes y SSRS&#41;](../report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)  
  
  
