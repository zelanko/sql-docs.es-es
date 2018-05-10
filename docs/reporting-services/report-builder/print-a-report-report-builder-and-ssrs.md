---
title: Imprimir un informe (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-builder
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: b96936c9-c387-41a9-8c19-6eb325769ffd
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 9a730f6d4ec36a3e8b1141a2494e3d97a9151213
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="print-a-report-report-builder-and-ssrs"></a>Imprimir un informe (Generador de informes y SSRS)
  Después de guardar un informe en un servidor de informes, puede ver e imprimir el informe desde un explorador, el portal web de Reporting Services o cualquier aplicación que use para ver un informe exportado. Antes de guardar un informe, puede imprimirlo desde su vista previa.  
  
 Cuando imprime un informe, puede especificar el tamaño del papel que se va a usar. El tamaño del papel determina el número de páginas de un informe y los datos del informe que caben en cada página. El tamaño del papel solamente afecta a los informes representados con representadores de saltos de página forzados: PDF, Imagen e Imprimir. El establecimiento del tamaño del papel no tiene ningún efecto en otros representadores. Para más información, vea [Comportamientos de la representación &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md).  
  
 Desde la barra de herramientas del visor de informes del portal web de Reporting Services o en la vista previa del Generador de informes, puede exportar un informe a un representador de saltos de página manuales o hacer clic en el botón Imprimir para imprimir una copia del informe. Es posible que necesite establecer el tamaño del papel u otras propiedades de configuración de página. Use el cuadro de diálogo **Propiedades del informe** para cambiar las propiedades de configuración de página, incluyendo el tamaño del papel.  
  
 Puede especificar los márgenes de impresión de la página en dos ubicaciones diferentes: en modo de diseño y en modo de ejecución.  
  
-   **Modo de diseño.** Al establecer los márgenes de página en modo de diseño, esta configuración se guarda en la definición de informe al guardar el informe.  
  
-   **Modo de ejecución.** Al establecer los márgenes de página en modo de ejecución, esta información no se guarda en la definición de informe. La siguiente vez que imprima el informe, recibirá la configuración de la definición de informe, a menos que indique de nuevo sus márgenes de impresión.  
  
    > [!NOTE]  
    >  Los márgenes de impresión no se muestran en los modos de diseño o de ejecución. No hay ninguna relación entre el área expuesta de diseño y el área de impresión de su informe. Para ver los márgenes de impresión, en modo de ejecución haga clic en Diseño de impresión en la pestaña **Ejecutar** de la Cinta de opciones.  
  
 Para más información sobre la paginación de informes, vea [Paginación en Reporting Services &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-print-a-report-in-report-builder"></a>Para imprimir un informe en el Generador de informes  
  
1.  Abra un informe.  
  
2.  En la pestaña Inicio, haga clic en **Ejecutar**.  
  
3.  (opcional) Haga clic en **Diseño de impresión** para ver el aspecto que tendrá el informe cuando se imprima.  
  
4.  (opcional) Haga clic en **Configurar página** para configurar el papel, la orientación y los márgenes.  
  
    > [!NOTE]  
    >  Los valores predeterminados de estas opciones proceden de las propiedades de informe, que se establecen en la vista Diseño. Los valores que establece en el cuadro de diálogo **Configurar página** solamente valen para esta sesión. Cuando cierre este informe y lo vuelva a abrir, tendrá de nuevo los valores predeterminados.  
  
5.  Haga clic en **Imprimir**.  
  
6.  En el cuadro de diálogo **Imprimir** , seleccione una impresora y especifique otras opciones de impresión.  
  
### <a name="to-print-a-report-from-a-web-browser-application"></a>Para imprimir un informe desde una aplicación de explorador web  
  
1.  En el portal web de Reporting Services, vaya al informe que quiere imprimir. Abra el informe.  
  
3.  En la barra de herramientas que se encuentra en la parte superior del informe, haga clic en **Imprimir**.  
  
    > [!NOTE]  
    >  La primera vez que imprima un informe HTML, el servidor de informes le pedirá que instale el control ActiveX que se usa para imprimir. Para poder imprimir, deberá instalar y configurar el control.  
  
4.  En el cuadro de diálogo **Imprimir** , seleccione una impresora y haga clic en **Imprimir**.  
  
### <a name="to-print-a-report-from-other-applications"></a>Para imprimir un informe desde otras aplicaciones  
  
1.  En el portal web de Reporting Services, vaya al informe que quiere imprimir. Abra el informe.  
  
2.  En la barra de herramientas situada en la parte superior del informe, seleccione un formato de representación y, a continuación, haga clic en **Exportar**. El informe se abre en la aplicación de visor correspondiente al formato de representación.  
  
     Por ejemplo, si selecciona PDF, el informe se abre en Adobe Acrobat Reader.  
  
3.  En el menú **Archivo** de dicho programa, haga clic en **Imprimir**.  
  
### <a name="to-change-paper-size"></a>Para cambiar el tamaño del papel  
  
1.  Haga clic con el botón derecho fuera del cuerpo del informe y haga clic en **Propiedades del informe**.  
  
2.  En **Configurar página**, seleccione un valor en la lista **Tamaño de papel** . Cada opción rellena las propiedades **Ancho** y **Alto** . También puede especificar un tamaño personalizado escribiendo valores numéricos en los cuadros **Ancho** y **Alto** . [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  Los valores de tamaño tienen una unidad predeterminada en función de la configuración regional del usuario. Para designar una unidad diferente, escriba un designador de unidad física, por ejemplo cm, mm, pt o pc después del valor numérico.  
  
### <a name="to-set-page-margins-in-design-mode"></a>Para establecer los márgenes de página en modo de diseño  
  
-   Haga clic con el botón derecho en el área azul que rodea la superficie de diseño, haga clic en **Propiedades del informe**y luego en la página **Configurar página** .  
  
### <a name="to-set-page-margins-in-run-mode"></a>Para establecer los márgenes de página en modo de ejecución  
  
-   Haga clic en **Configurar página** en la pestaña **Ejecutar** .  
  
## <a name="see-also"></a>Ver también  
 [Imprimir informes &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-builder/print-reports-report-builder-and-ssrs.md)   
 [Exportación de informes &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)   
 [Propiedades del informe (cuadro de diálogo), Configurar página &#40;Generador de informes&#41;](http://msdn.microsoft.com/library/eb3b5d01-7b82-4808-a58b-9e096742f8c6)   
 [Vista de diseño de informe &#40;Generador de informes&#41;](../../reporting-services/report-builder/report-design-view-report-builder.md)  
  
  
