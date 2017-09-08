---
title: "Introducción a las extensiones de representación | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
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
- formats [Reporting Services], rendering extensions
- rendering extensions [Reporting Services], about extensions
ms.assetid: 909356a0-4709-43e5-b597-33bd9bb22882
caps.latest.revision: 41
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: bf4ef7421e85e95d40a28803adec2c279b9a80bc
ms.contentlocale: es-es
ms.lasthandoff: 08/12/2017

---
# <a name="rendering-extensions-overview"></a>Información general de las extensiones de representación
  Una extensión de representación es un componente o módulo de un servidor de informes que transforma los datos de informes y la información de diseño en un formato específico del dispositivo. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] incluye siete extensiones de representación: HTML, Excel, Word, CSV o texto, XML, imagen y PDF. Puede crear extensiones de representación adicionales para generar informes en otros formatos.  
  
> [!NOTE]  
>  Para determinar qué extensiones de representación están disponibles, puede ver la lista de extensiones instaladas en el archivo RSReportServer.config.  
  
 En la tabla siguiente se describen las extensiones de representación que se incluyen con [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].  
  
|Extension Name|Description|  
|--------------------|-----------------|  
|**XML**|Representa un informe en XML. El informe se abre en un explorador. Las transformaciones adicionales aplicadas a esta salida XML pueden constituir una manera rentable de evitar desarrollar una extensión de representación propia.|  
|**CSV**|Representa un informe en formato delimitado por comas. El informe se abre en una herramienta de visualización asociada a los formatos de archivo CSV.|  
|**IMAGE**|Representa un informe en formato orientado a la página. El formato se muestra como **TIFF** en el cuadro desplegable Exportar de la barra de herramientas del informe.|  
|**PDF**|Representa un informe en Adobe Acrobat Reader. El formato se muestra como **Archivo de Acrobat (PDF)** en el cuadro desplegable Exportar de la barra de herramientas del informe.|  
|**EXCEL**|Representa un informe en [!INCLUDE[ofprexcel](../../../includes/ofprexcel-md.md)].|  
|**WORD**|Representar un informe en [!INCLUDE[ofprword](../../../includes/ofprword-md.md)].|  
|**HTML 4.0** (forma parte de la extensión de representación HTML)|HTML es el formato que se usó inicialmente para representar el informe. Si el explorador admite HTML 4.0, ése es el formato que se utiliza. De lo contrario, se utiliza HTML 3.2.|  
|**MHTML** (forma parte de la extensión de representación HTML)|Representa un informe en MHTML. El informe se abre en Internet Explorer. El formato se muestra como **Archivo web** en el cuadro desplegable Exportar de la barra de herramientas del informe.|  
|**NULL**|No representa un informe en un formato concreto. Esta extensión de representación es útil para colocar los informes en la memoria caché. La representación NULL se debería utilizar junto con una ejecución o entrega programada.|  
  
 Para obtener más información sobre los formatos recomendados y sus usos, vea [exportar informes &#40; El generador de informes y SSRS &#41; ](../../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md).  
  
 Cada una de las extensiones de representación que se implementan mediante [!INCLUDE[msCoName](../../../includes/msconame-md.md)] y se distribuyen con [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] usa un conjunto común de interfaces. De este modo se asegura de que cada extensión implementa una funcionalidad comparable y reduce la complejidad del código de la representación en el núcleo del servidor de informes.  
  
## <a name="rendering-object-model"></a>Modelo de objetos de representación  
 Cuando se procesa un informe, el resultado es un modelo de objetos expuesto públicamente conocido como Modelo de objetos de representación (ROM). El Modelo de objetos de representación es una colección de clases que definen el contenido, diseño y datos de un informe que se ha procesado. El ROM está disponible para los programadores que desean diseñar, desarrollar e implementar las extensiones de representación personalizadas para [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. ROM se genera cuando el servidor de informes procesa la definición XML de un informe junto con los datos del mismo definidos por el usuario. Cuando el procesamiento se completa, una extensión de representación utiliza el modelo de objetos público para definir la salida del informe. Las clases públicas disponibles del ROM se definen en el **Microsoft.ReportingServices.OnDemandReportRendering** espacio de nombres.  
  
## <a name="writing-custom-rendering-extensions"></a>Escribir extensiones de representación personalizadas  
 Antes de decidir crear una extensión de representación personalizada, debería evaluar alternativas más simples. Puede hacer lo siguiente:  
  
-   Personalizar la salida representada especificando la configuración de la información de los dispositivos para las extensiones existentes.  
  
-   Agregar formato personalizado y características de presentación combinando Transformaciones XSL (XSLT) con la salida del formato de representación XML.  
  
 Escribir una extensión de representación personalizada es difícil. Normalmente, debe admitir todas las combinaciones posibles de elementos de informe y requiere que implemente centenares de clases, interfaces, métodos y propiedades. Si debe representar un informe en un formato que no se incluye con [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] y decide escribir su propia implementación de código administrado de una extensión de representación, el código de extensión de representación debe implementar la **Microsoft.ReportingServices.OnDemandReportRendering.IRenderingExtension** interfaz, y es necesario para el servidor de informes.  
  
 Para obtener documentación complementaria y notas del producto en [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], vea los recursos técnicos más recientes en el [sitio web de Reporting Services](http://go.microsoft.com/fwlink/?LinkId=19951).  
  
## <a name="see-also"></a>Vea también  
 [Implementar una extensión de representación](../../../reporting-services/extensions/rendering-extension/implementing-a-rendering-extension.md)   
 [Biblioteca de extensión de Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
