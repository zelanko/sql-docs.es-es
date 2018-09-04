---
title: Mostrar números de página u otras propiedades del informe (Generador de informes y SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.suite: pro-bi
ms.topic: conceptual
ms.assetid: c7d95245-4709-4d04-acb4-59bf71e60d97
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: af478c71325204d5c23a8917de566c48be2f89d7
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/30/2018
ms.locfileid: "43277718"
---
# <a name="display-page-numbers-or-other-report-properties-report-builder-and-ssrs"></a>Mostrar números de página u otras propiedades del informe (Generador de informes y SSRS)
  Es fácil agregar números de página, un título del informe, nombre de archivo y otras propiedades del informe a los encabezados o pies de página de su informe. Estas propiedades se almacenan como campos en la carpeta Campos integrados del panel Datos de informe:  
  
-   Tiempo de ejecución  
  
-   Número de página  
  
-   ReportFolder  
  
-   Nombre del informe  
  
-   Dirección URL del servidor de informes  
  
-   Páginas totales  
  
-   Id. de usuario  
  
-   Lenguaje  
  
 Para un número de página, puede desear agregar la palabra "Página" antes del número. También puede desear mostrar el número total de páginas.  
  
> [!NOTE]  
>  Agregar el número total de páginas al pie de página puede provocar un rendimiento lento cuando ejecuta el informe u obtiene de él una vista previa.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-page-number-or-other-report-properties"></a>Para agregar un número de página u otras propiedades del informe  
  
1.  En el panel Datos de informe, expanda la carpeta Campos integrados.  
  
    > [!NOTE]  
    >  Si no ve el panel Datos de informe, en la pestaña Ver haga clic en **Datos de informe**.  
  
2.  Arrastre el campo **Número de página** desde el panel Datos de informe al encabezado o el pie del informe.  
  
    > [!NOTE]  
    >  El pie de página se agrega automáticamente al informe. Para agregar un encabezado de página, en la pestaña **Insertar** haga clic en **Encabezado**y, a continuación, en **Agregar encabezado**.  
    >   
    >  Se agrega un cuadro de texto contiene la expresión simple [&PageNumber].  
  
### <a name="to-add-the-word-page-before-the-page-number"></a>Para agregar la palabra "Página" antes del número de página  
  
1.  Haga clic con el botón derecho en el cuadro de texto que contiene [&PageNumber] y haga clic en **Expresiones**.  
  
     El cuadro de texto **Establecer expresión para: Valor** contiene la expresión =Globals!PageNumber.  
  
2.  Coloque el cursor después del signo = y escriba **"Página " &**.  
  
     La expresión ahora es ="Página "&Globals!PageNumber  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-add-total-number-of-pages-after-the-page-number"></a>Para agregar el número total de páginas después del número de página  
  
1.  Haga clic con el botón secundario en el cuadro de texto con la expresión y haga clic en **Expresiones**.  
  
2.  Escriba **&" de "&** al final de la expresión.  
  
3.  En el panel Categoría, expanda **Campos integrados** y haga doble clic en **TotalPages**.  
  
     La expresión es ahora ="Página "&Globals!PageNumber &" de "&Globals!TotalPages  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Ver también  
 [Encabezados y pies de página &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/page-headers-and-footers-report-builder-and-ssrs.md)   
 [Dar formato al texto en un cuadro de texto &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/format-text-in-a-text-box-report-builder-and-ssrs.md)  
  
  
