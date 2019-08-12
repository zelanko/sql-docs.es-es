---
title: 'Anclado de elementos de informe paginados en paneles de Power BI: Reporting Services | Microsoft Docs'
ms.date: 12/05/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
description: Puede anclar elementos de informe paginados de Reporting Services locales a un panel del servicio Power BI, como un nuevo icono.
ms.topic: conceptual
helpviewer_keywords:
- pbi
- dashboard
- pin
- powerbi
- power bi integration
ms.assetid: 1d96c3f7-2fd4-40f7-8d1c-14a7f54cdb15
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 8e91341c5c1d6b4f9ddd521a4735f22f63907784
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892001"
---
# <a name="pin-reporting-services-paginated-report-items-to-dashboards-in-power-bi"></a>Anclado de elementos de informe paginados de Reporting Services a paneles de Power BI

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../includes/ssrs-appliesto-pbirs.md)]

Puede anclar un elemento de informe paginado de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] local a un panel del servicio [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)], como un nuevo icono.   Para anclarlos, el administrador tendrá que integrar primero el servidor de informes con Azure Active Directory y [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)].  
  
##  <a name="bkmk_requirements_to_pin"></a> Requisitos para el anclado  
  
-   El servidor de informes está configurado para su integración con [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] . Para más información, vea [Integración del servidor de informes de Power BI &#40;Administrador de configuración&#41;](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md). Si no se ha configurado el servidor de informes, no verá el botón **Anclar al panel de Power BI** en la barra de herramientas del visor de informes.  
  
     ![Barra de herramientas del Visor de informes](../reporting-services/media/ssrs-report-powerbi.png)  
  
-   Puede anclar elementos desde el Visor de informes de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] en [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)], por ejemplo `https://myserver/Reports`.  No se pueden anclar elementos de [!INCLUDE[ssRBnoversion](../includes/ssrbnoversion.md)], desde el Diseñador de informes de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], ni desde una dirección URL de servidor de informes.  Por ejemplo, `https://myserver/ReportServer`.  
  
-   Tendrá que configurar el explorador para permitir elementos emergentes en el sitio del servidor de informes.  
  
-   Tendrá que configurar los informes para las credenciales almacenadas si quiere que el elemento anclado se actualice.  Cuando se ancla un elemento, se crea automáticamente una suscripción de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para administrar la actualización de datos del elemento en el panel.  Si en el informe no se usan credenciales almacenadas, cuando se ejecute la suscripción, verá un mensaje de error similar a este en la página **Mis suscripciones**.  
  
    "PowerBI Delivery error: dashboard: IT Spend Analysis Sample, visual: Chart2, error: (Error de entrega de PowerBI: panel: ejemplo de análisis de gasto en TI, objeto visual: gráfico 2, error:) La acción actual no se puede completar. Las credenciales del origen de datos del usuario no cumplen los requisitos necesarios para ejecutar este informe o conjunto de datos compartido. Es posible que las credenciales del origen de datos del usuario".
 
    Para más información sobre cómo almacenar credenciales, vea la sección "Configurar credenciales almacenadas para un origen de datos específico de informe (modo Nativo)" de [Almacenamiento de las credenciales en un origen de datos de Reporting Services](../reporting-services/report-data/store-credentials-in-a-reporting-services-data-source.md).  
  
##  <a name="bkmk_supported_items"></a> Elementos que puede anclar  
 Los siguientes elementos de informe se pueden anclar en un panel de [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] .  No se pueden anclar elementos que estén anidados dentro de una región de datos. Por ejemplo, no se puede anclar un elemento que esté anidado dentro de una tabla o lista de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
-   Gráficos  
-   Paneles del medidor.  
-   Mapas  
-   Imágenes  
-   Los artículos deben estar en el cuerpo del informe.  No se pueden anclar elementos que se encuentren en el encabezado o en el pie de página.  
-   Puede anclar elementos individuales que estén dentro de un rectángulo de nivel superior, pero no puede anclarlos todos como un único grupo.  
  
##  <a name="bkmk_to_pin"></a> Para anclar un elemento de informe  
  
1. Compruebe que haya iniciado sesión en [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]. En el [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)], seleccione el elemento de menú **Mi configuración** e inicie sesión. Para más información, consulte [La configuración de la integración de Power BI &#40;portal web&#41;](my-settings-for-power-bi-integration-web-portal.md).

    ![ssRS_WebPortal_MySettings](../reporting-services/media/ssrs-webportal-mysettings.png)  
  
2. Vaya a la carpeta del [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] que contiene el informe y visualícelo.  
  
3. Mientras ve el informe, haga clic en el botón **Anclar a panel de Power BI** de la barra de herramientas.  Se le pedirá que inicie sesión, si no lo ha hecho aún.  Si no ve el botón [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] , se deberá a que el servidor de informes aún no se ha integrado con [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]. Para más información, vea [Integración del servidor de informes de Power BI &#40;Administrador de configuración&#41;](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md).  
  
    ![ssRS_Report_PowerBI](../reporting-services/media/ssrs-report-powerbi.png)  
  
4. Haga clic en el elemento de informe que quiere anclar a [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]. Solo puede anclar un elemento cada vez.  El Visor de informes presenta una vista sombreada del informe. En ella, los elementos de informe que se pueden anclar aparecerán resaltados, mientras que los que no, tendrán un sombreado oscuro.  
  
    **(1)** seleccione el grupo que contiene el panel que quiere anclar, **(2)** seleccione el panel donde también quiere anclar el elemento y **(3)** seleccione la frecuencia con la que quiere que se actualice el icono en el panel.   ![nota](https://docs.microsoft.com/analysis-services/analysis-services/instances/install-windows/media/ssrs-fyi-note.png "nota") Las suscripciones de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] administran la actualización y, después de anclar el elemento, se pueden modificar para configurar una programación de actualización distinta.  
  
    ![ssRS_Pin_to_PowerBI](../reporting-services/media/ssrs-pin-to-powerbi.png)  
  
5. Seleccione **Anclar**.  
  
    En el diálogo **Anclaje correcto** , puede seleccionar el vínculo **Muéstrelo en Power BI aquí** para ir al panel y ver el elemento que acaba de anclar.  
  
6. Haga clic en **Cerrar** para devolver el informe a la vista normal.  
  
##  <a name="bkmk_in_the_dashboard"></a> En el panel

Después de anclar el elemento de informe en el panel, el icono parece igual que cualquier otro del panel y no existe ninguna indicación visual de que provenga de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. En la siguiente lista se resume cómo se rellenan las propiedades del icono a partir de elemento de informe.  
  
En el panel de [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] , el elemento de informe anclado se comporta como los demás iconos:

**(1)** Puede anclar el icono a otros paneles.

**(2)** En **Detalles del icono**, verá que se usa el título de informe de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] como el predeterminado del icono.

**(3)** El subtítulo del icono se obtiene a partir de la fecha y hora en la que se ha anclado el icono o en que se han actualizado los datos por última vez desde [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. La suscripción de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] que se creó automáticamente al anclar el elemento de informe administra la actualización.

**(5)** Si hace clic en el icono en sí, [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] usa el **vínculo personalizado (4)** para ir a la página [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] del servidor de informes registrado. El vínculo se estableció cuando se ancló el elemento desde [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. Si no está conectado al servidor de informes a través de Internet, se le mostrará un error en el explorador.  

![ssrs_pinned_tile_details](../reporting-services/media/ssrs-pinned-tile-details.png "ssrs_pinned_tile_details")  
  
##  <a name="bkmk-troubleshoot"></a> Solucionar problemas  
  
-   **No[!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] hay ningún botón en la barra de herramientas del Visor de informes:** este mensaje indica que el servidor de informes no se ha integrado con [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]. Para más información, vea [Integración del servidor de informes de Power BI &#40;Administrador de configuración&#41;](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md).  
  
- **No se puede anclar:** al intentar anclar un elemento, se muestra el siguiente mensaje de error (vea la sección [Elementos que puede anclar](#bkmk_supported_items)).  
  
      Cannot Pin: There are no report items on this page that you can pin to [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)].  
  
-   **En los elementos anclados se muestran datos obsoletos** en un panel de [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] y ya se han actualizado durante un período de tiempo.  El token de las credenciales de usuario ha expirado y tendrá que volver a iniciar sesión.  El registro de las credenciales de usuario en Azure y [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] es válido durante 90 días. En el [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)], haga clic en **Mi configuración**. Para más información, vea [La configuración de la integración de Power BI &#40;portal web&#41;](my-settings-for-power-bi-integration-web-portal.md).  
  
-   **Los elementos anclados muestran datos obsoletos** en un panel de [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] y no se han actualizado ni siquiera una vez.  El problema es que el informe no está configurado para utilizar credenciales almacenadas. Un informe debe usar credenciales almacenadas, porque la acción de anclar un elemento de informe crea una suscripción de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para administrar la programación de actualización de los iconos. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] requieren credenciales almacenadas. Si revisa la página **Mis suscripciones**, verá un mensaje de error similar a este:  
  
        PowerBI Delivery error: dashboard: SSRS items, visual: Image3, error: The current action can't be completed. The user data source credentials do not meet the requirements to run this report or shared dataset. Either the user data source credentials are not stored in the report server database, or the user data source is configured not to require credentials but the unattended execution account is not specified. (rsInvalidDataSourceCredentialSetting)
  
-   **Credenciales de Power BI expiradas:**  está tratando de anclar un elemento y se le muestra el siguiente mensaje de error. En el [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)], haga clic en **Mi configuración** y, en la página que se muestre, haga clic en **Iniciar sesión**. Para más información, consulte [La configuración de la integración de Power BI &#40;portal web&#41;](my-settings-for-power-bi-integration-web-portal.md).  
  
        Cannot Pin: Unexpected Server Error: Missing, invalid or expired Power BI credentials.  
  
-   **No se puede anclar**: si intenta anclar elementos a un panel que se encuentra en estado de solo lectura, verá un mensaje de error similar a este:  
  
        Server Error: The item 'Dashboard deleted 015cf022-8e2f-462e-88e5-75ab0a04c4d0' can't be found. (rsItemNotFound)  
  
##  <a name="bkmk_subscription_management"></a> Administración de suscripciones  
 Además de los problemas relacionados con las suscripciones descritos en la sección de solución de problemas, la información siguiente ayuda a mantener las suscripciones relacionadas con [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)].
  
-   **Se ha cambiado el nombre de un elemento:** si se cambia el nombre de un elemento de informe anclado o lo elimina, el icono de [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] no se volverá a actualizar y verá un mensaje de error similar al siguiente.  Si cambia el nombre del elemento al que tenía originalmente, la suscripción comenzará a funcionar de nuevo y el icono se actualizará de acuerdo con la programación establecida para tal fin.  
  
        PowerBI Delivery error: dashboard: SSRS items, visual: Image1, error: Error: Report item 'Image1' cannot be found.  
  
     También puede editar las propiedades de suscripción y cambiar el **nombre visual del informe** al nombre del elemento de informe pertinente. ![cambiar el objeto visual que se usa para la actualización de power bi](../reporting-services/media/ssrs-powerbi-subscription-visual.png "cambiar el objeto visual que se usa para la actualización de power bi")  
  
-   **Eliminación de un icono**. Si elimina un icono en [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)], la suscripción asociada no se elimina en [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] , y en la página **Mis suscripciones**, verá un error similar al siguiente. Puede eliminar la suscripción.  
  
        PowerBI Delivery error: dashboard: SSRS items, visual: Image3, error: The item 'Tile deleted af7131d9-5eaf-480f-ba45-943a07d19c9f' cannot be found.  

## <a name="video"></a>Vídeo

<iframe width="560" height="315" src="https://www.youtube.com/embed/QhPQObqmMPc" frameborder="0" allowfullscreen></iframe>

## <a name="see-also"></a>Consulte también  
 [Integración del servidor de informes de Power BI &#40;Administrador de configuración&#41;](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md)   
 [La configuración de la integración de Power BI &#40;portal web&#41;](my-settings-for-power-bi-integration-web-portal.md)  
 [Paneles en Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/)  
  
  
[!INCLUDE[feedback_stackoverflow_msdn_connect_md](../includes/feedback-stackoverflow-msdn-connect-md.md)]

