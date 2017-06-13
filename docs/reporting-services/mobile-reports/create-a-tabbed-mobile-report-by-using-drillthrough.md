---
title: "Crear un informe móvil con fichas mediante la obtención de detalles | Informes de Reporting Services móviles | Documentos de Microsoft"
ms.custom: 
ms.date: 03/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c4d5d80d-370a-4a6d-8b76-698bd5ba5ba6
caps.latest.revision: 9
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 6554f808c19540d2a3b7cbe3fdf4e86c5fe7a357
ms.contentlocale: es-es
ms.lasthandoff: 06/13/2017

---
# <a name="create-a-tabbed-mobile-report-by-using-drillthrough"></a>Crear un informe móvil con fichas mediante la obtención de detalles
Sepa cómo crear un informe móvil de [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] que se vea y funcione como un informe en pestañas con obtención de detalles y parámetros.

En este informe, por ejemplo, los medidores en la parte superior actúan como pestañas. Cuando haga clic en el medidor Transporte, los datos del resto del gráfico se filtran según los datos de transporte.

![06-Mobile-Report-Web-Viewer-Transportation](../../reporting-services/mobile-reports/media/tabbed-mobile-report-web-viewer-transportation-complete.png)

En segundo plano, realmente esto es un conjunto de cinco informes independientes, cada uno con un parámetro diferente que filtra el informe para que coincida con el medidor seleccionado en la parte superior del informe. Crear todos los cinco informes en primer lugar, para cada uno de los cinco informes, realice los otros cuatro medidores en drillthroughs a los otros cuatro informes.

Estos son los pasos de este ejemplo.

## <a name="create-the-basic-report"></a>Crear el informe básico

1. Cree un informe denominado Ventas, con cinco medidores:

    * Sales
    * Transporte
    * Combustible
    * Almacenamiento
    * Gastos varios

   ![01 ventas Mobile Report Publisher](../../reporting-services/mobile-reports/media/01-sales-mobile-report-publisher.png)
    
2. Establecer **acentos** a **en** para el medidor de ventas, por lo tanto contrastará con la el resto del informe: en este caso, blanco sobre fondo negro.

    ![01a-Sales-Accent-Mobile-Report-Publisher](../../reporting-services/mobile-reports/media/01a-sales-accent-mobile-report-publisher.png)
    
3. Guárdelo en un [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] servidor de informes.

## <a name="make-copies-of-the-report"></a>Realizar copias del informe

1. Realizar cuatro copias del informe de ventas y asignarles un nombre: 

    * Transporte
    * Combustible
    * Almacenamiento
    * Gastos varios

3. Para guardar la [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] servidor de informes.

## <a name="set-the-gauge-as-a-drillthrough"></a>Establecer el medidor como una obtención de detalles

En esta sección, se establece cada medidor (excepto el indicador de ventas) como una obtención de detalles en su informe correspondiente.

1. En el informe de ventas, seleccione el medidor de transporte.

    ![02-Sales-Create-DrillThrough-Mobile-Report-Publisher](../../reporting-services/mobile-reports/media/02-sales-create-drillthrough-mobile-report-publisher.png)

2. Con el **diseño** pestaña seleccionada, en la **propiedades Visual** panel, seleccione **destino de obtención de detalles**.

3. Seleccione **informe móvil**.

4. Vaya a y seleccione el informe que será el destino para la obtención de detalles, en este caso, "Finanzas - Transportation."

    ![03-Sales-SELECT-Dashboard-Mobile-Report-Publisher](../../reporting-services/mobile-reports/media/03-sales-select-dashboard-mobile-report-publisher.png)

5. En **Configurar informe de destino**, seleccione el parámetro para filtrar el informe y seleccione **aplicar**.

   ![04-Sales-Apply-Parameters-Mobile-Report-Publisher](../../reporting-services/mobile-reports/media/04-sales-apply-parameters-mobile-report-publisher.png)
   
6. Repita estos pasos para cada uno de los otros indicadores en el informe de ventas. 

## <a name="set-the-gauges-for-the-other-reports"></a>Establece los indicadores para los demás informes

1.  Abra el informe de transporte, establezca el medidor de ventas como una obtención de detalles en el informe de ventas y los otros tres medidores como drillthroughs a los informes correspondientes.

2. En el informe de transporte, establezca **acentos** para el medidor de transporte para **en**, por otra parte el el resto del informe.

3. Repita estos pasos para los informes de combustible, almacenamiento y los gastos varios. 

## <a name="view-the-report-in-the-web-portal"></a>Ver el informe en el portal web

1. Vaya a la [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] servidor de informes y abra uno de los informes. 

2. Tenga en cuenta que cada uno de los indicadores tiene un icono de obtención de detalles en la esquina superior derecha.

    ![Web-Viewer-drillthrough-icon-mobile-report-builder](../../reporting-services/mobile-reports/media/web-viewer-drillthrough-icon-mobile-report-builder.png)

3. Seleccione uno de los medidores para ir al informe filtrado por de datos ese del medidor.

   ![06-Mobile-Report-Web-Viewer-Transportation](../../reporting-services/mobile-reports/media/06-mobile-report-web-viewer-transportation.png)

### <a name="see-also"></a>Vea también
    
* [Agregar parámetros a un informe para dispositivos móviles](../../reporting-services/mobile-reports/add-parameters-to-a-mobile-report-reporting-services.md)
* [Agregar obtención de detalles de un informe para dispositivos móviles a otros informes para dispositivos móviles o direcciones URL](../../reporting-services/mobile-reports/add-drillthrough-from-a-mobile-report-to-other-mobile-reports-or-urls.md)




  


