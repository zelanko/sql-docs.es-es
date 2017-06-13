---
title: Bibliotecas de clases de elemento de informe personalizado | Documentos de Microsoft
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- custom report items, RDL
- RDL [Reporting Services], custom report items
ms.assetid: f18c5d8f-1d6b-4f0b-8657-c14896c2ce0d
caps.latest.revision: 27
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: f216228c01e835e88cd9d4c7d7d4190648a386db
ms.contentlocale: es-es
ms.lasthandoff: 06/13/2017

---
# <a name="custom-report-item-class-libraries"></a>Bibliotecas de clases de elemento de informe personalizado
  Elementos de informe personalizados usan las clases de la **Microsoft.ReportDesigner** espacio de nombres. Las clases utilizadas para implementar un elemento de informe personalizado pueden estar agrupadas en dos categorías principales: las clases únicas diseñadas para admitir la infraestructura del elemento de informe personalizado y las clases contenedora administradas que encapsulan la funcionalidad de los elementos del lenguaje RDL (Report Definition Language) pertinentes. Para obtener un ejemplo de código sobre cómo utilizar estas clases, consulte [muestras de producto de SQL Server Reporting Services](http://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="custom-report-item-infrastructure-classes"></a>Clases de infraestructura del elemento de informe personalizado  
 Las clases siguientes se utilizan para implementar un elemento de informe personalizado.  
  
> [!NOTE]  
>  Las tablas siguientes no constituyen listas completas; incluyen solo las propiedades utilizadas de forma más habitual y los métodos para cada clase.  
  
### <a name="microsoftreportdesignercustomreportitemdesigner"></a>Microsoft.ReportDesigner.CustomReportItemDesigner  
 Ésta es la clase del elemento de informe personalizado principal. La clase principal de la implementación del elemento de informe personalizado debe heredar de esta clase.  
  
#### <a name="public-properties"></a>Propiedades públicas  
  
|||  
|-|-|  
|**Nombre**|El nombre del elemento de informe personalizado.|  
|**Tipo**|El tipo del elemento de informe personalizado.|  
|**CustomData**|Un objeto <xref:Microsoft.ReportingServices.RdlObjectModel.CustomData> que encapsula las propiedades de datos del elemento de informe personalizado especificado en el momento del diseño.|  
|**CustomProperties**|Una colección de propiedades personalizadas para el elemento de informe personalizado.|  
|**Alto**|El alto del control de elemento de informe personalizado.|  
|**Ancho**|El ancho del control de elemento de informe personalizado.|  
|**Informe**|Un contenedor para las propiedades del nivel de informe, como la lista de conjuntos de datos en el informe.|  
|**AltReportItem**|El objeto de elemento de informe alternativo que se utilizará cuando no se admita el control en tiempo de ejecución del elemento de informe personalizado.|  
|**Estilo**|Las propiedades de estilo del elemento de informe personalizado.|  
|**Elementos gráficos**|Una ventana de elementos gráficos utilizada para la edición interactiva del control.|  
|**Sitio**|El **ISite** del componente.|  
|**Clase DesignerVerbCollection**|Una matriz de verbos personalizados para el menú contextual del control.|  
  
#### <a name="public-methods"></a>Métodos públicos  
  
|||  
|-|-|  
|**BeginEdit**|Activa la edición interactiva para el control.|  
|**DoDefaultAction**|Se le llama al hacer doble clic o al presionar Retorno en el control.|  
|**EndEdit**|Desactiva la edición interactiva para el control.|  
|**GetService**|Devuelve un objeto que representa un servicio.|  
|**InitializeNewComponent**|Se llama cuando se crea un nuevo elemento de informe personalizado.|  
|**Invalidar**|Vuelve a dibujar toda la superficie del control.|  
|**OnDragEnter**<br /><br /> **OnDragDrop**|Se llama al arrastrar un objeto al control.|  
|**OnPaint**|Llama en respuesta a la **Paint** eventos.|  
  
### <a name="microsoftreportdesignercustomreportitemattribute"></a>Microsoft.ReportDesigner.CustomReportItemAttribute  
 Este es el atributo utilizado para identificar el tipo del elemento de informe personalizado. El nombre debe coincidir con el valor de la \< **nombre**> atributo de la **ReportItem** elemento en el archivo de configuración del Diseñador de informes.  
  
#### <a name="public-methods"></a>Métodos públicos  
  
|||  
|-|-|  
|**CustomReportItemAttribute**|Construye el objeto CustomReportItemAttribute.|  
  
### <a name="microsoftreportdesignerlocalizednameattribute"></a>Microsoft.ReportDesigner.LocalizedNameAttribute  
 Este es el atributo que se utiliza para especificar el nombre para mostrar que debe usarse con el diseñador de elementos de informe personalizados.  
  
#### <a name="public-methods"></a>Métodos públicos  
  
|||  
|-|-|  
|**LocalizedNameAttribute**|Construye el objeto LocalizedNameAttribute.|  
  
### <a name="microsoftreportdesigneradornment"></a>Microsoft.ReportDesigner.Adornment  
 El **elementos gráficos** clase es usada por el componente de tiempo de diseño de elemento de informe personalizado para proporcionar áreas fuera del rectángulo principal de la superficie de diseño. Estas áreas pueden administrar los eventos de interfaz de usuario, como los clics del mouse y las operaciones de arrastrar y colocar.  
  
#### <a name="public-methods"></a>Métodos públicos  
  
|||  
|-|-|  
|**OnShow**|Llamado cuando el **elementos gráficos** está activado.|  
|**OnHide**|Llamado cuando el **elementos gráficos** está desactivada.|  
|**Paint**|Llama en respuesta a la **Paint** eventos.|  
|**OnDragEnter**<br /><br /> **OnDragOver**<br /><br /> **OnDragLeave**<br /><br /> **OnDragDrop**|Se llama cuando se arrastra un objeto en el **elementos gráficos**.|  
  
### <a name="microsoftreportdesigneradornerservice"></a>Microsoft.ReportDesigner.AdornerService  
 Esta clase se utiliza para proporcionar una colección de servicios de presentación utilizada por el elemento de informe personalizado para admitir **elementos gráficos** objetos para el componente de tiempo de diseño de elemento de informe personalizado.  
  
#### <a name="public-properties"></a>Propiedades públicas  
  
|||  
|-|-|  
|**AdornerWindowBounds**|Los límites de la ventana de adorno.|  
|**AdornerWindowRegion**|La región de la ventana de adorno.|  
|**AdornerWindowGraphics**|Un contexto gráfico para la ventana de adorno.|  
  
#### <a name="public-methods"></a>Métodos públicos  
  
|||  
|-|-|  
|**ComponentRectInDesignerFrame**|Devuelve los límites del componente traducidos en coordenadas de marco de diseñador.|  
|**InvalidateAdorner**|Invalida la ventana de adorno.|  
|**PointToAdorner**|Devuelve un punto en coordenadas de pantalla traducido en las coordenadas de ventana de adorno.|  
  
### <a name="microsoftreportdesignerexpressioneditor"></a>Microsoft.ReportDesigner.ExpressionEditor  
 Esta clase se puede utilizar desde el control en tiempo de diseño del elemento de informe personalizado para invocar el editor de expresiones.  
  
#### <a name="public-methods"></a>Métodos públicos  
  
|||  
|-|-|  
|**EditValue**|Invoca el editor de expresiones, inicializado con el valor del objeto determinado.|  
  
### <a name="microsoftreportdesignerifieldsdataobject"></a>Microsoft.ReportDesigner.IFieldsDataObject  
 Esta clase es una colección de campos [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y se utiliza para admitir los eventos arrastrar y colocar en el entorno de diseño. Hereda de **IReportItemDataObject**.  
  
#### <a name="public-properties"></a>Propiedades públicas  
  
|||  
|-|-|  
|**DataSetName**|El nombre del conjunto de datos que contiene los campos que se van a quitar.|  
|**Campos**|La colección de campos (**Microsoft.ReportDesigner.Field**) va a quitar.|  
  
## <a name="see-also"></a>Vea también  
 [Lenguaje de definición de informe &#40; SSRS &#41;](../../reporting-services/reports/report-definition-language-ssrs.md)   
 [Crear un componente de tiempo de ejecución del elemento de informe personalizado](../../reporting-services/custom-report-items/creating-a-custom-report-item-run-time-component.md)   
 [Crear un componente de tiempo de diseño de elemento de informe personalizado](../../reporting-services/custom-report-items/creating-a-custom-report-item-design-time-component.md)  
  
  
