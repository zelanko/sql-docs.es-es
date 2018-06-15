---
title: Imprimir informes desde un explorador con el control de impresión (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-builder
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 10054250-d915-4bcb-8a1d-26837db4e932
caps.latest.revision: 13
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f96460a280bd11f59ffd0e042eefbbc9be0b0188
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "33019002"
---
# <a name="print-reports-from-a-browser-with-the-print-control-report-builder-and-ssrs"></a>Imprimir informes desde un explorador usando el control de impresión (Generador de informes y SSRS)
  Aunque los exploradores son las aplicaciones cliente habitualmente más usadas para ver un informe, la funcionalidad de impresión que incluyen no es la ideal para imprimir informes. La funcionalidad de impresión de un explorador está diseñada para imprimir páginas web. Normalmente, las páginas que imprime desde un explorador incluyen todos los elementos visuales de una página web, además de la información del encabezado y del pie de página que identifica la página o el sitio web. Al imprimir desde un explorador, se imprime el contenido de la ventana actual. En el caso de un informe compuesto por varias páginas, el explorador imprime como máximo la primera página y posiblemente incluso menos si la página del informe tiene unas dimensiones superiores a las de una página impresa.  
  
 Para mejorar la calidad de impresión de los informes que ve en un explorador y para imprimir varias páginas, puede usar la funcionalidad de impresión del lado cliente ofrecida en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. La impresión del lado cliente proporciona un cuadro de diálogo **Imprimir** estándar que puede usarse para seleccionar una impresora, especificar páginas y márgenes, y previsualizar el informe antes de su impresión. La impresión del lado cliente está concebida para que se use en lugar del comando **Imprimir** del menú **Archivo** del explorador. Si utiliza la impresión del lado cliente, el informe se imprime tal y como se diseñó, sin los elementos adicionales que se ven en la impresión de una página web.  
  
 Para usar la impresión del lado cliente, necesita instalar un control ActiveX de [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Para obtener más información, vea [Habilitar y deshabilitar la impresión del lado cliente para Reporting Services](../../reporting-services/report-server/enable-and-disable-client-side-printing-for-reporting-services.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="print-options"></a>Opciones de impresión  
 Para configurar las propiedades de impresión del informe, en el cuadro de diálogo **Imprimir** , haga clic en el botón **Propiedades** . El**Tamaño de papel** viene determinado por el alto y el ancho del tamaño de página del informe, tal y como se estableció en la definición de informe. Los valores disponibles dependen del tipo de impresora y de sus capacidades. Las opciones Ancho y Alto muestran los valores predeterminados como están determinados por los controladores de impresión configurados en el equipo. Si cambia estos valores, el informe se imprime con las nuevas dimensiones. El ancho y el alto de página están determinados por la **Orientación**, que se establece en **Vertical** u **Horizontal**. La orientación predeterminada mostrada depende del alto y del alto de página del informe.  
  
> [!NOTE]  
>  El cuadro de diálogo **Imprimir** y la configuración predeterminada de impresora correspondientes al alto, al ancho y a la orientación de página dependen de la definición del informe.  
  
### <a name="print-preview"></a>Vista previa de impresión  
 Para mostrar una vista previa de un informe, en el cuadro de diálogo **Imprimir** , haga clic en el botón **Vista previa** . Al hacer clic en la opción de vista previa se abre la primera página del informe en una ventana de vista previa independiente. A medida que el informe se representa en el servidor de informes, se proporcionan más páginas. Un informe en vista previa se representa en formato EMF. Puede navegar hasta la página anterior o siguiente hasta llegar a la última página y hasta que el botón **Siguiente** aparezca deshabilitado.  
  
### <a name="adjusting-print-margins"></a>Ajustar los márgenes de impresión  
 Puede modificar los márgenes de impresión en el informe EMF representado antes de imprimir el informe. Para ello, en el cuadro de diálogo **Imprimir** , haga clic en el botón **Vista previa** . En la parte superior de la página de vista previa, haga clic en el botón **Márgenes** . A continuación se muestra el cuadro de diálogo Márgenes. Configure los márgenes superior, inferior, izquierdo y derecho según sea necesario. [!INCLUDE[clickOK](../../includes/clickok-md.md)] El cuadro de diálogo se cierra y la configuración se almacena para representar la vista previa y la impresión.  
  
## <a name="see-also"></a>Ver también  
 [Imprimir informes &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-builder/print-reports-report-builder-and-ssrs.md)   
 [Imprimir un informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-builder/print-a-report-report-builder-and-ssrs.md)  
  
  
