---
title: Exportar a un archivo de imagen (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 020d8ea2-de07-4212-a2bb-2ed0df2c8db8
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: fd3a6e7126775479ae7ca0c6b6d138a0625476af
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66107888"
---
# <a name="exporting-to-an-image-file-report-builder-and-ssrs"></a>Exportar a un archivo de imagen (Generador de informes y SSRS)
  La extensión de presentación en imágenes presenta un informe en un mapa de bits o metarchivo. De manera predeterminada, una extensión de representación en imágenes genera un archivo TIFF del informe, que se puede ver en varias páginas. Cuando el cliente recibe la imagen, se puede mostrar en un visor de imágenes y se puede imprimir. En este tema se proporciona información específica del representador de imágenes y se describen las excepciones a las reglas de representación.  
  
 La extensión de presentación en imágenes puede generar archivos en cualquiera de los formatos que admite [!INCLUDE[ndptecgdiplus](../../includes/ndptecgdiplus-md.md)]: BMP, EMF, EMFPlus, GIF, JPEG, PNG y TIFF. En el caso del formato TIFF, el nombre de archivo del flujo principal es *ReportName*.tif. Para los demás formatos, que se representan como una única página por archivo, el nombre del archivo es *ReportName_Page.ext* donde. *ext* es la extensión de archivo correspondiente al formato elegido. Para generar un archivo en otro formato admitido por Imagen, especifique cualquiera de las cadenas anteriores en el parámetro **OutputFormatDeviceInfo** .  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="SupportedImageFormats"></a> Formatos de imagen admitidos  
 En la tabla siguiente se muestra la extensión de archivo y el elemento MimeType para cada formato de representador de imágenes.  
  
|**Tipo**|**Extensión**|**MIMEType**|  
|--------------|-------------------|------------------|  
|BMP|BMP|image/bmp|  
|GIF|GIF|image/gif|  
|JPEG|JPEG|image/jpeg|  
|PNG|png|image/png|  
|TIFF|tif|image/tiff|  
|EMF|EMF|image/emf|  
|EMFPlus|EMF|image/emf|  
  
  
##  <a name="RenderingMultiplePages"></a> Representar varias páginas  
 TIFF es el único formato que admite varios documentos de página en un único archivo. Otros formatos, como JPG o PNG, generan las páginas de una en una y requieren una llamada independiente a la extensión de representación para cada página.  
  
  
##  <a name="Interactivity"></a> Interactividad  
 Ninguno de los formatos de imagen generados por este representador admite la interactividad. No se representan los elementos interactivos siguientes:  
  
-   Hipervínculos  
  
-   Mostrar u ocultar  
  
-   Mapa del documento  
  
-   Vínculos de obtención de detalles o vínculos click-through  
  
-   Ordenación de usuarios finales  
  
-   Encabezados fijos  
  
-   Marcadores  
  
  
##  <a name="DeviceInfo"></a> Configuración de la información del dispositivo  
 Puede cambiar parte de la configuración predeterminada de este representador cambiando los valores de configuración de la información del dispositivo. Para obtener más información, vea [Image Device Information Settings](../image-device-information-settings.md).  
  
  
## <a name="see-also"></a>Consulte también  
 [Paginación en Reporting Services &#40;Generador de informes y SSRS&#41;](../report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [Comportamientos de la representación &#40;Generador de informes y SSRS&#41;](../report-design/rendering-behaviors-report-builder-and-ssrs.md)   
 [Funcionalidad interactiva para diferentes extensiones de representación de informes &#40;Generador de informes y SSRS&#41;](interactive-functionality-different-report-rendering-extensions.md)   
 [Representar elementos de informe &#40;Generador de informes y SSRS&#41;](../report-design/rendering-report-items-report-builder-and-ssrs.md)   
 [Tablas, matrices y listas &#40;Generador de informes y SSRS&#41;](../report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)  
  
  
