---
title: Imprimir informes (SSRS) | Microsoft Docs
ms.date: 05/24/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-builder
ms.topic: conceptual
ms.assetid: 4bad1b6e-7d94-4b17-9502-ccd3dce0fdd9
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 45b38940afcd0fe73ad2c79abc59db9dc7b549b3
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 05/14/2019
ms.locfileid: "65581157"
---
# <a name="print-reports---reporting-services-ssrs"></a>Imprimir informes: Reporting Services (SSRS)
  Después de guardar un informe en un servidor de informes, puede verlo e imprimirlo desde el portal web o cualquier aplicación que use para ver un informe exportado. Antes de guardar un informe, puede imprimirlo desde su vista previa.  
  
 Topo el procesamiento de impresión se realiza a petición y en el equipo cliente. No existe ninguna funcionalidad de impresión del servidor que le permita enrutar un trabajo de impresión directamente desde un servidor de informes a una impresora conectada al servidor web. Los usuarios de cada uno de los informes se encargan de seleccionar las impresoras y las opciones de impresión con la ayuda del cuadro de diálogo estándar **Imprimir** .  
  
 Los creadores de informes que diseñan informes específicamente para su impresión pueden utilizar saltos de página, encabezados y pies de página, expresiones e imágenes de fondo para crear un diseño basado en la impresión. Algunos ejemplos de elementos de diseño de informes destinados a la impresión son los términos y condiciones que imprime en la parte posterior de cada informe, o elementos gráficos y de texto que son un reflejo del membrete.  
  
 Debido al modo en que se implementa la paginación para los distintos formatos de representación, es posible que no pueda lograr unos resultados de impresión óptimos con cada uno de los informes en los distintos formatos de representación. La siguiente lista proporciona ejemplos:  
  
1.  Las páginas de los informes están diseñadas para albergar cantidades variables de datos. Por ejemplo, los informes que incluyen una matriz pueden ocasionar que una página aumente de manera horizontal y vertical en función de si un usuario alterna de forma interactiva filas y columnas. Un usuario que no expanda una matriz obtendrá unos resultados de impresión diferentes de los de otro usuario que sí la expanda.  
  
2.  No puede combinar páginas en modo horizontal y vertical en el mismo informe, ni hay ningún medio para crear un diseño basado en la impresión que reemplace o coexista con el diseño de un informe tal como se representa en un explorador o en otra aplicación.  
  
3.  En la mayoría de los informes exportados, las copias impresas de los informes incluyen todo lo que es visible en el informe, tal y como lo ve el usuario en el monitor de un equipo. Se conserva el espacio en blanco de la superficie de diseño del informe. Para agregar o quitar páginas en blanco adicionales en formato horizontal, cambie el ancho de página del informe.  
  
> [!NOTE]  
>  Si utiliza el comando Imprimir del explorador, es probable que las copias impresas de los informes HTML solo incluyan el contenido de la primera página. Es posible obtener mejores resultados en la impresión de informes HTML usando la funcionalidad de impresión del cliente de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para obtener más información, vea [Imprimir informes desde un explorador usando el control de impresión &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-builder/print-reports-from-a-browser-with-the-print-control-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="in-this-section"></a>En esta sección  
 [Imprimir informes desde un explorador usando el control de impresión &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-builder/print-reports-from-a-browser-with-the-print-control-report-builder-and-ssrs.md)  
 Describe cómo usar la impresión del lado cliente para imprimir informes desde el portal web.  
  
 [Imprimir informes desde otras aplicaciones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-builder/print-reports-from-other-applications-report-builder-and-ssrs.md)  
 Describe cómo imprimir informes exportados a otra aplicación.  
  
 [Imprimir un informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-builder/print-a-report-report-builder-and-ssrs.md)  
 Proporciona instrucciones paso a paso sobre cómo imprimir informes, cómo controlar los márgenes de una página y cómo especificar el tamaño del papel para los informes que se representarán mediante representadores de saltos de página manuales: PDF, Image o Print.  
  
## <a name="see-also"></a>Consulte también  
 [Exportación de informes &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)   
 [Encabezados y pies de página &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/page-headers-and-footers-report-builder-and-ssrs.md)   
 [Imágenes &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/images-report-builder-and-ssrs.md)   
 [Paginación en Reporting Services &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)  
  
  
