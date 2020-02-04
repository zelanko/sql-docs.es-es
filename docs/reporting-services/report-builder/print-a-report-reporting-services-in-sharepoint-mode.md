---
title: Imprimir un informe (Reporting Services en el modo de SharePoint) | Microsoft Docs
ms.date: 05/14/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-builder
ms.topic: conceptual
helpviewer_keywords:
- printing reports, SharePoint Web application
- printing reports
ms.assetid: 026784f7-8cb4-4351-93ee-230b2ab0f8f5
author: maggiesMSFT
ms.author: maggies
monikerRange: '>=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 407d20b06c6dccdb63f5455ffe24a3505d8bd823
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "65875210"
---
# <a name="print-a-report-reporting-services-in-sharepoint-mode"></a>Imprimir un informe (Reporting Services en el modo de SharePoint)
  Para un servidor de informes que se ejecuta en el modo integrado de SharePoint, existen tres formas de imprimir un informe desde una aplicación web de SharePoint:  
  
-   **Desde un sitio de SharePoint** Elija **Imprimir** en el menú **Acciones** que se muestra en la barra de tareas del informe al abrirlo. Esto proporciona a Reporting Services funcionalidad para imprimir, que incluye un cuadro de diálogo **Imprimir** estándar que se utiliza para seleccionar una impresora, especificar páginas y márgenes y obtener una vista previa del informe. Esta función de impresión está concebida para utilizarse en lugar del comando Imprimir del menú Archivo del explorador. Al imprimir de esta forma, el informe se imprime tal y como se diseñó, sin los elementos adicionales que se ven en la impresión de una página web.  
  
-   **Desde un explorador** Las funciones de impresión de un explorador funcionan mejor para los informes HTML que ocupan una sola página. Normalmente, las páginas que imprime desde un explorador incluyen todos los elementos visuales de una página web, además de la información del encabezado y del pie de página que identifica la página o el sitio web. Al imprimir desde un explorador, solo se imprime el contenido de la ventana actual. Si el informe es largo, el explorador solamente imprime una porción del mismo (normalmente solo la primera página).  
  
-   **Desde una aplicación de destino** Puede exportar un informe para utilizar las funciones de impresión de una aplicación de destino, como Microsoft Office Excel o Adobe Acrobat Reader. Algunos formatos de aplicación, como TIFF o PDF, son perfectos para imprimir informes de varias páginas. Al exportar un informe en una aplicación de escritorio, podrá utilizar cualquier función de impresión especializada que ofrezca la aplicación. Para exportar un informe, elija **Exportar** en el menú **Acciones** que se muestra en la barra de tareas del informe al abrirlo.  
  
> [!NOTE]  
>  Para poder imprimir un informe, debe tener permiso para verlo.  
  
 Para obtener mejores resultados a la hora de imprimir un informe desde una página web, utilice el comando **Imprimir** del menú **Acciones** . La acción **Imprimir** está ligada a un control de impresión de cliente que se descarga desde el servidor de informes. La descarga tiene lugar una vez, la primera vez que se selecciona **Imprimir**.  
  
 Los creadores de informes pueden diseñar informes expresamente para imprimirlos o para un formato de aplicación concreto. Debido al modo en que se implementa la paginación para los distintos formatos de aplicación, es posible que no pueda lograr unos resultados de impresión óptimos con cada uno de los informes en los distintos formatos de exportación. En contraste con los informes diseñados para una salida de impresión, las páginas de los informes en pantalla están diseñadas para adaptarse a cantidades de datos variables. Por ejemplo, los informes que incluyen una matriz pueden ocasionar que una página aumente de manera horizontal y vertical en función de cómo se expandan las filas y las columnas. Al imprimir un informe de tamaño variable, un usuario que no expanda una matriz obtendrá unos resultados de impresión diferentes de los de otro usuario que sí la expanda. En la mayoría de los informes exportados, las copias impresas de los informes incluyen todo lo que es visible en el informe, tal y como lo ve el usuario en el monitor de un equipo.  
  
### <a name="how-to-print-reports-from-the-actions-menu"></a>Cómo imprimir informes en el menú Acciones  
  
1.  Abra el informe.  
  
2.  En el menú **Acciones** , haga clic en **Imprimir**. Si no ve el menú **Acciones** , significa que se ha ocultado la barra de herramientas del informe y que no puede utilizar sus funciones. Si se muestra el menú **Acciones** pero no aparece el comando **Imprimir** en este menú, significa que se ha deshabilitado la funcionalidad de impresión en el servidor de informes y que no puede utilizarla.  
  
3.  En el cuadro de diálogo **Imprimir** , seleccione la impresora y la configuración que desee utilizar y, a continuación haga clic en **Aceptar**.  
  
     Para modificar la configuración predeterminada, haga clic en el botón **Propiedades** . El tamaño de página viene determinado por el alto y el ancho del tamaño de página del informe tal y como se estableció en la definición del informe. La extensión a la que puede cambiar las dimensiones de las páginas depende de las capacidades de la impresora que use.  
  
     Para ver el informe antes de imprimirlo, haga clic en el botón **Vista previa** . Se abre la primera página del informe en una ventana de vista previa independiente. A medida que el informe se representa en el servidor de informes, se proporcionan más páginas. Un informe en vista previa se representa en formato EMF. Puede navegar hasta la página anterior o siguiente hasta llegar a la última página y hasta que el botón **Siguiente** aparezca deshabilitado. Para modificar los márgenes de impresión de la página de vista previa, haga clic en el botón **Márgenes** . Se mostrará el cuadro de diálogo **Márgenes** . Configure los márgenes superior, inferior, derecho e izquierdo y haga clic en **Aceptar**. El cuadro de diálogo se cierra y la configuración se almacena para representar la vista previa y la impresión.  
  
## <a name="see-also"></a>Consulte también  
 [Habilitar y deshabilitar la impresión del lado cliente para Reporting Services](../../reporting-services/report-server/enable-and-disable-client-side-printing-for-reporting-services.md)  
  
  
