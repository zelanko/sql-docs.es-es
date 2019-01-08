---
title: Bibliotecas de clases de elemento de informe personalizado | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- custom report items, RDL
- RDL [Reporting Services], custom report items
ms.assetid: f18c5d8f-1d6b-4f0b-8657-c14896c2ce0d
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: e65ae16a2297c0f54f16e31e770623c8edd80639
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/13/2018
ms.locfileid: "53376807"
---
# <a name="custom-report-item-class-libraries"></a>Bibliotecas de clases de elemento de informe personalizado
  Los elementos de informe personalizados utilizan las clases del espacio de nombres `Microsoft.ReportDesigner`. Las clases utilizadas para implementar un elemento de informe personalizado pueden estar agrupadas en dos categorías principales: las clases únicas diseñadas para admitir la infraestructura del elemento de informe personalizado y las clases contenedora administradas que encapsulan la funcionalidad de los elementos del lenguaje RDL (Report Definition Language) pertinentes. Para obtener un ejemplo de código que ilustre cómo se usan estas clases, vea [Muestras de productos de SQL Server Reporting Services](https://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="custom-report-item-infrastructure-classes"></a>Clases de infraestructura del elemento de informe personalizado  
 Las clases siguientes se utilizan para implementar un elemento de informe personalizado.  
  
> [!NOTE]  
>  Las tablas siguientes no constituyen listas completas; incluyen solo las propiedades utilizadas de forma más habitual y los métodos para cada clase.  
  
### <a name="microsoftreportdesignercustomreportitemdesigner"></a>Microsoft.ReportDesigner.CustomReportItemDesigner  
 Ésta es la clase del elemento de informe personalizado principal. La clase principal de la implementación del elemento de informe personalizado debe heredar de esta clase.  
  
#### <a name="public-properties"></a>Propiedades públicas  
  
|||  
|-|-|  
|`Name`|El nombre del elemento de informe personalizado.|  
|`Type`|El tipo del elemento de informe personalizado.|  
|`CustomData`|Un objeto <xref:Microsoft.ReportingServices.RdlObjectModel.CustomData> que encapsula las propiedades de datos del elemento de informe personalizado especificado en el momento del diseño.|  
|`CustomProperties`|Una colección de propiedades personalizadas para el elemento de informe personalizado.|  
|`Height`|El alto del control de elemento de informe personalizado.|  
|`Width`|El ancho del control de elemento de informe personalizado.|  
|`Report`|Un contenedor para las propiedades del nivel de informe, como la lista de conjuntos de datos en el informe.|  
|`AltReportItem`|El objeto de elemento de informe alternativo que se utilizará cuando no se admita el control en tiempo de ejecución del elemento de informe personalizado.|  
|`Style`|Las propiedades de estilo del elemento de informe personalizado.|  
|`Adornment`|Una ventana de elementos gráficos utilizada para la edición interactiva del control.|  
|`Site`|El `ISite` del componente.|  
|`DesignerVerbCollection`|Una matriz de verbos personalizados para el menú contextual del control.|  
  
#### <a name="public-methods"></a>Métodos públicos  
  
|||  
|-|-|  
|`BeginEdit`|Activa la edición interactiva para el control.|  
|`DoDefaultAction`|Se le llama al hacer doble clic o al presionar Retorno en el control.|  
|`EndEdit`|Desactiva la edición interactiva para el control.|  
|`GetService`|Devuelve un objeto que representa un servicio.|  
|`InitializeNewComponent`|Se llama cuando se crea un nuevo elemento de informe personalizado.|  
|`Invalidate`|Vuelve a dibujar toda la superficie del control.|  
|`OnDragEnter`<br /><br /> `OnDragDrop`|Se llama al arrastrar un objeto al control.|  
|`OnPaint`|Se le llama como respuesta al evento `Paint`.|  
  
### <a name="microsoftreportdesignercustomreportitemattribute"></a>Microsoft.ReportDesigner.CustomReportItemAttribute  
 Este es el atributo utilizado para identificar el tipo del elemento de informe personalizado. El nombre debe coincidir con el valor del atributo <`Name`> del elemento `ReportItem` en el archivo de configuración del diseñador de informes.  
  
#### <a name="public-methods"></a>Métodos públicos  
  
|||  
|-|-|  
|`CustomReportItemAttribute`|Construye el objeto CustomReportItemAttribute.|  
  
### <a name="microsoftreportdesignerlocalizednameattribute"></a>Microsoft.ReportDesigner.LocalizedNameAttribute  
 Este es el atributo que se utiliza para especificar el nombre para mostrar que debe usarse con el diseñador de elementos de informe personalizados.  
  
#### <a name="public-methods"></a>Métodos públicos  
  
|||  
|-|-|  
|`LocalizedNameAttribute`|Construye el objeto LocalizedNameAttribute.|  
  
### <a name="microsoftreportdesigneradornment"></a>Microsoft.ReportDesigner.Adornment  
 El componente de tiempo de diseño del elemento de informe personalizado utiliza la clase `Adornment` para proporcionar áreas fuera del rectángulo principal de la superficie de diseño. Estas áreas pueden administrar los eventos de interfaz de usuario, como los clics del mouse y las operaciones de arrastrar y colocar.  
  
#### <a name="public-methods"></a>Métodos públicos  
  
|||  
|-|-|  
|`OnShow`|Se llama cuando `Adornment` está activado.|  
|`OnHide`|Se llama cuando `Adornment` está desactivado.|  
|`Paint`|Se le llama como respuesta al evento `Paint`.|  
|`OnDragEnter`<br /><br /> `OnDragOver`<br /><br /> `OnDragLeave`<br /><br /> `OnDragDrop`|Se le llama cuando se arrastra un objeto a `Adornment`.|  
  
### <a name="microsoftreportdesigneradornerservice"></a>Microsoft.ReportDesigner.AdornerService  
 Esta clase se utiliza para proporcionar una colección de servicios de presentación utilizada por el elemento de informe personalizado para admitir los objetos `Adornment` para el componente en tiempo de diseño del elemento de informe personalizado.  
  
#### <a name="public-properties"></a>Propiedades públicas  
  
|||  
|-|-|  
|`AdornerWindowBounds`|Los límites de la ventana de adorno.|  
|`AdornerWindowRegion`|La región de la ventana de adorno.|  
|`AdornerWindowGraphics`|Un contexto gráfico para la ventana de adorno.|  
  
#### <a name="public-methods"></a>Métodos públicos  
  
|||  
|-|-|  
|`ComponentRectInDesignerFrame`|Devuelve los límites del componente traducidos en coordenadas de marco de diseñador.|  
|`InvalidateAdorner`|Invalida la ventana de adorno.|  
|`PointToAdorner`|Devuelve un punto en coordenadas de pantalla traducido en las coordenadas de ventana de adorno.|  
  
### <a name="microsoftreportdesignerexpressioneditor"></a>Microsoft.ReportDesigner.ExpressionEditor  
 Esta clase se puede utilizar desde el control en tiempo de diseño del elemento de informe personalizado para invocar el editor de expresiones.  
  
#### <a name="public-methods"></a>Métodos públicos  
  
|||  
|-|-|  
|`EditValue`|Invoca el editor de expresiones, inicializado con el valor del objeto determinado.|  
  
### <a name="microsoftreportdesignerifieldsdataobject"></a>Microsoft.ReportDesigner.IFieldsDataObject  
 Esta clase es una colección de campos [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y se utiliza para admitir los eventos arrastrar y colocar en el entorno de diseño. Hereda de `IReportItemDataObject`.  
  
#### <a name="public-properties"></a>Propiedades públicas  
  
|||  
|-|-|  
|`DataSetName`|El nombre del conjunto de datos que contiene los campos que se van a quitar.|  
|`Fields`|La colección de campos (`Microsoft.ReportDesigner.Field`) que se va a quitar.|  
  
## <a name="see-also"></a>Vea también  
 [Lenguaje RDL (Report Definition Language) &#40;SSRS&#41;](../reports/report-definition-language-ssrs.md)   
 [Creación de un componente de tiempo de ejecución de elemento de informe personalizado](creating-a-custom-report-item-run-time-component.md)   
 [Creación de un componente de tiempo de diseño de elemento de informe personalizado](creating-a-custom-report-item-design-time-component.md)  
  
  
