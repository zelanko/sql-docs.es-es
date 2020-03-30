---
title: 'Anclado de elementos de informe paginados en paneles de Power BI: Reporting Services | Microsoft Docs'
ms.date: 01/14/2020
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
ms.openlocfilehash: da984efa4e0b4d964cf947929094ee7b392063f2
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "75952479"
---
# <a name="pin-reporting-services-paginated-report-items-to-dashboards-in-power-bi"></a>Anclado de elementos de informe paginados de Reporting Services a paneles de Power BI

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../includes/ssrs-appliesto-pbirs.md)]

Puede anclar un elemento de informe paginado de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] local a un panel del servicio [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)], como un nuevo icono.   Para anclarlos, el administrador tendrá que integrar primero el servidor de informes con Azure Active Directory y [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)].  
  
##  <a name="requirements-to-pin"></a><a name="bkmk_requirements_to_pin"></a> Requisitos para el anclado  
  
-   El servidor de informes está configurado para su integración con [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] . Para más información, vea [Integración del servidor de informes de Power BI &#40;Administrador de configuración&#41;](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md). Si no se ha configurado el servidor de informes, no verá el botón **Anclar al panel de Power BI** en la barra de herramientas del visor de informes.  
  
     ![Barra de herramientas del Visor de informes](../reporting-services/media/ssrs-report-powerbi.png)  
  
-   Puede anclar elementos desde el Visor de informes de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] en [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)], por ejemplo `https://myserver/Reports`.  No se pueden anclar elementos de [!INCLUDE[ssRBnoversion](../includes/ssrbnoversion.md)], desde el Diseñador de informes de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], ni desde una dirección URL de servidor de informes.  Por ejemplo, `https://myserver/ReportServer`.  
  
-   Tendrá que configurar el explorador para permitir elementos emergentes en el sitio del servidor de informes.  
  
-   Tendrá que configurar los informes para las credenciales almacenadas si quiere que el elemento anclado se actualice.  Cuando se ancla un elemento, se crea automáticamente una suscripción de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para administrar la actualización de datos del elemento en el panel.  Si en el informe no se usan credenciales almacenadas, cuando se ejecute la suscripción, verá un mensaje de error similar a este en la página **Mis suscripciones**.  
  
    "Error de entrega de Power BI: panel: objeto visual, IT Spend Analysis Sample: Chart2, error: No se puede completar la acción actual. Las credenciales del origen de datos del usuario no cumplen los requisitos necesarios para ejecutar este informe o conjunto de datos compartido. Es posible que las credenciales del origen de datos del usuario".
 
    Para más información sobre cómo almacenar credenciales, vea la sección "Configurar credenciales almacenadas para un origen de datos específico de informe (modo Nativo)" de [Almacenamiento de las credenciales en un origen de datos de Reporting Services](../reporting-services/report-data/store-credentials-in-a-reporting-services-data-source.md).  
  
##  <a name="items-you-can-pin"></a><a name="bkmk_supported_items"></a> Elementos que puede anclar  
 Los siguientes elementos de informe se pueden anclar en un panel de [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] .  No se pueden anclar elementos que estén anidados dentro de una región de datos. Por ejemplo, no se puede anclar un elemento que esté anidado dentro de una tabla o lista de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
-   Gráficos  
-   Paneles del medidor.  
-   Mapas  
-   Imágenes  
-   Los artículos deben estar en el cuerpo del informe.  No se pueden anclar elementos que se encuentren en el encabezado o en el pie de página.  
-   Puede anclar elementos individuales que estén dentro de un rectángulo de nivel superior, pero no puede anclarlos todos como un único grupo.  
  
##  <a name="to-pin-a-report-item"></a><a name="bkmk_to_pin"></a> Para anclar un elemento de informe  
  
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
  
##  <a name="in-the-dashboard"></a><a name="bkmk_in_the_dashboard"></a> En el panel

Después de anclar el elemento de informe en el panel, el icono parece igual que cualquier otro del panel y no existe ninguna indicación visual de que provenga de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. En la siguiente lista se resume cómo se rellenan las propiedades del icono a partir de elemento de informe.  
  
En el panel de [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] , el elemento de informe anclado se comporta como los demás iconos:

**(1)** Puede anclar el icono a otros paneles.

**(2)** En **Detalles del icono**, verá que se usa el título de informe de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] como el predeterminado del icono.

**(3)** El subtítulo del icono se obtiene a partir de la fecha y hora en la que se ha anclado el icono o en que se han actualizado los datos por última vez desde [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. La suscripción de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] que se creó automáticamente al anclar el elemento de informe administra la actualización.

**(5)** Si hace clic en el icono en sí, [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] usa el **vínculo personalizado (4)** para ir a la página [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] del servidor de informes registrado. El vínculo se estableció cuando se ancló el elemento desde [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. Si no está conectado al servidor de informes a través de Internet, se le mostrará un error en el explorador.  

![ssrs_pinned_tile_details](../reporting-services/media/ssrs-pinned-tile-details.png "ssrs_pinned_tile_details")  
  
##  <a name="troubleshoot-issues"></a><a name="bkmk-troubleshoot"></a> Solucionar problemas  
  
-   **No hay botón de [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] en la barra de herramientas del Visor de informes:**  Este mensaje indica que el servidor de informes no se ha integrado con [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]. Para más información, vea [Integración del servidor de informes de Power BI &#40;Administrador de configuración&#41;](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md).  
  
- **No se puede anclar**: cuando trata de anclar un elemento, verá el mensaje de error siguiente: Vea la sección [Elementos que se pueden anclar](#bkmk_supported_items).  
  
    "No se puede anclar: no hay ningún elemento de informe en esta página que pueda anclar a [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)]".  
  
-   **En los elementos anclados se muestran datos obsoletos** en un panel de [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] y ya se han actualizado durante un período de tiempo.  El token de las credenciales de usuario ha expirado y tendrá que volver a iniciar sesión.  El registro de las credenciales de usuario en Azure y [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] es válido durante 90 días. En el [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)], haga clic en **Mi configuración**. Para más información, vea [La configuración de la integración de Power BI &#40;portal web&#41;](my-settings-for-power-bi-integration-web-portal.md).  
  
-   **Los elementos anclados muestran datos obsoletos** en un panel de [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] y no se han actualizado ni siquiera una vez.  El problema es que el informe no está configurado para utilizar credenciales almacenadas. Un informe debe usar credenciales almacenadas, porque la acción de anclar un elemento de informe crea una suscripción de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para administrar la programación de actualización de los iconos. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] requieren credenciales almacenadas. Si revisa la página **Mis suscripciones**, verá un mensaje de error similar a este:  
  
    "Error de entrega de Power BI: panel: elementos SSRS, objeto visual: Image3, error: No se puede completar la acción actual. Las credenciales del origen de datos del usuario no cumplen los requisitos necesarios para ejecutar este informe o conjunto de datos compartido. Es posible que las credenciales del origen de datos del usuario no estén almacenadas en la base de datos del servidor de informes, o bien que el origen de datos del usuario esté configurado para no requerir credenciales pero no se haya configurado la cuenta de ejecución desatendida. (rsInvalidDataSourceCredentialSetting)"
  
-   **Credenciales de Power BI expiradas:**  está tratando de anclar un elemento y se le muestra el mensaje de error siguiente. En el [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)], haga clic en **Mi configuración** y, en la página que se muestre, haga clic en **Iniciar sesión**. Para más información, consulte [La configuración de la integración de Power BI &#40;portal web&#41;](my-settings-for-power-bi-integration-web-portal.md).  
  
    "No se puede anclar: error de servidor inesperado: Faltan las credenciales de Power BI, no son válidas o expiraron".  
  
-   **No se puede anclar**: si intenta anclar un elemento a un panel que se encuentra en estado de solo lectura, verá un mensaje de error similar a este:  
  
    "Error de servidor: No se encuentra el elemento "Dashboard deleted 015cf022-8e2f-462e-88e5-75ab0a04c4d0". (rsItemNotFound)"  

-   **Los iconos de las aplicaciones Power BI muestran datos obsoletos:** Si ancla un elemento de informe de Reporting Services a un panel y, a continuación, distribuye ese panel en una aplicación, el elemento de informe anclado de ese panel no se actualizará. 

##  <a name="subscription-management"></a><a name="bkmk_subscription_management"></a> Administración de suscripciones  
 Además de los problemas relacionados con las suscripciones descritos en la sección de solución de problemas, la información siguiente ayuda a mantener las suscripciones relacionadas con [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)].
  
-   **Se ha cambiado el nombre de un elemento:** si se cambia el nombre de un elemento de informe anclado o se elimina, el icono de [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] no se volverá a actualizar y verá un mensaje de error similar al siguiente.  Si cambia el nombre del elemento al que tenía originalmente, la suscripción comenzará a funcionar de nuevo y el icono se actualizará de acuerdo con la programación establecida para tal fin.  
  
    "Error de entrega de Power BI: panel: elementos SSRS, objeto visual: Image1, error: Error: No se encuentra el elemento de informe "image1".  
  
    También puede editar las propiedades de suscripción y cambiar el **nombre visual del informe** al nombre del elemento de informe pertinente. ![Cambio del objeto visual usado para la actualización de Power BI](../reporting-services/media/ssrs-powerbi-subscription-visual.png "Cambio del objeto visual usado para la actualización de Power BI")  
  
-   **Eliminación de un icono**. Si elimina un icono en [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)], la suscripción asociada no se elimina en [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], y en la página **Mis suscripciones**, verá un error similar al siguiente. Puede eliminar la suscripción.  
  
    "Error de entrega de Power BI: panel: elementos SSRS, objeto visual: Image3, error: No se encuentra el elemento "Tile deleted af7131d9-5eaf-480f-ba45-943a07d19c9f".  

## <a name="video"></a>Vídeo

<iframe width="560" height="315" src="https://www.youtube.com/embed/QhPQObqmMPc" frameborder="0" allowfullscreen></iframe>

## <a name="see-also"></a>Consulte también  
 [Integración del servidor de informes de Power BI &#40;Administrador de configuración&#41;](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md)   
 [La configuración de la integración de Power BI &#40;portal web&#41;](my-settings-for-power-bi-integration-web-portal.md)  
 [Paneles en Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/)  
  
  
[!INCLUDE[feedback_stackoverflow_msdn_connect_md](../includes/feedback-stackoverflow-msdn-connect-md.md)]

